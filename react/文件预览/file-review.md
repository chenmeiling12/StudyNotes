#### 一.excel 文件预览

1.安装 handsontable、axios、xlsx

2.引入库

```
import { App, Spin } from "antd";
import axios from "axios";
import Handsontable from "handsontable";
import { useCallback, useRef, useState } from "react";
import * as xlsx from "xlsx";
```

3.定义类型

```
interface XlsxDto {
  sheetNames: string[] | null;
  sheets: {
    [key: string]: any;
  } | null;
  clickSheetName: string | null;
  reviewStatus: boolean | null;
}
```

4.定义初始值

```
const fileUrl ="";

  // 状态对象，包含与Excel文件相关的数据
  const [xlsxDto, setXlsxDto] = useState<XlsxDto>({
    sheetNames: null,
    sheets: null,
    clickSheetName: null,
    reviewStatus: null,
  });

  const { message } = App.useApp();

  // 用于引用HTML元素<div>。在渲染完成后会被赋值为实际的DOM元素，用于Handsontable实例的容器
  const containerRef = useRef<HTMLDivElement | null>(null);

  // 用于引用Handsontable实例。在创建Handsontable实例后会被赋值，用于操作表格数据。
  const hotRef = useRef<Handsontable | null>(null);

  // useCallback避免在每次渲染时都重新创建该函数
  const updateXlsxDto = useCallback((k: keyof XlsxDto, v: any) => {
    setXlsxDto((prev) => ({ ...prev, [k]: v }));
  }, []);
```

5.用于从指定的 URL 加载 Excel 文件，并在成功加载后将其内容显示在网页中

```
 const loadFile = async () => {
      if (fileUrl)
        axios
          .get(fileUrl, {
            responseType: "arraybuffer", //指定响应数据类型为 arraybuffer，适用于二进制数据。
            timeout: 1000 * 60 * 60, //设置请求超时时间为1小时
          })
          .then((res) => {
            const workbook = xlsx.read(res.data); //读取响应数据并生成一个工作簿对象

            const jsonSheet = xlsx.utils.sheet_to_json(
              workbook.Sheets[workbook.SheetNames[0]],
              { header: 1 }
            );

            // 更新所有工作表、所有工作表名称、第一个工作表名称、文件加载成功
            updateXlsxDto("sheets", workbook.Sheets);
            updateXlsxDto("sheetNames", workbook.SheetNames);
            updateXlsxDto("clickSheetName", workbook.SheetNames[0]);
            updateXlsxDto("reviewStatus", true);

            //使用Handsontable库在指定的容器中创建一个表格，并传入JSON格式的数据
            hotRef.current = new Handsontable(containerRef.current!, {
              data: jsonSheet as any,
              rowHeaders: true,
              colHeaders: true,
              licenseKey: "non-commercial-and-evaluation",
            });
          })
          .catch(() => {
            message.error("文件暂时无法预览");
            updateXlsxDto("reviewStatus", false);
          });
    };

 loadFile();
```

6.渲染

```
<div className="flex flex-col space-y-2 w-full h-[37rem] overflow-scroll">
        {/* 判断文件状态
        当status不为null且不为false时，加载···；
        当status为true 预览组件；
        当status为false 提示文件不存在;
        */}
        {!xlsxDto.reviewStatus && xlsxDto?.reviewStatus !== false ? (
          <div className="h-full w-full flex justify-center items-center">
            <Spin />
          </div>
        ) : xlsxDto?.reviewStatus ? (
          <div ref={containerRef} className="w-full flex-1" />
        ) : (
          <div className="h-full w-full flex justify-center items-center">
            文件暂时无法预览
          </div>
        )}

        {/* 处理sheets工作表的列表 */}
        <div className="flex space-x-2 absolute bottom-0">
          {xlsxDto?.sheetNames?.map((item, index) => (
            <div
              key={index}
              className={`p-1 ${
                xlsxDto?.clickSheetName === item
                  ? "bg-[#4b4b4b] text-[#e9e9e9]"
                  : "bg-[#e9e9e9] text-[#4b4b4b]"
              } `}
              onClick={() => {
                if (xlsxDto?.sheets) {
                  //更新当前点击的工作表名称
                  updateXlsxDto("clickSheetName", item);

                  //更新工作表的当前数据，并将Excel工作表转换为JSON格式并显示
                  //header: 1表示第一行作为表头
                  hotRef.current?.updateData(
                    xlsx.utils.sheet_to_json(xlsxDto?.sheets[item], {
                      header: 1,
                    })
                  );
                }
              }}
            >
              {item}
            </div>
          ))}
        </div>
      </div>
    </div>
```

#### 二.word 文件预览

1.安装 docx-preview

2.引入库

```
import { App } from "antd";
import { renderAsync } from "docx-preview";
import { useRef, useState } from "react";
```

3.定义初始值

```
const fileUrl = "";

  const { message } = App.useApp();

  const containerRef = useRef<HTMLDivElement | null>(null);

  const [isDocxError, setIsDocxError] = useState<boolean>(false);

```

4.从指定的 URL 加载一个文件，并在加载成功后渲染其内容。如果加载失败，则会显示错误消息并设置错误状态

```

const loadFile = async () => {
      if (fileUrl) {
        try {
          const response = await fetch(fileUrl);

          if (!response.ok) {
            throw new Error(`${response.status}`);
          }

          //使用 response.arrayBuffer() 方法将响应数据读取为 ArrayBuffer（二进制数据）。
          const arrayBuffer = await response.arrayBuffer();

          // 渲染文件内容到指定的容器中
          await renderAsync(arrayBuffer, containerRef.current!);
        } catch (error) {
          setIsDocxError(true);
          message.error("该文件无法预览");
        }
      }
    };

    loadFile();
```

5.渲染

```
<div>
 {!isDocxError ? (
        <div ref={containerRef} className="w-full flex-1" />
      ) : (
        <div className="h-full w-full flex justify-center items-center">
          文件暂时无法预览
        </div>
)}
</div>
```

三.pdf 和 txt 文件预览

```
<iframe src={fileUrl} width="100%" height="700" />
```

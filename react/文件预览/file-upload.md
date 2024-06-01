文件上传

1.安装 react-dropzone^14.2.3

```
yarn add react-dropzone
```

2.  在 onDrop 方法中拿到上传文件的值，使用 accept 去筛选上传文件的类型。

```
       <Dropzone
              onDrop={(file) => setExcelFile(file && file[0])}
              accept={{
                "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet":
                  [],
              }}
            >
              {({ getRootProps, getInputProps }) => (
                <div
                  {...getRootProps({
                    className: "dropzone",
                  })}
                >
                  <input {...getInputProps()} />
                  <Button
                    icon={<UploadOutlined />}
                    className="bg-[#F1EBFF] text-[#763DFA] border-0"
                  >
                    點擊上傳
                  </Button>
                </div>
              )}
            </Dropzone>
```

3.  把文件转化成 FormData 上传

```
const formData = new FormData();

excelFile && formData.append("file", excelFile);
```

### 4.定义文件上传接口

```
export const PostFile = async (categoryId: string, data: FormData) => {
  return await api.post<GetAttachUrl>(
    `/api/AiTk/faqs/add?categoryId=${categoryId}`,
    data
  );
};
```

5.调用接口

```
PostFile(importClassify, formData)
      .then(() =>
//调用成功时
      })
      .catch(() => {
        //上传失败时
      })
      .finally(() => {
//清空数据
      });

```

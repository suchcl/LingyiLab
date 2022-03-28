### react中实现导出excel

不错的参考：https://blog.csdn.net/sinat_15625949/article/details/121275084

数据导出到excel，通常有两种实现方式：

1. 接口直接返回列表数据导出

接口返回列表数据，我理解是实现成本较低，方式较为令狐的一种方式，所以我在实现类似功能的时候，比较喜欢让服务端直接返回一个列表数据。

接口返回列表数据，前端在实现导出到excel的时候，可以使用js-export-excel包，可以参考：https://github.com/cuikangjie/js-export-excel

具体实现：

```tsx
// 导入js-export-excel包
const ExportJsonExcel = require('js-export-excel');

// 导出到excel
const downloadJsonToExcel = (list: any, title: string[], name: string) => {
// 表格数据
const option: Record<string, any> = {};
option.fileName = name;
option.datas = [
    {
    sheetData: list || [],
    sheetName: 'sheet',
    sheetHeader: title,
    },
];

const toExcel = new ExportJsonExcel(option);
toExcel.saveExcel();
};

// 导出到excel事件的响应函数
const getExportUser = async () => {
    try {
        const exportUser = await exportExcel();
        setUser(exportUser.data);
        downloadJsonToExcel(user, ['姓名', '性别', '手机'], '候选人姓名');
    } catch (err) {
        console.log(err);
    }
};

// DOM
<Button
    type="primary"
    className={style.btn}
    onClick={getExportUser}
>
    导出到excel
</Button>
```

2. 接口返回字节流文件导出
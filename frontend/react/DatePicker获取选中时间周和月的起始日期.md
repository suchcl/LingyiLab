### DatePicker、RangePicker、momengt获取指定时间的周、月的第一天和最后一天

1. moment()获取当前月份

```js
moment().daysInMonth();  // 获取当前日期所在月份的天数

```

js中日期的两个必要知识点：

```js
getDay(); // 获取当前日期是一周中的第几天
getDate(); // 获取当前日期是当前月中的哪1天
```

2. antd中使用DatePicker时，获取选中日期所在周、月的第一天和最后1天

```tsx
const handlechange = (date: any, dateString: string) => {
        const startDayOfWeek = (new Date(date[0])).getDay();
        const endDayOfWeek = (new Date(date[1])).getDay();
        console.log("起始日期周的第一天:",date[0].subtract(startDayOfWeek - 1, 'days').format("YYYY-MM-DD"));
        console.log("结束日期周的最后一天:",date[1].add(7 - endDayOfWeek, 'days').format('YYYY-MM-DD'));

        const startDayOfMonth = (new Date(date[0])).getDate();
        const endDayOfMonth = (new Date(date[1])).getDate();
        console.log("起始日期月的第一天:",date[0].subtract(startDayOfMonth - 1, 'days').format('YYYY-MM-DD'));
        console.log("起始日期月的最后一天:",date[1].add(date[1].daysInMonth() - endDayOfMonth, 'days').format('YYYY-MM-DD'));
    }

    return (
        <RangePicker
            style={{ width: '260px' }}
            locale={locale}
            picker="week"
            onChange={handlechange}
        />
    );
```
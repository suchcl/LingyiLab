### ant-vue-design时间控件快捷筛选时间范围，可选择今天、昨天、最近一周、最近2周、最近1个月、3个月、半年

之前在使用element-ui，其中有个时间控件使用起来方便，就是日期范围控件，看可以便捷的筛选最近1周、2周、1个月、3个月、半年等这样的快捷筛选方式，使用起来感觉简单、易用，体验挺好，最近一个项目在使用ant-design-vue,也想要实现个类似的时间范围选择的效果。element-ui的效果的样子：

![快捷选择时间范围](../public/images/i31.png)

我在ant-design-vue里面没有找到类似的控件，最终发现了RangePicker，可查看demo的时候并没有和element-ui中那个效果类似的案例，这我也不能为了一个控件就再引入一个UI库呀（如果必须要这种效果的话，自己不会实现，也只能引入了）。不过好在最后发现了RangePicker的一个属性：ranges，可以预设时间范围快捷选择，直接上代码吧：

```javascript
<a-range-picker @change="onChange" :ranges="dataRange"></a-range-picker>
<script>
import moment from "moment"; //使用到了moment控件，需要引入一下
let dataRange = {
  今天: [moment().startOf("day"), moment()],
  昨天: [
    moment().startOf("day").subtract(1, "days"),
    moment().startOf("day").subtract(1, "days"),
  ],
  最近一周: [moment().startOf("day").subtract(1, "weeks"), moment()],
  最近两周: [moment().startOf("day").subtract(2, "weeks"), moment()],
  最近1个月: [moment().startOf("day").subtract(1, "months"), moment()],
  最近3个月: [moment().startOf("day").subtract(3, "months"), moment()],
  最近半年: [moment().startOf("day").subtract(6, "months"), moment()],
  最近1年: [moment().startOf("day").subtract(1, "years"), moment()],
};
export default {
  data() {
    return {
      dataRange
    };
  },
  methods: {
    onChange(data, dataString) {
      console.log(data);
      console.log(dataString);
    },
  },
};
</script>
```

最终效果如下：

![ant-vue-design时间控件快捷筛选时间范围，可选择今天、昨天、最近一周、最近2周、最近1个月、3个月、半年](../public/images/i30.png)

虽然在样式上和element-ui有些差距，但是功能已无任何问题。
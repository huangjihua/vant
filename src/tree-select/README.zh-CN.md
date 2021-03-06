# TreeSelect 分类选择

### 引入

```js
import Vue from 'vue';
import { TreeSelect } from 'vant';

Vue.use(TreeSelect);
```

## 代码演示

### 单选模式

`item`为分类显示所需的数据，数据格式见下方示例。`main-active-index`表示左侧高亮选项的索引，`active-id`表示右侧高亮选项的 id

```html
<van-tree-select
  :items="items"
  :active-id.sync="activeId"
  :main-active-index.sync="activeIndex"
/>
```

```js
export default {
  data() {
    return {
      items,
      activeId: 1,
      activeIndex: 0
    };
  }
}
```

### 多选模式

`active-id`为数组格式时，可以选中多个右侧选项

```html
<van-tree-select
  :items="items"
  :active-id.sync="activeIds"
  :main-active-index.sync="activeIndex"
/>
```

```js
export default {
  data() {
    return {
      items,
      activeIds: [1, 2],
      activeIndex: 0
    };
  }
}
```

### 自定义内容

通过`content`插槽可以自定义右侧区域的内容

```html
<van-tree-select
  height="55vw"
  :items="items"
  :main-active-index.sync="active"
>
  <template slot="content">
    <van-image v-if="active === 0" src="https://img.yzcdn.cn/vant/apple-1.jpg" />
    <van-image v-if="active === 1" src="https://img.yzcdn.cn/vant/apple-2.jpg" />
  </template>
</van-tree-select>
```

```js
export default {
  data() {
    return {
      active: 0,
      items: [{ text: '分组 1' }, { text: '分组 2' }]
    }
  }
}
```

### 提示信息

设置`dot`属性后，会在图标右上角展示一个小红点。设置`info`属性后，会在图标右上角展示相应的徽标

```html
<van-tree-select
  height="55vw"
  :items="items"
  :main-active-index.sync="activeIndex"
/>
```

```js
export default {
  data() {
    return {
      activeIndex: 0,
      items: [
        { text: '浙江', children: [], dot: true },
        { text: '江苏', children: [], info: 5 }
      ]
    }
  }
}
```

## API

### Props

| 参数 | 说明 | 类型 | 默认值 |
|------|------|------|------|
| items | 分类显示所需的数据 | *Item[]* | `[]` |
| height | 高度，默认单位为`px` | *number \| string* | `300` |
| main-active-index | 左侧选中项的索引 | *number \| string* | `0` |
| active-id | 右侧选中项的 id，支持传入数组 | *number \| string \|<br>(number \| string)[]* | `0` |
| max `v2.2.0` | 右侧项最大选中个数 | *number \| string* | `Infinity` |

### Events

| 事件名 | 说明 | 回调参数 |
|------|------|------|
| click-nav | 点击左侧导航时触发 | index：被点击的导航的索引 |
| click-item | 点击右侧选择项时触发 | data: 该点击项的数据 |

### Slots

| 名称 | 说明 |
|------|------|
| content | 自定义右侧区域内容 |

### Item 数据结构

`items` 整体为一个数组，数组内包含一系列描述分类的对象，每个分类里，`text`表示当前分类的名称，`children`表示分类里的可选项。

```js
[
  {
    // 导航名称
    text: '所有城市',
    // 导航名称右上角徽标
    info: 3,
    // 是否在导航名称右上角显示小红点
    dot: true,
    // 导航节点额外类名
    className: 'my-class',
    // 该导航下所有的可选项
    children: [
      {
        // 名称
        text: '温州',
        // id，作为匹配选中状态的标识符
        id: 1,
        // 禁用选项
        disabled: true
      },
      {
        text: '杭州',
        id: 2
      }
    ]
  }
]
```

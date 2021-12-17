<!--
 * @Author: shenxh
 * @Date: 2021-12-17 09:50:10
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-17 10:59:47
 * @Description: 选择器
-->

- [选择器](#选择器)
  - [id 选择器 (唯一性)](#id-选择器-唯一性)
  - [class 选择器](#class-选择器)
  - [标签选择器](#标签选择器)
- [举例](#举例)

# 选择器

## id 选择器 (唯一性)
根据 id 选取对应元素, 因为 id 具有唯一性, 所以这种方式最多会选取一个元素

## class 选择器
根据 class 选取对应元素, 会返回一个数组, 包含所有符合该 class 的元素

## 标签选择器
根据元素标签选取对应元素, 会返回一个数组, 包含所有符合该标签的元素

# 举例
```
<div id="box1" class="item1"></div>
<div id="box2" class="item item2"></div>
<div id="box3" class="item item3"></div>
```
```
// id 选择器
const _id = document.getElementById('box1');
// class 选择器
const _class = document.getElementsByClassName('item');
// 标签选择器
const _tag = document.getElementsByTagName('div');

console.log(_id); // id 为 box1 的元素
console.log(_class); // [id 为 box2 的元素, id 为 box3 的元素]
console.log(_tag); // [id 为 box1 的元素, id 为 box2 的元素, id 为 box3 的元素]
```
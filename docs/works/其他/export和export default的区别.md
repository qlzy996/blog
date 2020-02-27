

**export和export default的区别**

一、export的使用
1.直接输出
export let words = 'hello world!!!' 
export function output() { 
　　// ... 
}
2.先定义再输出
复制代码
let firstWords = 'hello'
let secondWords = 'world'
let thirdWords = '!!!'

function output() {
    // ...
}

export {firstWords, secondWords, thirdWords, output}

二、export default的使用
1.export default 用于规定模块的默认对外接口
2.很显然默认对外接口只能有一个，所以 export default 在同一个模块中只能出现一次
3.export default只能直接输出，不能先定义再输出。

三、二者在 import 方式上区别

(1)export的输出与import输入

export function output() {
    // ...
}

import {output} from './example'
(2)export default的输出与import输入

export default function output() {
    // ...
}

import output from './example'
特殊注意，export default 的 import 方式不需要使用大括号包裹。
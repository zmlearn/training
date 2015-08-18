# 简单问答游戏（针对前端工程师）

## 任务描述：

实现一个简单的性格测试网页游戏，在移动端页面上显示问答题目游戏.

现有测试题目列表, 储存在文件 `test.json` 中, 格式如下

```js
{
    "questions": [
        {
            "title": "第一个问题",
            "selections": [
                {
                    "text": "第一个选项, 选我跳到第二题.",
                    "next": 1
                },
                {
                    "text": "第二个选项, 选我跳到第三题.",
                    "next": 2
                },
                {
                    "text": "第三个选项, 选我跳到第四题.",
                    "next": 3
                }
            ] 
        },
        {
            "title": "第二个问题",
            "selections": [
                {
                    "text": "第一个选项, 选我跳到类型 A.",
                    "type": "A"
                },
                {
                    "text": "第二个选项, 选我跳到第三题.",
                    "next": 2
                },
                {
                    "text": "第三个选项, 选我跳到第四题.",
                    "next": 3
                }
            ] 
        },
        {
            "title": "第三个问题",
            "selections": [
                {
                    "text": "第一个选项, 选我跳到类型 B.",
                    "type": "B"
                },
                {
                    "text": "第二个选项, 选我跳到类型 C.",
                    "type": "C"
                },
                {
                    "text": "第三个选项, 选我跳到第四题.",
                    "next": 3
                }
            ] 
        },
        {
            "title": "第四个问题",
            "selections": [
                {
                    "text": "第一个选项, 选我跳到类型 D.",
                    "type": "D"
                },
                {
                    "text": "第二个选项, 选我跳到类型 E.",
                    "type": "E"
                }
            ] 
        }
    ],
    "types": {
        "A": "人好胃口也好",
        "B": "人渣",
        "C": "大人渣",
        "D": "超级人渣",
        "E": "呵呵哈哈"
    }
}
```

## 任务要求

1. 使用 XMLHttpRequest 获取以上 json 文件中的内容并转为 JavaScript 对象.
2. 添加一个开始测试的按钮, 点击开始测试跳转到第一道题.
3. 按照题目中的描述, 当用户选择具体选项时跳转到对应的题目.
4. 当得出结论时, 跳转到结论界面.

除以上要求外, 注意是一个单页, 整个过程无刷新产生, 不能使用第三方库 (如 JQuery).
时间为一周, 团队其他成员会参与 code review 和分享.

## 提示

第一题对应 0, 第二题对应 1, 第三题对应 2... 以此类推.


## 任务时间

8月18日 至 8月25日

## 学习资料

## HTML

- [知乎上的一些Web基本概念介绍](http://www.zhihu.com/question/22689579)
- [慕课网HTML+CSS基础课程](http://www.imooc.com/learn/9)
- [w3school html教程](http://w3school.com.cn/html/index.asp)
- [MDN HTML](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Introduction)

## CSS

- [MDN CSS](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Getting_started)
- [w3school css](http://w3school.com.cn/css/index.asp)
- [慕课网HTML+CSS基础课程](http://www.imooc.com/learn/9)

## JavaScript

- [MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript)
- [慕课网JavaScript入门](http://www.imooc.com/learn/36)
- [慕课网JavaScript教程](http://www.imooc.com/learn/10)
- [w3school](http://www.w3school.com.cn/js/)
- [Codecademy](http://www.codecademy.com/tracks/javascript)

## 编辑器

- [Sublime Text](http://code.tutsplus.com/courses/perfect-workflow-in-sublime-text-2)
- [Visual Studio Code](http://code.visualstudio.com/)

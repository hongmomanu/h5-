# 传递监听数据方式
```js
  window.postMessage(messageData,'*');
  window.addEventListener('message',(data)=>{/*do somethin*/});
```

# 例子
```js
  window.postMessage({evtName:'play',data:'dom1'},'*');
```

# 传递题目数据:
        
### 选择题
```js
  window.postMessage({evtName:'sendQuestion',data:[{"ID":"AVr5woRJPywbg_0lhGCU","Content":"倒数等于本身的数是（　　）",
     "Options":["选项A","选项B","选项C","选项D"],"CateName":"选择题","Degree":"2",
     "Answer":"D","Method":"【解答】解：因为只有（+1）×（+1）=1，（-1）×（-1）=1，<br />所以倒数等于本身的数是±1．<br />故选D．",
     "Analyse":"【分析】根据倒数的定义可知倒数等于本身的数是±1．"}]}) 
```
###  问答题:
```js
  data:[{
        "ID": "AVr1yKAOPywbg_0lb84Q",
        "Content": "直接写出得数． <table style=\"margin-left:0px;width:650px;\"><tbody><tr><td>402-78=</td><td>6.25+3.75=</td><td>0.9-0.01=</td><td>3.6÷9=</td></tr><tr><td>8×9×1.25=</td><t$
        "CateName": "解答题",
         "Degree":"2",
        "Answer": "",
        "Method": "<table style=\"margin-left:0px;width:650px;\"><tbody><tr><td>402-78=324，</td><td>6.25+3.75=10，</td><td>0.9-0.01=0.89，</td><td>3.6÷9=0.4，</td></tr><tr><td>8×9×1.25=90>$
        "Analyse": ""
      }]
```
### 说明: Content 题目内容， Options：选项，CateName 题目类型，Answer 答案（选择题），Method 解答， Analyse 分析（如果有）， Degree 难度

 
### 课件：

根据目前的开发情况，课件里面有写了这些方法：

例题精讲和提升训练有需要翻页功能，这个方法定义为 last和next，传递的方法为：

window.frames[0].postMessage({sc:'last'},'*');
window.frames[0].postMessage({sc:'next'},'*');

例题精讲、能量加油站和提升训练里都有测试题，现在的请求方法是：

window.parent.postMessage({sc:'ltjj',ls:'get'},'*');
window.parent.postMessage({sc:'ltjj',ls:'set',num:kk,ans:nn},'*');

参数sc表示当前是哪个环节，分别是'ltjj'、'nljyz'和'tsxl'，ls表示是要请求获取还只是提交数据，get为请求获取，set为提交数据，

例题精讲和提升训练4个题目是分开提交的，所以多传递了两个参数，num表示第几道题，ans表示提交的答案。

能量加油站最后提交的时候多传递了一个参数，答题成绩，参数是 score。

测试题的格式，这个demo设定的是这样子的，一个多维数组，每一个数组代表一个题，第一个位置是题目，第二个位置选项，第三个位置是正确答案，因为demo里面只有选择题，也没有关系反馈内容的什么的，其他的参数暂时没有添加，添加的话，可以一起定一个规则，比如第四个位置是题型……这样。

	var aass=[['4×25=?',['10','20','100'],'C'],
		  ['5×17×2=?',['30','170','100'],'B'],
		  ['16×25=?',['300','20','400'],'C'],
		  ['5×32=?',['160','19','88'],'A'],
		  ['25×8=?',['100','200','150'],'B']];

详细情况，源文件里有一个cs.html的文件，是开发过程中测试用的，里面有有着这些个调用的方法，现在里面的测试题是我在cs.html这个文件里面写死的，提交的时候，对应了alert了一下参数
 
 
###总结，课件请求一次一般有两个以上的参数，sc表示当前环节，ls表示说明是要请求获取数据还是只提交内容，后面添加的参数就是内容，比如成绩和答案。

## 内嵌页面相关交互补充

1、开始加载课件时，由外部组件内嵌页面要打开的地址及用户身份(教师或学生，涉及区分展示)
    

2、内嵌页面加载完成后，不要自动播放动画或视频，通知外层页面 (由老师确认所有学员都加载成功后再正式开始)
>	涉及事件: domReady(加载成功) || startClass(开始课程)

3、老师点选某一项目时，内层页面通知外部，最好能不自动切换，所有的操作都由外部通知
>	涉及事件: pickedStep(选择栏目) || gotoStep(展示选择栏目)

4、涉及音频、视频播放，通知外部，由老师指定多媒体的开始、暂停、终止
>	涉及事件: mediaEvent('play', 'puase', stop') || mediaAction('play', 'puase', 'stop')

5、进入题目交互环节后，由外部传入题目、选项
>	涉及事件: null || showQuestion({title:'', options:[], id:''})

6、学生答题后，点击提交后通知外层(提交答案统一点击提交按钮)
>	涉及事件: submitResult({id: '', result: '' || ['A', 'B', 'C']})

7、老师宣布答案及解答内容
>	涉及事件: showAnswers({id: '', answer: '' || [], detail: ''})

8、交互格式：
```js
    /* 从外向里 */
    var innerCourse = document.getElementById('html5Box');
    // 开始课程
    innerCourse.postMessage({
        action: 'startClass',
        data: null
    });
    // 暂停播放
    innerCourse.postMessage({
        action: 'mediaAction',
        data: {
            id: mediaId,
            type: 'puase',
            during: 21000
        }
    });
    // 展示题目
    innerCourse.postMessage({
        action: 'showQuestion',
        data: {
            type: 'choiceType',
            id: questionId,
            title: "下面哪一条表述是正确的",
            options: [
                '1+1=2',
                '1*1=2',
                '1-1=2'
            ]
        }
    });
    // 展示结果
    innerCourse.postMessage({
        action: 'showAnswers',
        data: {
            id: questionId,
            userResult: true || false,
            answer: 2,
            dertail: '1+1=2， 1*1=1， 1-1=0'
        }
    });

    /* 从里向外 */
    var outerWindow = window.parent;
    // 加载完毕
    outerWindow.postMessage({
        action: 'classReadey',
        data: null
    });
    // 选择某栏目(点击某个元素，截获该元素的点击事件并通知外层，等待外部通知内部展示那一栏目)
    outerWindow.postMessage({
        action: 'pickedStep',
        data: {
            id: 'goToMedia'
        }
    });
    // 停止多媒体播放(传递消息到外层，不做任何处理，等待外部通知暂停与否)
    outerWindow.postMessage({
        action: 'mediaEvent', 
        data: {
            id: mediaId,
            type: 'puase',
            during: 21000
        }
    });
    // 提交答案(提交学生选择结果，单选或多选，或者多个填空的内容)，结果的正确与否由外层通知
    outerWindow.postMessage({
        action: 'submitResult',
        data: {
            id: 'questionId',
            result: 2 || [2, 3]
        }
    });


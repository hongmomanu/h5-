传递监听数据方式:
	window.postMessage(messageData,'*');
	window.addEventListener('message',(data)=>{/*do somethin*/});

例子：
	window.postMessage({evtName:'play',data:'dom1'},'*');

传递题目数据:
        选择题：
	window.postMessage({evtName:'sendQuestion',data:{"ID":"AVr5woRJPywbg_0lhGCU","Content":"倒数等于本身的数是（　　）",
										"Options":["选项A","选项B","选项C","选项D"],"CateName":"选择题","Degree":"2",
										"Answer":"D","Method":"【解答】解：因为只有（+1）×（+1）=1，（-1）×（-1）=1，<br />所以倒数等于本身的数是±1．<br />故选D．",
										"Analyse":"【分析】根据倒数的定义可知倒数等于本身的数是±1．"}})

        问答题:
	data:{
        "ID": "AVr1yKAOPywbg_0lb84Q",
        "Content": "直接写出得数． <table style=\"margin-left:0px;width:650px;\"><tbody><tr><td>402-78=</td><td>6.25+3.75=</td><td>0.9-0.01=</td><td>3.6÷9=</td></tr><tr><td>8×9×1.25=</td><td>25×2.4=</td><td>4-<span  mathtag=\"math\" ><table cellspacing=\"-1\" cellpadding=\"-1\" style=\"width:auto;display:inline-table;*display:inline;vertical-align:middle;margin:0;padding:0;text-align:center;line-height:normal;\" style=\"display:inline-table;vertical-align:middle\"><tr><td style=\"border-bottom:1px solid black\">5</td></tr><tr><td>6</td></tr></table></span>=</td><td>349÷72≈</td></tr></tbody></table>",
        "CateName": "解答题",
	   "Degree":"2",	
        "Answer": "",
        "Method": "<table style=\"margin-left:0px;width:650px;\"><tbody><tr><td>402-78=324，</td><td>6.25+3.75=10，</td><td>0.9-0.01=0.89，</td><td>3.6÷9=0.4，</td></tr><tr><td>8×9×1.25=90，</td><td>25×2.4=60，</td><td>4-<span  mathtag=\"math\" ><table cellspacing=\"-1\" cellpadding=\"-1\" style=\"width:auto;display:inline-table;*display:inline;vertical-align:middle;margin:0;padding:0;text-align:center;line-height:normal;\" style=\"display:inline-table;vertical-align:middle\"><tr><td style=\"border-bottom:1px solid black\">5</td></tr><tr><td>6</td></tr></table></span>=3<span  mathtag=\"math\" ><table cellspacing=\"-1\" cellpadding=\"-1\" style=\"width:auto;display:inline-table;*display:inline;vertical-align:middle;margin:0;padding:0;text-align:center;line-height:normal;\" style=\"display:inline-table;vertical-align:middle\"><tr><td style=\"border-bottom:1px solid black\">1</td></tr><tr><td>6</td></tr></table></span>，</td><td>349÷72≈5．</td></tr></tbody></table>",
        "Analyse": "",
     
      } 

      说明: Content 题目内容， Options：选项，CateName 题目类型，Answer 答案（选择题），Method 解答， Analyse 分析（如果有）， Degree 难度




	


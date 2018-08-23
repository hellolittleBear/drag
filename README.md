## 原声实现文件目录功能（简单功能）

> 这是一个简单版本，由于面试和工作准备，优化以后再说吧，如果有疑问可以加我QQ：1748416084 	
**注：喜欢被骚扰**

### 数据
数据直接使用json数据，反正js和json都一样使用不是？？
```
{
	"data":[
		{
			"name":"桌面事业部",
			"type":0,
			"lv":"A",
			"manager":"YangHt",
			"phone":"13699254***",
			"children":[
				{
					"name":"测试部",
					"type":1,
					"lv":"B",
					"manager":"LuJ",
					"phone":"13699254***",
					"children":[
						{
							"name":"输入法组",
							"type":1,
							"lv":"C",
							"manager":"LiXm",
							"phone":"13699254***",
							"children":[
								{
									"name":"输入法组",
									"type":1,
									"lv":"D",
									"manager":"ZhaoF",
									"phone":"13699254***",
									"children":[
										{
											"name":"输入法组",
											"type":1,
											"lv":"E",
											"manager":"WangAy",
											"phone":"13699254***",
											"children":[]
										},{
											"name":"输入法组",
											"type":1,
											"lv":"E",
											"manager":"ZhaoL",
											"phone":"13699254***",
											"children":[]
										},{
											"name":"输入法组",
											"type":1,
											"lv":"E",
											"manager":"LiLy",
											"phone":"13699254***",
											"children":[]
										}
									]
								},
								{
									"name":"Android组",
									"type":0,
									"lv":"D",
									"manager":"ZhouPj",
									"phone":"13699254***",
									"children":[]
								},
								{
									"name":"手机壁纸组",
									"type":0,
									"lv":"D",
									"manager":"LiJ",
									"phone":"13699254***",
									"children":[]
								}
							]
						},
						{
							"name":"iOS组",
							"type":1,
							"lv":"C",
							"manager":"CuiYf",
							"phone":"13699254***",
							"children":[]
						}
					]
				},
				{
					"name":"无线商务合作部",
					"type":1,
					"lv":"B",
					"manager":"WangXf",
					"phone":"13699254***",
					"children":[]
				},
				{
					"name":"开发组",
					"type":1,
					"lv":"B",
					"manager":"LiZt",
					"phone":"13699254***",
					"children":[]
				}
			]
		},
		{
			"name":"EHR组",
			"type":1,
			"lv":"A",
			"manger":"LiQ",
			"phone":"13901234***",
			"children":[
				{
					"name":"总账核算组",
					"type":1,
					"lv":"B",
					"manager":"WangX",
					"phone":"18911208***",
					"children":[
						{
							"name":"总账核算组",
							"type":1,
							"lv":"C",
							"manager":"XiangX",
							"phone":"13699254***",
							"children":[
								{
									"name":"总账核算组",
									"type":1,
									"lv":"D",
									"manager":"PengJl",
									"phone":"13699254***",
									"children":[]
								},{
									"name":"总账核算组",
									"type":0,
									"lv":"D",
									"manager":"WangY",
									"phone":"13699254***",
									"children":[]
								},{
									"name":"总账核算组",
									"type":1,
									"lv":"D",
									"manager":"ShiJ",
									"phone":"13699254***",
									"children":[]
								}
							]
						},
						{
							"name":"总账核算组",
							"type":1,
							"lv":"C",
							"manager":"YaoQ",
							"phone":"13699254***",
							"children":[]
						},
						{
							"name":"总账核算组",
							"type":1,
							"lv":"C",
							"manager":"LuYm",
							"phone":"13699254***",
							"children":[]
						}
					]
				},
				{
					"name":"商务拓展部",
					"type":1,
					"lv":"B",
					"manager":"LiuL",
					"phone":"13699254***",
					"children":[
						{
							"name":"商务拓展部",
							"type":0,
							"lv":"C",
							"manager":"LiXq",
							"phone":"13699254***",
							"children":[]
						},{
							"name":"商务拓展部",
							"type":0,
							"lv":"C",
							"manager":"YangXf",
							"phone":"13699254***",
							"children":[]
						}
					]
				}
			]
		},
		{
			"name":"薪酬运营组",
			"type":1,
			"lv":"A",
			"manger":"LiQs",
			"phone":"010-51413****",
			"children":[
				{
					"name":"BO组",
					"type":1,
					"lv":"B",
					"manager":"PanXx",
					"phone":"010-31314****",
					"children":[]
				},
				{
					"name":"薪酬运营组",
					"type":1,
					"lv":"B",
					"manager":"LiJ",
					"phone":"13699254***",
					"children":[]
				},
				{
					"name":"薪酬运营组",
					"type":1,
					"lv":"B",
					"manager":"GaoS",
					"phone":"010-31314****",
					"children":[]
				},
				{
					"name":"薪酬运营组",
					"type":1,
					"lv":"B",
					"manager":"TianW",
					"phone":"13699254***",
					"children":[]
				}
			
			]
		}
	
	]
}
```
### 拖动
使用h5的新特性，drag功能，
- dragable
- dragstart
- dragover
- dragenter
- drop
展示代码：
```
  // 拖动事件
  drag(el) {
    let ele = el;
    el.setAttribute('draggable', true);
    /*拖动目标 source*/
    el.addEventListener("dragstart", (event) => {
      event.dataTransfer.setData("Text",ele.id);
    }, false);
    /*被放置目标*/
    el.addEventListener("dragover", (event) => {
      // 取消默认不能放置内部机制
      event.preventDefault();
    }, false);
    el.addEventListener("dragenter",(event) => {  
      // 鼠标经过的元素....  可优化，事件委托body
      event.preventDefault();
    }, false);
    // 拖动落下的目标
    el.addEventListener("drop", (event) => {
      event.preventDefault();
      let sourceId =event.dataTransfer.getData("Text");  // 源id
      let distId = ele.id;  // 目标id
      /**
        * 现在就是对json数据的修改了.... 然后重新渲染table
        * 调用 drapJson...
        * 思想： 看似dom改变，实则数据改变
        * 获取自身数据和父组件数据.... 父组件插入自身数据
      */
      this.updateDomTree(sourceId, distId);
    }, false)
  }
```
### 右键事件
```
el.addEventListener('contextmenu', (e) => {
      e.preventDefault();
      menu.style.left = e.clientX+'px';
      menu.style.top = e.clientY+'px';
      menu.style.display = 'inline-block';
      this.currentClick = el.id;
    }, false); 
```
### 显示样式-- 层级样式
```
  // 显示table数据  数据、挂载点
  showTableDOM(domtree, render) {
    for(let i = 0; i < domtree.length; i++) {
      let _createDom = this.createDOM(render);
      _createDom.td_arr[0].innerHTML = domtree[i].lv; // 层级
      _createDom.td_arr[1].innerHTML = domtree[i].type;  // 类型，是否可以移动
      _createDom.td_arr[2].innerHTML = domtree[i].name; // 文件名
      _createDom.td_arr[3].innerHTML = domtree[i].manager; // 主管
      _createDom.td_arr[4].innerHTML = domtree[i].phone; // 联系电话
      if(!flag) {
        domtree[i].id = "xu_"+Math.random().toString().slice(2);
        _createDom.tr.id = domtree[i].id; // 设置domtree数据的id进行匹配赋值
      } else {
        _createDom.tr.id = domtree[i].id;
      }
      _createDom.td_arr[2].style.textIndent = ( domtree[i].lv.charCodeAt()-65 ) * 12 + "px";
      // 拖动
      this.drag(_createDom.tr);
      if(domtree[i].children) {
        this.showTableDOM(domtree[i].children, render);
      }
    }
  }
}
```
### 全部代码
请查看第四题


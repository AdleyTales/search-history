# javascript实现历史记录

#### 效果展示：
![历史记录效果图](img/demo.png)


#### 代码code：

```html
    <!DOCTYPE html>
    <html>

    <head>
      <meta charset="utf-8">
      <title></title>
      <style media="screen">
        #history-conter {
          margin-top: 20px;
        }
        span{
          font-size: 12px;
          font-family: sans-serif;
          padding: 6px 15px;
          background-color: #ccc;
          color: #444;
          border: 1px dashed #777;
          margin: 5px 15px;
          border-radius: 3px;
        }
        span:nth-child(odd) {
          background: #FFE4B5;
        }
        span:nth-child(even) {
          background: #EEE8CD;
        }
        span:hover {
          cursor: pointer;
          background: yellow;

        }
      </style>
    </head>

    <body>

      <input type="text" name="" value="" id="keyword">
      <button onclick="fnSearch();">搜 索</button>
      <div id="history-conter"></div>

      <script src="https://cdn.bootcss.com/jquery/3.2.1/jquery.js"></script>
      <script>

        document.onkeydown = function(ev){
          // 兼容 chrome firefox
          var ev = ev || event;
          if(ev.keyCode == 13){
            fnSearch()
          }
        }


        var count = 5;

        // 将所有的值放到本地存储
        function fnSearch() {

          if ($('#keyword').val().trim() == '') {
            alert('请输入搜索内容');
          } else {
            var inputVal = $('#keyword').val().replace(/(^\s*)|(\s*$)/g, '');

            if (localStorage.getItem('key') === null || undefined) {
              localStorage.setItem('key', inputVal);
            } else {

              var storageArr  = localStorage.getItem('key').split('-'),
                  new_inputStorageStr = '';

              // 数组去重  去掉重复搜索的值
              storageArr.map(function(item,index){
                if(item == inputVal) {
                  storageArr.splice(index,1);
                }
              });

              if (storageArr.length > count) {
                storageArr.pop(inputVal);
              }

              storageArr.unshift(inputVal);
              new_inputStorageStr = storageArr.join('-');
              localStorage.setItem('key', new_inputStorageStr);

            }

          }

          $('#keyword').val('');
          showHistory();

        }

        showHistory();

        // 显示多少条历史记录
        function showHistory(){
          var arr = localStorage.getItem('key').split('-');

          var container = document.querySelector('#history-conter');
          var str = '';

          arr.forEach(function(item,index){
            str += `<span>${item}</span>`;
          });

          container.innerHTML = `<div>${str}</div>`;

        }


      </script>
    </body>

    </html>


```

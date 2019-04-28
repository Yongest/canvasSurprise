# canvasSurprise
使用canvas做一个刮一刮抽奖的功能。
	
## 效果图
![](https://raw.githubusercontent.com/yongest/canvasSurprise/master/img/dog.png)
![](https://raw.githubusercontent.com/yongest/canvasSurprise/master/img/33.png)


## 具体代码
    <body>
        <canvas id="cvs" width="320" height="150" style="border: solid 1px #ccc"></canvas>

        <script type="text/javascript">
         
            //获取画布元素
             /** @type {HTMLCanvasElement} */
            var cvs=document.getElementById("cvs");
            //获取工具集
            var cxt=cvs.getContext("2d");
            var height = cvs.height;
            var width = cvs.width;
            var giftsArr = ['一等奖','二等奖','三等奖','没中奖'];
            var randomGift = giftsArr[Math.floor(Math.random()*giftsArr.length)];

            cxt.font = 'bold 25px 黑体';
            cxt.textAlign ='center';
            cxt.textBaseline = 'middle';
            cxt.fillStyle = 'red';
            // 将得到的中将信息绘制到画布中间
            cxt.fillText(randomGift,width/2,height/2);

            // 将绘制的中奖信息另存为图片，并且作为画布元素的背景图片
            var img = cvs.toDataURL('image/png',1);

            cvs.style.background = `url('${img}')`;


            // 绘制矩形盖住中将信息
            cxt.clearRect(0,0,width,height);

            // 设置矩形的绘制颜色。
            cxt.fillStyle = '#ddd';
            // 绘制遮罩层
            cxt.fillRect(0,0,width,height);

            var flag = false;
            
            //pc端
            cvs.addEventListener('mousedown',function(e){
                flag = true;
                // globalCompositeOperation 属性设置或返回如何将一个源（新的）图像绘制到目标（已有）的图像上。
               // 源图像 = 您打算放置到画布上的绘图。
                //目标图像 = 您已经放置在画布上的绘图。
                
                cxt.globalCompositeOperation='destination-out';
            })
            
            cvs.addEventListener('mousemove',function(e){
                if(flag){
                    var x = e.clientX;
                    var y = e.clientY;
                    cxt.fillRect(x-15,y-15,30,30)
                }
            })
           
            cvs.addEventListener('mouseup',function(){
                flag = false;
            })


            //手机端
            cvs.addEventListener('touchstart',function(e){
                flag = true;
                cxt.globalCompositeOperation='destination-out';
            })
             cvs.addEventListener('touchmove',function(e){
                // console.log(e);
                if(flag){
                    var x = e.touches[0].clientX;
                    var y = e.touches[0].clientY;
                    cxt.fillRect(x-15,y-15,30,30)
                }
                
            })
            cvs.addEventListener('touchend',function(){
                flag = false;
            })
        </script>
    </body>
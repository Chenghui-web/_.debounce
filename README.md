#_.throttle 和 _.debounce 的差异

> 可以用电梯举个例子 ：

    想象每天上班大厦底下的电梯。把电梯完成一次运送，类比为一次函数的执行和响应。假设电梯有两种运行策略 throttle 和 debounce ，超时设定为15秒，不考虑容量限制
    
    
* throttle 策略的电梯。保证如果电梯第一个人进来后，15秒后准时运送一次，不等待。如果没有人，则待机
    
* debounce 策略的电梯。如果电梯里有人进来，等待15秒。如果又人进来，15秒等待重新计时，直到15秒超时，开始运送。

> 应用场景： 常用于输入时触发接口，频繁请求的话会造成接口压力 

``` javascript 
let _= require ("lodash");

  methods: {
    addressInput: _.debounce(
      function(type){
        var url = 'http://api.map.baidu.com/place/v2/suggestion?query='+address+'&region='+address+'&output=json&ak=你的AK'
        if(type!=''){
          $.ajax({
            url: url,
            dataType: "jsonp",
            jsonp: "callback",
            context: document.body,
            success: function(data) {
              result = data.result;
              // console.log(result)
              if(type=='send'){
                  _this.addressSend = data.result?data.result:''
  
              }else{
                  _this.addressArrive=  data.result?data.result:''
              }
            }
          });
        }
      },
      500
    ),
```

# Mqtt
mqtt在支付宝ios出现乱码


###使用方式

>>```
mqttConnection() {
      //debugger
      console.log('创建连接')
      const options = {
       keepalive: 60,
        clean: true, 
        connectTimeout: 10 * 1000,
        clientId:  my.getStorageSync({ key: 'mobile' }).data,
        my: my
      }
      console.log('mobile:' +  my.getStorageSync({ key: 'mobile' }).data)
      //不加密路径
      //加密路径
      const url = '连接的地址';
      mqttClient = connect('连接的地址',options)
      console.log(mqttClient);
      mqttClient.on('reconnect', (error) => {
        console.log('正在重连:', error)
      });
      //
      mqttClient.on('error', (error) => {
        console.log('连接失败:', error)
      });
      let topic = '地址';
      mqttClient.on('connect', (e) => {
        console.log(e);
        //订阅一个主题
        console.log('成功连接服务器')
        console.log('订阅主题:', topic);
        mqttClient.subscribe(topic, { qos: 1 }, function (err) {
          console.log(err);
          if (!err) {
            console.log("订阅成功")
          }
        })
      })
    },mqttCallback: function (callback,that) {
    mqttClient.on('message', function (topic, message) {
      if (callback) {
        callback(message.toString(), mqttClient,that);
      }
    })
  },mqttReconnect:function(){

    if(mqttClient==null||mqttClient==''){
      console.log('未连接调用mqttConnection')
      this.mqttConnection();
    }else{
      console.log('重连中重连中重连中重连中重连中重连中重连中重连中')
      mqttClient.on('reconnect', (error) => {
        console.log('正在重连:', error)
      });
    }
  },
  //断开mqtt连接
  mqttEnd:function(){
    console.log(111111111111111111111111111111111111111111111111)
    if (mqttClient == null || mqttClient == '') {
      console.log('未连接无需执行end')
    } else {
      console.log('正在关闭连接')
      mqttClient.end();
      mqttClient=null;
    }
  },
```

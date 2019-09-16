# AWS SDK 心得記錄

## 官方SDK問題
 [Aws sdk](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/index.html#In_Node_js)眾所皆知的API 參考文件位置(nodejs)，這邊都是果去callback的範例，也未使用也未使用你要有Promise的寫法，如果要使用Promise的範例：
 
1. 必須到官方網站中，找到類似的官方教學文件(API以外的文件)，可能會有，但寫法上個人覺得比較特別，也不符合我個人寫作的style
[Aws 建立ec2的範例](https://docs.aws.amazon.com/zh_tw/sdk-for-javascript/v2/developer-guide/ec2-example-creating-an-instance.html)

2. github，期待官方把example code補齊，舉例ec2就還一推沒有範例 :[awsdocs](https://github.com/awsdocs/aws-doc-sdk-examples/tree/master/javascript/example_code)

3. 我的做法多半就是看者API文件的舊的code，改成符合自已style寫法，但是找API的時候最大的問題是，命名不直觀，舉例建立ec2Instances 叫做runInstances，不是createInstances

## 個人寫法

### describeImages
```javascript=
const EC2 = new AWS.EC2({apiVersion: '2016-11-15', region: 'us-west-2',az: "us-west-2a"});
let params = {

    Filters: [
      {
        Name: 'name',
        Values: [
          'ubuntu/images/hvm-ssd/ubuntu-xenial-16.04-amd64-server-20180814',
          /* more items */
        ]
      }, 
      {
        Name: 'state',
        Values: [
          'available',
          /* more items */
        ]
      }
      /* more items */
    ]
};  

let AMI= await EC2.describeImages(params).promise();
console.log(AMI.Images[0].ImageId);
    

```

### 關於key&region設定



###### tags: `NodeJS` `AWS`
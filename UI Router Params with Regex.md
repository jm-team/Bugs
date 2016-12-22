### 天坑地雷

>在添加UI Router正则匹配的时候，请不要在参数与正则之间添加空格，否则路由匹配会失败

```javascript
var templateUrl = require('page/price/price-detail.html');

module.exports = {
    title: "Price",
    // url: '/:dataType/:timeType',
    // warning: DO NOT ADD SPACE BETWEEN params and their regex pattern, else the router will match fail.
    // 警告：请不要在参数与正则之间添加空格，否则路由匹配会失败
    url: '/{dataType:spot|futures}/{timeType:daily|weekly|monthly}', 
    templateUrl: templateUrl,
    controller: 'PriceCtrl',
    resolve: {
        /*@ngInject*/
        loadCtrl: function ($q) {
            var defer = $q.defer();
            require.ensure([], function (require) {
                defer.resolve(require('controller/priceCtrl.js'));
            }, 'price');
            return defer.promise;
        }
    }
};
```

>匹配路径：

```
/price/spot/daily
/price/spot/weekly
/price/spot/monthly
/price/futures/daily
/price/futures/weekly
/price/futures/monthly
```

JS------
========

                                                       JS常见的小代码
        
 一：去掉数组里面的重复项。
         
         比如 如下一个数组：var arr = [1,2,4,3,4,3]; 我想要得到数组 [1,2,4,3].为这样的 写一个函数去掉重复的项。
         
         var unique = function(arr){
            arr = arr || [];
            var obj = {},
                newArray = [];
            if(arr.length > 0){
               for(var i = 0, len = arr.length; i < len; i+=1){
                  var curItem = arr[i],
                      itemTemp = typeof(curItem) + curItem;
                  if(obj[itemTemp] !== 1){
                      newArray.push(curItem);
                      obj[itemTemp] = 1;
                  }
               }
            }
            return newArray;
         };
         
         
二： 返回数组里面的最大项：
     
     比如需求如下 有个数组 var arr = [1,2,3,4,5]; 想返回数组里面的最大项。 我们只需要写如下函数即可：
     
            var maxValue = function(arr){
                arr = arr || [];
                var i,
                    tempVal = 0;
                for(i = 0, len = arr.length; i < len; i+=1){
                    var curVal = arr[i];
                    if(curVal > tempVal){
                         tempVal = curVal;
                    }
                }
                return tempVal;
            }
            
三： 数组里面的项从小到大的排序问题：
     
     有时候我们的需求要数组里面的数字从小到大排序问题，那么我们常见的方法有sort这个方法 可以使数字从小到大的排序 但是
     用这个sort排序有个问题就是它根据ASCLL编码来排序的 比如数组[1,23,5],它排序后我们期望的是[1,5,23],但是它却返回了
     [1,23,5],为什么呢？他首先计算2的ASCLL编码是50(因为1的ASCLL编码是49)，5的ASCLL编码是53，所以50小于53.这是我们不
     想要的结果。那么至于这种情况我们自己可以写个简单的函数来支持下：如下：
     
     var compareNum = function(a,b){
         if(a > b){
            return 1;
         }else if(a < ｂ){
            return -1;
         }else {
            return 0;
         }
         
     }
     
     然后调用 数组.sort(compareNum);就ok了 但是我们有个更简单函数可以代替上面的函数：如下 
     
     数组.sort(function(a,b){
        return a - b;
     })
     
  
四：对象根据数组排序的问题。
    
    有时候我们有这么样的一个需求 向服务器发一个请求 带参数 商品ID 数组传过去 但是后台返回一个数组 里面是以对象的形式存在
    时候，由于后台开发人员懒的缘故，没有给我们排序，而我们前端需求是向服务器请求参数的顺序传过去 返回的后顺序和传过去一
    样的顺序。
    
    比如这么一个数组：var shopId = ['001','002','003','004']; 服务器返回的如下：
    
    var  callId = [
            {
               'itemId': '003'
            },
            {
                'itemId': '004'
            },
            {
               'itemId': '002'
            },
            {
               'itemId': '001'
            }];
            
   但是我是想返回的顺序是：
     
     var  callId = [
            {
               'itemId': '001'
            },
            {
                'itemId': '002'
            },
            {
               'itemId': '003'
            },
            {
               'itemId': '004'
            }];
     
     这样的。 代码可以这样写：
     
     var sorting = function(shopId,callId){

         var obj = {};
         
         for(var i = 0, ilen = shopId.length; i < ilen; i+=1){
            obj[shopId[i]] = i;
         }

        for(var j = 0, jlen = callId.length; j < jlen; j+=1){
            var curItem = callId[j];
            curItem._id = obj[curItem.itemId];
         }
         
         var compareId = callId.sort(function(a,b){
              return a._id - b._id;
         });
         
         return compareId;
      };
      
      console.log(sorting(shopId,callId));


  但是如果是这样的两个数组 ：  
  
  var shopId = ['001','002','003','004'],
      callId = ['004','003','002','001'];
      
   callId 我想根据shopId排序 这样的问题该怎么解决？我倒现在没有更好的办法 只想到一种方法，但是对性能不是最好的，暂时
   只能解决这个问题，思路还是和上面的一样的，首先把要排序的数组转换为对象 然后就根据上面的方法 对象根据数组的排序问题
   进行排序，那么最后获取对应的值 再进行一次循环 分别放入数组里面去 最终这个数组就是我们想要的值。
   
   代码如下：
   
   var sorting = function(shopId,callId){
   
       var obj = {},
				ret = [];
      for(var i = 0, ilen = shopId.length; i < ilen; i+=1){
         obj[shopId[i]] = i;
       }

      for(var j = 0, jlen = callId.length; j < jlen; j+=1){
         ret.push({'itemId':callId[j]});
       }

      for(var k = 0, klen = ret.length; k < klen; k+=1){
          var curItem = ret[k];
          curItem._id = obj[curItem.itemId];
       }
       
      var compareId = ret.sort(function(a,b){
           return a._id - b._id;
      });
       return compareId;
    };
     var test = sorting(shopId,callId);
     var tarrs = [];
     for(var n = 0, nlen = test.length; n < nlen; n+=1){
       tarrs.push(test[n].itemId);
     }
     console.log(tarrs);

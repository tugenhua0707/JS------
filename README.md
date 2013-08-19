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
     
  
     
     
            

# 怎么使用DataGrid翻页缓存功能

#### DataGrid缓存功能是什么
是你在DataGrid页面进行了查询，翻页等操作，点击编辑，查看进入子页面后，再返回主页面，刚才在主页面的查询条件、页数会被保存了下来。

#### DataGrid缓存功能有以下几个特性
* 默认支持，使用`disableCache:true`关闭。
* 默认缓存的参数是主页面上的`$scope.conditions`，可缓存多个使用`cacheConditionKey:['conditions','projectType']`配置来实现。
* 如果你在dataGrid页面使用了其他组件，可能值没有勾选上刚才缓存的，实际上值是缓存了的，需要你调用对应组件的方法。使用配置`initCondition:function(condition){}`，帮你缓存的值会传入进来，然后你就可以做初始化组件的操作了。

#### SAMPLE
以项目管理查询页面为准，我在主查询页面 ng-model上绑定的多个查询条件值都在`$scope.conditions`上面，比如：`ng-model="conditions.queryValue"`,`ng-model="conditions.queryStartDate"`，我仍然使用了个不是`conditions`上面的` ng-model="projectType"`,所以我需要缓存值就是**conditions**以及**projectType**，在gridOptions配置上就写上`cacheConditionKey:['conditions','projectType']`。

我还使用了`yn-select`下拉多选组件，为了初始化选中效果，配置上`initCondition:function(condition){}`。
> 运气好的是`yn-select`因为有个异步等待过程，所有不需要你主动初始选中效果了，如果你有缓存的参数的话。

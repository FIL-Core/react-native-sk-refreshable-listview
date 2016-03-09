# react-native-sk-refreshable-listview

##What is it

react-native-sk-refreshable-listview is a component wraps ListView, supports: 1 pull down to refresh 2 pull up to load more 3 scroll to top 4 scroll to bottom

##How to use it

1. `npm install react-native-sk-refreshable-listview@latest --save`

2. Write this in index.ios.js / index.android.js

```javascript


```
![](https://raw.githubusercontent.com/shigebeyond/react-native-sk-refreshable-listview/master/demo.gif)

##Properties

Any [View property](http://facebook.github.io/react-native/docs/view.html) and the following:

| Prop | Description | Default |
|---|---|---|
|**`onRefresh`**|A promise which to refresh data (load first page of data). I use this promise to tell when to stop loading (render loading view). |*None*|
|**`onLoadMore`**|A promise which to load more data (load next page of data). I use this promise to tell when to stop loading (render loading view). |*None*|

##Methods

| Method | Description | Params |
|---|---|---|
|**`scrollToTop`**|scroll to top. |*None*|
|**`scrollToBottom`**|scroll to bottom. |*None*|

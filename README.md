# react-native-sk-refreshable-listview

##What is it

react-native-sk-refreshable-listview is a component wraps ListView, supports: 1 pull down to refresh 2 pull up to load more 3 scroll to top 4 scroll to bottom

##How to use it

1. `npm install react-native-sk-refreshable-listview@latest --save`

2. Write this in index.ios.js / index.android.js

```javascript

var React = require('react-native');
var {
  StyleSheet,
  Text,
  View,
  TouchableHighlight
} = React;

var GiftedListView = require('react-native-gifted-listview');

var Example = React.createClass({

  /**
   * Will be called when refreshing
   * Should be replaced by your own logic
   * @param {number} page Requested page to fetch
   * @param {function} callback Should pass the rows
   * @param {object} options Inform if first load
   */
  _onFetch(page = 1, callback, options) {
    setTimeout(() => {
      var rows = ['row '+((page - 1) * 3 + 1), 'row '+((page - 1) * 3 + 2), 'row '+((page - 1) * 3 + 3)];
      if (page === 3) {
        callback(rows, {
          allLoaded: true, // the end of the list is reached
        });        
      } else {
        callback(rows);
      }
    }, 1000); // simulating network fetching
  },


  /**
   * When a row is touched
   * @param {object} rowData Row data
   */
  _onPress(rowData) {
    console.log(rowData+' pressed');
  },

  /**
   * Render a row
   * @param {object} rowData Row data
   */
  _renderRowView(rowData) {
    return (
      <TouchableHighlight
        style={styles.row}
        underlayColor='#c8c7cc'
        onPress={() => this._onPress(rowData)}
      >  
        <Text>{rowData}</Text>
      </TouchableHighlight>
    );
  },

  render() {
    return (
      <View style={styles.container}>
        <View style={styles.navBar} />
        <GiftedListView
          rowView={this._renderRowView}
          onFetch={this._onFetch}
          firstLoader={true} // display a loader for the first fetching
          pagination={true} // enable infinite scrolling using touch to load more
          refreshable={true} // enable pull-to-refresh for iOS and touch-to-refresh for Android
          withSections={false} // enable sections
          customStyles={{
            refreshableView: {
              backgroundColor: '#eee',
            },
          }}

          PullToRefreshViewAndroidProps={{
            colors: ['#ff0000', '#00ff00', '#0000ff'],
            progressBackgroundColor: '#c8c7cc',
          }}
        />
      </View>
    );
  }
});

var styles = {
  container: {
    flex: 1,
    backgroundColor: '#FFF',
  },
  navBar: {
    height: 64,
    backgroundColor: '#CCC'
  },
  row: {
    padding: 10,
    height: 44,
  },
};

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

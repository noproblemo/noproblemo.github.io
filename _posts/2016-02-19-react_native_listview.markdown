---
layout: post
title: ListView
---
{% include JB/setup %}

# ListView

 변경되는 데이터의 리스트를 효율적으로 세로로 스크롤될 수 있게 표현해준다.  
 마치 IOS Table View Controller와 같이.

## Qick and GOGO

 ListView를 표현하는데 있어 꼭 필요한 것은 DataSource를 인스턴스해야 한다는것. 

~~~javascript
getInitialState: function() {
  var ds = new ListView.DataSource({rowHasChanged: (r1, r2) => r1 !== r2});
  return {
    dataSource: ds.cloneWithRows(['row 1', 'row 2']),
  };
},

render: function() {
  return (
    <ListView
      dataSource={this.state.dataSource}
      renderRow={(rowData) => <Text>{rowData}</Text>}
    />
  );
},
~~~

## ListView.DataSource

> DataSource 의 구조를 알아야 하는데.. 해당 문서는 아직 없다.  
> 참고할 만한 사이트는  
> [Section headers in React Native ListView Components](http://richardkho.com/section-headers-in-react-native-listview-components/)와 [React Native ListView with Section Headers](http://moduscreate.com/react-native-listview-with-section-headers/) 이 있다.  
> [ListViewDataSource](https://github.com/facebook/react-native/blob/951b5f951746b42a7b3782c239a2aea2079b8aba/Libraries/CustomComponents/ListView/ListViewDataSource.js) 소스를 보면 나름 주석이 달려 있다.  

 ListView는 2가지 형태가 있다.  
 그냥 list만 보여주는 것과, section 형태로 보여주는 것.

 그래서 DataSource의 구조는 2가지 형태로 작성할 수 있는데... 소스에 달려있는 주석을 참고하여 구조를 잡고, 위 링크들을 참고하여 구현을 참고한다. 



~~~javascript
/**
 * Provides efficient data processing and access to the
 * `ListView` component.  A `ListViewDataSource` is created with functions for
 * extracting data from the input blob, and comparing elements (with default
 * implementations for convenience).  The input blob can be as simple as an
 * array of strings, or an object with rows nested inside section objects.
 *
 * To update the data in the datasource, use `cloneWithRows` (or
 * `cloneWithRowsAndSections` if you care about sections).  The data in the
 * data source is immutable, so you can't modify it directly.  The clone methods
 * suck in the new data and compute a diff for each row so ListView knows
 * whether to re-render it or not.
 *
 * In this example, a component receives data in chunks, handled by
 * `_onDataArrived`, which concats the new data onto the old data and updates the
 * data source.  We use `concat` to create a new array - mutating `this._data`,
 * e.g. with `this._data.push(newRowData)`, would be an error. `_rowHasChanged`
 * understands the shape of the row data and knows how to efficiently compare
 * it.
 *
 * ```
 * getInitialState: function() {
 *   var ds = new ListViewDataSource({rowHasChanged: this._rowHasChanged});
 *   return {ds};
 * },
 * _onDataArrived(newData) {
 *   this._data = this._data.concat(newData);
 *   this.setState({
 *     ds: this.state.ds.cloneWithRows(this._data)
 *   });
 * }
 * ```
 */

class ListViewDataSource {
 /**
   * You can provide custom extraction and `hasChanged` functions for section
   * headers and rows.  If absent, data will be extracted with the
   * `defaultGetRowData` and `defaultGetSectionHeaderData` functions.
   *
   * The default extractor expects data of one of the following forms:
   *
   *      { sectionID_1: { rowID_1: <rowData1>, ... }, ... }
   *
   *    or
   *
   *      { sectionID_1: [ <rowData1>, <rowData2>, ... ], ... }
   *
   *    or
   *
   *      [ [ <rowData1>, <rowData2>, ... ], ... ]
   *
   * The constructor takes in a params argument that can contain any of the
   * following:
   *
   * - getRowData(dataBlob, sectionID, rowID);
   * - getSectionHeaderData(dataBlob, sectionID);
   * - rowHasChanged(prevRowData, nextRowData);
   * - sectionHeaderHasChanged(prevSectionData, nextSectionData);
   */
  constructor(params: ParamType) {
~~~

내용을 간추리면  

* A `ListViewDataSource` is created with functions for extracting data from the input blob.  
* The input blob can be as simple as an array of strings, or an object with rows nested inside section objects  
* To update the data in the datasource, use `cloneWithRows` (or   `cloneWithRowsAndSections` if you care about sections).  
* The data in the data source is immutable, so you can't modify it directly.  
* The clone methods suck in the new data and compute a diff for each row so ListView knows whether to re-render it or not.  

section 관련 내용은 **모든 주석이** 알짜네.  

~~~javascript
/**
   * You can provide custom extraction and `hasChanged` functions for section
   * headers and rows.  If absent, data will be extracted with the
   * `defaultGetRowData` and `defaultGetSectionHeaderData` functions.
   *
   * The default extractor expects data of one of the following forms:
   *
   *      { sectionID_1: { rowID_1: <rowData1>, ... }, ... }
   *
   *    or
   *
   *      { sectionID_1: [ <rowData1>, <rowData2>, ... ], ... }
   *
   *    or
   *
   *      [ [ <rowData1>, <rowData2>, ... ], ... ]
   *
   * The constructor takes in a params argument that can contain any of the
   * following:
   *
   * - getRowData(dataBlob, sectionID, rowID);
   * - getSectionHeaderData(dataBlob, sectionID);
   * - rowHasChanged(prevRowData, nextRowData);
   * - sectionHeaderHasChanged(prevSectionData, nextSectionData);
   */
~~~
  
따라서,  
`DataSource`의 구조는 어느정도 그려지는데..

Contructor는 아래의 4개의 params을 받고, **any** 라니까, 꼭 다 있어야 할 필욘 없어 보임.

 * `getRowData(dataBlob, sectionID, rowID);`
 * `getSectionHeaderData(dataBlob, sectionID);`
 * `rowHasChanged(prevRowData, nextRowData);`
 * `sectionHeaderHasChanged(prevSectionData, nextSectionData);`

여기서, section의 headers와 rows를 위해 custom extraction 함수와 `hasChnaged`의 함수들을 제공할 수 있으며 만약 제공되지 않는다면 `defaultGetRowData`와 `defaultGetSectionHeaderData` 함수가 담당할 것이다. 

`default` 함수들은 데이터 구조를 다음의 형태로 간주한다. 

* `{ sectionID_1: { rowID_1: <rowData1>, ... }, ... }`
* `{ sectionID_1: [ <rowData1>, <rowData2>, ... ], ... }`
* `[ [ <rowData1>, <rowData2>, ... ], ... ]`

__이에 예상컨데, section의 데이터 형태는 아마 다음과 같지 않을까?__

~~~javascript
var sectionData = {
    '일반' : [
        {'일반row1':{}},
        {'일반row2':{}}
    ],
    'app' : [
        {'appRow1':{}},
        {'appRow2':{}}
    ]
}
~~~

하지만, 아래와 같은 **Error** 이 난다. 

~~~javascript 
[warn][tid:com.facebook.React.JavaScript] Objects are not valid as a React child (found: object with keys {button, value}). If you meant to render a collection of children, use an array instead or wrap the object using createFragment(object) from the React add-ons. Check the render method of `Text`.
~~~

다시 `Constructor`를 훑어봤다. 

~~~javascript
constructor(params: ParamType) {
    invariant(
      params && typeof params.rowHasChanged === 'function',
      'Must provide a rowHasChanged function.'
    );
    this._rowHasChanged = params.rowHasChanged;
    this._getRowData = params.getRowData || defaultGetRowData;
    this._sectionHeaderHasChanged = params.sectionHeaderHasChanged;
    this._getSectionHeaderData =
      params.getSectionHeaderData || defaultGetSectionHeaderData;

    this._dataBlob = null;
    this._dirtyRows = [];
    this._dirtySections = [];
    this._cachedRowCount = 0;

    // These two private variables are accessed by outsiders because ListView
    // uses them to iterate over the data in this class.
    this.rowIdentities = [];
    this.sectionIdentities = [];
  }
~~~

그리고, 기본 함수들도..

~~~javascript 
var invariant = require('invariant');
var isEmpty = require('isEmpty');
var warning = require('warning');

function defaultGetRowData(
  dataBlob: any,
  sectionID: number | string,
  rowID: number | string
): any {
  return dataBlob[sectionID][rowID];
}

function defaultGetSectionHeaderData(
  dataBlob: any,
  sectionID: number | string
): any {
  return dataBlob[sectionID];
}
~~~

문제는 section data의 구조는 어느정도 맞는데, rowData의 구조가 애매해서 알 길이 없다.  
이 부분에 대해 [React Native ListView with Section Headers](http://moduscreate.com/react-native-listview-with-section-headers/) 에 어느정도 나와 있지만, 데이터를 다시 만들어야 하는 부분이라서, 도움이 되질 않았다.  
다시, 에러 내용을 확인하고 `object using createFragment(object) from the React add-ons` 이 부분에 대해 힌트를 얻어 다음과 같이 데이터 구조를 바꾸었고 제대로 랜더링이 되었다. 

~~~javascript
var sectionData = {
    '일반' : { 
        '일반row1':React.addons.createFragment({}),
        '일반row2':React.addons.createFragment({})
    },
    'app' : {
        'appRow1':React.addons.createFragment({}),
        'appRow2':React.addons.createFragment({})
    }
}
~~~

## 결론

ListView를 그냥 사용하려면 데이터 구조는 크게 문제가 되질 않지만, header와 같이 사용하려면 다른 데이터 구조를 사용해야 하는데, 일반적인 json 구조가 ListView의 `cloneWithRowsAndSections` 메소드에서 사용하는 구조와 맞지않아 custom function을 사용하여 데이터 구조를 만든다는 것.

따라서, json 구조를 (rowData안에 row가 child로 여러개 가지고 있을 경우) 바로 사용할 수 없다는 것. 





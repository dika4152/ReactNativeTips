# LOAD MORE IN FLATLIST

For implementing loadmore in Flatlist

1. make the state for loadmore state

2. make a function that gonna use for fetching more data with the params like the code below, call the api in this function too :

```
  const loadMoreData = ({ distanceFromEnd }: { distanceFromEnd: number }) => {
    if (data?.page_info.has_next_page && distanceFromEnd < 10) {
      getMorePortofolio({
        data,
        searchBy: search || '',
        setData,
        setLoad: setLoadMore,
        setError
      });
    }
  };
```

3. now use the flatlist props, "onEndReach" that put the loadMore function in this props and "onEndReachTreshold" with value 0.01. Here is the example: 

```
      <FlatList
        data={data?.contents}
        extraData={data?.contents}
        contentContainerStyle={{
          padding: 20
        }}
        style={{
          alignSelf: 'center'
        }}
        refreshControl={<RefreshControl refreshing={load} onRefresh={() => getPortofolio({
          setData,
          setLoad,
          setError
        })} />}
        onEndReached={loadMoreData}
        onEndReachedThreshold={0.01}
        />
 ```
 
 4. (Optional) use the flatlist props for load more ui, put the UI in the props "ListFooterComponent". Here is the example:
 ```
      <FlatList
        data={data?.contents}
        extraData={data?.contents}
        contentContainerStyle={{
          padding: 20
        }}
        style={{
          alignSelf: 'center'
        }}
        refreshControl={<RefreshControl refreshing={load} onRefresh={() => getPortofolio({
          setData,
          setLoad,
          setError
        })} />}
        onEndReached={loadMoreData}
        onEndReachedThreshold={0.01}
        ListFooterComponent={() => {
          if (loadMore) return (<CourseListPlaceholder />);
          return null
        }}
        />
  ```

# ReactNativeTips

## 1. loadMore FlatList in ScrollView
make a state onEndReach with boolean type.

in ScrollView, use onScroll nativeEvent to measure the position of the shown layout.

update onEndReach to true when closing to end of the layout, and update again onEndReach to false when away from the end of the layout.

if you are using regular ScrollView, use onScroll like this : 
```
onScroll={(e) => {
  const { layoutMeasurement, contentOffset, contentSize } = e.nativeEvent
  const paddingToright = 20;
  if (layoutMeasurement.height + contentOffset.y >= contentSize.height - paddingToright) {
    setOnEndReach(true)
  } else {
    setOnEndReach(false)
  }
}}
```

if you are using Animated ScrollView, use onScroll like this :  
```
onScroll={Animated.event(
  [{ nativeEvent: { contentOffset: { y: scrollY } } }],
  {
    useNativeDriver: true,
    listener: (e) => {
      const { layoutMeasurement, contentOffset, contentSize } = e.nativeEvent
      const paddingToright = 20;
      if (layoutMeasurement.height + contentOffset.y >= contentSize.height - paddingToright) {
        setOnEndReach(true)
      } else {
        setOnEndReach(false)
      }
    }
  }
)}
```

and now use the onEndReach to trigger loadMore in FlatList

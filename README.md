# ReactNativeTips

## 1. loadMore FlatList in ScrollView
make a state endReach with boolean type.

in ScrollView, use onScroll nativeEvent to measure the position of the shown layout.

update endReach to true when closing to end of the layout, and update again endReach to false when away from the end of the layout.

if you are using regular ScrollView, use onScroll like this : 
```
onScroll={(e) => {
  const { layoutMeasurement, contentOffset, contentSize } = e.nativeEvent
  const paddingToright = 20;
  if (layoutMeasurement.height + contentOffset.y >= contentSize.height - paddingToright) {
    setEndReach(true)
  } else {
    setEndReach(false)
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
        setEndReach(true)
      } else {
        setEndReach(false)
      }
    }
  }
)}
```

and now use the endReach to trigger loadMore in FlatList

# StatusBar

## 概述

+ StatusBar 是用来控制应用程序状态栏的组件
+ 状态栏是显示当前时间、Wi-Fi 和蜂窝网络信息、电池电量和/或其他状态图标的区域，通常位于屏幕顶部

+ 官方 API 文档地址：https://reactnative.dev/docs/statusbar

  ```js
  import React, { useState } from 'react';
  import { Button, Platform, SafeAreaView, StatusBar, StyleSheet, Text, View } from 'react-native';

  const STYLES = ['default', 'dark-content', 'light-content'];
  const TRANSITIONS = ['fade', 'slide', 'none'];

  const App = () => {
    const [hidden, setHidden] = useState(false);
    const [statusBarStyle, setStatusBarStyle] = useState(STYLES[0]);
    const [statusBarTransition, setStatusBarTransition] = useState(TRANSITIONS[0]);

    const changeStatusBarVisibility = () => setHidden(!hidden);

    const changeStatusBarStyle = () => {
      const styleId = STYLES.indexOf(statusBarStyle) + 1;
      if (styleId === STYLES.length) {
        setStatusBarStyle(STYLES[0]);
      } else {
        setStatusBarStyle(STYLES[styleId]);
      }
    };

    const changeStatusBarTransition = () => {
      const transition = TRANSITIONS.indexOf(statusBarTransition) + 1;
      if (transition === TRANSITIONS.length) {
        setStatusBarTransition(TRANSITIONS[0]);
      } else {
        setStatusBarTransition(TRANSITIONS[transition]);
      }
    };

    return (
      <SafeAreaView style={styles.container}>
        <StatusBar
          animated={true}
          backgroundColor="#61dafb"
          barStyle={statusBarStyle}
          showHideTransition={statusBarTransition}
          hidden={hidden} />
        <Text style={styles.textStyle}>
          StatusBar Visibility:{'\n'}
          {hidden ? 'Hidden' : 'Visible'}
        </Text>
        <Text style={styles.textStyle}>
          StatusBar Style:{'\n'}
          {statusBarStyle}
        </Text>
        {Platform.OS === 'ios' ? (
          <Text style={styles.textStyle}>
            StatusBar Transition:{'\n'}
            {statusBarTransition}
          </Text>
        ) : null}
        <View style={styles.buttonsContainer}>
          <Button
            title="Toggle StatusBar"
            onPress={changeStatusBarVisibility} />
          <Button
            title="Change StatusBar Style"
            onPress={changeStatusBarStyle} />
          {Platform.OS === 'ios' ? (
            <Button
              title="Change StatusBar Transition"
              onPress={changeStatusBarTransition} />
          ) : null}
        </View>
      </SafeAreaView>
    );
  };

  const styles = StyleSheet.create({
    container: {
      flex: 1,
      justifyContent: 'center',
      backgroundColor: '#ECF0F1'
    },
    buttonsContainer: {
      padding: 10
    },
    textStyle: {
      textAlign: 'center',
      marginBottom: 8
    }
  });

  export default App;
  ```


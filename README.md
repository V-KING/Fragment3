1. 如果提示需要初始化
会自动的初始化位null
这样肯定是不正确的，怎么能是null呢，所以初始化的肯定是一个接口类

2. 如果wifi没有开起来:并不会提示你wifi没开

3. 当连接断掉后，发起连接方就会挂掉。
原因：监听器那里，mReceiver.getPeerDevices().get(0)是没有东西的。
所以；要在点击的时候，也要发现peers。


# 广播
http://www.cnblogs.com/qianlifeng/archive/2011/03/06/1972305.html
1. 广播相当于发送的是intent
```java
Intent intent = new Intent();  //Itent就是我们要发送的内容
intent.putExtra("data", "this is data from broadcast "+Calendar.getInstance().get(Calendar.SECOND));  
intent.setAction(flag);   //设置你这个广播的action，只有和这个action一样的接受者才能接受者才能接收广播
sendBroadcast(intent);   //发送广播
```

2. 接收方代码如下：
```java
String action = intent.getAction();
if (WifiP2pManager.WIFI_P2P_STATE_CHANGED_ACTION.equals(action)) {
	//dosometing
}
```
3. sendBroadcast

## 作用：
1. 实现了不同的程序之间的数据传输与共享
2. 起到了一个通知的作用，比如在service中要通知主程序，更新主程序的UI等。因为service是没有界面的，所以不能直接获得主程序中的控件，这样我们就只能在主程序中实现一个广播接受者专门用来接受service发过来的数据和通知了

## 相关function
String action = intent.getAction();
if (WifiP2pManager.WIFI_P2P_STATE_CHANGED_ACTION.equals(action)) {}

int state = intent.getIntExtra(WifiP2pManager.EXTRA_WIFI_STATE, -1);//intent中没有就返回-1


# 类之间继承 和 强制转换
新建类之前考虑继承哪个类？实现哪个接口，在用到某个接口的时候就可以将类强制转换成接口，让其他函数使用

# ListFragment
setListAdapter(new WiFiPeerListAdapter(getActivity(), R.layout.row_devices, peers));

adapter的view要绑定的view就是getView?

# Fragment
1. 和activity一样也是有生命周期
2. 不同的是你要在onCreateView() 函数中define你的额layout
3. 不管是Activity还是Fragment都是有一个借口函数onSaveInstanceState(Bundle outState)

# Bundle
1. Fragment和Activity都是可以用Bundle来传递数据
2. 不管是Activity还是Fragment都是有一个借口函数onSaveInstanceState(Bundle outState)


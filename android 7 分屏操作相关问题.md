


[多窗口生命周期 官档](https://developer.android.com/guide/topics/ui/multi-window.html?hl=zh-cn#lifecycle)


> 进行分屏操作, activity 生命周期发生变化

1. 长按(口), Activity首先调用onMultiWindowChanged->onPause->onStop->onDestroy->onCreate->onStart- >onResume->onPause(焦点切入到另一屏)
2. 来回切焦点(onPause->onResume来回交替, 这就证明了, 如果是播放类的app, 暂停不能放在onPause里面)
3. 来回拖动窗口大小当拖到1/3, 或者2/3之处, 生命周期都是销毁再重启然后再进入到onPause或者onResume(取决于是否有焦点)
4. 分屏模式进入到桌面如果有焦点则调用onPause, 没有焦点则不发生生命周期的变化!








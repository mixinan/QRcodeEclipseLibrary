#给Eclipse 中的项目增加“扫描二维码”功能

>点击上方**绿色按钮**，选择**Downloa ZIP**，下载本目录到你的电脑。
>
![点击绿色按钮下载](https://github.com/mixinan/1603/blob/master/download.png)

##一、导入资源


1. 把 zxing.jar 文件放在 libs 目录下
2. 把 ids.xml 文件放在 res/values 目录下
3. 把三张图片放在 drawable-hdpi 目录下
4. 把 activity_capture.xml 文件放在 res/layout 目录下
5. 把 raw 文件夹放在 res 目录下
6. 把 zxing 文件夹放在 src 目录下
7. 打开报错的类文件，Ctrl + Shift + O 替换R为你项目的R



##二、配置清单文件


添加权限：

	<uses-permission android:name="android.permission.CAMERA"/>
    <uses-permission android:name="android.permission.VIBRATE"/>


注册“扫描界面”的activity（里面的属性值，最好让系统自动提示，防止出错）：

	<activity android:name="zxing.activity.CaptureActivity"/>




##三、在代码中调用

在需要扫描二维码的地方（一般是点击按钮），执行如下代码，跳转到扫描界面：

	Intent intent = new Intent(MainActivity.this, CaptureActivity.class);
	startActivityForResult(intent, 0);

扫描成功以后，会跳转回来，并带回解析结果：

	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		if(resultCode==RESULT_OK){
			Bundle bundle=data.getExtras();
			String result=bundle.getString("result");

			// 把扫描并解析后的结果，显示在相应的 textView 上，或进行其它操作
			tv.setText(result);
		}
	}



---
以上可以完成解析二维码图片的功能。可扫描下方图片测试。

![扫描测试](https://github.com/mixinan/1603/blob/master/QRcodeTest.png)

二维码生成（也很简单），可参考`慕课网`视频教程：**[扫一扫](http://www.imooc.com/learn/648)**

本文所发的 zxing 源码，移植自该视频讲师所发的适用于 studio 项目的源码。感谢。
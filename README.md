### LeakcanaryForEclipse集成
#### 1.克隆本项目与需要集成的项目放置同意路径,并eclipse加载此项目
#### 2.AndroidManifest.xml配置
	
	<!-- To store the heap dumps and leak analysis results. -->
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />

	<service
        android:name="com.squareup.leakcanary.DisplayLeakService"
        android:enabled="false" />
    
    <service
        android:name="com.squareup.leakcanary.internal.HeapAnalyzerService"
        android:enabled="false"
        android:process=":leakcanary" />

    <activity
        android:name="com.squareup.leakcanary.internal.DisplayLeakActivity"
        android:enabled="false"
        android:icon="@drawable/leak_canary_icon"
        android:label="@string/leak_canary_display_activity_label"
        android:taskAffinity="com.squareup.leakcanary.{your Application ID}"
        android:theme="@style/leak_canary_LeakCanary.Base" >
    </activity>

#### 3.在合适位置添加打开DisplayLeakActivity.java的事件

	@Override
	public boolean onCreateOptionsMenu(Menu menu) {
		getMenuInflater().inflate(R.menu.main, menu);
		return true;
	}

	@Override
	public boolean onOptionsItemSelected(MenuItem item) {
		switch (item.getItemId()) {
		case R.id.action_settings:
			startActivity(new Intent(MainActivity.this, DisplayLeakActivity.class));
			break;
		}
		return super.onOptionsItemSelected(item);
	}

#### 注:Leakcanary的具体配置详见[https://github.com/square/leakcanary](https://github.com/square/leakcanary "Leakcanary")
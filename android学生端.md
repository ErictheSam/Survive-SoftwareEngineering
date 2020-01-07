
#### android学生界面
#### 模块一:LoginAcativity:登陆
<br>

函数名|参数|函数功能
--|--|--
onCreate|Bundle savedInstanceState|创建登陆界面，初始化调用得意音通SDK的参数，初始化界面元素。
http_Login|void|新建线程调用服务器接口登陆，根据返回信息判断登陆信息是否正确
login|void|根据用户输入的密码进行登录，调用http_login向服务器进行验证。
onBackPressed|void|重写onBackPressed，禁止该页面的回退键
onLoginSuccess|void|登陆成功的操作
onLoginFailed|void|登陆失败的操作
validate|void|检查输入的用户名和密码是否合格（是否为空，长度检测，学号为数字）
onresume|void|重写resume函数，每次回退到该界面检查权限是否被允许
<br>

#### 模块二:MainActivity:课程列表界面   
函数名|参数|函数功能    
--|--|--
onCreate|Bundle savedInstanceState|初始化该用户课程列表，将获取到的课程信息通过recyclerview的adapter展示到界面
http_getcourse|void|调用服务器接口获取该用户课程列表
initData|void|初始化list，异步调用http_getcourse,并用handler机制通告主线程获取课程列表完成


#### 模块三:CourseAdapter:MainActivity的适配器  
函数名|参数|函数功能    
--|--|--
CourseAdapter|List<String> list1,List<String> list2,List<String> list3|根据参数初始化课程名字，课程老师，课程介绍
getItemCount|void|返回recyclerview的规模
onCreateViewHolder|ViewGroup parent, int viewType|返回一个新的viewHolder对象
onBindViewHolder|CourseAdapter.ViewHolder holder, int position|将对应position的课程信息绑定到viewholder，并且对每一个item进行点击监听
##### 内部类：ViewHolder,作为recyclerview的总的界面框架



#### 模块四:CheckinActivity:用户签到以及签到记录界面 
函数名|参数|函数功能    
--|--|--
onCreate|Bundle savedInstanceState|初始化界面元素以及成员变量
http_getrecord|void|调用服务器接口获取该学生该课程的所有签到记录
onResume|void|重写回退函数，每当用户重新进入该界面会调用http_getrecor函数来刷新签到记录并进行必要的权限检查，最后调用getSpeakerId来获取该用户在得意音通的声纹数据库里的唯一speakerid
getSpeakerId|void|获取用户在得意音通的声纹数据库里的唯一id
checkModel|void|查看该用户是否已经建立声纹模型
sendErrorMessage|int i,String S|发送相应编号的错误类型
showToast|Context context,String msg|在参数显示在对应界面上
showAlertDialog|String title, String msg|新建一个alterdialog，标题即为参数的title，内容即为msg
dismissAlertDialog|void|删除上述创建的alterdialog界面
checkPermissions|void|检查相应权限是否打开
onRequestPermissionsResult|int requestCode,String[] permissions,int[] grantResults|重写权限回调函数，获取相应权限
onPermissionGranted|String permission|获取GPS权限
checkGPSIsOpen|void|检查GPS权限是否打开

#### 模块五:RecordAdapter:作为checkinActivity的适配器，类似上面的CourseAdapter
函数名|参数|函数功能    
--|--|--
RecordAdapter|List<String> list1,List<String> list2,List<String> list3|根据参数初始化签到时间，签到记录，课程信息
getItemCount|void|返回recyclerview的规模
onCreateViewHolder|ViewGroup parent, int viewType|返回一个新的viewHolder对象
onBindViewHolder|CourseAdapter.ViewHolder holder, int position|将对应position的课程信息绑定到viewholder，并且对每一个item进行点击监听
##### 内部类：ViewHolder,作为recyclerview的总的界面框架

#### 模块六:Audio_Record:录音
函数名|参数|函数功能    
--|--|--
onCreate|Bundle savedInstanceState|调用init函数初始化界面以及参数
init|void|初始化界面并且调用getText函数获取声纹文本
http_verifytime|void|调用服务器接口获取当前课程的签到时间并且判断当前签到时间是否合法
getText|String intentFlag|根据是录入声纹还是声纹签到分别调用对应的获取文本的接口
getblueteeth|void|获取当前ibeacon蓝牙设备的设备信息
onresume|void|重写resume函数，当录音暂停后可以继续录音
showToast|Context context,String msg|在参数显示在对应界面上
onPause|void|暂停录音
onDestroy|void|结束录音，释放录音资源
getTrainText|void|获取声纹录入的文本
getVerifyText|void|获取声纹验证的文本
verify|byte[] voice|根据录入的声音二进制文件上传到得意音通服务器进行声纹验证
uploadVoice|int index, byte[] voice|将录入的语音上传到得意音通服务器
createModel|void|未注册声纹用户根据声纹在得意音通服务器创建声纹模型
sendErrorMessage|Handler handler, int i, String s|handler发送不同的信息
startRecord|void|开始录音
stopRecord|void|结束录音
checkPermissions|void|检查权限
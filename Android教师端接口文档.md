### TeacherActivity
功能：显示教师端课程信息及课堂列表
父类：AppCompatActivity
函数名|参数|函数功能
--|--|--
initView|void|界面初始化，绑定xml文件
http_getcourseinfo|void|通过url获取课程信息
http_getcoursetime|void|通过url获取该课程每节课堂的时间
binddata|void|绑定数据，即新建子线程调用http_getcourseinfo()和http_getcoursetime()
onCreate|Bundle savedInstanceState|@Override 创建活动
<br>
<br>

### TeacherCheckinActivity
功能：显示课堂未签到记录
父类：AppCompatActivity
函数名|参数|函数功能
--|--|--
initView|void|界面初始化，绑定xml文件
http_getabsentstudent|void|通过url获取缺席学生
binddata|void|绑定数据，即新建子线程调用http_getabsentstudent
http_addassign|int studentid|通过url为id为studentid的学生补签到
addassign|int studentid|补签到，即新建子线程调用http_addassign(int)
onActivityResult|int requestCode, int resultCode, Intent data|@Override 根据type为2的对话框活动传回的是确定还是取消决定是否补签到
onCreate|Bundle savedInstanceState|@Override 创建活动
<br>
<br>

### StudentListActivity
功能：显示课程学生列表
父类：AppCompatActivity
函数名|参数|函数功能
--|--|--
initView|void|界面初始化，绑定xml文件
http_getallstudent|void|通过url获取选修该课程的所有学生
binddata|void|绑定数据，即新建子线程调用http_getallstudent
onCreate|Bundle savedInstanceState|@Override 创建活动
<br>
<br>

### DialogActivity
父类：AppCompatActivity
属性：type，用于确定是哪种对话，type为1表示显示实到人数，2表示是否确认补签到，3表示显示课程总人数
组合：AlertDialog，此为Android Studio自带的对话框类
函数名|参数|函数功能
--|--|--
onCreate|Bundle savedInstanceState|@Override 创建活动
<br>
<br>

### GraphActivity
功能：绘制生成课堂签到饼图
父类：AppCompatActivity
组合：PieChartData，PieChartView，SliceValue，此为第三方库lecho.lib.hellocharts所有，用于画饼图及绑定数据
函数名|参数|函数功能
--|--|--
onCreate|Bundle savedInstanceState|@Override 创建活动
<br>
<br>

### Graph2Activity
功能：绘制生成课程签到情况折线图
父类：AppCompatActivity
组合：LineChartData，SimpleLineChartValueFormatter，Line，Axis，Viewport此为第三方库lecho.lib.hellocharts所有，用于画折线图及绑定数据
函数名|参数|函数功能
--|--|--
initViews|void|界面初始化，绑定xml文件
http_getcourseinfo|void|通过url获取课程信息
http_getpresentstudent|String starttime|通过url获取开始时间为starttime的课堂的到场学生人数
http_getcoursetime|void|通过url获取该课程每节课堂的时间
binddata|void|绑定数据，即新建子线程调用http_getcourseinfo、http_getpresentstudent、http_getcoursetime
initAxisXLables|void|设置x轴的显示
initAxisPoints|void|图表每个点的显示
initLineChart|void|生成折线图
onCreate|Bundle savedInstanceState|@Override 创建活动
<br>
<br>

### NameListAdapter
功能：适配StudentListActivity里的RecyclerView
父类：RecyclerView.Adapter<NameListAdapter.ViewHolder>
函数名|参数|函数功能
--|--|--
NameListAdapter|List<String> list1, List<String> list2, List<Integer> list3, int _choise|构造函数
getItemCount|void|获取列表大小
onCreateViewHolder|@NonNull ViewGroup parent, int viewType|创建ViewHolder
setOnItemClickListener|NameListAdapter.OnItemClickListener listener|激活点击监听
onBindViewHolder|@NonNull final NameListAdapter.ViewHolder holder, final int position|绑定ViewHolder
内部类：ViewHolder
其父类：RecyclerView.ViewHolder
函数名|参数|函数功能
--|--|--
ViewHolder|View itemView|构造函数
<br>
<br>

### TeacherCourseAdapter
功能：适配TeacherCheckinActivity里的RecyclerView
父类：RecyclerView.Adapter<NameListAdapter.ViewHolder>
函数名|参数|函数功能
--|--|--
NameListAdapter|List<String> list1,List<String> list3|构造函数
getItemCount|void|获取列表大小
onCreateViewHolder|@NonNull ViewGroup parent, int viewType|创建ViewHolder
setOnItemClickListener|NameListAdapter.OnItemClickListener listener|激活点击监听
onBindViewHolder|@NonNull final NameListAdapter.ViewHolder holder, final int position|绑定ViewHolder
内部类：ViewHolder
其父类：RecyclerView.ViewHolder
函数名|参数|函数功能
--|--|--
ViewHolder|View itemView|构造函数
反思：所有Adapter的构成类似，但具体实现不一样，由于没有在一开始就想好需要多个Adapter，就在实践过程里一个一个加了进去，如果用更OOP的方法会好一些，不过我们总的体量也不大，负担也没有大多少。

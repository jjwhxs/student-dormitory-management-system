### 系统介绍

基于SpringBoot和Vue实现的学生宿舍管理系统采用前后端分离的架构方式，系统设计了三种角色，分别是学生、宿舍管理员、系统管理员，每种角色拥有不同的菜单权限，学生可以在系统中进行查看当前宿舍学生人数、住宿人数、报修数量、空舍数量、查看我的宿舍、申请调宿、申请报修、查看个人信息等操作，宿舍管理员可以在系统中进行查看当前宿舍学生人数、住宿人数、报修数量、空舍数量、查看学生信息、查看楼宇信息、查看公告信息、查看房间信息、查看报修信息、查看调寝信息、访客管理、查看个人信息等操作，系统管理员可以在系统中进行查看当前宿舍学生人数、住宿人数、报修数量、空舍数量、查看学生信息、宿管信息、查看楼宇信息、查看公告信息、查看房间信息、查看报修信息、查看调寝信息、访客管理、查看所有用户信息等操作。

### 技术选型

开发工具：idea2020.3+Webstorm2020.3

运行环境：jdk1.8+maven3.6.0+MySQL5.7+nodejs14.21.3

服务端技术：Springboot+Mybatis-Plus+SpringSecurity+Fastjson

前端技术：html+css+Vue+axios+Element-UI+echarts

### 成果展示

用户登录
<img width="1910" height="1004" alt="用户登录" src="https://github.com/user-attachments/assets/72e9dfd5-16ef-4868-9071-b4a86cecb439" />

首页
<img width="1891" height="1045" alt="首页" src="https://github.com/user-attachments/assets/ff93468d-bd53-4928-aae9-b89517ee1ffe" />

用户管理->学生信息
<img width="1910" height="1045" alt="用户管理-学生信息" src="https://github.com/user-attachments/assets/042f34e0-b0d8-48e9-9363-0e80a2156bb8" />

宿舍管理->楼宇管理
<img width="1910" height="1045" alt="宿舍管理-楼宇管理" src="https://github.com/user-attachments/assets/4e7f7365-275d-41bc-a297-b1f8bd2fb5f9" />

信息管理->报修信息
<img width="1910" height="1045" alt="信息管理-报修信息" src="https://github.com/user-attachments/assets/45ea192b-2153-455a-ab05-cea1fe712029" />

申请管理->调宿申请
<img width="1910" height="1045" alt="申请管理-调宿申请" src="https://github.com/user-attachments/assets/a8a0130b-82f8-4ee5-9c9a-26caf810c1ba" />

访客管理
<img width="1910" height="1045" alt="访客管理" src="https://github.com/user-attachments/assets/366df770-8bb7-4807-8cf8-30a63db6dd15" />

个人信息
<img width="1910" height="1045" alt="个人信息" src="https://github.com/user-attachments/assets/8054e532-ddd6-4b8d-8baa-9cd4ac537ff0" />

### 源码展示

@RestController

@RequestMapping("/dormManager")

public class DormManagerController {

@Resource

private DormManagerService dormManagerService;

//宿管添加

@PostMapping("/add")

public Result<?> add(@RequestBody DormManager dormManager) {

    int i = dormManagerService.addNewDormManager(dormManager);
    if (i == 1) {
        return Result.success();
    } else {
        return Result.error("-1", "添加失败");
    }
    
}

//宿管信息更新

@PutMapping("/update")

public Result<?> update(@RequestBody DormManager dormManager) {

    int i = dormManagerService.updateNewDormManager(dormManager);
    if (i == 1) {
        return Result.success();
    } else {
        return Result.error("-1", "更新失败");
    }
    
}

//宿管删除

@DeleteMapping("/delete/{username}")

public Result<?> delete(@PathVariable String username) {

    int i = dormManagerService.deleteDormManager(username);
    if (i == 1) {
        return Result.success();
    } else {
        return Result.error("-1", "删除失败");
    }
    
}

//宿管查找

@GetMapping("/find")

public Result<?> findPage(@RequestParam(defaultValue = "1") Integer pageNum,
                          @RequestParam(defaultValue = "10") Integer pageSize,
                          @RequestParam(defaultValue = "") String search) {
                          
    Page page = dormManagerService.find(pageNum, pageSize, search);
    if (page != null) {
        return Result.success(page);
    } else {
        return Result.error("-1", "查询失败");
    }
    
}

//宿管登录

@PostMapping("/login")

public Result<?> login(@RequestBody User user, HttpSession session) {

    Object o = dormManagerService.dormManagerLogin(user.getUsername(), user.getPassword());
    if (o != null) {
        System.out.println(o);
        //存入session
        session.setAttribute("Identity", "dormManager");
        session.setAttribute("User", o);
        return Result.success(o);
    } else {
        return Result.error("-1", "用户名或密码错误");
    }
    
}

}

### 账号地址及其它说明

1、地址说明

登录页：localhost:8080

2、账号说明

学生：stu1/123456

宿舍管理员：dorm1/123456

系统管理员：admin/123456

3、目录结构展示

<img width="435" height="177" alt="目录结构展示" src="https://github.com/user-attachments/assets/619d3619-29e9-4e58-ba79-2ba8483bb310" />

4、项目结构展示

<img width="1701" height="949" alt="项目结构展示" src="https://github.com/user-attachments/assets/730e2929-b7e7-4664-835a-54a6244058a1" />

5、运行步骤

1）创建数据库、导入sql脚本

2）修改application.properties中的数据库配置文件，启动服务端

3）在frontend目录下打开cmd，执行npm install下载依赖

4）下载完毕后启动前端npm run serve，访问端口

### 获取方式(可远程调试)

访问链接(在浏览器中手动输入下图中的地址)：

<img width="1075" height="136" alt="链接" src="https://github.com/user-attachments/assets/ed419870-40a8-4c92-9498-5cc2455449cb" />

若资源获取失败，可添加happy35596339(vx)或1204901965(qq)进行交流

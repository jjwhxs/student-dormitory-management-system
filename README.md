### 系统介绍

基于SpringBoot和Vue实现的学生宿舍管理系统采用前后端分离的架构方式，系统设计了三种角色，分别是学生、宿舍管理员、系统管理员，每种角色拥有不同的菜单权限，学生可以在系统中进行查看当前宿舍学生人数、住宿人数、报修数量、空舍数量、查看我的宿舍、申请调宿、申请报修、查看个人信息等操作，宿舍管理员可以在系统中进行查看当前宿舍学生人数、住宿人数、报修数量、空舍数量、查看学生信息、查看楼宇信息、查看公告信息、查看房间信息、查看报修信息、查看调寝信息、访客管理、查看个人信息等操作，系统管理员可以在系统中进行查看当前宿舍学生人数、住宿人数、报修数量、空舍数量、查看学生信息、宿管信息、查看楼宇信息、查看公告信息、查看房间信息、查看报修信息、查看调寝信息、访客管理、查看所有用户信息等操作。

### 技术选型

开发工具：idea2020.3+Webstorm2020.3

运行环境：jdk1.8+maven3.6.0+MySQL5.7+nodejs14.21.3

服务端技术：Springboot+Mybatis-Plus+SpringSecurity+Fastjson

前端技术：html+css+Vue+axios+Element-UI+echarts

### 成果展示

用户登录 输入图片说明

首页 输入图片说明

用户管理->学生信息 输入图片说明

宿舍管理->楼宇管理 输入图片说明

信息管理->报修信息 输入图片说明

申请管理->调宿申请 输入图片说明

访客管理 输入图片说明

个人信息 输入图片说明

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

输入图片说明

4、项目结构展示

输入图片说明

5、运行步骤

1）创建数据库、导入sql脚本

2）修改application.properties中的数据库配置文件，启动服务端

3）在frontend目录下打开cmd，执行npm install下载依赖

4）下载完毕后启动前端npm run serve，访问端口

### 获取方式(可远程调试)

访问链接(在浏览器中手动输入下图中的地址)： 输入图片说明

若资源获取失败，可添加happy35596339(vx)或1204901965(qq)进行交流

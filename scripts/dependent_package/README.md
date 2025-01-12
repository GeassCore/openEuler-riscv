##### 1. 实现功能

该自动化脚本实现的功能输入需要查询的包，生成与所输入包存在依赖和被依赖关系的所有包的关系图

##### 2. 文档说明

getspec.py  执行该文件可获取openEuler-riscv的所有包的spec，获取到的spec存放在specfile.json中

specfile.json  存放openEuler-riscv的所有包的spec信息

getbuildrequires.py 执行改文件可根据spec文件获取所有包的依赖包，获得的依赖包存放在buildrequiresfile.json中

buildrequiresfile.json 存放所有包的依赖包的信息

inputfile.json 提供给用户输入需要查询的包，可输入多个

run.py 执行该文件可生成所要查询包的（inputfile.json里输入的包）相关依赖和被依赖包的关系图（pdf文档）

graph-output 生成的关系图存放在该文件夹中

requirements.txt 执行该文件夹中的py档需要安装的python第三方库

getobs.py 执行该文件会抓取https://build.openeuler.org/project/monitor/openEuler:Mainline:RISC-V 界面的unresolvable和succeeded状态的包,并将获得这些包存放在packagelist.json中

packagelist.json 存放getobs.py中获取的unresolvable和succeeded状态的包

getfailrequires.py 生成packagelist.xlsx report

packagelist.xlsx 第一个sheet内容是https://build.openeuler.org/project/monitor/openEuler:Mainline:RISC-V 界面succeeded状态的包；第二个sheet内容是unresolvable状态的包的所有依赖包；将所有unresolvable状态的包的依赖包和所有succeeded状态的包的依赖包用自动化做了对比(没有去掉-dev，pkgconfig等后缀)，这样对比出来的没有在succeeded中的依赖包存放在第三个sheet

##### 3. 使用方法

在inputfile.json中写入要查询的包，保存，然后执行run.py文件，就可以生成包的依赖关系图了。这里需要注意：

1）在inputfile.json中写入要查询的包，可一次输入多个。建议一次不要输入太多包，否则生成的图在显示一张图上可能会模糊不清

2）由于查询所使用的buildrequiresfile.json中存储的包名分别是spec文件中的Name和BuildRequires栏位的包名，所以写入需要查询的包名必须要与spec文件中的Name和BuildRequires栏位的包名保持一致，否则会查询不到

3）运行前需要安装requirements.txt里python第三方库，执行pip install -r requirements.txt可一次性安装，另外由于依赖关系图是由graphviz生成的，所以还需要安装graphviz程序，graphviz安装程序下载地址http://www.graphviz.org/download/

4）将constant.py文件中的'your gitee account token'换成使用者gitee账号对应的token(个人设置->私人令牌)






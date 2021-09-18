### Node获取系统环境变量

process是node的全局模块，提供当前Node进程信息并对其进行控制。我们可以在Node环境中通过process来设置或者获取进程的相关信息，比如获取系统的环境变量。我们新建一个process.js文件吧。然后在命令行（其实就是node环境）执行它：

process.js,内容如下：

```javascript
console.log(process.env);
```

有如下的输出：

```bash
{ ALLUSERSPROFILE: 'C:\\ProgramData',
  APPDATA: 'C:\\Users\\ya596\\AppData\\Roaming',
  CommonProgramFiles: 'C:\\Program Files\\Common Files',
  'CommonProgramFiles(x86)': 'C:\\Program Files (x86)\\Common Files',
  CommonProgramW6432: 'C:\\Program Files\\Common Files',
  COMPUTERNAME: 'SUCHCL',
  ComSpec: 'C:\\WINDOWS\\system32\\cmd.exe',
  DriverData: 'C:\\Windows\\System32\\Drivers\\DriverData',
  egg_env: 'test',
  FPS_BROWSER_APP_PROFILE_STRING: 'Internet Explorer',
  FPS_BROWSER_USER_PROFILE_STRING: 'Default',
  HOMEDRIVE: 'C:',
  HOMEPATH: '\\Users\\ya596',
  LOCALAPPDATA: 'C:\\Users\\ya596\\AppData\\Local',
  LOGONSERVER: '\\\\SUCHCL',
  NUMBER_OF_PROCESSORS: '12',
  NVM_HOME: 'C:\\app\\nvm',
  NVM_SYMLINK: 'C:\\Program Files\\nodejs',
  OneDrive: 'C:\\Users\\ya596\\OneDrive',
  OneDriveConsumer: 'C:\\Users\\ya596\\OneDrive',
  OS: 'Windows_NT',
  Path:
   'C:\\Program Files (x86)\\VMware\\VMware Player\\bin\\;C:\\Windows\\system32;C:\\Windows;C:\\Windows\\System32\\Wbem;C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\;C:\\Windows\\System32\\OpenSSH\\;C:\\Program Files (x86)\\NVIDIA Corporation\\PhysX\\Common;C:\\Program Files\\NVIDIA Corporation\\NVIDIA NvDLISR;C:\\app\\Git\\cmd;D:\\NodeJs\\node_global;C:\\app\\nvm;C:\\Program Files\\nodejs;D:\\app\\platform-tools;D:\\app\\Yarn\\bin\\;C:\\WINDOWS\\system32;C:\\WINDOWS;C:\\WINDOWS\\System32\\Wbem;C:\\WINDOWS\\System32\\WindowsPowerShell\\v1.0\\;C:\\WINDOWS\\System32\\OpenSSH\\;C:\\Users\\ya596\\AppData\\Local\\Programs\\Python\\Python39\\Scripts\\;C:\\Users\\ya596\\AppData\\Local\\Programs\\Python\\Python39\\;C:\\Users\\ya596\\AppData\\Local\\Microsoft\\WindowsApps;C:\\Users\\ya596\\AppData\\Roaming\\npm;D:\\app\\Fiddler;C:\\Users\\ya596\\AppData\\Local\\Yarn\\bin;D:\\app\\Microsoft VS Code\\bin;C:\\Users\\ya596\\AppData\\Local\\Microsoft\\WindowsApps',
  PATHEXT: '.COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC;.CPL',
  PROCESSOR_ARCHITECTURE: 'AMD64',
  PROCESSOR_IDENTIFIER: 'Intel64 Family 6 Model 165 Stepping 2, GenuineIntel',
  PROCESSOR_LEVEL: '6',
  PROCESSOR_REVISION: 'a502',
  ProgramData: 'C:\\ProgramData',
  ProgramFiles: 'C:\\Program Files',
  'ProgramFiles(x86)': 'C:\\Program Files (x86)',
  ProgramW6432: 'C:\\Program Files',
  PSModulePath:
   'C:\\Users\\ya596\\Documents\\WindowsPowerShell\\Modules;C:\\Program Files\\WindowsPowerShell\\Modules;C:\\WINDOWS\\system32\\WindowsPowerShell\\v1.0\\Modules',
  PUBLIC: 'C:\\Users\\Public',
  SystemDrive: 'C:',
  SystemRoot: 'C:\\WINDOWS',
  TEMP: 'C:\\Users\\ya596\\AppData\\Local\\Temp',
  TMP: 'C:\\Users\\ya596\\AppData\\Local\\Temp',
  USERDOMAIN: 'SUCHCL',
  USERDOMAIN_ROAMINGPROFILE: 'SUCHCL',
  USERNAME: 'ya596',
  USERPROFILE: 'C:\\Users\\ya596',
  windir: 'C:\\WINDOWS',
  WSLENV: 'WT_SESSION::WT_PROFILE_ID',
  WT_PROFILE_ID: '{61c54bbd-c2c6-5271-96e7-009a87ff44bf}',
  WT_SESSION: 'f4cbd8d6-d227-46e1-8114-4a919c8f9a46',
  ZES_ENABLE_SYSMAN: '1' }
```

从输出信息可以看出输出的是一个对象，那么如果我们想获取其中的某个具体的变量，就可以直接通过对象访问属性的方式获取就可以了，比如我们获取其中的egg_env，这个是我自定义的一个系统环境变量，本地开发时用的，那么我就可以直接通过process.env.egg_env,看效果：

```javascript
    console.log(process.env.egg_env); // test
```

通过node来获取系统环境变量还是很方便的，我们可以根据环境变量做很多项目的事情，如本地开发环境、测试服务器的测试环境、沙盒服务器的沙盒环境、线上的生产环境，我们不需要做任何代码上的区分，只需要在服务器上将环境变量标识符设置成对应的值即可。
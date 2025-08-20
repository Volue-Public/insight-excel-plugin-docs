.. _troubleshooting:

Troubleshooting
===============

*******************************************
Change your Microsoft Office update channel
*******************************************

#. Close any Office instance.  
#. Create a file called Monthly_Channel.bat with the following text:

    .. code-block:: shell

        setlocal 
        reg query HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\ /v CDNBaseUrl if %errorlevel%==0 (goto SwitchChannel) else (goto End) 
        :SwitchChannel 
        reg add HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration /v CDNBaseUrl /t REG_SZ /d "https://officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60" /f 
        reg delete HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration /v UpdateUrl /f 
        reg delete HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration /v UpdateToVersion /f 
        reg delete HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Updates /v UpdateToVersion /f 
        reg delete HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Office\16.0\Common\OfficeUpdate\ /f 
        :End 
        Endlocal

#. Run the Monthly_Channel.bat file as administrators, by right clicking on the file and choose run as administrator.

    .. image:: /_static/images/excel-img-run-as-administrations.png
       :width: 250

#. After running the file, open excel, check if you have the Monthly channel available. It can take some time until it is available. Go to account and check if you have as the image below:

    .. image:: /_static/images/excel-plugin-monthly-channel.png
       :width: 500

#. Run the office update by clicking Update Options > Update now. 

    .. image:: /_static/images/excel-plugin-update-office.png
       :width: 350
       
You can find out more on:  https://docs.microsoft.com/en-us/office365/troubleshoot/administration/switch-channel-for-office-365

.. _otherInstallMethods:

**************************
Other installation methods
**************************

There are two other ways to install the add-in that have worked for other clients that avoid the need of using the MS Store:

#. Office 365 alternative
    Make the add-in available on your Office 365 managed add-ins. 
    It can be configured for only one user or for multiple users. 
    It will appear on the Admin Managed tab of the Add-ins button. 
    You will need to import our manifest (:download:`Download manifest </WAPIExcelPlugin.xml>`) on to your company’s Office Admin console.

    Here is also Microsoft help link: 
    https://docs.microsoft.com/en-us/office/dev/add-ins/publish/centralized-deployment

#. Sideload alternative:
    You create a network share where you place the manifest (:download:`Download manifest </WAPIExcelPlugin.xml>`). 
    It can be an existing shared folder that different users can access or a shared folder created on a personal computer for only one user. 
    Define the shared folder as a trusted catalog. 

    Detail instructions here (We recommend the video from the step where you already have the manifest file):
    https://docs.microsoft.com/en-us/office/dev/add-ins/testing/create-a-network-shared-folder-catalog-for-task-pane-and-content-add-ins

*********************************
IE11 Local storage access denied
*********************************

This happens when you are still using IE11 as your Office browser and you get a blank screen when opening the Add-in. 

.. note::
    The browser depends on your OS and Office version. Verify the list here: https://docs.microsoft.com/en-us/office/dev/add-ins/concepts/browsers-used-by-office-web-add-ins

You can debug the issue using the tool F12. To learn how to use this tool check: https://docs.microsoft.com/en-us/office/dev/add-ins/testing/debug-add-ins-using-f12-developer-tools-on-windows-10
If you see an *An internal error has occurred in the Microsoft Internet Extension*, you can follow the solutions below:

1. Close IE and Excel and run this command:

.. code-block:: sh

    icacls %userprofile%\Appdata\LocalLow /t /setintegritylevel (OI)(CI)L

2. If it is still not working, open regedit and delete the following two folder from the registry:

.. code-block:: yaml

    Computer\HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\5.0\Cache\Extensible Cache
    Computer\HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\5.0\LowCache\Extensible Cache

3. If it is still not working, delete the entire Internet Explorer folder from the registry:

.. code-block:: sh

    Computer\HKEY_CURRENT_USER\Software\Microsoft\Internet Explorer

More information here: 
https://stackoverflow.com/questions/48331783/ie-11-office-js-access-is-denied-trying-to-use-localstorage

*********************************
Browser version is not supported
*********************************

 .. image:: /_static/images/excel-plugin-browsers-not-supported.png
       :width: 250

Excel Plugin uses a browser either Internet Explorer or Edge. If you receive a warning that the browser is not supported, it may indicate that you need to install IE or Edge, depending on your MS Office version and Windows version. 
Please check the table on `this site <https://docs.microsoft.com/en-us/office/dev/add-ins/concepts/browsers-used-by-office-web-add-ins>`__  to show which browser is used. 

If you have Windows 10 and want to install IE, go to **Windows Features** and select **Turn Windows features on or off**. 

More information: https://docs.microsoft.com/en-us/office/dev/add-ins/concepts/browsers-used-by-office-web-add-ins 

************************************
App crashes after new release
************************************

Sometimes after releasing new updates on the app, the static files, such as Javascript, HTML, and CSS, do not get reloaded. Here an example view on a missing CSS file:  

 .. image:: /_static/images/excel-plugin-missing-style-cache.png
       :width: 250

To solve the issue, you should clear up the browser's cache. Which browser the app is using in your machine can be referred to the part above (Browser version is not supported). If the cache is not successfully cleared, please run the command below in a Command Prompt: 

.. code-block:: Bash

    del /s /f /q %LOCALAPPDATA%\Packages\Microsoft.Win32WebViewHost_cw5n1h2txyewy\AC\#!123\INetCache\

More information: https://docs.microsoft.com/en-us/office/dev/add-ins/testing/troubleshoot-development-errors#changes-to-static-files-such-as-javascript-html-and-css-do-not-take-effect
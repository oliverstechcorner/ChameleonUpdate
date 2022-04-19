# Chameleon Update Server
You've directly visited the Chameleon Update Server. 

This domain is used allow [Windows Chameleon](https://winchameleon.tk) to check for updates.

## How the system works
The update system is a fairly simple batch script, of which connects to the corrosponding page on this domain and returns with either 'latest' or 'notlatest'.

The API link is: `http://update.winchameleon.tk/check/x.xx/latest.txt`
where x.xx is your requested version to check.

If you would like to use the checking script in your own project, the batch code is here:

```bat
@echo off

rem Connect to API and check whether the file can be found
powershell -Command "Invoke-WebRequest http://update.winchameleon.tk/check/0.2/latest.txt -OutFile latest.txt" > nul

if exist "latest.txt" (
    rem Tell user if it was successful
    echo You are using the latest version of Chameleon.
) else (
    rem If not, tell user it was not and then ask if they would like to go to the download page
    echo You are using an outdated version of Chameleon!
    set /p opendownload=Open download page to download latest version? [Y/N] 
    rem Check their choice
    goto :checkopen
)


del latest.txt /f > nul
pause
exit

:checkopen
if /i %opendownload%==y goto :opendownload
if /i %opendownload%==n goto :quitscript

:opendownload
rem Open the download page in their default browser
start https://www.winchameleon.tk/download
exit

:quitscript
rem Delete the latest file and quit
del latest.txt /f > nul
exit
```

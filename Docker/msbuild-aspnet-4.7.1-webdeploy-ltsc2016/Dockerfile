# escape=`
FROM microsoft/dotnet-framework-build:4.7.1-windowsservercore-ltsc2016

SHELL ["powershell.exe", "-ExecutionPolicy", "Bypass", "-Command"]
RUN Invoke-WebRequest -UseBasicParsing https://download.visualstudio.microsoft.com/download/pr/100196686/e64d79b40219aea618ce2fe10ebd5f0d/vs_BuildTools.exe -OutFile vs_BuildTools.exe; `
    Start-Process vs_BuildTools.exe -ArgumentList  '--add', 'Microsoft.VisualStudio.Workload.WebBuildTools', '--quiet', '--norestart', '--nocache' -NoNewWindow -Wait;
# Install Chocolatey and necessary tools
RUN iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))

RUN choco install webdeploy -y

# Install Web Targets
RUN nuget Install MSBuild.Microsoft.VisualStudio.Web.targets -Version 14.0.0.3
RUN mkdir 'C:\Program Files (x86)\MSBuild\Microsoft\VisualStudio\v15.0'
RUN mv 'C:\MSBuild.Microsoft.VisualStudio.Web.targets.14.0.0.3\tools\VSToolsPath\*' 'C:\Program Files (x86)\MSBuild\Microsoft\VisualStudio\v15.0'

ENTRYPOINT ["powershell"]

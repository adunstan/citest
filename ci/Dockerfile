# !IMPORTANT!
# * Pass -m 2GB (or more) when building the image.
# * Configure Docker to use disks larger than the default 20 GB.
FROM cirrusci/windowsservercore:2019

SHELL ["powershell", "-NoLogo", "-NoProfile", "-Command"]


RUN \
	pwd ; \
    choco feature disable -n=usePackageExitCodes ; \
	choco install -y --no-progress --version=16.8.3.0 visualstudio2019buildtools


# cirrus does something odd with this command, so it's stuck in a bat file
# and copied to the docker container and thene executed
COPY ci/inst-tools.bat .
RUN \
	cmd /c .\inst-tools.bat

RUN \
    choco install -y --no-progress strawberryperl ; \
	choco install -y --no-progress winflexbison diffutils ; \
    Rename-Item -Path c:\ProgramData\chocolatey\bin\win_flex.exe flex.exe ; \
    Rename-Item -Path c:\ProgramData\chocolatey\bin\win_bison.exe bison.exe ; \
    Remove-Item C:\ProgramData\chocolatey\logs\*.* -Force -Recurse ; \
    Remove-Item C:\Users\ContainerAdministrator\AppData\Local\Temp\*.* -Force -Recurse

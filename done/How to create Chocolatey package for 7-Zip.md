#how-to , #windows , #chocolatey , #package 

### Prerequisites

1.  Prepare environment  for Chocolatey
2.  Prepare installation package for 7-Zip, from offical website of 7-Zip

### How to create Chocolatey package for 7-Zip

1.  Go to the folder you want to create, and open Command Prompt
2.  Use choco create a empty package - choco new 7-Zip
3.  Copy installation package for 7-Zip to `<your folder>/7-Zip/tools/`
4.  Edit 7-zip.nuspec and tools/chocolateyinstall.ps1
5.  Delete unused files such as `Readme.md` ... and your tree for folder will become shown below
6.  Go to the 7-Zip folder, and use choco package it - choco new 7-zip.nuspec

### Step by Step

1.  Go to the folder you want to create, and open Command Prompt
2.  Use choco create a empty package - choco new 7-Zip
```powershell
C:\Users\Administrator>cd ISAAC

C:\Users\Administrator\ISAAC>choco new 7-Zip
Chocolatey v0.10.15
Creating a new package specification at C:\Users\Administrator\ISAAC\7-Zip
Generating template to a file
 at 'C:\Users\Administrator\ISAAC\7-Zip\7-zip.nuspec'
Generating template to a file
 at 'C:\Users\Administrator\ISAAC\7-Zip\tools\chocolateyinstall.ps1'
Generating template to a file
 at 'C:\Users\Administrator\ISAAC\7-Zip\tools\chocolateybeforemodify.ps1'
Generating template to a file
 at 'C:\Users\Administrator\ISAAC\7-Zip\tools\chocolateyuninstall.ps1'
Generating template to a file
 at 'C:\Users\Administrator\ISAAC\7-Zip\tools\LICENSE.txt'
Generating template to a file
 at 'C:\Users\Administrator\ISAAC\7-Zip\tools\VERIFICATION.txt'
Generating template to a file
 at 'C:\Users\Administrator\ISAAC\7-Zip\ReadMe.md'
Generating template to a file
 at 'C:\Users\Administrator\ISAAC\7-Zip\_TODO.txt'
Successfully generated 7-Zip package specification files
 at 'C:\Users\Administrator\ISAAC\7-Zip'
```

3.  Copy installation package for 7-Zip to `<your folder>/7-Zip/tools/`
4.  Edit 7-zip.nuspec and tools/chocolateyinstall.ps1
**7-zip.nuspec**
```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2015/06/nuspec.xsd">
  <metadata>
    <id>7-zip</id>
    <version>22.01</version>
    <title>7-Zip (Install)</title>
    <authors>__REPLACE_AUTHORS_OF_SOFTWARE_COMMA_SEPARATED__</authors>
    <projectUrl>https://_Software_Location_REMOVE_OR_FILL_OUT_</projectUrl>
    <tags>7-zip SPACE_SEPARATED</tags>
    <summary>__REPLACE__</summary>
    <description>__REPLACE__MarkDown_Okay </description>
  </metadata>
  <files>
    <file src="tools\**" target="tools" />
  </files>
</package>
```
**tools/chocolateyinstall.ps1**
```powershell
$ErrorActionPreference = 'Stop'; # stop on all errors

$toolsDir   = "$(Split-Path -parent $MyInvocation.MyCommand.Definition)"
$fileLocation = Join-Path $toolsDir '7z2201-x64.exe'

$packageArgs = @{
  packageName   = $env:ChocolateyPackageName
  fileType      = 'EXE' #only one of these: exe, msi, msu
  file         = $fileLocation

  softwareName  = '7-Zip*' #part or all of the Display Name as you see it in Programs and Features. It should be enough to be unique

  silentArgs   = '/S'           # NSIS

  validExitCodes= @(0) #please insert other valid exit codes here
}

Install-ChocolateyPackage @packageArgs # https://chocolatey.org/docs/helpers-install-chocolatey-package
```
    
5. Delete unused files such as Readme.md ... and your tree for folder will become shown below
**tools/chocolateyinstall.ps1**
```powershell
C:.
└───7-Zip
    │   7-zip.nuspec
    │
    └───tools
            7z2201-x64.exe
            chocolateyinstall.ps1
```
    
6.  Go to the 7-Zip folder, and use choco package it - choco new 7-zip.nuspec
    
    ```powershell
    C:\Users\Administrator\ISAAC>cd 7-Zip
    
    C:\Users\Administrator\ISAAC\7-Zip>choco pack 7-zip.nuspec
    Chocolatey v0.10.15
    Attempting to build package from '7-zip.nuspec'.
    Successfully created package 'C:\Users\Administrator\ISAAC\7-Zip\7-zip.22.01.nupkg'
    ```

### Reference article

[https://blog.chocolatey.org/2016/01/create-chocolatey-packages/](https://blog.chocolatey.org/2016/01/create-chocolatey-packages/)
# DLLirant

DLLirant is a tool to automatize the DLL Hijacking and DLL Proxying researches on a specified binary.

![alt text](https://raw.githubusercontent.com/Sh0ckFR/DLLirant/main/screenshot.png)
![alt text](https://raw.githubusercontent.com/Sh0ckFR/DLLirant/main/screenshot2.png)
![alt text](https://raw.githubusercontent.com/Sh0ckFR/DLLirant/main/screenshot3.png)

## Live Demo

![alt text](https://raw.githubusercontent.com/Sh0ckFR/DLLirant/main/live.gif)

## How to install

* Install LLVM for Windows: https://llvm.org/builds/
* Do not forget to check the "Add LLVM to the system PATH for current user" during the installation.

## How to use

Select the desired PE file, if it is an .exe, the application will currently search for DLL Search Order Hijacking, if you select a DLL, the application will offer you to proxy it.

Regarding the second option, you must specify a path for the proxy DLL, this path can be specified in two ways:

* With a name, this will generate the proxy DLL and rename it with the name of the selected DLL, and the application will copy the selected (original) DLL and rename it with the name you selected.

* With a path, this option will generate a single file, the proxy DLL that will call the functions exported from the DLL specified in the text box.

Concerning the error messages during the tests of your error, you currently have 10 seconds to validate them, this bug will be fixed in the next versions, so do not go to drink a coffee to then validate all the boxes :)

You can also create an `import` directory and place the missing DLL files that your application need if necessary (the DLL files will be copied automatically in the `output` directory with the targeted binary).

## Python version

This version is deprecated but if you want to use it, you must install `pefile` with pip and:

Use the `cd` command to your DLLirant directory and to test a binary:

```
python3 DLLirant.py -f "C:\THEFULLPATH\YourBinary.exe"
```

If you want to create a proxy dll, you can use the -p option on the original vulnerable dll (read https://itm4n.github.io/dll-proxying/ for more informations):

```
python3 DLLirant.py -p "C:\THEFULLPATH\VulnerableDLL.dll"
```

## How it works

The script will create an output directory in the same directory of DLLirant, copy the targeted binary to the output directory.

Via the PeNet library, the script will extract the dll names required by the binary, and test each imports functions available one by one by compilate a custom DLL with the required exported functions.

If a function required by the binary is executed, the custom DLL will create a `C:\\DLLirant\\output.txt` file and display a MessageBox to be sure that a DLL Hijacking is possible.

A `DLLirant-results.txt` will be also created in the DLLirant directory with all potential DLL Hijacking available.

## Technical posts (in French)

* https://sh0ckfr.com/pages/martine-a-la-recherche-de-la-dll-hijacking-perdue/
* https://sh0ckfr.com/pages/martin-et-le-dll-proxying-de-cristal/

---
title: wxPythonで作ったUIをpy2exeで変換すると見た目が変わる問題
author: 鉄
type: post
date: 2013-03-29T11:38:45+00:00
url: /2013/wxpython-b-py2exe-differ-appearance/
categories:
  - python

---
wxPythonを使って頑張って作ったGUIをPythonが入ってないPCの人も使えるようにするのにpy2exeで変換したら見た目が変わってしまった(古い？TK?)のでその対処法。

### 必要なファイル

Microsoft.VC90.CRT.manifest
  
msvcm90.dll
  
msvcp90.dll
  
msvcr90.dll

の4つのファイルが必要。自分の環境だとPython 2.7 Portableを入れたフォルダに全部入っていたので、Py27MSdllsというフォルダをsetup.pyと同じ階層に作って全部入れました。

Microsoft.VC90.CRT.manifest の中で示されてるdllのバージョンが合ってるかどうか確認する。
  
違ってたら適宜修正する。

    
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?><br>
    <!-- Copyright (c) Microsoft Corporation.  All rights reserved. --><br>
    <assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0"><br>
        <noInheritable/><br>
        <assemblyIdentity<br>
            type="win32"<br>
            name="Microsoft.VC90.CRT"<br>
            <s>version="9.0.21022.8"</s>
            <span style=color:red;>version="9.0.30729.6161"</span><br>
            processorArchitecture="x86"<br>
            publicKeyToken="1fc8b3b9a1e18e3b"<br>
        /><br>
        <file name="msvcr90.dll" /> <file name="msvcp90.dll" /> <file name="msvcm90.dll" /><br>
    </assembly><br>
    

### setup.py

setup.pyを書き換えて用意したこれらのファイルを読み込むように変更する。

    # -*- coding: utf-8 -*-<br>
    #<br>
    # setup.py<br>
    <br>
    from distutils.core import setup<br>
    import py2exe<br>
    import glob<br>
    <br>
    <br>
    class Target(object):<br>
        """ A simple class that holds information on our executable file. """<br>
        def __init__(self, **kw):<br>
            """ Default class constructor. Update as you need. """<br>
            self.__dict__.update(kw)<br>
            <br>
    MANIFEST_TEMPLATE = """<br>
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?><br>
    <assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0"><br>
      <assemblyIdentity<br>
        version="5.0.0.0"<br>
        processorArchitecture="x86"<br>
        name="%(prog)s"<br>
        type="win32"<br>
      /><br>
      <description>%(prog)s</description><br>
      <trustInfo xmlns="urn:schemas-microsoft-com:asm.v3"><br>
        <security><br>
          <requestedPrivileges><br>
            <requestedExecutionLevel<br>
                level="asInvoker"<br>
                uiAccess="false"><br>
            </requestedExecutionLevel><br>
          </requestedPrivileges><br>
        </security><br>
      </trustInfo><br>
      <dependency><br>
        <dependentAssembly><br>
          <assemblyIdentity<br>
                type="win32"<br>
                name="Microsoft.VC90.CRT"<br>
                version="9.0.30729.6161"<br>
                processorArchitecture="x86"<br>
                publicKeyToken="1fc8b3b9a1e18e3b"><br>
          </assemblyIdentity><br>
        </dependentAssembly><br>
      </dependency><br>
      <dependency><br>
        <dependentAssembly><br>
            <assemblyIdentity<br>
                type="win32"<br>
                name="Microsoft.Windows.Common-Controls"<br>
                version="6.0.0.0"<br>
                processorArchitecture="X86"<br>
                publicKeyToken="6595b64144ccf1df"<br>
                language="*"<br>
            /><br>
        </dependentAssembly><br>
      </dependency><br>
    </assembly><br>
    """<br>
    <br>
    other_resources = [(24, 1, MANIFEST_TEMPLATE % dict(prog="MyAppName"))]<br>
    py26MSdll = glob.glob(r"Py27MSdlls\*.*")<br>
    data_files = [("", py26MSdll),]<br>
    <br>
    py2exe_options = {"compressed":1,<br>
                      "optimize":2,<br>
                      "bundle_files":2}<br>
    <br>
    setup(<br>
        data_files = data_files,<br>
        options={"py2exe": py2exe_options},<br>
        windows= [Target(script = 'movie_info.py', other_resources = other_resources)]<br>
        )

これで上手く行けば見た目がWindowsXP以降のキレイな表示に変わります。

### 環境

Windows 7(64bit)
  
Python 2.7.3

### 参考

the appearance of wxpython using py2exe &#8211; Google グループ  
<https://groups.google.com/forum/?fromgroups=#!topic/wxpython-users/OJ91DqSm3xw>

py2exe-python26 &#8211; wxPyWiki  
<http://wiki.wxpython.org/py2exe-python26>


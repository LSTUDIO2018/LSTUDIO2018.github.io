---
title: XLua
date: 2020-09-23 04:02:38
tags:

---



## 自定义路径加载

```C#
private LuaEnv _luaEnv;   
    void Start()
    {
        _luaEnv=new LuaEnv();
        // _luaEnv.DoString("CS.UnityEngine.Debug.Log('Hello World')");
        _luaEnv.AddLoader(CLoader);//这里是加载到这个hello.lua文件
        _luaEnv.DoString("require 'hello'");//这里是调用hello.lua
        
        _luaEnv.Dispose();
    }

    private byte[] CLoader(ref string filename)
    {
        byte[] byte_path = null;
        string lua_path = Application.dataPath + "/Scripts/Lua/" + filename + ".lua";
        string path_content = File.ReadAllText(lua_path);
        byte_path = System.Text.Encoding.UTF8.GetBytes(path_content);
        return byte_path;
    }
```
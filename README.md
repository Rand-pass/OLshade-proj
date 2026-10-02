The project was compiled using the MinGW compiler.

---

To quickly launch the injector, simply place the contents of the "overlord" folder into the game's main folder.

System.psp contains some modified game shaders specifically to support multiple render targets. It requires fixing and the addition of other shaders.
Load deferred rendering shaders into the OLshaders folder.

---
The project consists of two parts:

d3d9.dll - main injector

mingw32.exe build argument

g++ -shared -m32 -std=c++17 -O2 -o d3d9.dll main.cpp src/*.c src/hde/*.c d3d9.def -I. -Iinclude -static-libgcc -static-libstdc++ -Wl,-Bstatic -lwinpthread -Wl,-Bdynamic -Wl,--enable-stdcall-fixup -ld3d9 -ld3dx9 -lgdi32

OLshade64.exe - 64 bit dx11 wrapper

mingw64.exe build argument

g++ -m64 -std=c++17 -O2 -o OLshade64.exe RendererMain.cpp D3D11Bridge.cpp PipelineManager.cpp ShaderPass.cpp ConfigManager.cpp GuiOverlay.cpp imgui/*.cpp imgui/backends/imgui_impl_win32.cpp imgui/backends/imgui_impl_dx11.cpp -I. -Iinclude -Iimgui -Iimgui/backends -static-libgcc -static-libstdc++ -Wl,-Bstatic -lwinpthread -Wl,-Bdynamic -ld3d11 -ldxgi -ld3dcompiler -ldxguid -limm32 -lgdi32 -ldwmapi

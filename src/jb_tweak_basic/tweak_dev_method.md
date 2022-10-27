# tweak开发手段

TODO：

【已解决】iOS中Cydia Substrate

---

* use Frida for research-level tweaking
  * https://www.frida.re
    * Frida • A world-class dynamic instrumentation framework | Inject JavaScript to explore native apps on Windows, macOS, GNU/Linux, iOS, Android, and QNX
    * you can make experiments without process restarting
    * Of course production-level tweaks must be supplied as native .dylib/.plist pair
* attach to iOS processes：using plain lldb or using xcode lldb session
* dylib-level tweaking/hooking/detouring
  * 基于`CydiaSubstrate`
    * `Theos/Logos`
      * Special DSL that is translated to C. General-purpose solution to start with
    * Direct calling of substrate functions (MSHookXxx family).
      * Theos/logos is just brief DSL wrapper around it
  * `CaptainHook`
    * ure C/ObjC way of doing things, header-only, uses many #define's under the hood
    * Use it if you don't want to lose syntax highlighting and navigation support in IDE project
  * `fishhook`
    * Pure C way of doing things
    * facebook 开源的一个库
    * [facebook/fishhook: A library that enables dynamically rebinding symbols in Mach-O binaries running on iOS](https://github.com/facebook/fishhook)
  * `AutoHook`
    * Creating tweaks without Logos directly from Xcode
      * [Tutorial Creating tweaks without Logos directly from Xcode : jailbreakdevelopers (reddit.com)](https://www.reddit.com/r/jailbreakdevelopers/comments/8xb9b6/tutorial_creating_tweaks_without_logos_directly/)
  * Object-oriented method of hooking with pre-post-instead semantic
    * https://github.com/steipete/Aspects
  * Method Swizzle
    * 通过 runtime 交换方法的实现

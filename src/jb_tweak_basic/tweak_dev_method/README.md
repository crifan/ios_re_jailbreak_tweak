# tweak开发手段

* 开发越狱插件的主要手段/工具/框架 = dylib-level tweaking/hooking/detouring
  * 底层机制和原理
    * 基于: [CydiaSubstrate](../../jb_tweak_basic/tweak_dev_method/cydiasubstrate.md)
      * 直接调用
        * Direct calling of substrate functions (MSHookXxx family)
    * `CaptainHook`
      * ure C/ObjC way of doing things, header-only, uses many #define's under the hood
      * Use it if you don't want to lose syntax highlighting and navigation support in IDE project
    * `fishhook`
      * Pure C way of doing things
      * facebook 开源的一个库
        * https://github.com/facebook/fishhook
          * facebook/fishhook: A library that enables dynamically rebinding symbols in Mach-O binaries running on iOS
    * `AutoHook`
      * Creating tweaks without Logos directly from Xcode
        * [Tutorial Creating tweaks without Logos directly from Xcode : jailbreakdevelopers (reddit.com)](https://www.reddit.com/r/jailbreakdevelopers/comments/8xb9b6/tutorial_creating_tweaks_without_logos_directly/)
    * Object-oriented method of hooking with pre-post-instead semantic
      * https://github.com/steipete/Aspects
    * Method Swizzle
      * 通过Runtime交换方法的实现
  * 相对上层的（集成/封装）工具
    * [Theos/Logos](../../tweak_dev/theos_logos/README.md)
    * [iOSOpenDev](../../tweak_dev/iosopendev.md)
    * [MonkeyDev](../../tweak_dev/monkeydev.md)

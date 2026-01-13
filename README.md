# wine-tkg-build

configure wine-tkg and compile &amp; releases wine-tkg

由于社区进展缓慢：

- 对于 **10.17+** 的版本，不得不停止 esync 与 fsync 支持。Wine 现已可在高版本内核上加载 ntsync 支持。
- 对于 **10.16+** 的版本，停止构建支持 Proton winevulkan 与 mf 的移植支持。
- Proton 10-3 进度放缓，因去 Steam 补丁进展缓慢。
- 不再对高版本 Wine 的编译完成版本在 Termux 上进行测试，NumBox 项目更新暂时停止，且未能找到方便测试的环境。

# Release

wineVer-N

N代表第N次编译

wine-wineVer-[mfdxgi]-N-tkg-stg-ge.tar.xz

现在对于只应用wine_do_not_create_dxgi_device_manager.patch的版本，命名为,mfdxgi

文件名过长的问题也进行解决,stg代表staging补丁已经应用

# TkG

customization.cfg:
```bash
_proton_battleye_support="false"

_proton_eac_support="false"

_GE_WAYLAND="false"

_mk11_fix="false"

_proton_fs_hack="true"

_msvcrt_nativebuiltin="true"

_win10_default="true"
```

advanced-customization.cfg:

```bash
# Custom GCC flags to use instead of system-wide makepkg flags set in /etc/makepkg.conf. Default is "-pipe -O2 -ftree-vectorize". Don't use -march=native if you want to share your builds accross different machines!
_GCC_FLAGS="-O3 -pipe -msse3 -mfpmath=sse -ftree-vectorize -Wno-error=implicit-function-declaration -Wno-error=incompatible-pointer-types"
# Custom LD flags to use instead of system-wide makepkg flags set in /etc/makepkg.conf. Default is "-pipe -O2 -ftree-vectorize".
_LD_FLAGS="-Wl,-O3,--sort-common,--as-needed"
# Same as _GCC_FLAGS but for cross-compiled binaries.
_CROSS_FLAGS="-O3 -pipe -msse3 -mfpmath=sse -ftree-vectorize -Wno-error=implicit-function-declaration -Wno-error=incompatible-pointer-types"
# Same as _LD_FLAGS but for cross-compiled binaries.
_CROSS_LD_FLAGS="-Wl,-O3,--sort-common,--as-needed"

_NOLIB32="wow64"
```

# Thanks

- [wine-tkg-git](https://github.com/Frogging-Family/wine-tkg-git)

- [proton wine](https://github.com/ValveSoftware/wine/tree)
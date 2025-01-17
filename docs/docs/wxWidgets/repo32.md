# wxWidgets 3.2.4 Packages and Repositories
---

## Preface
---

This page is for the stable release, wx3.2.4. The CodeLite packages for Linux now use wxWidgets >=3.1. As wx3.2.4 is newly released, few current (November 2023) distro versions will supply it. I've therefore built 3.2.4 packages for the commonest ones.

## Fetching CodeLite keys
---

The packages are signed with the CodeLite public key so, if you haven't done so before, you should tell apt or rpm about this by doing as superuser (su or sudo depending on your distro): 

```bash
apt-key adv --fetch-keys https://repos.codelite.org/CodeLite.asc
```

or

```bash
rpm --import https://repos.codelite.org/CodeLite.asc
```


!!! Tip
  Since ubuntu 21.10, using apt-key displays the following message:
  ```bash
  Warning: apt-key is deprecated. Manage keyring files in trusted.gpg.d instead (see apt-key(8))
  ```
  Don't panic! it's only a warning. apt-key still works.


## Ubuntu and debian
---

If you use a debian-based distro there are the following wxWidgets repositories available: 

Repository | Available | Versions | Component
-----------|-----------|----------|-----------
debian	| `https://repos.codelite.org/wx3.2/debian/` | bookworm | libs
ubuntu | `https://repos.codelite.org/wx3.2/ubuntu/` |  jammy mantic | universe


The repositories also contain wx3.1.0 to wx3.2.3 builds (including some i386 ones) for debian stretch, buster and bullseye, and ubuntu trusty, wily to kinetic.

The ubuntu ones should also work on other *buntus of the same version, and on derivatives e.g. Mint.

Now let apt know that the repository exits. If you use an apt front-end e.g. synaptic, tell it to Add a repository, using as data the appropriate entry in the table above. If you do things by hand, add the appropriate url to /etc/apt/sources.list. Become superuser and either use a text editor to edit /etc/apt/sources.list, adding a line similar to:

```bash
deb https://repos.codelite.org/wx3.2/debian/ bookworm libs
```

or, in a terminal, do something like: 

```bash
sudo apt-add-repository 'deb https://repos.codelite.org/wx3.2/ubuntu/ mantic universe'
```

The line to add is different for different distros/versions; choose the appropriate one: 

Distro/release | Line to append
---------------|-------------------
debian bookworm| `deb https://repos.codelite.org/wx3.2/debian/ bookworm libs`
ubuntu jammy | `deb https://repos.codelite.org/wx3.2/ubuntu/ jammy universe`
ubuntu mantic| `deb https://repos.codelite.org/wx3.2/ubuntu/ mantic universe`

!!! Tip
If you prefer, you can instead enter a specific version e.g. `https://repos.codelite.org/wx3.2.4/debian`

You then need to update the repositories. In synaptic, click the Reload button. If you're doing things by hand, do: 

```bash
sudo apt-get update
```

Synaptic users can then select and install as usual. By hand you can do: 

```bash
apt-get install libwxbase3.2-0-unofficial \
                libwxbase3.2unofficial-dev \
                libwxgtk3.2-0-unofficial \
                libwxgtk3.2unofficial-dev \
                wx3.2-headers \
                wx-common \
                libwxgtk-media3.2-0-unofficial \
                libwxgtk-media3.2unofficial-dev \
                libwxgtk-webview3.2-0-unofficial \ 
                libwxgtk-webview3.2unofficial-dev \ 
                libwxgtk-webview3.2-0-unofficial-dbg \ 
                libwxbase3.2-0-unofficial-dbg \
                libwxgtk3.2-0-unofficial-dbg \
                libwxgtk-media3.2-0-unofficial-dbg \
                wx3.2-i18n \
                wx3.2-examples
```

The first 6 of the debs are required; the others optional (and of decreasing importance). 

`wx-common` and `wx3.2-i18n` will conflict with the distro's wx2.8 equivalents. That is unlikely to matter too much; 
but `wx-common` contains `wxrc` so, if you use this, be aware that there may be differences after upgrading. 


!!! Tip
    Building some of the samples provided by the wx3.2-examples package may fail because of failure to detect GTK+ files. If so, try this compilation line:  
    ```bash
    LDFLAGS=$(pkg-config --libs gtk+-3.0) CXXFLAGS=$(pkg-config --cflags gtk+-3.0) make -j$(nproc)
    ```  
    If all else fails, you might need to create symlinks.

## Fedora and openSUSE
---
There are currently rpms available for fedora 39,  and openSUSE 15.5.

Distro|Release|x86_64
------|-------|------
fedora| `39`|[wxBase32][32] [wxBase32-debuginfo][41] [wxGTK32][33] [wxGTK32-debuginfo][37] [wxGTK32-debugsource][42] [wxGTK32-devel][34] [wxGTK32-devel-debuginfo][43] [wxGTK32-gl][35] [wxGTK32-gl-debuginfo][44] [wxGTK32-media][36] [wxGTK32-media-debuginfo][45]
openSUSE|`15.5`|[libwx_baseu_net][8] [libwx_baseu][9] [libwx_baseu_xml][10] [libwx_gtk3u_adv][11] [libwx_gtk3u_aui][12] [libwx_gtk3u_core][13] [libwx_gtk3u_gl][14]  [libwx_gtk3u_html][15] [libwx_gtk3u_media][16] [libwx_gtk3u_propgrid][17] [libwx_gtk3u_qa][18] [libwx_gtk3u_ribbon][19] [libwx_gtk3u_richtext][20] [libwx_gtk3u_stc][21]  [libwx_gtk3u_xrc][23] [wxWidgets-3_2-devel][24] 

There are also source rpms for [Fedora][51] and [openSUSE][52]. The fedora srpm should also build on CentOS 8. 

Either download the required rpms and install them as usual, or download and install in one step; e.g. 

```bash
rpm -Uvh https://repos.codelite.org/wx3.2.4/wx3.2-packages/suse/wxWidgets-3_2-3.2.4-0.src.rpm
```


!!! Note
    Some of these rpms may conflict with the wx2.8 devel ones. 

 [1]: https://forums.wxwidgets.org/viewtopic.php?f=19&t=47403&p=200198#p200198
 [8]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/suse/15.5/libwx_baseu_net-suse15-3.2.4-0.x86_64.rpm
 [9]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/suse/15.5/libwx_baseu-suse15-3.2.4-0.x86_64.rpm
 [10]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/suse/15.5/libwx_baseu_xml-suse15-3.2.4-0.x86_64.rpm
 [11]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/suse/15.5/libwx_gtk3u_adv-suse15-3.2.4-0.x86_64.rpm
 [12]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/suse/15.5/libwx_gtk3u_aui-suse15-3.2.4-0.x86_64.rpm
 [13]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/suse/15.5/libwx_gtk3u_core-suse15-3.2.4-0.x86_64.rpm
 [14]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/suse/15.5/libwx_gtk3u_gl-suse15-3.2.4-0.x86_64.rpm
 [15]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/suse/15.5/libwx_gtk3u_html-suse15-3.2.4-0.x86_64.rpm
 [16]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/suse/15.5/libwx_gtk3u_media-suse15-3.2.4-0.x86_64.rpm
 [17]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/suse/15.5/libwx_gtk3u_propgrid-suse15-3.2.4-0.x86_64.rpm
 [18]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/suse/15.5/libwx_gtk3u_qa-suse15-3.2.4-0.x86_64.rpm
 [19]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/suse/15.5/libwx_gtk3u_ribbon-suse15-3.2.4-0.x86_64.rpm
 [20]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/suse/15.5/libwx_gtk3u_richtext-suse15-3.2.4-0.x86_64.rpm
 [21]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/suse/15.5/libwx_gtk3u_stc-suse15-3.2.4-0.x86_64.rpm
 [22]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/suse/15.5/libwx_gtk3u_webview-suse15-3.2.4-0.x86_64.rpm
 [23]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/suse/15.5/libwx_gtk3u_xrc-suse15-3.2.4-0.x86_64.rpm
 [24]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/suse/15.5/wxWidgets-3_2-devel-3.2.4-0.x86_64.rpm
 [25]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/suse/15.5/wxWidgets-3_2-plugin-sound_sdlu-3_2-3.2.4-0.x86_64.rpm

 [32]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/fedora/39/wxBase32-3.2.4-1.fc39.x86_64.rpm
 [33]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/fedora/39/wxGTK32-3.2.4-1.fc39.x86_64.rpm
 [34]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/fedora/39/wxGTK32-devel-3.2.4-1.fc39.x86_64.rpm
 [35]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/fedora/39/wxGTK32-gl-3.2.4-1.fc39.x86_64.rpm
 [36]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/fedora/39/wxGTK32-media-3.2.4-1.fc39.x86_64.rpm
 [37]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/fedora/39/wxGTK32-debuginfo-3.2.4-1.fc39.x86_64.rpm
 
 [41]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/fedora/39/wxBase32-debuginfo-3.2.4-1.fc39.x86_64.rpm
 [42]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/fedora/39/wxGTK32-debugsource-3.2.4-1.fc39.x86_64.rpm
 [43]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/fedora/39/wxGTK32-devel-debuginfo-3.2.4-1.fc39.x86_64.rpm
 [44]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/fedora/39/wxGTK32-gl-debuginfo-3.2.4-1.fc39.x86_64.rpm
 [45]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/fedora/39/wxGTK32-media-debuginfo-3.2.4-1.fc39.x86_64.rpm
 
 [51]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/fedora/wxGTK32-3.2.4-1.fc.src.rpm
 [52]: https://repos.codelite.org/wx3.2.4/wx3.2-packages/suse/wxWidgets-3_2-3.2.4-0.src.rpm


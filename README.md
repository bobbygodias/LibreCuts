# LibreCuts

<div align="center">
  <img src="src/images/featureGraphic.png" alt="LibreCuts Banner" width="100%"/>
  <br/>
  <br/>

  <a href="https://github.com/sponsors/tharunbirla">
    <img src="https://img.shields.io/badge/Sponsor_LibreCuts-ea4aaa?style=for-the-badge&logo=githubsponsors&logoColor=white" height="35" alt="Sponsor tharunbirla" />
  </a>
  <a href="LICENSE">
    <img src="https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge" height="35" alt="License" />
  </a>
  <br/>
  <br/>
  <a href="https://github.com/tharunbirla/LibreCuts/releases/latest">
    <img src="src/images/badges/badge_github.png" alt="Get it on GitHub" height="96" />
  </a>
  <a href="https://f-droid.org/packages/com.tharunbirla.librecuts/">
    <img src="src/images/badges/badge_fdroid.png" alt="Get it on F-Droid" height="96" />
  </a>
  <a href="https://apps.obtainium.imranr.dev/redirect?r=obtainium://add/https://github.com/tharunbirla/LibreCuts">
    <img src="src/images/badges/badge_obtainium.png" height="96" alt="Get it on Obtainium" />
  </a>
  <a href="https://discord.gg/gwr3nE7YW">
    <img src="src/images/badges/badge_discord.png" height="96" alt="Join Discord" />
  </a>
  <a href="https://hosted.weblate.org/engage/librecuts/">
    <img src="https://hosted.weblate.org/widget/librecuts/librecuts/287x66-grey.png" height="96" alt="Translation status" />
  </a>
</div>

<br/>

**LibreCuts** is a free, open-source video editor for Android that prioritizes simplicity, efficiency, and privacy. Built for seamless performance, it empowers creators to easily select, edit, and export watermark-free videos locally on their device.


---

## 🛠️ Community Repair Fork / Fork comunitário de reparo

> Upstream original: [tharunbirla/LibreCuts](https://github.com/tharunbirla/LibreCuts) — MIT licensed.  
> This fork keeps the original project and attribution intact while documenting a community-tested ARM64 repair.

### 🇧🇷 Resumo em português

Este fork existe para registrar e compartilhar um **reparo comunitário testado** para um crash ao abrir vídeo em ambiente **ARM64 / Android 15 (API 35)**. O erro visível era `FFmpegKit failed to start`; a cadeia de erro apontava para falha no carregamento nativo, incluindo `UnsatisfiedLinkError`, `libavcodec.so` e `.dynamic section header was not found`.

A versão **Repair1 native-fixed** funcionou em teste real com **aproximadamente 82 minutos de vídeo + legenda SRT**, sem reproduzir o crash original.

**Ambiente técnico do teste (sem marca/modelo do aparelho):**
- Android 15 / API 35
- ARM64-v8a
- MediaTek Helio G100, octa-core, até 2.2 GHz
- 12 GB de RAM física
- GPU Mali-G57 MC2

Isto é um **workaround/reparo confirmado nesse ambiente**, não uma promessa de correção universal. A ideia do fork é deixar diagnóstico, binários e contexto suficientes para que qualquer pessoa possa estudar, adaptar, melhorar e, se fizer sentido, devolver uma solução mais limpa ao upstream. Open source é isso.

### 🇺🇸 Repair notes — the longer version

Yo — if you landed here because LibreCuts face-plants right when you try to open a video, I ran into the same damn thing. Instead of patching my copy and bouncing, I'm leaving the findings here so another playa — maintainer, contributor, random dev, he, she, they, or an Apache helicopter — can study it, improve it, fork it, or push a cleaner fix upstream. Ya dig?

#### What happened

On the affected ARM64 / Android 15 setup, selecting a video could fail immediately with:

```text
FFmpegKit failed to start
```

The underlying crash chain included a native-loader failure around FFmpegKit / FFmpeg libraries, with messages involving:

```text
UnsatisfiedLinkError
libavcodec.so
.dynamic section header was not found
```

So the important part was not RAM pressure, GPU horsepower, or a long-video workload. The failure happened during native startup, before normal editing could really get going.

#### What this fork preserves

The working repair build is named:

```text
LibreCuts-Repair1-native-fixed-arm64-v8a.apk
```

It preserves the earlier subtitle/export-side repair work and the native-loading repair that allowed the app to get past the FFmpegKit startup failure in the tested environment.

This is intentionally documented as a **confirmed working repair**, not as some holy universal fix carved into stone. Different Android builds, ABIs, vendor loaders, packaging pipelines, or future LibreCuts versions may need a cleaner or different approach.

#### Real-world test

The repaired build was tested with:

- about **82 minutes of video**
- an imported **SRT subtitle track**
- ARM64-v8a
- Android 15 / API 35
- MediaTek Helio G100 (octa-core, up to 2.2 GHz)
- 12 GB physical RAM
- Mali-G57 MC2 GPU

The original FFmpegKit startup crash did **not** recur during that test.

No manufacturer, device model, custom Android skin, serial, or other device-identifying information is needed to reproduce the technical context, so none is documented here.

#### APK integrity

```text
LibreCuts-arm64-v8a.apk
SHA-256: cabdf4356fef9df2a048f88db27a6009953b8e920787e956071e074ecc8b04ca

LibreCuts-Repair1-native-fixed-arm64-v8a.apk
SHA-256: de269c5d51483aed2ae7327ce938e86ff89f8a5d7dd195e0d7ef2bd818a55df4
```

#### Why publish the fork?

Because that's the whole point of this stuff.

Find a bug. Understand as much of the failure as you can. Fix the damn thing. Test it in the real world. Document what worked. Share it. Let somebody else make it better.

If this repair gives the upstream maintainer a useful clue for a cleaner beta, even better. No ownership games, no gatekeeping — just voluntary contribution and useful code.

Word up. Open source, baby.

---

## ✊ Keep Android Open

[![Keep Android Open](https://img.shields.io/badge/Keep-Android_Open-brightgreen?style=for-the-badge&logo=android)](https://keepandroidopen.org/)

Google's mandatory developer verification policy goes into effect in **September 2026** (in just a few months). This mandate requires all independent developers to submit government ID and centrally register with Google, threatening user privacy, sideloading freedom, and the distribution of free and open-source software (FOSS) on Android. 

Help resist this gatekeeping and support the movement at [keepandroidopen.org](https://keepandroidopen.org/).

---

## 🚀 Features

- **Trim** - Remove unwanted parts from the beginning or end of a video clip with a real-time timeline control.
- **Overlays** - Place text, stickers, images, GIFs, and video overlays on top of video clips to create engaging content. Includes support for continuous media looping.
- **Masking** - Apply various mask shapes to your overlays for creative effects.
- **Chroma Key** - Remove backgrounds from any overlay using the green screen effect.
- **Keyframes** - Animate overlays across the screen with keyframe support.
- **Subtitles (Captions)** - Import custom `.srt` subtitle files with a dedicated toolbar slider for resizing and fully interactive touch-based positioning directly on the video preview.
- **Layer Management** - Easily reorder overlay layers to control what renders on top.
- **Audio** - Manage soundtracks effortlessly by importing custom music or audio tracks, recording voice overs, applying audio ducking and fades, amplifying volume up to 200%, and muting original audio.
- **Audio Export** - Export your project's entire audio mix as a standalone MP3 file.
- **Snapshots** - Capture and save high-quality frame grabs (snapshots) directly from the video editor.
- **Crop** - Adjust the aspect ratio of a video with custom cropping support.
- **Merge** - Combine multiple video segments into a continuous sequence with drag-to-rearrange functionality.
- **Transition** - Apply transitions with animated visual previews in the toolbar.
- **Speed** - Change the speed of a video clip using a custom speed slider for granular control.
- **Adjust & Filters** - Modify video brightness, contrast, saturation, and apply color filters.
- **Canvas Background** - Add a blurred background or a solid color for a cohesive look when your video aspect ratio does not match the project frame.
- **Reverse** - Reverse video playback.
- **Timeline Organization** - Enhanced editing with snapping functionality, overlay duplication, freeze frame actions, and improved UI visual styling.
- **Project Save & Import** - Save non-destructive project state as a `.lcprj` file to save and reopen editable project files anytime.
- **Freehand Drawing** - Draw directly on top of video clips with custom brush color and stroke controls.
- **Custom Fonts** - Import `.ttf` or `.otf` font files to customize text overlay typography.
- **Fullscreen Preview** - Switch to true fullscreen preview mode with expanded timeline view and overlay controls.
- **Android 13+ Themed Icon** - Supports native monochrome adaptive icons for Android 13+ system themes.
- **Hardware Acceleration** - Super-fast and reliable video exports using device hardware-accelerated `h264_mediacodec` encoding (with seamless automatic fallback to software encoding for maximum device compatibility) and accurate FFmpeg progress calculation.

## 📱 Screenshots

<div align="center">
  <table>
    <tr>
      <td align="center"><img src="src/images/sc_1.png" width="100%" alt="Home Screen"/></td>
      <td align="center"><img src="src/images/sc_2.png" width="100%" alt="Editor Screen"/></td>
      <td align="center"><img src="src/images/sc_3.png" width="100%" alt="Audio Import"/></td>
      <td align="center"><img src="src/images/sc_4.png" width="100%" alt="Timeline"/></td>
    </tr>
    <tr>
      <td align="center"><b>Home Screen</b></td>
      <td align="center"><b>Editor Screen</b></td>
      <td align="center"><b>Audio Import</b></td>
      <td align="center"><b>Timeline</b></td>
    </tr>
  </table>
</div>

## 💖 Support LibreCuts

LibreCuts is built with passion and provided to the community for free. If this app has helped you create amazing videos, consider supporting its continued development! Your sponsorship helps keep the project alive and growing.

<div align="center">
  <br/>
  <a href="https://github.com/sponsors/tharunbirla"><img src="https://img.shields.io/badge/sponsor-30363D?style=for-the-badge&logo=GitHub-Sponsors&logoColor=%23EA4AAA" alt="GitHub Sponsors" /></a>
  &nbsp;&nbsp;
  <a href="https://www.patreon.com/tharunbirla"><img src="https://img.shields.io/badge/Patreon-F96854?style=for-the-badge&logo=patreon&logoColor=white" alt="Patreon" /></a>
  &nbsp;&nbsp;
  <a href="https://ko-fi.com/tharunbirla"><img src="https://img.shields.io/badge/Ko--fi-F16061?style=for-the-badge&logo=ko-fi&logoColor=white" alt="Ko-Fi" /></a>
  <br/>
  <br/>
</div>

## 🛠️ Getting Started

### Prerequisites

- Android Studio
- Android SDK

### Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/tharunbirla/LibreCuts.git
   ```
2. **Open the project in Android Studio**:
   - Launch Android Studio and select "Open an existing Android Studio project."
   - Navigate to the cloned directory and select it.
3. **Build the project**:
   - Click on "Build" in the menu, then select "Make Project."
4. **Run the app**:
   - Connect an Android device or start an emulator.
   - Click on the "Run" button in Android Studio.

## 🔒 Permissions

LibreCuts requires the following permissions to function properly:

- **READ_EXTERNAL_STORAGE**: To read videos from the device.
- **WRITE_EXTERNAL_STORAGE**: (For older Android versions) To save edited videos.
- **POST_NOTIFICATIONS**: To show notifications related to video editing.
- **READ_MEDIA_AUDIO/VIDEO/IMAGES**: For accessing media files on devices running Android 13 (API level 33) and above.

## 🔧 Troubleshooting & Support

If you encounter any export failures, codec errors, or unexpected crashes during your editing workflow:
- Refer to our comprehensive [Error Codes & Troubleshooting Guide](https://github.com/tharunbirla/LibreCuts/wiki/Error-Codes-&-Troubleshooting) on the Wiki.
- Join our [Discord Community](https://discord.gg/gwr3nE7YW) for real-time support, suggestions, and app updates.

## 🤝 Contributing

Contributions are welcome! If you have suggestions or improvements, feel free to create a pull request or open an issue.

1. Fork the repository.
2. Create a new branch for your feature or bug fix.
3. Commit your changes.
4. Push to the branch.
5. Submit a pull request.

## 📝 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

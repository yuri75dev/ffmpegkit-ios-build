# FFmpegKitNext for iOS

Builds [FFmpegKitNext](https://github.com/arthenica/ffmpeg-kit-next) for iOS on GitHub Actions,
with no Nix or Homebrew needed on your own Mac. The recipe follows the project's own CI
(`ios-build-scripts.yml` on the `development` branch).

## What gets built

- Slices: `arm64` (device) and `arm64-simulator` (Apple silicon), minimum iOS 15.0 by default.
- System libraries: AudioToolbox, VideoToolbox, zlib, bzip2, libiconv.
- External libraries, matching the legacy FFmpegKit audio package: lame, libilbc,
  libvorbis (+libogg), opencore-amr, opus, shine, soxr, speex, twolame (+libsndfile), vo-amrwbenc.
- FFmpeg and FFprobe are both included in `ffmpegkit` (`FFmpegKit`, `FFprobeKit`,
  `MediaInformationSession`).

## Running

Actions → build ios → Run workflow. Inputs:

- `ref`: ffmpeg-kit-next tag or commit, defaults to `v9.0.0`;
- `xcode`: Xcode version on the `macos-26` runner, defaults to `26.6`;
- `ios-target`: minimum iOS version of the libraries, defaults to `15.0`;
- `extra-options`: additional `ios.sh` options, for example `--enable-lib-libwebp`.

Output: a release named `<ref>-<run number>` with `ffmpegkit-ios.zip` and `build.log`.
The archive contains a `FFmpegKit/` folder with eight xcframeworks and a `Package.swift`
(package and product `ffmpeg-kit`, module `ffmpegkit`). Add it as a local package:
`.package(path: "…/FFmpegKit")`.

## License

Release binaries are LGPL-3.0 with no GPL libraries. Each release description links to the
exact source commit, and the license files are included inside the xcframeworks.

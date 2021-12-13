# Youtube Plyr IFrame

This is a fork of [youtube_player_iframe](https://github.com/sarbagyastha/youtube_player_flutter/tree/master/packages/youtube_player_iframe) which fixes some game breaking things.

Flutter plugin for playing or streaming YouTube videos inline using the official [**iFrame Player API**](https://developers.google.com/youtube/iframe_api_reference).
The package exposes almost all the API provided by **iFrame Player API**. So, it's 100% customizable.

Supported Platforms:
- **Android** 
- **iOS** (Platform design -> eg. Airplay, Captions)
- **Web**
## Salient Features
* Inline Playback
* Supports captions
* No need for API Key
* Supports custom controls
* Retrieves video meta data
* Supports Live Stream videos
* Supports changing playback rate
* Support for both Android and iOS
* Adapts to quality as per the bandwidth
* Exposes builders for building custom controls
* Playlist Support (Both custom and Youtube's playlist)


For Web, Flutter's [HtmlElementView](https://api.flutter.dev/flutter/widgets/HtmlElementView-class.html).
For Android & iOS, the package uses [flutter_inappwebview](https://pub.dartlang.org/packages/flutter_inappwebview) under-the-hood.

Since *flutter_inappwebview* relies on Flutter's mechanism for embedding Android and iOS views, this plugin might share some known issues tagged with the [platform-views](https://github.com/flutter/flutter/labels/a%3A%20platform-views) label.

## Requirements
* **Project**: Flutter Version `>=2.0.0` and `Sound Null Safety`
* **Android**: `minSdkVersion 23` and add support for `androidx` (see [AndroidX Migration](https://flutter.dev/docs/development/androidx-migration))
* **iOS**: `--ios-language swift`, Xcode version `>= 12`
* **Web**: See setup

## Setup

### Web
No Configuration required, if developing without the need to load thumbnails. (Inline thumbnails will still load.)

To load thumbnails the HTML renderer is needed.

- Run: `flutter run -d chrome --web-renderer html`
- Build: `flutter build web --web-renderer html --profile`

Read for more information:
- [Web renderers](https://flutter.dev/docs/development/tools/web-renderers)
- [Displaying images on the web
](https://flutter.dev/docs/development/platform-integration/web-images)

### iOS
No Configuration Required.

[Follow the guide here for complete iOS setup](https://pub.dev/packages/flutter_inappwebview#important-note-for-ios)

### Android
Set `minSdkVersion` of your `android/app/build.gradle` file to at least 23.

[Follow the guide here for complete Android setup](https://pub.dev/packages/flutter_inappwebview#important-note-for-android)

#### Using the player

```dart
YoutubePlayerController _controller = YoutubePlayerController(
    initialVideoId: 'K18cpp_-gP8',
    params: YoutubePlayerParams(
        playlist: ['nPt8bK2gbaU', 'gQDByCdjUXw'], // Defining custom playlist
        startAt: Duration(seconds: 30),
        showControls: true,
        showFullscreenButton: true,
    ),
);

YoutubePlayerIFrame(
    controller: _controller,
    aspectRatio: 16 / 9,
),

-------------- OR --------------

YoutubePlayerControllerProvider( // Provides controller to all the widget below it.
  controller: _controller,
  child: YoutubePlayerIFrame(
    aspectRatio: 16 / 9,
  ),
);

// Access the controller as: `YoutubePlayerControllerProvider.of(context)` or `controller.ytController`.
```

# ExoPlayer Demo Project

#### This repo updated for r2.5.1 version.

You can play audio and video with ExoPlayer.


### Playing Audio

```
        player = ExoPlayerFactory.newSimpleInstance(getApplicationContext(), trackSelector, loadControl);

        bandwidthMeter = new DefaultBandwidthMeter();
        dataSourceFactory = new DefaultDataSourceFactory(this, Util.getUserAgent(this, "mediaPlayerSample"), (TransferListener<? super DataSource>) bandwidthMeter);
        extractorsFactory = new DefaultExtractorsFactory();
        mediaSource = new ExtractorMediaSource(Uri.parse(radioUrl), dataSourceFactory, extractorsFactory, null, null);
        player.prepare(mediaSource);
```

You can manage player visibility using simpleExoPlayerView.setControllerShowTimeoutMs(0);

```


### Playing Video

We need to SimpleExoPlayerView for playing videos.

```
        simpleExoPlayerView = (SimpleExoPlayerView) findViewById(R.id.player_view);
        simpleExoPlayerView.requestFocus();

        TrackSelection.Factory videoTrackSelectionFactory =
                new AdaptiveTrackSelection.Factory(bandwidthMeter);

        trackSelector = new DefaultTrackSelector(videoTrackSelectionFactory);

        player = ExoPlayerFactory.newSimpleInstance(this, trackSelector);

        simpleExoPlayerView.setPlayer(player);

        player.setPlayWhenReady(shouldAutoPlay);
/*        MediaSource mediaSource = new HlsMediaSource(Uri.parse("https://storage.googleapis.com/exoplayer-test-media-0/play.mp3"),
                mediaDataSourceFactory, mainHandler, null);*/

        DefaultExtractorsFactory extractorsFactory = new DefaultExtractorsFactory();

        MediaSource mediaSource = new ExtractorMediaSource(Uri.parse("http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4"),
                mediaDataSourceFactory, extractorsFactory, null, null);

        player.prepare(mediaSource);
```

 If you use hls or dash formats, you need to use HlsMediaSource as a MediaSource.
 
 For hls

```
MediaSource mediaSource = new HlsMediaSource(Uri.parse("https://storage.googleapis.com/exoplayer-test-media-0/play.mp3"),
                mediaDataSourceFactory, mainHandler, null);
player.prepare(mediaSource);
```

For dash

```
MediaSource mediaSource = new DashMediaSource(uri, buildDataSourceFactory(false),
            new DefaultDashChunkSource.Factory(mediaDataSourceFactory), mainHandler, null);
player.prepare(mediaSource);
```

If you use mp4, flv, mkv or other formats, you need to use ExtractorMediaSource as a MediaSource. Also we are using the ExtractorMediaSource for playing audio formats.Supported formats; mkv, mp4, mp3, ogg, ac3, flv, wav, flac.

```
*Audio*/
            MediaSource mediaSource = new ExtractorMediaSource(
                    Uri.parse("https://storage.googleapis.com/exoplayer-test-media-0/play.mp3"),
                mediaDataSourceFactory, extractorsFactory, null, null);


        /*Video*/
//        MediaSource mediaSource = new ExtractorMediaSource(Uri.parse("http://techslides.com/demos/sample-videos/small.mp4"),
//                mediaDataSourceFactory, extractorsFactory, null, null);
```

Reference from : https://github.com/google/ExoPlayer
```

License
--------


    Copyright 2017 Viram Purohit.

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

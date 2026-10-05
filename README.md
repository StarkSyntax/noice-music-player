NOICE - Native Offline Interface for Curated Entertainment

An offline Android music player. It plays the songs already on your phone, with no accounts, no ads, no internet and no tracking. Deep black screens, hand-drawn doodle controls, and one accent colour that you choose.

Why "NOICE"?

NOICE = Nice + Noise.

Music is noise arranged nicely, and the word is also a nod to Jake Peralta in Brooklyn Nine-Nine, who says it constantly. The long name came afterwards, so the letters had something to stand for.

Features

Browse

Five tabs: Albums, Library, Artists, Favorites, Playlists
Albums group songs by album name, so one movie is one album
Artists are split on , ; / &, so a song with two singers appears under both
Search by title, artist or album
Sort the library by title, artist, recently added or longest first

Play

PLAY plays a whole list in order. SHUFFLE plays it in random order
Now Playing: swipe the cover to skip, seek bar, shuffle, repeat, heart
Lock-screen and notification controls, background playback, pauses when headphones unplug
Mini-player on every screen

Queue

Play next puts a song right after the current one
Add to queue puts it after the songs you queued by hand, but before the rest of the list
The full queue is visible in Now Playing, with remove and clear
Sleep timer (15 to 90 minutes). It runs inside the playback service, so it still works if you swipe the app away

Your stuff

Favorites, via the heart in Now Playing or the ⋮ menu
Playlists: create, rename, delete, add and remove songs
The ⋮ menu on every song: Play next, Add to queue, Add to playlist, Favorite, Track details, Album, Artist, Share

Look

Pure black background throughout
Doodle style: wobbly hand-drawn outlines, a thin inner sketch line and diagonal hatching, inspired by the logo
Accent colour picker in Settings: 8 vivid presets, 8 soft presets, and a colour plus softness slider for your own mix. The whole app recolours live
Tech
	
Language	Kotlin 2.0
UI	Jetpack Compose (Material 3 for the base theme only; every control is custom-drawn)
Playback	Media3 (ExoPlayer, MediaSession, MediaSessionService)
Library	MediaStore
Storage	SharedPreferences (accent colour, favorites, playlists, sort order)
Min / target SDK	26 / 35
Package	com.starksyntax.musicplayer
How the doodle look works

All in ui/doodle/. No image assets are used for the controls.

Every shape is a sampled outline whose points are nudged by deterministic noise, so the same seed always gives the same wobble and nothing flickers.
Outlines are smoothed with Catmull-Rom curves so the wobble reads as a pen line.
Pen details are added on top: a thin inner line, and short diagonal hatch strokes.

Icons are drawn from point lists on a 24×24 grid in DoodleIcons.kt.

Project layout
app/src/main/java/com/starksyntax/musicplayer/
├── data/        Song, MusicRepository (MediaStore), Library (albums, artists, playlists, sort), UserPrefs
├── playback/    PlaybackService (ExoPlayer + session + sleep timer), PlayerViewModel, PlayerUiState
└── ui/
    ├── doodle/  the drawing engine, icons and custom components
    ├── theme/   colours, typography, accent CompositionLocals
    └── *.kt     screens: Home, Now Playing, Settings, Detail, Dialogs, ...
Build and run

You need Android Studio (recent) and JDK 17 (the one bundled with Android Studio is fine).

Open the folder that contains settings.gradle.kts.
Let Gradle sync. The wrapper uses Gradle 8.9.
Connect a phone with USB debugging on, or start an emulator with some audio files on it.
Press Run.
On first launch, allow access to audio files. On Android 13 or newer, allow notifications too, for the playback controls.
Install problems (Samsung)

If the install fails with INSTALL_FAILED_VERIFICATION_FAILURE, the phone's app verifier timed out. Retry first, then turn off Auto Blocker or Play Protect scanning temporarily, or run:

adb shell settings put global verifier_verify_adb_installs 0
Known limits
The queue is not restored after the app is fully closed
No equalizer, crossfade or gapless settings
Playlist songs cannot be reordered yet
Dark theme only
When several artists are credited in one tag, splitting uses common separators, because tags have no standard format
The notification and lock-screen cover art comes from Android's own album art and may be blank for some files
Roadmap
Restore the last queue and position on launch
Reorder songs inside playlists and in the queue
Equalizer
A hand-drawn font to match the doodles (drop a .ttf into res/font and set it in Type.kt)
Privacy

Everything stays on your phone. NOICE reads your audio files through Android's MediaStore, makes no network requests, and has no analytics.

Author

Built by Prasanth (StarkSyntax) with Claude.

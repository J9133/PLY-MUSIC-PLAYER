pkgname=ply-player
pkgver=1.1.0
pkgrel=1
pkgdesc="Music player, GUI and CLI"
arch=('any')
license=('MIT')
depends=(
  'python'
  'tk'
  'python-gobject'
  'gst-python'
  'gst-plugins-base'
  'gst-plugins-good'
  'python-mutagen'
  'python-rich'
  'python-pillow'
)
optdepends=(
  'gst-plugins-ugly: extra codecs (MP3)'
  'gst-libav: M4A/AAC and extra codecs'
  'libayatana-appindicator: system tray support'
  'python-pystray: system tray support (AUR)'
)

_appid="io.github.ahmedrapi79123_cyber.PLY-MUSIC-PLAYER"

package() {
  cd "$startdir"

  install -d "$pkgdir/usr/share/ply"
  install -m644 main.py cli.py gui.py player.py playlist.py \
        library.py settings.py config.py themes.py \
        icons.py utils.py mpris.py "$pkgdir/usr/share/ply/"
  
  cp -r assets "$pkgdir/usr/share/ply/assets"
  find "$pkgdir/usr/share/ply/assets" -type d -exec chmod 755 {} +
  find "$pkgdir/usr/share/ply/assets" -type f -exec chmod 644 {} +

  install -d "$pkgdir/usr/bin"
  printf '#!/bin/sh\nexec python /usr/share/ply/main.py "$@"\n' \
      > "$pkgdir/usr/bin/ply"
  chmod 755 "$pkgdir/usr/bin/ply"

  install -d "$pkgdir/usr/share/applications"
  cat > "$pkgdir/usr/share/applications/${_appid}.desktop" << EOF
[Desktop Entry]
Name=PLY Music Player
GenericName=Music Player
Comment=Simple and lightweight music player
Exec=ply %U
Icon=${_appid}
Terminal=false
Type=Application
Categories=AudioVideo;Audio;Player;Music;
Keywords=Music;Audio;Player;MP3;OGG;WAV;FLAC;
StartupNotify=true
MimeType=audio/mpeg;audio/ogg;audio/x-wav;audio/flac;audio/opus;audio/mp4;
EOF

  install -Dm644 assets/music.png \
      "$pkgdir/usr/share/icons/hicolor/128x128/apps/${_appid}.png"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"

  python -m compileall -q -d /usr/share/ply "$pkgdir/usr/share/ply"
}
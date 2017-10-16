#!/usr/bin/bash
# Maintainer: Andy Pieters <OU@AndyPieters.me.uk>

pkgname="packet-tracer"
_pktracer_realname="PacketTracer"
pkgver=7.1
pkgrel=2
arch=('x86_64')
pkgdesc="Cisco Packet Tracer is a powerful network simulation program that allows students to experiment with network behavior and ask “what if” questions. As an integral part of the Networking Academy comprehensive learning experience, Packet Tracer provides simulation, visualization, authoring, assessment, and collaboration capabilities and facilitates the teaching and learning of complex technology concepts."
url="http://www.cisco.com/web/learning/netacad/course_catalog/PacketTracer.html"
license=('custom')
options=('!strip')
install=packet-tracer.install
depends=(qt4 gstreamer openssl gconf zip unzip qt5-tools)

source=(

	"${_pktracer_realname}${pkgver//./}_64bit_linux.tar.gz" 
	
	packet-tracer.install PacketTracer.desktop
	
	packet-tracer.{c,}sh
)

md5sums=('11863bafc8675eeb3b3bb685956f4395'
         'a49df8948e035f4b707a2a42aaa5667b'
         'f9b3405ff44d3f7a1eb8ffa0842788b8'
         '4683103ae7ddfff80788b40fbbb23a4e'
         '72d328d175254f1346002a298530fb36')
sha256sums=('9c993e54e92512b080730e82d2f1ade9aa6b7a95098d2ce15af2b1c547903126'
            '0fc72736633757bf6aac506b0bb0eb7073e9555e5e1854f4a533854bec881486'
            '16f1a78f4dad2c4d8e17d01a3a340c293b8b971345374c5888ee701dae849548'
            '2c2724ec3df0bf8b732db98fbdf07bbaa62bdb1c59d689184118d6ae61a2dc97'
            '215750c2a9830d714b87be1d779c386cf0aa503c06842495e83fb3bd6b408a5f')
sha512sums=('05b2c81f4ef6ca97b7199d71ad94d5ddbfc784206245785c0cbd2665e77ab9af429482e032678fe833f74d122534dc69a7085a9e89e13a7aacab959526843b42'
            '0cd82090818d4967d39a43f1bec81bace623fb7ec4de8ff0037f9375ad24077c10c68cd80b3c144bc711444191f7a384a043b75cd80e9bd76f4b1d094230fca8'
            '1a744e26489b9534562d0a8b3346437528a98ee8726022627b9f81687a380ce562dbaa25af7d698179ad46f9afe4373349bf5e007db1f2b460af42e0f0704120'
            'cf9337d8ec48add4ff390efe6da93a64cdc67544802e9c6469b17457678c3b9664bd3003352796185eb612f6eb0fa560acc03593feb75c3d06dc6c573c98386d'
            '60aee51a250db6b877045a2af4f4ac79a79c12124615ab39c9a1b77cb9e628582e106644a734c559ee98a33119a5e40807241b76227e3f3516fad2ee4f815a11')

package() {

	cd "$srcdir"

	__srcpath="$(pwd)"
	
	__realpkgdir="${pkgdir}/usr/share/${pkgname}"
	
	#cd "${srcdir}/${_pktracer_realname}${pkgver//./}"
	
	# create directories
	find -type d -exec install -d --owner=root --group=root --mode=0755 "${__realpkgdir}/{}" ';'

	# copy Executables
	find '(' -not -type d ')' -and -executable \
	     -exec install --mode=0555 --owner=root --group=root '{}' "${__realpkgdir}/{}" ';'

	# and the rest
	find '(' -not -type d ')' -and '(' -not -executable ')' -and '(' -not -type l ')' \
	     -exec install --mode=0444 --owner=root --group=root '{}' "${__realpkgdir}/{}" ';'

	# there are several symbolic links in the lib  folder
	find lib/ -type l -exec cp -d '{}' "${__realpkgdir}/lib/" ';'
	
	# convenience links
	install -d --mode=0755 --owner=root --group=root "${pkgdir}/usr/bin"
	ln -s "/usr/share/${pkgname}/bin/PacketTracer7" "${pkgdir}/usr/bin/PacketTracer"
	ln -s "/usr/share/${pkgname}/bin/PacketTracer7" "${pkgdir}/usr/bin/PacketTracer7"
	
	# install in profile
	install -d --mode=0755 --owner=root --group=root "${pkgdir}/etc/profile.d"
	install --mode=0555 --owner=root --group=root "${__srcpath}/packet-tracer."{,c}sh "${pkgdir}/etc/profile.d/"
	
	# install the desktop files
	install -d --mode=0755 --owner=root --group=root "${pkgdir}/usr/share/applications/"
	install --mode=0444 --owner=root --group=root "${__srcpath}/PacketTracer.desktop" "${pkgdir}/usr/share/applications/"
	
	# and link the eula
	install -d --mode=0555 --owner=root --group=root "${pkgdir}/usr/share/licenses/${pkgname}"
	ln -s "${__realpkgdir}/eula.txt" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
	
	# there are some binaries called zip and unzip which shouldn't really be
	# added because we have our own versions.
	
	#./pkg/packet-tracer/usr/share/packet-tracer/bin/Linux/unzip:
	
	unlink "${__realpkgdir}/bin/Linux/unzip"
	unlink "${__realpkgdir}/bin/Linux/zip"
	
	# and replace them with a symbolic link to the system version.
	# only notable differences are in the unzip program, the version
	# provided here having two additional options:
	# -O CHARSET specify char. encoding for DOS,Win, and OS/2 archives
	# -I CHARSET specify char. encoding for UNIX and other archives.
	# which I think are irrelevant here.
	
	ln -s /usr/bin/unzip "${__realpkgdir}/bin/Linux/unzip"
	
	ln -s /usr/bin/zip "${__realpkgdir}/bin/Linux/zip"
	
	# so without those two, there's no need to add the zip license
	
	unlink "${__realpkgdir}/bin/ZIP_LICENSE"
	
	# there are other binaries in the source, such as 
	# libqtaccessiblecompatwidgets.so and other S/O's.
	#
	# one could experiment with just leaving them out and relying on the 
	# LD to use the system ones.
	
	# install the app icons
	install -d "${pkgdir}/usr/share/icons/hicolor/48x48/apps/"
	install "./art/app.png" "${pkgdir}/usr/share/icons/hicolor/48x48/apps/pt7.png"

	# I'm not going to bother with the templates either, which only set the LD_LIBRARY_PATH anyho
	
	# linguist is provided by qt5-tools, so we will delete that and replace it with a 
	# symbolic link
	
	unlink "${__realpkgdir}/bin/linguist"
	
	ln -s "/usr/bin/linguist" "${__realpkgdir}/bin/linguist"
	
	# we need to make a few symbolic links to make sure the online assessement work
        # it basically tries to call packet tracer with the old name and locations

        ln -s /usr/share/packet-tracer/bin/PacketTracer7 "${__realpkgdir}/bin/packettracer"
        ln -s /usr/share/packet-tracer/extensions "${__realpkgdir}/bin/extensions"

}

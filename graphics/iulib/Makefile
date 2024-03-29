# Created by: Hiroto Kagotani <hiroto.kagotani@gmail.com>
# $FreeBSD: head/graphics/iulib/Makefile 327733 2013-09-20 18:35:44Z bapt $

PORTNAME=	iulib
PORTVERSION=	0.4
PORTREVISION=	12
CATEGORIES=	graphics
MASTER_SITES=	GOOGLE_CODE
EXTRACT_SUFX=	.tgz

MAINTAINER=	hiroto.kagotani@gmail.com
COMMENT=	A library of image understanding-related algorithms

LICENSE=	APACHE20

LIB_DEPENDS=	libpng15.so:${PORTSDIR}/graphics/png \
		libjpeg.so:${PORTSDIR}/graphics/jpeg \
		libtiff.so:${PORTSDIR}/graphics/tiff

OPTIONS_DEFINE=	SDL VIDIO
SDL_DESC=	Enable SDL for graphical debugging
VIDIO_DESC=	Enable Video Input/Output (using ffmpeg)

USES=		libtool
USE_GCC=	any
USE_PYTHON_BUILD=	yes
USE_AUTOTOOLS=	libtoolize aclocal automake autoconf
ACLOCAL_ARGS=	--automake-acdir=${ACLOCAL_DIR} -I${LOCALBASE}/share/aclocal
AUTOMAKE_ARGS=	--add-missing
USE_LDCONFIG=	yes
CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib
INSTALL_TARGET=	install-strip

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MSDL}
USE_SDL=	sdl gfx
PLIST_SUB+=	SDL=""
.else
CONFIGURE_ARGS+=--without-SDL
PLIST_SUB+=	SDL="@comment "
.endif

.if ${PORT_OPTIONS:MVIDIO}
LIB_DEPENDS+=	libavcodec.so:${PORTSDIR}/multimedia/ffmpeg
.endif

post-patch:
.if ! ${PORT_OPTIONS:MVIDIO}
	@${REINPLACE_CMD} -e 's/novidio, 0/novidio, 1/' ${WRKSRC}/configure.ac
.endif
	@${REINPLACE_CMD} -e 's/nov4l2, 0/nov4l2, 1/' ${WRKSRC}/configure.ac

pre-configure:
	@(cd ${CONFIGURE_WRKSRC} \
	  && ${SETENV} ${PYTHON_CMD} genAM.py >Makefile.am \
	  && ${SETENV} ${AUTOTOOLS_ENV} ${LIBTOOLIZE} --automake)

run-autotools: run-autotools-aclocal run-autotools-automake run-autotools-autoconf

.include <bsd.port.mk>

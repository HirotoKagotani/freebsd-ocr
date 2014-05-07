# Created by: Hiroto Kagotani <hiroto.kagotani@gmail.com>
# $FreeBSD: head/japanese/nhocr/Makefile 327737 2013-09-20 18:47:54Z bapt $

PORTNAME=	nhocr
PORTVERSION=	0.21
CATEGORIES=	japanese graphics
MASTER_SITES=	${MASTER_SITE_GOOGLE_CODE}

MAINTAINER=	hiroto.kagotani@gmail.com
COMMENT=	OCR engine for Japanese language

LICENSE=	APACHE20

BUILD_DEPENDS=	${LOCALBASE}/lib/libsip.a:${PORTSDIR}/graphics/O2-tools

GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--with-O2tools=${LOCALBASE} --datadir=${DATADIR}

post-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/share/ocropus/scripts
	${INSTALL_DATA} ${WRKSRC}/ocropus/rec-nhocr-0.3.lua ${STAGEDIR}${PREFIX}/share/ocropus/scripts/rec-nhocr.lua
	@${CAT} ${PKGMESSAGE}

.include <bsd.port.mk>

# Copyright (c) 2006, 2013, Oracle and/or its affiliates. All rights reserved.
# 
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; version 2 of the License.
# 
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
# 
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301 USA

INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/extra/yassl/taocrypt/mySTL
                    ${CMAKE_SOURCE_DIR}/extra/yassl/taocrypt/include)

INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/include)
ADD_DEFINITIONS(${SSL_DEFINES})
SET(TAOCRYPT_SOURCES		src/aes.cpp src/aestables.cpp src/algebra.cpp src/arc4.cpp src/asn.cpp src/coding.cpp 
				src/des.cpp src/dh.cpp src/dsa.cpp src/file.cpp src/hash.cpp src/integer.cpp src/md2.cpp 
				src/md4.cpp src/md5.cpp src/misc.cpp src/random.cpp src/ripemd.cpp src/rsa.cpp src/sha.cpp 
                                src/rabbit.cpp src/hc128.cpp
				include/aes.hpp include/algebra.hpp include/arc4.hpp include/asn.hpp include/block.hpp 
				include/coding.hpp include/des.hpp include/dh.hpp include/dsa.hpp include/dsa.hpp
				include/error.hpp include/file.hpp include/hash.hpp include/hmac.hpp include/integer.hpp 
				include/md2.hpp include/md5.hpp include/misc.hpp include/modarith.hpp include/modes.hpp
				include/random.hpp include/ripemd.hpp include/rsa.hpp include/sha.hpp
                                include/rabbit.hpp include/hc128.hpp)

IF(HAVE_EXPLICIT_TEMPLATE_INSTANTIATION)
  SET(TAOCRYPT_SOURCES ${TAOCRYPT_SOURCES} src/template_instnt.cpp)
ENDIF()

ADD_CONVENIENCE_LIBRARY(taocrypt ${TAOCRYPT_SOURCES})
RESTRICT_SYMBOL_EXPORTS(taocrypt)

INSTALL_DEBUG_SYMBOLS(taocrypt)
IF(MSVC)
   INSTALL_DEBUG_TARGET(taocrypt DESTINATION ${INSTALL_LIBDIR}/debug)
ENDIF()


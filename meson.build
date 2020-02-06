project( 'zlib', 'c', version : '1.2.11' )

sources = [
    'adler32.c',
    'compress.c',
    'crc32.c',
    'deflate.c',
    'gzclose.c',
    'gzlib.c',
    'gzread.c',
    'gzwrite.c',
    'inflate.c',
    'infback.c',
    'inftrees.c',
    'inffast.c',
    'trees.c',
    'uncompr.c',
    'zutil.c'
]

c_args = []
dep_args = []

if host_machine.system() != 'windows'
    c_args += '-DHAVE_HIDDEN'
    if meson.get_compiler( 'c' ).check_header( 'unistd.h' )
        c_args += '-DHAVE_UNISTD_H'
    endif
    libname = 'z'
else
    c_args += '-DZLIB_DLL'
    dep_args += '-DZLIB_DLL'
    sources += import( 'windows' ).compile_resources( 'win32/zlib1.rc' )
    libname = 'zlib1'
endif

zlib_lib = library( libname, sources : sources, c_args : c_args, install : true )
zlib_lic = files( 'LICENSE' )
zlib_dep = declare_dependency( include_directories : include_directories( '.' ), compile_args : dep_args, link_with : zlib_lib )
install_headers( 'zconf.h', 'zlib.h' )

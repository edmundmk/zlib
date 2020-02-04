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

if host_machine.system() != 'windows'
    export_args = [ '-DHAVE_HIDDEN' ]
    import_args = []
    if meson.get_compiler( 'c' ).check_header( 'unistd.h' )
        export_args += '-DHAVE_UNISTD_H'
    endif
    zlib_lib = library( 'z', sources : sources, c_args : export_args, install : true )
else
    export_args = [ '-DZLIB_DLL' ]
    import_args = [ '-DZLIB_DLL' ]
    sources += import( 'windows' ).compile_resources( 'win32/zlib1.rc' )
    zlib_lib = library( 'zlib1', sources : sources, c_args : export_args, install : true )
endif

zlib_lic = files( 'LICENSE' )
zlib_dep = declare_dependency( include_directories : include_directories( '.' ), compile_args : import_args, link_with : zlib_lib )
install_headers( 'zconf.h', 'zlib.h' )

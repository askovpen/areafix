project('areafix','c', version:'1.9.0')

cc = meson.get_compiler('c')

link_args = []
compile_args = []

if cc.get_id() == 'msvc'
  add_project_arguments(
    '-D_CRT_SECURE_NO_DEPRECATE',
    '-D_CRT_NONSTDC_NO_DEPRECATE', 
    '-DWIN32',
    '-D_WINDOWS',
    '-D_CONSOLE',
    language : 'c')
  if get_option('default_library') != 'static'
    add_project_arguments('-D_DLL', '-D_MAKE_DLL', language : 'c')
  endif

else
  add_project_arguments(
    '-DUNIX',
  language : 'c')
endif

src=files([
  'src/afglobal.c',
  'src/areafix.c',
  'src/callback.c',
  'src/query.c',
  'src/version.c'
])

headers = files([
  'areafix/afglobal.h',
  'areafix/areafix.h',
  'areafix/callback.h',
  'areafix/query.h',
  'areafix/version.h',
])

incdir = include_directories(['areafix','.'])

fidoconf_proj = subproject('fidoconf')
fidoconf_dep=fidoconf_proj.get_variable('fidoconf_dep')

libareafix = library('areafix', src,
  include_directories : incdir,
  dependencies:[fidoconf_dep],
  version:'1.9.0',
  install : true)

fidoconf_dep = declare_dependency(
  link_with: libareafix,
  dependencies: [fidoconf_dep],
  include_directories : incdir)

install_headers(headers, subdir: 'areafix')

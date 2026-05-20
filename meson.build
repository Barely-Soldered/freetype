project('freetype', 'c',
  version: '2.14.3',
  license: 'FTL',
  meson_version: '>= 1.0.0',
  default_options: ['c_std=c99', 'warning_level=1', 'default_library=static'],
)

zlib_dep = dependency('zlib', required: true)
libpng_dep = dependency('libpng', required: true)

freetype_sources = files(
  'src/base/ftbase.c',
  'src/base/ftinit.c',
  'src/base/ftbbox.c',
  'src/base/ftbitmap.c',
  'src/base/ftfstype.c',
  'src/base/ftgasp.c',
  'src/base/ftglyph.c',
  'src/base/ftmm.c',
  'src/base/ftpatent.c',
  'src/base/ftstroke.c',
  'src/base/ftsynth.c',
  'src/base/md5.c',
  'src/base/ftsystem.c',
  'src/base/ftdebug.c',
  'src/autofit/autofit.c',
  'src/cache/ftcache.c',
  'src/cff/cff.c',
  'src/gzip/ftgzip.c',
  'src/psaux/psaux.c',
  'src/pshinter/pshinter.c',
  'src/psnames/psnames.c',
  'src/raster/raster.c',
  'src/sdf/sdf.c',
  'src/sfnt/sfnt.c',
  'src/smooth/smooth.c',
  'src/svg/svg.c',
  'src/truetype/truetype.c',
)

if host_machine.system() == 'windows'
  winmod = import('windows')
  freetype_sources += winmod.compile_resources('src/base/ftver.rc')
endif

freetype_inc = include_directories('include')
freetype_public_inc = include_directories('include', is_system: true)

freetype_lib = static_library('freetype', freetype_sources,
  c_args: ['-DFT2_BUILD_LIBRARY=1'],
  include_directories: freetype_inc,
  dependencies: [zlib_dep, libpng_dep],
)

freetype_dep = declare_dependency(
  link_with: freetype_lib,
  include_directories: freetype_public_inc,
  dependencies: [zlib_dep, libpng_dep],
)

meson.override_dependency('freetype2', freetype_dep)
meson.override_dependency('freetype', freetype_dep)

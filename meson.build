project(
  'arc-theme-mono',
  version : 'idk',
  meson_version: '>= 0.53.0',
  license : 'GPL3',
  default_options : [
    'debug=false'
  ]
)

fs = import('fs')

variant_name = {
  'dark' : 'Arc-Mono',
}

prefix = get_option('prefix')
datadir = get_option('datadir')

install_dir = {
  'dark' : datadir / 'themes' / variant_name.get('dark'),
}

# sassc dependency
foreach theme : ['cinnamon', 'gnome-shell', 'gtk3', 'gtk4']
  if theme in get_option('themes')
    sassc = find_program('sassc')
    if get_option('debug')
      sassc_options = ['--line-numbers', '--style', 'nested']
    else
      sassc_options = ['--style', 'compact']
    endif
    break
  endif
endforeach

# inkscape dependency
foreach theme : ['gtk2', 'gtk3', 'gtk4', 'xfwm']
  if theme in get_option('themes')
    inkscape = find_program('inkscape', required : false)
    if inkscape.found()
      inkscape_ver = run_command(inkscape, '--version', check : true).stdout().split()[1]
    endif
    break
  endif
endforeach

# glib-compile-resources dependency
foreach theme : ['gnome-shell', 'gtk3', 'gtk4']
  if theme in get_option('themes')
    if theme == 'gnome-shell' and not get_option('gnome_shell_gresource')
      continue
    endif
    glib_compile_resources = find_program('glib-compile-resources')
    break
  endif
endforeach

install_file = meson.source_root() / 'meson/install-file.py'

meson.add_dist_script('meson/render-assets.py')

subdir('common')

project(
  'geany-code-format',
  'c',
  license : 'GPL-2.0-or-later',
  default_options : ['buildtype=release', 'prefix=/usr']
)

prefix = get_option('prefix')

plugin_name = meson.project_name().replace('geany-', '')
project_datadir = get_option('datadir') / meson.project_name()
project_docdir = get_option('datadir') / 'doc' / meson.project_name()
plugin_conf = plugin_name + '.conf'

doc_readme = 'Readme.md'

geany = dependency('geany')

conf_data = configuration_data()
conf_data.set('version', meson.project_version())

conf_data.set('prefix', prefix)
conf_data.set('project_datadir', project_datadir)
conf_data.set('project_docdir', project_datadir)

conf_data.set('plugin_conf', plugin_conf)
conf_data.set('doc_readme', doc_readme)

config_h = configure_file(
  input: 'config.h.in',
  output: 'config.h',
  configuration: conf_data,
)

library(
  plugin_name,
  sources: [
    config_h,
    'source/format.c',
    'source/plugin.c',
    'source/prefs.c',
    'source/process.c',
    'source/style.c',
  ],
  dependencies: [geany],
  name_prefix: '',
  install: true,
  install_dir: get_option('libdir') / 'geany',
)

install_data(
  sources: [
    'data' / plugin_conf,
  ],
  install_dir: project_datadir,
)

install_data(
  sources: [
    doc_readme,
  ],
  install_dir: project_docdir,
)

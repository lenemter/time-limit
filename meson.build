project('com.github.marbetschar.time-limit', 'vala', 'c')

gnome = import('gnome')
i18n = import('i18n')

add_project_arguments([
        '-DGETTEXT_PACKAGE="@0@"'.format(meson.project_name())
    ],
    language: 'c'
)

asresources = gnome.compile_resources(
    'as-resources',
    'data/' + meson.project_name() + '.gresource.xml',
    source_dir: 'data',
    c_name: 'as'
)

dependencies = [
    dependency('glib-2.0'),
    dependency('gtk4'),
    dependency('granite-7', version: '>=7.0.0'),
    meson.get_compiler('c').find_library('m', required : false)
]

subdir('src')
subdir('tests')

tests_exec = executable(
  meson.project_name() + '-tests',
  tests + sources,
  dependencies: dependencies,
  vala_args: '--define=IS_TEST'
)
test('Tests', tests_exec)

executable(
    meson.project_name(),
    asresources,
    sources,
    dependencies: dependencies,
    install: true
)

subdir('data')
subdir('po')

meson.add_install_script('meson/post_install.py')
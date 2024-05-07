project('libvivhook',
	'c', 'cpp',
	version: '1.0.0',
	license: 'MIT',
	default_options: [
		'c_std=gnu99',
	],
)

cc = meson.get_compiler('c')
add_project_arguments(cc.get_supported_arguments([
		'-feliminate-unused-debug-types',
		'-Wnested-externs',
		'-Wcast-qual',
		'-Wredundant-decls',
		'-Werror=write-strings',
		'-Wshadow',
]), language: ['c'])

add_project_arguments([
	'-D_GNU_SOURCE',
], language: 'c')

dl = cc.find_library('dl', required: true)
galcore = declare_dependency(
	include_directories: include_directories(get_option('galcore-include')),
	link_args: ['-L'+ get_option('galcore-lib'), '-lGAL'],
)

vivhook_src = files(
	'src/elf_hook.c',
	'src/flightrecorder.cpp',
	'src/viv_hook.c',
)

libvivhook = library('vivhook',
	vivhook_src,
	dependencies: [dl, galcore],
)

viv_interpose_src = vivhook_src + files(
	'src/viv_interpose.c',
)

viv_interpose = shared_library('viv_interpose',
	viv_interpose_src,
	name_prefix: '',
	dependencies: [dl, galcore],
)


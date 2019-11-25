project('steamaudio', license: 'proprietary', version: '2.0-beta17')

incdir = include_directories('include')

arch = host_machine.cpu_family()

sys = host_machine.system()
if sys == 'android'
	sys = 'Android'
elif sys == 'windows'
	sys = 'Windows'
	if arch == 'x86'
		sys = sys / 'x86'
	elif arch == 'x86_64'
		sys = sys / 'x64'
	else
		error('Unsupported cpu arch')
	endif
elif sys == 'linux'
	sys = 'Linux'
	if arch == 'x86'
		sys = sys / 'x86'
	elif arch == 'x86_64'
		sys = sys / 'x64'
	else
		error('Unsupported cpu arch')
	endif
elif sys == 'darwin'
	sys = 'OSX'
else
	error('Steamaudio does not support this system')
endif

libpath = meson.current_source_dir() / 'lib' / sys
cc = meson.get_compiler('c')

lib_phonon = cc.find_library('phonon', dirs: libpath)
steamaudio_dep = declare_dependency(
	include_directories: incdir,
	dependencies: lib_phonon,
)

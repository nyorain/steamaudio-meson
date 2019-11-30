project('steamaudio', license: 'proprietary', version: '2.0-beta17')

incdir = include_directories('include')
cc = meson.get_compiler('c')

arch = host_machine.cpu_family()
android = (cc.get_define('__ANDROID__') != '')

sys = host_machine.system()
if sys == 'windows'
	sys = 'Windows'
	if arch == 'x86'
		sys = sys / 'x86'
	elif arch == 'x86_64'
		sys = sys / 'x64'
	else
		error('Unsupported cpu arch')
	endif
elif sys == 'linux'
	# NOTE: steamaudio only provides the android library for armeabi,
	# not armv8-64 (meson arch is then aarch64)
	if android and arch == 'arm'
		sys = 'Android'
	elif arch == 'x86'
		sys = 'Linux' / 'x86'
	elif arch == 'x86_64'
		sys = 'Linux' / 'x64'
	else
		error('Unsupported cpu arch/system combination')
	endif
elif sys == 'darwin'
	sys = 'OSX'
else
	error('Steamaudio does not support this system')
endif

libpath = meson.current_source_dir() / 'lib' / sys

lib_phonon = cc.find_library('phonon', dirs: libpath)
steamaudio_dep = declare_dependency(
	include_directories: incdir,
	dependencies: lib_phonon,
)

#!/usr/bin/env python

import sys
env = Environment(CCFLAGS='-Wall -g', CPPFLAGS='-D_GNU_SOURCE')

opts = Variables('pkt2flow.conf')
opts.Add(PathVariable('PREFIX', 'Directory to install under', '/usr/local', PathVariable.PathIsDir))
opts.Update(env)
opts.Save('pkt2flow.conf', env)

Help(opts.GenerateHelpText(env))

idir_prefix = '$PREFIX'
idir_bin    = '$PREFIX/bin'

Export('env idir_prefix idir_bin')

platform = sys.platform
lib_path = ['/usr/local/lib', '/usr/lib']
libs = Glob('./*.a') + ['pcap']
cpp_path=['.']

if platform == 'darwin':
      env.Append(CPPFLAGS=['-Ddarwin'])

# Compile the programs
pkt2flow = env.Program(target = './pkt2flow', 
			source = Glob('./*.c'),
			LIBPATH = lib_path,
			LIBS = libs,
			CPPPATH = cpp_path)

# install the program
env.Install(dir = idir_bin, source = pkt2flow)

# create an install alias
env.Alias('install', idir_prefix)

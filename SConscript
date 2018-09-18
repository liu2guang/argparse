# 
# @File:   SConscript 
# @Author: buildpkg.py 
# @Date:   2018-09-19 00:16:09
#
# @LICENSE: {{license}}.
#
# Change Logs:
# Date           Author       Notes
# 2018-09-19     buildpkg.py  Generate the scons script automatically.

import os
from building import * 

# get current dir path
cwd = GetCurrentDir()

# init src and inc vars
src = []
inc = []

name    = "argparse"
version = "v1.0.0"

# print debug info
# print(name + '-' + version)
# print('PKG_USING_' + name.upper()) 

# add to project 
def make_pkg(f):
    fs = os.listdir(f)
    for f1 in fs:
        tmp_path = os.path.join(f, f1)

        if os.path.isdir(tmp_path):
            make_pkg(tmp_path)

        else: 
            suffix = os.path.splitext(tmp_path)[1]

            if suffix   == '.c':
                src.append(tmp_path)
            elif suffix == '.h':
                inc.append(f)
            
make_pkg(cwd) 

# add group to IDE project
objs = DefineGroup(name + '-' + version, src, depend = ['PKG_USING_' + name.upper()], CPPPATH = inc)

# traversal subscript
list = os.listdir(cwd)
if GetDepend('PKG_USING_' + name.upper()):
    for d in list:
        path = os.path.join(cwd, d)
        if os.path.isfile(os.path.join(path, 'SConscript')):
            objs = objs + SConscript(os.path.join(d, 'SConscript'))

Return('objs') 
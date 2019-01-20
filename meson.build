project('PyD', 'd',
    meson_version: '>=0.46',
    license: 'MIT',
    version: '0.10.5'
)

project_soversion = '0'


infra_src_dir = include_directories('infrastructure/')

pkgc = import('pkgconfig')
py_dep = dependency('python3')

pyd_src = [
    'infrastructure/deimos/python/abstract_.d',
    'infrastructure/deimos/python/ast.d',
    'infrastructure/deimos/python/boolobject.d',
    'infrastructure/deimos/python/bufferobject.d',
    'infrastructure/deimos/python/bytearrayobject.d',
    'infrastructure/deimos/python/bytesobject.d',
    'infrastructure/deimos/python/cellobject.d',
    'infrastructure/deimos/python/ceval.d',
    'infrastructure/deimos/python/classobject.d',
    'infrastructure/deimos/python/cobject.d',
    'infrastructure/deimos/python/codecs.d',
    'infrastructure/deimos/python/code.d',
    'infrastructure/deimos/python/compile.d',
    'infrastructure/deimos/python/complexobject.d',
    'infrastructure/deimos/python/context.d',
    'infrastructure/deimos/python/cStringIO.d',
    'infrastructure/deimos/python/datetime.d',
    'infrastructure/deimos/python/descrobject.d',
    'infrastructure/deimos/python/dictobject.d',
    'infrastructure/deimos/python/enumobject.d',
    'infrastructure/deimos/python/errcode.d',
    'infrastructure/deimos/python/eval.d',
    'infrastructure/deimos/python/fileobject.d',
    'infrastructure/deimos/python/floatobject.d',
    'infrastructure/deimos/python/frameobject.d',
    'infrastructure/deimos/python/funcobject.d',
    'infrastructure/deimos/python/genobject.d',
    'infrastructure/deimos/python/grammar.d',
    'infrastructure/deimos/python/import_.d',
    'infrastructure/deimos/python/internal/context.d',
    'infrastructure/deimos/python/internal/hamt.d',
    'infrastructure/deimos/python/intobject.d',
    'infrastructure/deimos/python/intrcheck.d',
    'infrastructure/deimos/python/iterobject.d',
    'infrastructure/deimos/python/listobject.d',
    'infrastructure/deimos/python/longintrepr.d',
    'infrastructure/deimos/python/longobject.d',
    'infrastructure/deimos/python/marshal.d',
    'infrastructure/deimos/python/memoryobject.d',
    'infrastructure/deimos/python/methodobject.d',
    'infrastructure/deimos/python/modsupport.d',
    'infrastructure/deimos/python/moduleobject.d',
    'infrastructure/deimos/python/node.d',
    'infrastructure/deimos/python/object.d',
    'infrastructure/deimos/python/objimpl.d',
    'infrastructure/deimos/python/odictobject.d',
    'infrastructure/deimos/python/osmodule.d',
    'infrastructure/deimos/python/parsetok.d',
    'infrastructure/deimos/python/pgenheaders.d',
    'infrastructure/deimos/python/pyarena.d',
    'infrastructure/deimos/python/pyatomic.d',
    'infrastructure/deimos/python/pycapsule.d',
    'infrastructure/deimos/python/pydebug.d',
    'infrastructure/deimos/python/pyerrors.d',
    'infrastructure/deimos/python/pymem.d',
    'infrastructure/deimos/python/pyport.d',
    'infrastructure/deimos/python/pystate.d',
    'infrastructure/deimos/python/pystrcmp.d',
    'infrastructure/deimos/python/pystrtod.d',
    'infrastructure/deimos/python/Python.d',
    'infrastructure/deimos/python/pythonrun.d',
    'infrastructure/deimos/python/pythread.d',
    'infrastructure/deimos/python/rangeobject.d',
    'infrastructure/deimos/python/setobject.d',
    'infrastructure/deimos/python/sliceobject.d',
    'infrastructure/deimos/python/stringobject.d',
    'infrastructure/deimos/python/structmember.d',
    'infrastructure/deimos/python/structseq.d',
    'infrastructure/deimos/python/symtable.d',
    'infrastructure/deimos/python/sysmodule.d',
    'infrastructure/deimos/python/timefuncs.d',
    'infrastructure/deimos/python/traceback.d',
    'infrastructure/deimos/python/tupleobject.d',
    'infrastructure/deimos/python/unicodeobject.d',
    'infrastructure/deimos/python/warnings.d',
    'infrastructure/deimos/python/weakrefobject.d',

    'infrastructure/pyd/class_wrap.d',
    'infrastructure/pyd/ctor_wrap.d',
    'infrastructure/pyd/def.d',
    'infrastructure/pyd/embedded.d',
    'infrastructure/pyd/exception.d',
    'infrastructure/pyd/extra.d',
    'infrastructure/pyd/func_wrap.d',
    'infrastructure/pyd/make_object.d',
    'infrastructure/pyd/make_wrapper.d',
    'infrastructure/pyd/op_wrap.d',
    'infrastructure/pyd/pyd.d',
    'infrastructure/pyd/pydobject.d',
    'infrastructure/pyd/references.d',
    'infrastructure/pyd/struct_wrap.d',
    'infrastructure/pyd/thread.d',

    'infrastructure/util/conv.d',
    'infrastructure/util/multi_index.d',
    'infrastructure/util/replace.d',
    'infrastructure/util/typeinfo.d',
    'infrastructure/util/typelist.d',
]

install_subdir('infrastructure/deimos/', install_dir: 'include/d/pyd/')
install_subdir('infrastructure/pyd/',    install_dir: 'include/d/pyd/')
install_subdir('infrastructure/util/',   install_dir: 'include/d/pyd/')

target_os = target_machine.system()

if target_os == 'linux'
    mod_versions = ['Python_Unicode_UCS4']
elif target_os == 'darwin'
    mod_versions = ['Python_Unicode_UCS2']
elif target_os == 'windows'
    mod_versions = ['Python_Unicode_UCS2']
else
    error('Tried to build for a (currently) unsupported operating system.')
endif

python_version = py_dep.version()
if python_version.version_compare('< 3.5')
    error(' The detected version of Python (' + python_version + ') is too low. Need at least Python 3.5.')
endif

mod_versions += [
    'Python_2_4_Or_Later',
    'Python_2_5_Or_Later',
    'Python_2_6_Or_Later',
    'Python_2_7_Or_Later',
    'Python_3_0_Or_Later',
    'Python_3_1_Or_Later',
    'Python_3_2_Or_Later',
    'Python_3_3_Or_Later',
    'Python_3_4_Or_Later',
    'Python_3_5_Or_Later'
]

if python_version.version_compare('>= 3.6')
    mod_versions += ['Python_3_6_Or_Later']
endif
if python_version.version_compare('>= 3.7')
    mod_versions += ['Python_3_7_Or_Later']
endif

pyd_lib = library('pyd',
        [pyd_src],
        include_directories: [infra_src_dir],
        dependencies: [py_dep],
        d_module_versions: mod_versions,
        install: true,
        version: meson.project_version(),
        soversion: project_soversion
)
pkgc.generate(name: 'pyd',
              libraries: pyd_lib,
              subdirs: 'd/pyd/',
              d_module_versions: mod_versions,
              version: meson.project_version(),
              description: 'D library that wraps the raw Python/C API with a cleaner, simpler interface.'
)

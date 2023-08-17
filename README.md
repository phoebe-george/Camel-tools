---
description: installation of camel-tool version 1.5.1 using easy-build
---

# camel-tools Installation



{% hint style="info" %}
First you must check the python version of all the dependencies

Second you need to check the python back-end as there is conflict between poetry and hatchling in  packaging that happen in request&#x20;

Third change the toolchain is some time better than change python version in the existing filse
{% endhint %}

***

### Using existing easy-build files but change the toolchain use

```bash
FLAGS= --use-existing-modules  --buildpath=/eb_build -r
eb (filename.eb) --try-toolchain=(ex:GCC,10.2.0) --try-update-deps --experimental ${FLAGS} 
```

{% hint style="info" %}
some times there are missing dependencies due change toolchain solve it by download this dependencies
{% endhint %}

#### Files name :

```bash
# SciPy-bundle include numpy panda scipy
#for missing dependencies
eb hypothesis-6.46.7-GCCcore-11.3.0.eb --try-toolchain=GCCcore,10.2.0 ${FLAGS}
eb pybind11-2.9.2-GCCcore-11.3.0.eb --try-toolchain=GCCcore,10.2.0 ${FLAGS}
# for install SciPy-bundle
eb SciPy-bundle-2022.05-fosscuda-2020b-Python-3.10.4.eb --try-toolchain=GCCcore,10.2.0 ${FLAGS}
 
 # for install dill
 eb dill-0.3.6-GCCcore-11.3.0.eb --try-toolchain=GCCcore,10.2.0 ${FLAGS}
 
```



### Files write from scratch

<pre class="language-bash"><code class="lang-bash"><strong># future create file
</strong><strong>cat > future-0.18.3.-fosscuda-2020b-Python-3.10.4.eb &#x3C;&#x3C; EOF
</strong>
# easy-build file configuration for future
easyblock = 'PythonPackage'

name = 'future'
version = '0.18.3'
versionsuffix = '-Python-%(pyver)s'

homepage = 'https://python-future.org/'
description = "python-future is the missing compatibility layer between Python 2 and Python 3."

toolchain = {'name': 'fosscuda', 'version': '2020b'}

sources = [SOURCE_TAR_GZ]
checksums = ['34a17436ed1e96697a86f9de3d15a3b0be01d8bc8de9c1dffd59fb8234ed5307']

dependencies = [('Python', '3.10.4')]

use_pip = True
download_dep_fail = True

moduleclass = 'lib'

EOF

# run command for future 
eb future-0.18.3.-fosscuda-2020b-Python-3.10.4.eb -r




# create six file 
cat > six-1.16.0-fosscuda-2020b-Python-3.10.4.eb &#x3C;&#x3C; EOF

# easy-build file configuration for six
easyblock = 'PythonPackage'

name = 'six'
version = '1.16.0'
versionsuffix = '-Python-%(pyver)s'

homepage = 'https://python-future.org/'
description = "Six is a Python 2 and 3 compatibility library.  It provides utility functions for smoothing over the differences between the Python v$

toolchain = {'name': 'fosscuda', 'version': '2020b'}

sources = [SOURCE_TAR_GZ]
checksums = ['1e61c37477a1626458e36f7b1d82aa5c9b094fa4802892072e49de9c60c4c926']

dependencies = [('Python', '3.10.4')]

use_pip = True
download_dep_fail = True

moduleclass = 'lib'
EOF

# run command for six
eb six-1.16.0-fosscuda-2020b-Python-3.10.4.eb -r



# create docot file 
cat > docopt-0.6.2-fosscuda-2020b-Python-3.10.4.eb &#x3C;&#x3C; EOF

# easy-build file configuration for docopt
 
easyblock = 'PythonPackage'

name = 'docopt'
version = '0.6.2'
versionsuffix = '-Python-%(pyver)s'

homepage = 'https://python-future.org/'
description = "creates beautiful command-line interfaces."

toolchain = {'name': 'fosscuda', 'version': '2020b'}

sources = [SOURCE_TAR_GZ]
checksums = ['49b3a825280bd66b3aa83585ef59c4a8c82f2c8a522dbe754a8bc8d08c85c491']

dependencies = [('Python', '3.10.4')]

use_pip = True
download_dep_fail = True

moduleclass = 'lib'

EOF

# run command for docopt
eb docopt-0.6.2-fosscuda-2020b-Python-3.10.4.eb -r





# create cachetools file 
cat > cachetools-5.3.1-fosscuda-2020b-Python-3.10.4.eb &#x3C;&#x3C; EOF

# easy-build file configuration for cachetools
 
easyblock = 'PythonPackage'

name = 'cachetools'
version = '5.3.1'
versionsuffix = '-Python-%(pyver)s'

homepage = 'https://python-future.org/'
description = "This module provides various memoizing collections and decorators, including variants of the Python Standard Library’s @lru_cache fun$

toolchain = {'name': 'fosscuda', 'version': '2020b'}

sources = [SOURCE_TAR_GZ]
checksums = ['dce83f2d9b4e1f732a8cd44af8e8fab2dbe46201467fc98b3ef8f269092bf62b']

dependencies = [('Python', '3.10.4')]

use_pip = True
download_dep_fail = True

moduleclass = 'lib'

EOF

# run command for cachetools
eb cachetools-5.3.1-fosscuda-2020b-Python-3.10.4.eb -r







# create scikit-learn file 
cat > scikit-learn-1.1.2-fosscuda-2020b-Python-3.10.4.eb &#x3C;&#x3C; EOF

# easy-build file configuration for scikit-learn
 
easyblock = 'PythonBundle'

name = 'scikit-learn'
version = '1.1.2'

homepage = 'https://scikit-learn.org/stable/index.html'
description = """Scikit-learn integrates machine learning algorithms in the tightly-knit scientific Python world,
building upon numpy, scipy, and matplotlib. As a machine-learning module,
it provides versatile tools for data mining and analysis in any field of science and engineering.
It strives to be simple and efficient, accessible to everybody, and reusable in various contexts."""

toolchain = {'name': 'fosscuda', 'version': '2020b'}

dependencies = [
    ('Python', '3.10.4'),
    ('SciPy-bundle', '2022.05'),
]

use_pip = True
sanity_pip_check = True

exts_list = [
    (name, version, {
        'modulename': 'sklearn',
        'checksums': ['7c22d1305b16f08d57751a4ea36071e2215efb4c09cb79183faa4e8e82a3dbf8'],
    }),
    ('sklearn', '0.0', {
        'checksums': ['e23001573aa194b834122d2b9562459bf5ae494a2d59ca6b8aa22c85a44c0e31'],
    }),
]

moduleclass = 'data'

EOF

# run command for scikit-learn
eb scikit-learn-1.1.2-fosscuda-2020b-Python-3.10.4.eb --buildpath=/eb_build -r







# create PyTorch file 
cat > PyTorch-1.9.0-fosscuda-2020b.eb &#x3C;&#x3C; EOF

# easy-build file configuration for PyTorch
 
name = 'PyTorch'
version = '1.9.0'

homepage = 'https://pytorch.org/'
description = """Tensors and Dynamic neural networks in Python with strong GPU acceleration.
PyTorch is a deep learning framework that puts Python first."""

toolchain = {'name': 'fosscuda', 'version': '2020b'}

sources = [{
    'filename': '%(name)s-%(version)s.tar.gz',
    'git_config': {
        'url': 'https://github.com/pytorch',
        'repo_name': 'pytorch',
        'tag': 'v%(version)s',
        'recursive': True,
    },
}]
patches = [
    'PyTorch-1.6.0_fix-test-dataloader-fixed-affinity.patch',
    'PyTorch-1.7.0_avoid-nan-in-test-torch.patch',
    'PyTorch-1.7.0_disable-dev-shm-test.patch',
    'PyTorch-1.7.1_correctly-pass-jit_opt_level.patch',
    'PyTorch-1.7.1_fix-alias-violation-in-bitwise-ops.patch',
    'PyTorch-1.8.1_dont-use-gpu-ccc-in-test.patch',
    'PyTorch-1.8.1_fix-arange-on-VSX.patch',
    'PyTorch-1.8.1_fix-faulty-asserts-and-skip-test.patch',
    'PyTorch-1.8.1_increase-distributed-test-timeout.patch',
    'PyTorch-1.8.1_skip_dist_autograd_sync_streams.patch',
    'PyTorch-1.9.0_avoid-failures-in-test_unary_ufuncs.patch',
    'PyTorch-1.9.0_fix-min-amount-of-devices-for-test.patch',
    'PyTorch-1.9.0_fix-testnn-on-A100.patch',
    'PyTorch-1.9.0_fix-use-after-destruct-in-cudaipctypes.patch',
    'PyTorch-1.9.0_fix-kineto-crash.patch',
    'PyTorch-1.9.0_fix-vsx-vector-functions.patch',
    'PyTorch-1.9.0_increase-test-cuda-tolerance.patch',
    'PyTorch-1.9.0_increase-tolerance-for-distributed-tests.patch',
    'PyTorch-1.9.0_limit-world-size-for-zero-redundancy-opt-test.patch',
    'PyTorch-1.9.0_skip-autograd-thread_shutdown-test.patch',
    'PyTorch-1.9.0_skip-lstm-serialization-test.patch',
    'PyTorch-1.9.0_skip-nccl-error-tests.patch',
]
checksums = [
    None,  # can't add proper SHA256 checksum, because source tarball is created locally after recursive 'git clone'
    # PyTorch-1.6.0_fix-test-dataloader-fixed-affinity.patch
    'a4208a46cd2098744daaba96cebb96cd91166f8fc616924315e05974bad80c67',
    'b899aa94d9e60f11ee75a706563312ccefa9cf432756c470caa8e623991c8f18',  # PyTorch-1.7.0_avoid-nan-in-test-torch.patch
    '622cb1eaeadc06e13128a862d9946bcc1f1edd3d02b259c56a9aecc4d5406b8a',  # PyTorch-1.7.0_disable-dev-shm-test.patch
    # PyTorch-1.7.1_correctly-pass-jit_opt_level.patch
    'd4d967d47f8a6172fcbf57f0a61835482968850967c4fdb01108b720696a988d',
    # PyTorch-1.7.1_fix-alias-violation-in-bitwise-ops.patch
    'e92f054f1297df83ace901e7af38222787b709ee29580f5f2b89a300ca03666b',
    '89ac7a8e9e7df2e64cf8404fe3a279f5e9b759fee41c9de3aaff9c22f385c2c6',  # PyTorch-1.8.1_dont-use-gpu-ccc-in-test.patch
    'eca718ce0ecc61b57659808179cc660919b3c25b5dce326f51c1cc5a5bfb9829',  # PyTorch-1.8.1_fix-arange-on-VSX.patch
    # PyTorch-1.8.1_fix-faulty-asserts-and-skip-test.patch
    '1601eacd336e01176bdbdbc5a2207743dc2999b535a738a8e36b3da3e8a2f3b6',
    # PyTorch-1.8.1_increase-distributed-test-timeout.patch
    '7a6e512274f0b8673f4f207a5bc53387d88be7e79833f42d20365668b2118071',
    # PyTorch-1.8.1_skip_dist_autograd_sync_streams.patch
    '7940e571f41c350d3b634e98b1658a7001c96fdb1b1920835b8f5484ce389d09',
    # PyTorch-1.9.0_avoid-failures-in-test_unary_ufuncs.patch
    'f600e6831f8a03af007845687d1e0f65b2394ca89a9dab5178e2cdc9bd384d43',
    # PyTorch-1.9.0_fix-min-amount-of-devices-for-test.patch
    'edb180d6967c507c147400a64422ff4499bcd5519f9be8d332890c317359dbad',
    '8e8b417782e2f3004462c32338e12685e7296d15207f3e3087dcb8015e648f98',  # PyTorch-1.9.0_fix-testnn-on-A100.patch
    # PyTorch-1.9.0_fix-use-after-destruct-in-cudaipctypes.patch
    '67960bf9140baf004b07e29f7c2b338e7bc4e4e4f2c931768be44f58526e605f',
    '1ed5e125f7922ea577d43053a6652aedc21cc036157e101c0e3b9aee9029d3b0',  # PyTorch-1.9.0_fix-kineto-crash.patch
    'a4733b6b16a0db4ee5f85f2b103abc29bd711cfc5253f8dd8494d2b0c1509516',  # PyTorch-1.9.0_fix-vsx-vector-functions.patch
    # PyTorch-1.9.0_increase-test-cuda-tolerance.patch
    '73de855ab1ed38043c7fb2a983927786b83d7547aefed926f19e554e2214838a',
    # PyTorch-1.9.0_increase-tolerance-for-distributed-tests.patch
    '725922f0000d51c03f726a34b249db8f53eee7e5c67417774a5113de954f5a5c',
    # PyTorch-1.9.0_limit-world-size-for-zero-redundancy-opt-test.patch
    'ff573660913ce055e24cfd194ce747ba5685091c631cfd443eae2a99d56b57ea',
    # PyTorch-1.9.0_skip-autograd-thread_shutdown-test.patch
    '94957de0fd5bcbea37482cb6d0d12b4608dccf50a10da0836e151b414954ccc3',
    # PyTorch-1.9.0_skip-lstm-serialization-test.patch
    '0fc14e29bd7530bcc09f4212df3c846072b1313216da86b827e102b85d695f49',
    '9634fb34fedff4589b9175a4e4c3f278b60d4dcbc7b36b0f19604748d32074f0',  # PyTorch-1.9.skip-nccl-error-tests.patch
]
osdependencies = [OS_PKG_IBVERBS_DEV]

builddependencies = [
    ('CMake', '3.18.4'),
    ('hypothesis', '6.46.7'),
]

dependencies = [
    ('Ninja', '1.10.1'),  # Required for JIT compilation of C++ extensions
    ('Python', '3.10.4'),
    ('protobuf', '3.14.0'),
    ('protobuf-python', '3.14.0'),
    ('pybind11', '2.6.0'),
    ('SciPy-bundle', '2020.11'),
    ('typing-extensions', '3.7.4.3'),
    ('PyYAML', '5.3.1'),
    ('MPFR', '4.1.0'),
    ('GMP', '6.2.0'),
    ('numactl', '2.0.13'),
    ('FFmpeg', '4.3.1'),
    ('Pillow', '8.0.1'),
    ('cuDNN', '8.0.4.30', '-CUDA-%(cudaver)s', SYSTEM),
    ('magma', '2.5.4'),
    ('NCCL', '2.8.3', '-CUDA-%(cudaver)s'),
]

# default CUDA compute capabilities to use (override via --cuda-compute-capabilities)
cuda_compute_capabilities = ['3.5', '3.7', '5.2', '6.0', '6.1', '7.0', '7.2', '7.5', '8.0']

custom_opts = ["USE_CUPTI_SO=1"]

excluded_tests = {
    '': [
        # Bad tests: https://github.com/pytorch/pytorch/issues/60260
        'distributed/elastic/utils/distributed_test',
        'distributed/elastic/multiprocessing/api_test',
        # These tests fail on A10s at the very least, they time out forever no matter how long the timeout is.
        # Possibly related to NCCL 2.8.3: https://docs.nvidia.com/deeplearning/nccl/release-notes/rel_2-8-3.html
        'distributed/test_distributed_fork',
        'distributed/test_distributed_spawn',
        # Fails on A10s: https://github.com/pytorch/pytorch/issues/63079
        'test_optim',
        # Test from this suite timeout often. The process group backend is deprecated anyway
        'distributed/rpc/test_process_group_agent',
    ],
    'POWER': [
        # Works when run alone, fails when run as part of the suite. So far only observed on PPC
        'distributed/rpc/test_tensorpipe_agent',
    ],
}
runtest = 'cd test &#x26;&#x26; PYTHONUNBUFFERED=1 %(python)s run_test.py --continue-through-error  --verbose %(excluded_tests)s'

sanity_check_commands = ["python -c 'import caffe2.python'"]
tests = ['PyTorch-check-cpp-extension.py']

moduleclass = 'devel'

EOF

# run command for PyTorch
eb PyTorch-1.9.0-fosscuda-2020b.eb --buildpath=/eb_build -r






# Before install Transformers you need to install some  dependencies
eb PyYAML-6.0-GCCcore-11.3.0.eb --try-toolchain=GCCcore,10.2.0 --buildpath=/eb_build -r
eb PyYAML-6.0-GCCcore-11.3.0.eb --try-toolchain=GCCcore,10.2.0 --buildpath=/eb_build -r
eb PyYAML-6.0-GCCcore-11.3.0.eb --try-toolchain=GCCcore,10.2.0 --buildpath=/eb_build -r

# create  Transformers file 
cat > Transformers-4.24.0-fosscuda-2020b.eb &#x3C;&#x3C; EOF

# easy-build file configuration for Transformers
easyblock = 'PythonBundle'

name = 'Transformers'
version = '4.24.0'

homepage = 'https://github.com/huggingface/transformers'
description = """
State-of-the-art Natural Language Processing for PyTorch and TensorFlow 2.0"""

toolchain = {'name': 'fosscuda', 'version': '2020b'}

builddependencies = [
    ('pkgconf', '1.8.0','', ('GCCcore' , '10.2.0')),
    ('Rust', '1.63.0','', ('GCCcore' , '10.2.0')),  # required for setuptools-rust, which is needed for tokenizers
]
dependencies = [
    ('Python', '3.10.4','', ('GCCcore' , '10.2.0')),
    ('SciPy-bundle', '2022.05'),
    ('PyYAML', '6.0','', ('GCCcore' , '10.2.0')),
    ('tqdm', '4.64.0','', ('GCCcore' , '10.2.0')),
]

use_pip = True
exts_list = [
    ('regex', '2022.10.31', {
        'checksums': ['a3a98921da9a1bf8457aeee6a551948a83601689e5ecdd736894ea9bbec77e83'],
    }),
    ('tokenizers', '0.13.2', {
        'checksums': ['f9525375582fd1912ac3caa2f727d36c86ff8c0c6de45ae1aaff90f87f33b907'],
    }),
    ('huggingface-hub', '0.10.1', {
        'source_tmpl': 'huggingface_hub-%(version)s.tar.gz',
        'checksums': ['5c188d5b16bec4b78449f8681f9975ff9d321c16046cc29bcf0d7e464ff29276'],
    }),
    ('transformers', version, {
        'checksums': ['486f353a8e594002e48be0e2aba723d96eda839e63bfe274702a4b5eda85559b'],
    }),
]

sanity_pip_check = True

moduleclass = 'math'

EOF

# run command for Transformers
eb Transformers-4.24.0-fosscuda-2020b.eb --buildpath=/eb_build  -r





# create  editdistance 
cat > editdistance-0.5.3-fosscuda-2020b-Python-3.10.4.eb &#x3C;&#x3C; EOF

# easy-build file configuration for editdistance

easyblock = 'PythonBundle'

name = 'editdistance'
version = '0.5.3'
versionsuffix = '-Python-%(pyver)s'

homepage = 'https://github.com/roy-ht/editdistance'
description = "Fast implementation of the edit distance(Levenshtein distance)"

toolchain = {'name': 'fosscuda', 'version': '2020b'}

#source_urls = ['https://files.pythonhosted.org/packages/5b/a0/e6204db320f9721e1787c8d64458f9f1302cc7cd6ae8cc82aa57532905b5/editdistance-0.6.2.tar.g$

dependencies = [('Python', '3.10.4' ,'',('GCCcore', '10.2.0'))]

use_pip = True


exts_list = [
        (name, version, {
                'checksums': ['89d016dda04649b2c49e12b34337755a7b612bfd690420edd50ab31787120c1f'],
        }),
]

moduleclass = 'tools'


EOF

# run command for editdistance
eb editdistance-0.5.3-fosscuda-2020b-Python-3.10.4.eb --use-existing-modules -build-path=/eb_build --rebuild -r







# create  emoji 
cat > emoji-2.7.0-fosscuda-2020b-Python-3.10.4.eb &#x3C;&#x3C; EOF

# easy-build file configuration for emoji
easyblock = 'PythonPackage'

name = 'emoji'
version = '2.7.0'
versionsuffix = '-Python-%(pyver)s'

homepage = 'https://python-future.org/'
description = "Emoji for Python. This project was inspired by kyokomi."

toolchain = {'name': 'fosscuda', 'version': '2020b'}

#source_urls = [PYPI_SOURCE]
sources = [SOURCE_TAR_GZ]
checksums = ['375cc08589704266099846c553b6572ec5be591374b4d2cd1623b8343d5c9abb']

dependencies = [('Python', '3.10.4')]

use_pip = True
#download_dep_fail = True

#exts_list = [
#        ('editdistance', '0.6.2', {
#        }),
#]
moduleclass = 'lib'

EOF

# run command for emoji
eb emoji-2.7.0-fosscuda-2020b-Python-3.10.4.eb -build-path=/eb_build -r







# create  pyrsistent 
cat > pyrsistent-0.19.3-fosscuda-2020b-Python-3.10.4.eb &#x3C;&#x3C; EOF

# easy-build file configuration for pyrsistent
easyblock = 'PythonPackage'

name = 'pyrsistent'
version = '0.19.3'
versionsuffix = '-Python-%(pyver)s'

homepage = 'https://python-future.org/'
description = "Pyrsistent is a number of persistent collections (by some referred to as functional data structures). Persistent in the sense that th$

toolchain = {'name': 'fosscuda', 'version': '2020b'}


sources = [SOURCE_TAR_GZ]
checksums = ['1a2994773706bbb4995c31a97bc94f1418314923bd1048c6d964837040376440']

dependencies = [('Python', '3.10.4')]

use_pip = True
#download_dep_fail = True

moduleclass = 'lib'

EOF

# run command for pyrsistent
eb pyrsistent-0.19.3-fosscuda-2020b-Python-3.10.4.eb -build-path=/eb_build -r





# create  tabulate 
cat > tabulate-0.9.0-fosscuda-2020b-Python-3.10.4.eb &#x3C;&#x3C; EOF

# easy-build file configuration for tabulate
 
easyblock = 'PythonBundle'

name = 'tabulate'
version = '0.9.0'
versionsuffix = '-Python-%(pyver)s'

homepage = 'https://github.com/astanin/python-tabulate'
description = "Pretty-print tabular data in Python, a library and a command-line utility."

toolchain = {'name': 'fosscuda', 'version': '2020b'}


#sources = [SOURCE_TAR_GZ]
#checksums = ['0095b12bf5966de529c0feb1fa08671671b3368eec77d7ef7ab114be2c068b3c']

dependencies = [('Python', '3.10.4')]

use_pip = True
#download_dep_fail = True

exts_list = [
        (name, version, {
                'checksums': ['0095b12bf5966de529c0feb1fa08671671b3368eec77d7ef7ab114be2c068b3c'],
        }),
        ('wcwidth', '0.2.6', {
                'checksums': ['a5220780a404dbe3353789870978e472cfe477761f06ee55077256e509b156d0'],
        }),
]

moduleclass = 'lib'

EOF

# run command for tabulate
eb tabulate-0.9.0-fosscuda-2020b-Python-3.10.4.eb -build-path=/eb_build -r






# create  tqdm 
cat > tqdm-4.64.0-GCCcore-10.2.0.eb &#x3C;&#x3C; EOF

# easy-build file configuration for tqdm
 asyblock = 'PythonPackage'

name = 'tqdm'
version = '4.64.0'

homepage = "https://github.com/tqdm/tqdm"
description = """A fast, extensible progress bar for Python and CLI"""

toolchain = {'name': 'GCCcore', 'version': '10.2.0'}

sources = [SOURCE_TAR_GZ]
checksums = ['40be55d30e200777a307a7585aee69e4eabb46b4ec6a4b4a5f2d9f11e7d5408d']

builddependencies = [('binutils', '2.38')]

dependencies = [('Python', '3.10.4')]

use_pip = True
download_dep_fail = True
sanity_pip_check = True

moduleclass = 'lib'


EOF

# run command for tqdm
eb tqdm-4.64.0-GCCcore-10.2.0.eb -build-path=/eb_build -r






<strong># create  muddler 
</strong>cat > muddler-0.1.3-fosscuda-2020b-Python-3.10.4.eb &#x3C;&#x3C; EOF

# easy-build file configuration for muddler
 
easyblock = 'PythonPackage'

name = 'muddler'
version = '0.1.3'
versionsuffix = '-Python-%(pyver)s'

homepage = 'https://github.com/CAMeL-Lab/muddler'
description = "Muddler is a tool for sharing derived data."

toolchain = {'name': 'fosscuda', 'version': '2020b'}

sources = [SOURCE_TAR_GZ]

checksums = ['324d64afdf9bfd93cb383ec4cdde37de4223562d813dfe2a18ba547b3f6185c4']

dependencies = [('Python', '3.10.4')]

use_pip = True
download_dep_fail = True

moduleclass = 'lib'
EOF

# run command for muddler
eb muddler-0.1.3-fosscuda-2020b-Python-3.10.4.eb -build-path=/eb_build -r

# Before install camel-kenlm you need to install Boost.Python first 
eb Boost.Python-1.79.0-GCC-11.3.0.eb --try-toolchain=GCC,10.2.0 --try-update-deps --experimental --buildpath=/eb_build -r

# create  camel-kenlm 
cat > camel-kenlm-2023.3.17.2-fosscuda-2020b-Python-3.10.4.eb  &#x3C;&#x3C; EOF

# easy-build file configuration for camel-kenlm
 easyblock = 'CMakeMake'

name = 'camel-kenlm'
version = '2023.3.17.2'
versionsuffix = '-Python-%(pyver)s'

homepage = 'https://github.com/CAMeL-Lab/camel-kenlm'
description = "Language model inference code by Kenneth Heafield"

toolchain = {'name': 'fosscuda', 'version': '2020b'}
#toolchainopts = {'optarch': 'mavx2', 'cstd': 'c++11'}

source_urls = [
'https://files.pythonhosted.org/packages/d7/39/7c216baa683bd1cd4b6bb1ba1bc6b5d11874fb4636ce08ad896f5b25f1d5/' ]
sources = [SOURCE_TAR_GZ]
checksums = ['ce325a573ea70f479994ea5ed156c29518910bc0c9ba0676f2f629d9a930a0eb']

builddependencies = [
    ('CMake', '3.20.1','', ('GCCcore' , '10.2.0')),
    ('Eigen', '3.4.0','', ('GCCcore' , '10.2.0')),
    ('pkg-config', '0.29.2','', ('GCCcore' , '10.2.0')),

]

dependencies = [('Python', '3.10.4'),
('Boost.Python', '1.79.0', '', ('GCC', '10.2.0'))]

separate_build_dir = True

configopts = "-DPy_ENABLE_SHARED=1 -DRDK_INSTALL_STATIC_LIBS=OFF -DRDK_INSTALL_INTREE=OFF "
configopts += "-DRDK_BUILD_INCHI_SUPPORT=ON "
configopts += "-DBoost_INCLUDE_DIR=$EBROOTBOOST/include -DBoost_LIBRARY_DIR_RELEASE=$EBROOTBOOST/lib "


options = {'modulename' : 'camelkenlm' }

moduleclass = 'tools'
EOF
#run command for camel-kenlm
eb camel-kenlm-2023.3.17.2-fosscuda-2020b-Python-3.10.4.eb --use-existing-modules -build-path=/eb_build -r

</code></pre>

***

### camel-tool file

<pre class="language-bash"><code class="lang-bash"># create  camel-tools 
cat > camel-tool-1.5.2-fosscuda-2020b.eb  &#x3C;&#x3C; EOF

# easy-build file configuration for camel-tools
easyblock = 'PythonPackage'

name = 'camel-tools'
version = '1.5.2'
versionsuffix = '-Python-%(pyver)s'

homepage = 'https://github.com/CAMeL-Lab/CAMeL_Tools'
description = """CAMeL Tools is suite of Arabic natural language processing tools developed by the CAMeL Lab at New York University $

#Please use GitHub Issues to report a bug or if you need help using CAMeL Tools."""

toolchain = {'name': 'fosscuda', 'version': '2020b'}

source_urls = [PYPI_LOWER_SOURCE]
sources = ['https://files.pythonhosted.org/packages/30/6e/f8573da209672f6f66577580d61d43681bb7c317aeacd7cd682a49832385/camel_tools-1.5.1.tar.gz']
checksums = ['595408967def3b24c1e87d2310dd649006f03c5444d2f0c6accc55d8cbb9accf']



dependencies = [
    ('Python', '3.10.4','', ('GCCcore' , '10.2.0')),
    ('future','0.18.3',versionsuffix),
    ('six','1.16.0' ,versionsuffix),
    ('docopt','0.6.2' ,versionsuffix),
    ('cachetools', '5.3.1', versionsuffix ),
    ('SciPy-bundle', '2022.05' ),
    ('scikit-learn','1.1.2' ),
    ('dill','0.3.6','', ('GCCcore' , '10.2.0')),
    ('PyTorch','1.7.1'),
    ('Transformers','4.24.0'),
    ('editdistance','0.5.3' ,versionsuffix),
    ('emoji','2.7.0' ,versionsuffix),
    ('pyrsistent','0.19.3' ,versionsuffix),
    ('tabulate','0.9.0' ,versionsuffix),
    ('tqdm','4.64.0','', ('GCCcore' , '10.2.0')),
    ('muddler','0.1.3' ,versionsuffix),
    ('camel-kenlm','2023.3.17.2' ,versionsuffix),
    ]


download_dep_fail = True
use_pip = True

moduleclass = 'data'
EOF

<strong>#run command for camel-tools
</strong> eb cameltool-1.5.2-fosscuda-2020b.eb --use-existing-modules -build-path=/eb_build -r
</code></pre>



***

### Related Links

1. [pypi](https://pypi.org/project/)
2. [camel-tool-JSON](https://pypi.org/pypi/camel-tools/1.5.1/json)

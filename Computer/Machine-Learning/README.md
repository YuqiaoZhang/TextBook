Deep Learning    
https://www.deeplearningbook.org/    
    

https://github.com/Intel-tensorflow/tensorflow       
https://pypi.org/project/intel-tensorflow/    

https://www.tensorflow.org/install/lang_c   

hello_tf.c  
```
#include <tensorflow/c/c_api.h>

int main() {
  printf("Hello from TensorFlow C library version %s\n", TF_Version());
  return 0;
}
```

build.sh
```
#!/bin/bash

g++ -c hello_tf.cpp \
-fPIE -fPIC -g -O0 \
-std=c++11 -D_GLIBCXX_USE_CXX11_ABI=0 \
-I "${HOME}/.local/lib/python3.5/site-packages/tensorflow/include" \
-o hello_tf.o        
     
# find . -name *tensorflow*so*
# find . -name *mklml*so*
# find . -name *omp*so*

g++ -pie hello_tf.o -g -O0 \
"${HOME}/.local/lib/python3.5/site-packages/tensorflow/python/_pywrap_tensorflow_internal.so" \
"${HOME}/.local/lib/python3.5/site-packages/tensorflow/libtensorflow_framework.so.2" \
"${HOME}/.local/lib/python3.5/site-packages/_solib_k8/_U@mkl_Ulinux_S_S_Cmkl_Ulibs_Ulinux___Uexternal_Smkl_Ulinux_Slib/libmklml_intel.so" \
"${HOME}/.local/lib/python3.5/site-packages/_solib_k8/_U@mkl_Ulinux_S_S_Cmkl_Ulibs_Ulinux___Uexternal_Smkl_Ulinux_Slib/libiomp5.so" \
-lpython3.5m \
-Wl,--enable-new-dtags \
-Wl,-rpath ${HOME}/.local/lib/python3.5/site-packages/tensorflow/python \
-Wl,-rpath ${HOME}/.local/lib/python3.5/site-packages/tensorflow \
-Wl,-rpath ${HOME}/.local/lib/python3.5/site-packages/_solib_k8/_U@mkl_Ulinux_S_S_Cmkl_Ulibs_Ulinux___Uexternal_Smkl_Ulinux_Slib \
-o hello_tf

# -fPIE / -fPIC 
# -pie / -lc++_shared
```
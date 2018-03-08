# tensorflow build

### bazel install

download [bazel-0.11.0-dist.zip](https://github.com/bazelbuild/bazel/releases/download/0.11.0/bazel-0.11.0-dist.zip)

```
$ wget https://github.com/bazelbuild/bazel/releases/download/0.11.0/bazel-0.11.0-dist.zip
$ mkdir bazel-0.11.0 && cd bazel-0.11.0
$ unzip ../bazel-0.11.0-dist.zip
$ ./compile.sh
$ cp output/bazel /usr/local/bin
```

### tensorflow install

```
$ git clone https://github.com/tensorflow/tensorflow
$ cd tensorflow
$ git checkout r1.6
$ ./configure
```

### bazel build

```
$ bazel build --config opt --copt=-msse4.1 --copt=-msse4.2 --copt=-mavx --copt=-mavx2 --copt=-mfma //tensorflow/tools/pip_package:build_pip_package
```

에러나면 `--jobs=4` 옵션 추가
>
```
$ bazel build --config opt --copt=-msse4.1 --copt=-msse4.2 --copt=-mavx --copt=-mavx2 --copt=-mfma //tensorflow/tools/pip_package:build_pip_package --jobs=6
```

### python whl

```
$ bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg
```

`tools/python_bin_path.sh` 파일없다고 에러
>
```
$ vi tools/python_bin_path.sh
```
```
PYTHON_BIN_PATH=/usr/bin/python
```
```
$ chmod 755 python_bin_path.sh
```
```
$ bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg
```

확인

```
$ ls /tmp/tensorflow_pkg
```

### pip로 tensorflow install

```
$ sudo pip install /tmp/tensorflow_pkg/tensorflow-1.6.0-cp35-cp35m-linux_x86_64.whl
```

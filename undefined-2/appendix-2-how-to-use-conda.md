# Conda

아나콘다(Anaconda)는 PYTHON 과 R 프로그래밍 언어로 된 과학 컴퓨팅(데이터 과학, 기계 학습 응용 프로그램, 대규모 데이터 처리, 예측 분석 등)분야의 패키지들의 모음을 제공하는 배포판이다.

Anaconda 배포판은 1,200 만 명이 넘는 사용자가 사용하며 Windows, Linux 및 MacOS에 적합한 1400 가지 이상의 인기있는 데이터 과학 패키지를 포함한다.

Anaconda를 설치하기 위해서는 [https://www.anaconda.com](https://www.anaconda.com/) 웹사이트에서 자신의 OS(예: Windows, MacOS, Linux)에 맞는 배포판을 다운받아 설치하면 된다.

현재 Anaconda 는 Python 3.7 기반의 버전과 Python 2.7 기반의 버전을 제공한다.

conda 는 아나콘다에서 패키지 버전 관리를 위해 제공되는 어플리케이션이다.

Python 사용자들이 패키지 설치 시 가장 어려움을 겪는 의존성 문제를 conda 를 활용함으로써 쉽게 해결할 수 있다.

본 문서는 KISTI 시스템에서 Python 사용자를 위하여 conda 패키지 활용하는 방법을 소개 한다.

소개 페이지의 "/home01/userID" 는 테스트 계정의 홈디렉토리로 자신에 맞는 경로로 적절히 변경해서 사용해야 한다.



## 가. Conda의 사용

* Miniconda는 https://docs.conda.io/en/latest/miniconda.html 사이트 에서 각 OS 에 맞는 버전을 다운 받을 수 있고, Anaconda 는 https://www.anaconda.com/distribution/#download-section 사이트 에서 각 OS 에 맞는 버전을 다운 받을 수 있다.

| **명령어 모음** | **내용**                                                                                                                                                                     |
| ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| clean      | Remove unused packages and caches.                                                                                                                                         |
| config     | <p>Modify configuration values in .condarc. This is modeled after the git config command.</p><p>Writes to the user .condarc file (/home01/userID/.condarc) by default.</p> |
| create     | Create a new conda environment from a list of specified packages.                                                                                                          |
| help       | Displays a list of available conda commands and their help strings.                                                                                                        |
| info       | Display information about current conda install.                                                                                                                           |
| init       | Initialize conda for shell interaction. \[Experimental]                                                                                                                    |
| install    | Installs a list of packages into a specified conda environment.                                                                                                            |
| list       | List linked packages in a conda environment.                                                                                                                               |
| package    | Low-level conda package utility. (EXPERIMENTAL)                                                                                                                            |
| remove     | Remove a list of packages from a specified conda environment.                                                                                                              |
| uninstall  | Alias for conda remove.                                                                                                                                                    |
| run        | Run an executable in a conda environment. \[Experimental]                                                                                                                  |
| search     | <p>Search for packages and display associated information.<br>The input is a MatchSpec, a query language for conda packages.</p><p>See examples below.</p>                 |
| update     | Updates conda packages to the latest compatible version.                                                                                                                   |
| upgrade    | Alias for conda update                                                                                                                                                     |



* Conda Initialize 방법&#x20;

conda init 명령으로 홈   디렉터리의 .bashrc에 설정을 추가할 수 있다.

```
$ source /apps/applications/Miniconda/23.3.1/etc/profile.d/conda.sh
$ conda init
$ source ~/.bashrc
```

* Conda 경로 변경 방법

conda 환경, 패키지 경로는 기본적으로 홈 디렉터리로 설정되어 있으나, scratch 와   같은 다른  경로로도 변경할 수 있다.

```
$ echo "export CONDA_ENVS_PATH=/scratch/$USER/.conda/envs" >> /home01/$USER/.bashrc
$ echo "export CONDA_PKGS_DIRS=/scratch/$USER/.conda/pkgs" >> /home01/$USER/.bashrc
$ source ~/.bashrc
```



## 나. Conda Environment 생성

* conda environment 는 Python 의 독립적인 가상 실행환경을 만들어 패키지들의 버전 관리에 용이 하다.
* "conda create -n \[ENVIRONMENT]" 을 이용하여 conda environment를 생성 할 수 있다.
* 기본 값으로 conda path 의 envs 아래 경로에 지정한 environment 이름으로 생성된다.

{% code title="- 예제 -" %}
```shell-session
※ conda initialize를 하지 않았다면 최초 1회 실행
$ source /apps/applications/Miniconda/23.3.1/etc/profile.d/conda.sh
$ conda init
$ source ~/.bashrc

$ conda create -n scikit-learn_0.21 
Collecting package metadata: done
Solving environment: done

## Package Plan ##

  environment location: /home01/userID/.conda/envs/scikit-learn_0.21

Proceed ([y]/n)? y

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use:
# > conda activate scikit-learn_0.21
#
# To deactivate an active environment, use:
# > conda deactivate
#

$ conda activate scikit-learn_0.21
(scikit-learn_0.21) $  
```
{% endcode %}



## 다. Conda Environment에 패키지 설치 및 확인

* conda install \[패키지명] 으로 패키지를 설치할 수 있다.
* conda 채널에 있는 패키지는 "conda install -c \[채널명] \[패키지명]" 와 같이 설치 할 수 있다.
* 위 항목("나. Conda environment 생성")에서 생성한 conda environment 경로 아래에 패키지 들이 설치 된다.

{% code title="- 예제 -" %}
```shell-session
$ source /apps/applications/Miniconda/23.3.1/etc/profile.d/conda.sh
$ conda activate scikit-learn_0.21
(scikit-learn_0.21) $ conda install scikit-learn
Collecting package metadata: done
Solving environment: done

## Package Plan ##

  environment location: /home01/userID/.conda/envs/scikit-learn_0.21
  added / updated specs:
    - scikit-learn

The following packages will be downloaded:
    package                    |            build
    ---------------------------|-----------------
    ca-certificates-2019.1.23  |                0         126 KB
    ...
      wheel-0.33.1               |           py37_0          39 KB
    ------------------------------------------------------------
                                           Total:       277.6 MB

The following NEW packages will be INSTALLED:

  blas               pkgs/main/linux-64::blas-1.0-mkl
 ...
   zlib               pkgs/main/linux-64::zlib-1.2.11-h7b6447c_3

Proceed ([y]/n)? y

Downloading and Extracting Packages
setuptools-40.8.0    | 643 KB    | ##################################### | 100% 
...
openssl-1.1.1b       | 4.0 MB    | ##################################### | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(scikit-learn_0.21) $ python -c "import sklearn"
(scikit-learn_0.21) $
```
{% endcode %}



## 라. Conda Environment 목록 확인

* "conda-env list" 또는 "conda env list" 를 이용하여 목록을 확인 할 수 있다.

{% code title="- 예제 -" %}
```shell-session
(scikit-learn_0.21) $ conda env list
# conda environments:
#
base                     /apps/applications/PYTHON/3.7
scikit-learn_0.21     *  /home01/userID/.conda/envs/scikit-learn_0.21
(scikit-learn_0.21) $ conda deactivate
$
```
{% endcode %}



## 마. Conda Environment 내보내기

* 내보내기 전 conda-pack 패키지 필요

※ (참고) [https://conda.github.io/conda-pack](https://conda.github.io/conda-pack)

* "conda pack -n \[ENVIRONMENT] -o \[파일명]" 을 이용하여 conda environment 를 다른 시스템에서 활용할 수 있다.

(예) 외부 인터넷이 연결되지 않는 다른 시스템에서 동일한 conda 환경을 이용하고자 할 때나, 다른 시스템에서 동일한 conda 환경이 필요할 때 재설치하지 않고 아래와 같이 conda 환경을 내보낼 수 있음

{% code title="- 예제 -" %}
```shell-session
$ conda activate scikit-learn_0.21
(scikit-learn_0.21) $ conda install -c conda-forge conda-pack
(scikit-learn_0.21) $ conda pack -n scikit-learn_0.21 -o scikit-learn_test.tar.gz
Collecting packages...
Packing environment at '/home01/userID/.conda/envs/scikit-learn_0.21' to 'scikit-learn_test.tar.gz'
[########################################] | 100% Completed |  4min 18.8s
(scikit-learn_0.21) $ ls -l scikit-learn_test.tar.gz
-rw-------. 1 userID in0162 1459826406 Mar 28 15:03 scikit-learn_test.tar.gz
(scikit-learn_0.21) $
```
{% endcode %}



## 바. Conda Environment 가져오기

* conda pack 을 이용하여 생성했던 conda environment 를 아래 -예제-와 같이 가져와 환경설정 후 사용 가능.

{% code title="- 예제 -" %}
```shell-session
$ mkdir -p $HOME/.conda/envs/scikit-learn_test
$ tar xvzf scikit-learn_test.tar.gz -C $HOME/.conda/envs/scikit-learn_test
※ scratch 가 conda 경로인 경우, /scratch/$USER/.conda 로 입력

$ conda activate scikit-learn_test
(scikit-learn_0.21) $ conda-unpack
(scikit-learn_0.21) $ conda deactivate
$
```
{% endcode %}



## 사. Conda Environment 삭제

* "conda-env remove -n \[ENVIRONMENT]" 또는 "conda env remove -n \[ENVIRONMENT]" 를 이용하여 삭제 할 수 있다.

<pre class="language-shell-session" data-title="- 예제 -"><code class="lang-shell-session"><strong>$ conda env remove -n scikit-learn_test
</strong>Remove all packages in environment /home01/userID/.conda/envs/scikit-learn_test:
</code></pre>



{% hint style="info" %}
2024년 3월 21일에 마지막으로 업데이트되었습니다.
{% endhint %}


---
description: Abaqus 지침서
---

# Abaqus (2023 버전 이전)

본 문서는 누리온 시스템에서 ABAQUS 소프트웨어 사용을 위한 기초적인 정보를 제공하고 있습니다.

따라서, ABAQUS 소프트웨어 사용법 및 누리온/리눅스 사용법 등은 포함되어 있지 않습니다.

누리온/리눅스 사용법에 대한 정보는 KISTI 홈페이지 (https://www.ksc.re.kr)의 기술지원 > 지침서 내 누리온 사용자 지침서 등을 참고하시기 바랍니다.



## **가. 사용 신청 시 유의사항**

* 사용 가능 사용자 그룹 : 대학교/산업체(중소기업)/출연연구소 사용자
* 신규사용자의 경우 KSC 홈페이지 사용 신청서 작성 시 반드시 '사용할 애플리케이션'에 Abaqus를 명시하여야 합니다.
* 기존사용자의 경우 account@ksc.re.kr로 계정, 소속, 아이디를 명기하고 신청을 해주시기  바랍니다.
* 산업체(중소기업) 소속의 경우 account@ksc.re.kr로 관련 서류(중소기업 확인서, 벤처기업 확인서 등)를 제출해야 합니다.
* 사용 중 소속이 변경되어 해당 소속에 해당되지 않는 경우 반드시 account@ksc.re.kr로 알려주시기 바랍니다.



## **나. 사용 정책**

* 사용자별 **최대 40개 CPU 코어 수행 가능**합니다.
* <mark style="color:red;">한정된 라이선스를 슈퍼컴 사용자들이 함께 사용하므로, 사용정책 기준을 초과하여 사용할 경우 해당 작업은 관리자가 강제 종료 합니다.</mark>
* <mark style="color:red;">부득이하게 많은 라이선스가 필요할 경우, KISTI 홈페이지 (https://www.ksc.re.kr)를 통해 사전에 관리자와 협의해야 합니다.</mark>
* 작업 제출 전 "lic\_check" 명령 에서 메뉴 선택을 통해 라이선스 상태를 확인 한 다음 작업을 제출하시기 바랍니다.
* 로그인 노드(login01\~04)의 과부하 방지를 위해 로그인 노드에서의 pre/post 작업은 허가하지 않습니다. 다만, VDI를 통해서 일부  pre/post 작업이 가능합니다. (참고 : 누리온 VDI 지침서 - [https://docs-ksc.gitbook.io/nurion-user-guide/undefined-2/appendix-9-how-to-use-vdi](https://docs-ksc.gitbook.io/nurion-user-guide/undefined-2/appendix-9-how-to-use-vdi))
* <mark style="color:red;">작업제출 스크립트에 "#PBS -A abaqus" 옵션을 사용해야 합니다.</mark>

## **다. 소프트웨어 설치 정보**

### **1. 설치 버전**

* 6.14-6, 2016, 2017, 2018, 2019, 2020, 2021, 2022, 2023

***

### **2. 설치 위치**

* /apps/commercial/abaqus

***

### **3. 실행 파일 경로**

* /apps/commercial/abaqus/Commands 디렉터리 내 위치
  * v6146 : /apps/commercial/abaqus/Commands/abq6146
  * v2016 : /apps/commercial/abaqus/Commands/abq2016hf19
  * v2017 : /apps/commercial/abaqus/Commands/abq2017hf13&#x20;
  * v2018 : /apps/commercial/abaqus/Commands/abq2018hf5&#x20;
  * v2019 : /apps/commercial/abaqus/Commands/abq2019hf5&#x20;
  * v2020 : /apps/commercial/abaqus/Commands/abq2020hf4&#x20;
  * v2021 : /apps/commercial/abaqus/Commands/abq2021&#x20;
  * v2022 : /apps/commercial/abaqus/Commands/abq2022&#x20;
  * v2023 : /apps/commercial/abaqus/Commands/abq2023hf7

***

### 4. env 파일 경로&#x20;

* /apps/commercial/abaqus 버전별 디렉터리 내 위치&#x20;
  * v6.14-6 : \
    /apps/commercial/abaqus/6146/6.14-6/SMA/site/abaqus\_v6.env&#x20;
  * v2016 : \
    /apps/commercial/abaqus/2016/SimulationServices/V6R2016x/linux\_a64/SMA/site/abaqus\_v6.env&#x20;
  * v2017 : \
    /apps/commercial/abaqus/2017/SimulationServices/V6R2017x/linux\_a64/SMA/site/abaqus\_v6.env&#x20;
  * v2018 : \
    /apps/commercial/abaqus/2018/SimulationServices/V6R2018x/linux\_a64/SMA/site/abaqus\_v6.env&#x20;
  * v2019 : \
    /apps/commercial/abaqus/2019/SimulationServices/V6R2019x/linux\_a64/SMA/site/abaqus\_v6.env&#x20;
  * v2020 : \
    /apps/commercial/abaqus/2020/EstProducts/2020/linux\_a64/SMA/site/abaqus\_v6.env&#x20;
  * v2021 : \
    /apps/commercial/abaqus/2021/EstProducts/2021/linux\_a64/SMA/site/abaqus\_v6.env&#x20;
  * v2022 :\
    /apps/commercial/abaqus/2022/EstProducts/2022/linux\_a64/SMA/site/abaqus\_v6.env&#x20;
  * v2023 :\
    /apps/commercial/abaqus/2023/EstProducts/2023/linux\_a64/SMA/site/abaqus\_v6.env

## **라. 소프트웨어 실행 방법**

### **1. 실행 방법**

* 다음과 같이 batch mode로 job을 실행하기 위한 명령어 입력합니다.

<table data-header-hidden><thead><tr><th width="188"></th><th></th></tr></thead><tbody><tr><td><strong>형식</strong></td><td>[<strong>command</strong>] [<strong>option</strong>]</td></tr><tr><td>Commands</td><td><p>abq6146 (6-14.6버전)</p><p>abq2016hf19 (2016 버전)</p><p>abq2017hf13 (2017 버전)</p><p>abq2018hf5 (2018 버전)</p><p>abq2019hf5 (2019 버전)<br>abq2020hf4 (2020 버전)<br>abq2021 (2021 버전)<br>abq2022 (2022 버전)<br>abq2023hf7 (2023버전)</p></td></tr><tr><td>예제(6.14-6 버전)</td><td><p>abq6146 job=<mark style="color:blue;"><strong>job_name</strong></mark> [cpus=<mark style="color:blue;"><strong>ncpus</strong></mark>] [input=<mark style="color:blue;"><strong>inp_file</strong></mark>] [interactive]</p><p>abq6146 job=<mark style="color:blue;"><strong>job_name</strong></mark> oldjob=<mark style="color:blue;"><strong>old_job_name</strong></mark></p><p>abq6146 help</p><p>abq6146 information=environment</p><p>abq6146 viewer [res=<mark style="color:blue;"><strong>res_name</strong></mark>]</p></td></tr></tbody></table>

* 파란 글씨 부분을 작업명, 사용코어 수, 입력 파일 명으로 수정 후 사용하시기 바랍니다.
* Interactive 방식의 실행은 CPU time이 20분으로 제한되어 있습니다.
* 장시간의 계산 작업은 PBS라는 스케줄러를 이용하여 작업을 제출해야 합니다.
* 작업 제출 전 "lic\_check" 명령을 실행하여 라이선스 상태를 확인 후 작업을 제출하시기 바랍니다.

***

### **2. 스케쥴러 작업 스크립트 파일 작성**

* 누리온 시스템에서는 로그인 노드에서 PBS라는 스케쥴러를 사용하여 작업을 제출해야 합니다.
* 누리온 시스템에서 PBS 를 사용하는 예제 파일들이 아래의 경로에 존재하므로 사용자 작업용 파일을 만들 때 이를 참고하시기 바랍니다.
* 예제 파일 경로 - 6.14-6 버전
  * /apps/commercial/test\_samples/abaqus/abaqus\_v6146.sh **(단일노드에서 수행)**
  * /apps/commercial/test\_samples/abaqus/abaqus\_v6146\_multinode.sh **(멀티 노드에서 수행)**
* 예제 파일 경로 - 2023 버전
  * /apps/commercial/test\_samples/abaqus/abaqus\_v2023.sh **(단일노드에서 수행)**
  * /apps/commercial/test\_samples/abaqus/abaqus\_v2023\_multinode.sh **(멀티 노드에서 수행)**



※ 아래 예제는 누리온 시스템 에서의 ABAQUS 2023 버전에 대한 예제입니다. **(단일노드에서 수행)**

```bash
#!/bin/sh
#PBS -V
#PBS -N abaqus_test
#PBS -q commercial
#PBS -l select=1:ncpus=40:mpiprocs=40:ompthreads=1
#PBS -l walltime=04:00:00
#PBS -A abaqus

cd $PBS_O_WORKDIR

###### Do not edit #####
TOTAL_CPUS=$(wc -l $PBS_NODEFILE | awk '{print $1}')
#######################

cp /apps/commercial/abaqus/2023/EstProducts/2023/linux_a64/SMA/site/abaqus_v6.env .
/apps/commercial/abaqus/Commands/abq2023hf7 job=c2 cpus=${TOTAL_CPUS} int

```

* 위에서 파란색으로 표기된 부분은 사용자가 적절히 수정해야 합니다.
* <mark style="color:red;">2019년 3월 PM 이후 부터는 "#PBS -A abaqus" 옵션이 없는 경우 작업제출이 되지 않습니다.</mark>
* **작업 제출은 스크래치 디렉토리에서만 가능** 합니다.
* 사용자별 스크래치 디렉토리는 /scratch/$USER입니다.
* <mark style="color:red;">스크래치 디스크는 작업 종료 후 일정 시간(2023년 8월 현재 정책: 15일)이 지나면 삭제되기 때문에, 작업이 완료 된경우 빠른 시일 내에 백업하시길 권장합니다.</mark>
* 기타 PBS에 관련된 명령어 및 사용법은 누리온 사용자 지침서를 참조하시면 됩니다.



※ 아래 예제는 누리온 시스템 에서의 ABAQUS 2023 버전에 대한 예제입니다. **(멀티노드에서 수행)**

```bash
#!/bin/sh
#PBS -V
#PBS -N abaqus_test
#PBS -q commercial
#PBS -l select=2:ncpus=20:mpiprocs=20:ompthreads=1
#PBS -l walltime=04:00:00
#PBS -A abaqus

cd $PBS_O_WORKDIR

###### Do not edit #####
export MPI_IC_ORDER=TCP
TOTAL_CPUS=$(wc -l $PBS_NODEFILE | awk '{print $1}')
nodes="["
for n in $(sort -u $PBS_NODEFILE)
do
nodes="${nodes}['$n',$(grep -c $n $PBS_NODEFILE)],"
done
nodes=$(echo ${nodes} | sed -e "s/,$/]/")
echo "abaquslm_license_file=\"2501@vaccine02.ext\"" > abaqus_v6.env
echo "mp_host_list=${nodes}" >> abaqus_v6.env
########################

/apps/commercial/abaqus/Commands/abq2023hf7 job=c2 cpus=${TOTAL_CPUS} mp_mode=mpi int


```

* <mark style="color:red;">위에서 빨간색으로 표기된 부분은 수정하면 안됩니다.</mark>
* <mark style="color:red;">2019년 3월 PM 이후 부터는 "#PBS -A abaqus" 옵션이 없는 경우 작업제출이 되지 않습니다.</mark>
* 위에서 파란색으로 표기된 부분은 사용자가 적절히 수정해야 합니다.
* **작업 제출은 스크래치 디렉토리에서만 가능** 합니다.
* 사용자별 스크래치 디렉토리는 /scratch/$USER입니다.
* <mark style="color:red;">스크래치 디스크는 작업 종료 후 일정 시간(2023년 8월 현재 정책: 15일)이 지나면 삭제되기 때문에, 작업이 완료 된경우 빠른 시일 내에 백업하시길 권장합니다.</mark>
* 기타 PBS에 관련된 명령어 및 사용법은 누리온 사용자 지침서를 참조하시면 됩니다.

***

### **3. 작업 제출 방법**

* 예제 : 스크립트 파일 이름이 abaqus.sh 인 경우

```shell-session
$ qsub abaqus.sh
```

***

### **4. 작업 상태 확인**

```shell-session
$ qstat (또는 qstat -u $USER) 
```

***

### **5. 제출된 작업을 강제로 종료**

* 사용 방법 : qdel
* 작업ID는 qstat 명령어 실행 시 제일 왼쪽에 표시 되는 정보입니다.(ex. 1771476.pbs)
* 예제 : 작업ID 가 1771476.pbs 인 경우

```shell-session
$ qdel  1771476.pbs
```

***

### **6. PBS 상에서 사용 가능한 자원 확인**

```shell-session
$ pbs_status
```

## **라. abaqus 수행 오류 관련**

* 6월 정기점검시 Lustre 파일시스템의 I/O 성능 향상을 위한 기능이 /scratch 파일시스템에 적용되었습니다.
* 이로 인해 현재 abaqus 수행시 아래와 같은 \*\*\[관련 오류 메시지]\*\*가 출력되면서 파일 접근에 대한 오류가 발생할 수 있습니다. (다만, 특정 작업의 경우 오류 메시지가 출력되지 않고 작업이 R 상태로 진행되지 않을 수 있습니다.)
* 아래 오류 메시지와 유사한 파일 접근 오류가 발생하는 경우, 다음의 절차를 먼저 진행하시고 작업을 제출하시기 바랍니다.

**\[stripe count 설정 방법]**

```shell-session
$ mkdir
$ lfs setstripe -c 4
$ cp *.inp # .inp 파일은 abaqus의 input 파일을 지칭합니다.
$ cp *.sh # .sh 파일은 abaqus 작업제출 스크립트를 지칭합니다.
$ cd
$ qsub
```

* \* : 입력 데이터가 위치하고 있으며, 출력 데이터가 기록될 디렉토리
* \* 하위 디렉토리를 생성하는 경우 동일한 작업을 수행하셔야 합니다.

<mark style="color:red;">※ restart 작업과 같이 기존 파일을 활용해야 하는 경우,</mark>\ <mark style="color:red;">(stripe count 설정을 수행한 디렉토리)로 cp 명령어를 이용하여</mark> <mark style="color:red;">**기존 파일을 복사**</mark><mark style="color:red;">하여 작업을 수행해주시기 바랍니다.</mark>\ <mark style="color:red;">(mv 명령어 사용 시 기존의 속성을 유지하기 때문에 오류가 발생할 수 있습니다.)</mark>

**\[관련 오류 메시지]**

| <p>(1) <strong>***ERROR: *** Error: Extend failed (utl_File: read)</strong></p><p>(2) <em><strong>NOTE: DUE TO AN INPUT ERROR THE ANALYSIS PRE-PROCESSOR HAS BEEN UNABLE TO INTERPRET SOME DATA. SUBSEQUENT ERRORS MAY BE CAUSED BY THIS OMISSION</strong></em></p><p><em><strong>(3) terminate called after throwing an instance of 'utl_FileExceptionExtend'</strong></em></p><p>ABAQUS/pre rank 0 received signal 6 (Aborted)</p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |


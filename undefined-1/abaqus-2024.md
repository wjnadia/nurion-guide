---
description: Abaqus 2024hf6 버전 지침서
---

# Abaqus (2024 버전 이후)

Abaqus 2024hf6 버전은 누리온 시스템 OS인 CentOS 7.9 버전을 지원하지 않기 때문에 2023 버전 이전과동일한 방법으로는 작업 수행이 불가합니다.&#x20;

다만, singularity  이미지를 활용하면 다른 OS 컨테이너 환경에서 Abaqus를 안정적으로 구동할 수 있습니다. 이 문서에서는 singularity 이미지를 통한 Abaqus 2024hf6 버전 활용 방법에 대해 안내합니다.

## 가. 사용 신청 시 유의사항

* 사용 가능 사용자 그룹 : 대학교/산업체(중소기업)/출연연구소 사용자
* 신규사용자의 경우 KSC 홈페이지 사용 신청서 작성 시 반드시 '사용할 애플리케이션'에 Abaqus를 명시하여야 합니다.
* 기존 사용자의 경우 account@ksc.re.kr로 계정, 소속, 아이디를 명기하고 신청 바랍니다.
* 산업체(중소기업) 소속의 경우 account@ksc.re.kr로 관련 서류(중소기업 확인서, 벤처기업 확인서 등)를 제출해야 합니다.
* 사용 중 소속이 변경되어 해당 소속에 해당되지 않는 경우 반드시 account@ksc.re.kr로 알려 주십시오.

## 나. 사용 정책

* 사용자별 최대 40개 CPU 코어 수행 가능합니다.
* 한정된 라이선스를 슈퍼컴 사용자들이 함께 사용하므로, 사용정책 기준을 초과하여 사용할 경우 해당 작업은 관리자가 강제 종료 합니다.
* 부득이하게 많은 라이선스가 필요할 경우, KISTI 홈페이지 (https://www.ksc.re.kr)를 통해 사전에 관리자와 협의해야 합니다.
* 작업 제출 전 "lic\_check" 명령 에서 메뉴 선택을 통해 라이선스 상태를 확인 한 다음 작업을 제출 바랍니다.
* 로그인 노드(login01\~04)의 과부하 방지를 위해 로그인 노드에서의 pre/post 작업은 허가하지 않습니다. 다만, VDI를 통해서 일부 pre/post 작업이 가능합니다. (참고 : [누리온 VDI 지침서](https://docs-ksc.gitbook.io/nurion-user-guide/undefined-2/appendix-9-how-to-use-vdi))
* 작업제출 스크립트에 "#PBS -A abaqus" 옵션을 사용해야 합니다.

## 다. 소프트웨어 설치 정보

### 1. 설치 버전

* 2024hf6

### 2. 설치 위치

* /apps/commercial/abaqus/2024

### 3. 이미지 파일 경로

* /apps/commercial/abaqus/2024/abaqus\_2024hf6.sif

## 라. 소프트웨어 실행 방법

### 1. PBS 작업 스크립트 파일 작성

* 누리온 시스템에서는 PBS 스케쥴러에 작업 스크립트를 제출하여 abaqus를 실행해야 합니다.
* 작업 스크립트는 계산노드에서 실행될 환경설정, 실행명령이 포함된 스크립트 입니다.
* 아래는 예시로 작성된 작업 스크립트 샘플 파일이며 복사하여 활용 가능합니다.

\[작업 스크립트 예시]

* /apps/commercial/test\_samples/abaqus/abaqus\_v2024.sh

```
#!/bin/sh
#PBS -V
#PBS -N abaqus_test
#PBS -q commercial
#PBS -l select=1:ncpus=40:mpiprocs=1:ompthreads=1
#PBS -l walltime=04:00:00
#PBS -A abaqus
#PBS -W sandbox=PRIVATE

cd $PBS_O_WORKDIR

###### Do not edit #####
SCRIPT_PATH="$0"
TOTAL_CPUS=$(grep "^#PBS -l select=" "$SCRIPT_PATH" | sed -n 's/.*ncpus=\([0-9]\+\).*/\1/p')
if [ ! -f "$HOME/.lmod" ]; then
    touch "$HOME/.lmod"
fi
source /apps/Modules/lmod/8.7.37/init/bash
#######################

module load abaqus/2024
abq2024hf6 job=e1 cpus=$TOTAL_CPUS int verbose=3
```

※ abaqus 2024 이미지를 통한 실행은 단일 노드에서만 가능하며 멀티 노드에서는 지원되지 않습니다.


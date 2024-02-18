# The-Git-War

<aside>
💡 이 게임은 Git의 기본적인 사용 외에도, <br>
1. Branch의 상태 체크 <br>
2. Branch들의 연결성 <br>
3. 충돌 해결 <br>
을 훈련하기 위해 고안되었습니다.

</aside>

## 🌱 게임 환경

1. 총 3그룹, 각 그룹별로 3 페어가 있고, 각 그룹에는 도우미가 한명씩 있습니다.
이들은 여러분을 도와줄 것입니다.
2. 게임 시작 전, 로컬 환경에서 깃을 만들고, 깃허브의 깃과 연결합니다. (`git init` / `git clone`)
3. 깃허브에는 총 13개의 브랜치가 있습니다.
    - `main` : 게임 설명서 (건들지 마시오)
    - `team1`, `team2`, `team3` : 각 팀의 메인 브랜치 (라운드 종료 또는 게임 종료 시, 각 팀의 페어 브랜치들을 merge하는 용도)
    - `team1_pair1`, `team1_pair2`, … : 각 페어별 브랜치 (3그룹x3페어 = 9개)
4. 각 페어들은 깃허브와 같은 상태로 게임에 필요한 모든 브랜치들을 연동시킵니다.
    - 자신과 자기팀 뿐만이 아닌, 상대를 포함한 모든 페어들의 브랜치 (`team1_pair1`, …)
    - 자신의 팀의 메인 브랜치 (`team1`)
5. 각 페어들은 각자 자신들의 페어 브랜치로 `checkout` 한 상태에서 게임을 시작합니다.
6. 각 브랜치에는 `.gitignore` 파일과 관리해야할 파일들이 3개씩 존재합니다.
    - 파일의 종류는 게임 규칙에 따라 자유롭게 설정 가능합니다.
    - (default는 각 분단의 명단 리스트)

## 📖 게임 규칙

<aside>
[Mission]
우리 팀의 브랜치를 사수하고 (상태를 유지하고), <br>
상대 팀의 브랜치를 공격하라 (망가뜨려라)

</aside>

1. 게임은 총 3라운드, 각 15분씩 진행됩니다.
2. 게임시작 전, 그리고 라운드 사이사이 짧은 작전시간이 있습니다.
3. 매 라운드마다 각 팀별로 세 페어 중, 한  페어는 수비, 두 페어는 공격을 담당합니다.
라운드가 돌 때마다 수비 페어가 바뀝니다.
    - 공격자들은 상대팀들의 페어 브랜치로 침투하여, 현재 (커밋) 상태를 변경시키는 공격을 진행합니다.
    - 수비자들은 공격자들의 커밋 공격에 대응하여, 공격자들이 바꾸어 놓은 상태를 원래대로 돌려놓는 수비를 진행합니다.
        - 파일의 원본을 복사해놓고, 수비할 때마다 붙여넣기를 하는 식의 수비는 실격입니다.
        - `git revert` , `git reset` 등의 커밋 상태를 직접 되돌리는 경우 실격입니다.
        - 실무라고 생각하고, 프로그램의 상태를 수동으로 직접 고친다고 생각해주세요.
4. 수비 페어는 자기 페어 브랜치 뿐만 아니라, 우리 팀에 속한 모든 브랜치를 사수해야 합니다.
5. 깃의 사용은 오직 로컬 깃의 CLI로만 합니다. (Github, IDE 사용 금지)
    - 공격 확인 (커밋 메시지나 상태, 변경사항 확인) 등의 읽기 작업 정도만 깃허브를 활용할 수 있습니다.
6. `main` 브랜치와 각 팀의 의 메인 브랜치 (`team1`)는 건드리면 실격입니다.
7. `.gitignore` 파일은 기본적으로 건드릴 수 없습니다.
    - git master의 공격 시, 활용됩니다.
8. ~~라운드가 진행되는 동안, 페어끼리는 이야기할 수 있지만, 팀끼리는 직접 대화할 수 없습니다. (커밋 메시지로 이야기 하세요)~~
9. 게임이 끝난 후, 점수를 합산해서 꼴찌 팀, 그리고 전체 꼴찌 페어는 벌칙 (노래큐),
전체 1등 페어는 방어/면제권을 획득합니다.

## 🤼‍♂️ 컨벤션

<aside>
💡 [커밋 메시지의 기본 형식]

> `태그 (-옵션): <커밋 내용 요약>`<br/>
ex) >`resolve: 'team1_pair1' -> 'team1' 머지를 하며 충돌이 난 부분을 해결한 후 다시 커밋합니다.`<br/>
ex) > `defend -merge -conflict: 머지 당한 브랜치를 원상태로 복구하였습니다.`<br/>
ex) > `attack -add -change: 1.txt 내용을 수정하고, 4.txt 파일을 추가하였습니다.`<br/>

</aside>

> <b><span style="color:red">컨벤션 규칙 엄수!</span>
> 

### 태그 종류

#### Defense

- `feat` : 새로운 내용 추가
- `fix` : 내용 단순 수정
- `merge` : 머지 처리
- `resolve` : 충돌 해결
- `defend` : 공격에 대한 방어 처리
    - 옵션에 공격자의 옵션을 그대로 적어줄 것
    - 공격 이전의 상태로 되돌리기
    - 단, reset, revert는 불가!
    - ex) `defend -merge -conflict:`
    

#### Attack

- `attack` : 공격 (옵션을 함께 작성할 것)
    - `-add`  : 파일 추가 공격
    - `-change` : 내용 수정 공격
    - ~~`-delete` : 파일 삭제 공격~~
    - `-merge` : 머지를 통한 공격
    - `-conflict` : 충돌을 일으키는 공격
    - `-override` : 공격을 하기 위해 pull 받는 과정에서의 전처리 (exception)
- 옵션은 동시에 최대 2개까지만..
    - ex) `attack -merge -conflict:` 
    → 머지를 하고, 충돌 난 상태로 냅둔 상태
    
- 공격자의  경우, 공격 내용을 구체적으로 작성해주어야 합니다! (첫 줄에 어떤 공격인지 파악할 수 있어야함)
    - ex) >”`attack -change -delete: file1 내용 변경, file2 삭제`"
    - ex) >” `attack -merge: t1-p1 branch => t1-p2 branch 머지 진행` ”
    - ex) > “`attack -merge -conflict: t1-p1 branch => t1-p2 branch 머지 진행, 그 과정에 충돌난 상태로 push`"
    - ex) > 2 step attack : 공격을 하는 과정에 다른 누군가 먼저 공격을 한 경우
        - 1) first commit: `attack -change: file1 내용 변경`
        - 2) second commit: `attack -override -change: file1 내용 변경`  (← 수비팀은 이거 하나만 해결해도 점수 인정)

## 🥊 공격 방식 & 제한

<aside>
💡 같은 페어에게 연속으로 2번 공격을 할 수 없습니다! (1공격 = 1커밋) <br/>
파일 개수는 0~5개로 유지해야 합니다. <br/>
형평성을 위해, 원본 파일 3개에 대한 삭제 공격은 할 수 없습니다. <br/>
</aside>

1. 내용 수정 → -change
2. 충돌 일으키기  : 충돌 난 상태로 커밋을 하여 push → -change -conflict
3. 브랜치간 머지시켜버리기 : 머지한 상태로 커밋하여 push → -merge (-conflict)

### 💣 주의!

라운드별로 깃 마스터가 unknown 공격을 한번 할 수 있습니다.😈
라운드가 끝나기 전까지 공격을 인지하고 처리하세요!

- ~~원격 페어 브랜치 삭제~~
- ~~원격 팀 메인 브랜치에 몰래 커밋 `[sneak] 깃 마스터의 침입`~~
- virus / bomb 공격 (몰래 심어진 바이러스 / 폭탄을 지워보시오)

## 🏆 점수 산정 방식

<aside>
💡 1. 라운드별로 점수 계산<br/>
💡 2. 점수는 페어별로 매긴 뒤, 팀 합산

</aside>

### Defenders

#### +

- 기본 기능 완성 (+1)
- 공격에 대한 대처 (+2)
    - 공격자의 커밋 하나에 대응할 때마다 산정됩니다.
    - 공격을 여러번 쌓여있는데, 각각의 공격을 순차적으로 해결하지 않고,
    한꺼번에 한번만 해결한 경우, 공격에 대한 대처는 1번만 한 것입니다.
- 제한 시간 안에 우리 팀의 모든 문제 해결 (+5)
- 깃 마스터에 의한 바이러스 퇴치 (+3)

#### -

- convention rule 위반 (→ 0점: 수비 실패)
- 충돌을 해결하지 못한 채로 push (-1)

### Attackers

#### +

- 공격을 올바르게 함 (+1)
- 공격 옵션을 여러개 (+0.5)
- 공격을 상대가 막지 못함 (+1)
- 예술 점수 (+1)

#### -

- convention rule 위반 (→ 0점: 공격 무효)
- 파일 개수를 변형시킬 때, 범위를 벗어나는 경우 (0~5개 사이가 아닌 경우)

## soccer DB 테이블 정의 (2-1 번 과정)

### Player (player_id, name, age, team, position, preferred_foot, transfer_value)

- player_id : 선수 고유 ID
  
- name : 축구 선수 이름

- age : 선수 나이

- team : 축구 팀

- position : 축구 포지션

- preferred_foot : 주발이 무엇인지

- transfer_value : 이적시장 가치 (선수를 영입할 때 얼마가 필요한지)

<br/>

### Team (team_id, name, founded_year, home_stadium, league)

- team_id : 팀 고유 id

- name : 팀 이름

- founded_year : 창단 연도

- home_stadium : 홈 구장 이름 

- league : 소속 리그

<br/>

### leagues (league_id, league_name, country, tier, number_of_teams)

- league_id : 리그 고유 식별자

- league_name : 이름

- country : 리그 소속 국가

- tier : 리그 수준

- number_of_teams : 참여 팀 수

<br/>

### matches (match_id, league_id, season, match_date, home_team_id, away_team_id, stadium, referee_name, attendance)

- match_id : 경기 고유 ID 

- league_id : 리그 ID

- season : 시즌 정보

- match_date : 경기 날짜

- home_team_id : 홈 팀 ID

- away_team_id : 원정 팀 ID

- stadium : 경기장 이름

- referee_name : 주심 이름

- attendance : 관중 수

<br/>

### transfers (transfer_id, player_id, player_name, from_team, to_team, transfer_fee)

- transfer_id : 이적 고유 ID

- player_id :  이적한 선수 ID

- player_name : 이적 선수 이름

- from_team : 이전 소속 팀 

- to_team : 새 소속 팀 

<br/>

### 각 테이블 문장으로 설명 (2-2 과정)

### Player 테이블

Player 테이블은 player_id(INT, PRIMARY KEY), name(VARCHAR, NOT NULL), age(INT, CHECK(age > 0)), team(INT, FOREIGN KEY), position(VARCHAR, NOT NULL), preferred_foot(VARCHAR, CHECK(preferred_foot IN ('left', 'right', 'both'))), transfer_value(INT, CHECK(transfer_value >= 0)) 속성으로 구성됩니다.
각 선수는 하나의 팀에 소속되므로 team 속성은 Team 테이블의 team_id를 참조하며 1:N 관계를 형성합니다.

<br/>

### Team 테이블

Team 테이블은 team_id(INT, PRIMARY KEY), name(VARCHAR, NOT NULL, UNIQUE), founded_year(YEAR, CHECK(founded_year >= 1800)), home_stadium(VARCHAR), league(INT, FOREIGN KEY) 속성으로 구성됩니다.
각 팀은 하나의 리그에 속하므로 league는 Leagues 테이블의 league_id를 참조하고, 하나의 리그는 여러 팀을 가질 수 있어 1:N 관계입니다.

<br/>

### Leagues 테이블

Leagues 테이블은 league_id(INT, PRIMARY KEY), league_name(VARCHAR, NOT NULL), country(VARCHAR), tier(INT, CHECK(tier > 0)), number_of_teams(INT, CHECK(number_of_teams >= 0)) 속성으로 구성됩니다.

<br/>

### Matches 테이블

Matches 테이블은 match_id(INT, PRIMARY KEY), league_id(INT, FOREIGN KEY), season(YEAR), match_date(DATE), home_team_id(INT, FOREIGN KEY), away_team_id(INT, FOREIGN KEY), stadium(VARCHAR), referee_name(VARCHAR), attendance(INT, CHECK(attendance >= 0)) 속성으로 구성됩니다.
각 경기는 하나의 리그에 속하고, 두 팀(홈, 원정)이 참여하므로 league_id, home_team_id, away_team_id는 모두 외래키이며, Team 및 Leagues 테이블과 1:N 관계입니다.

<br/>

### Transfers 테이블

Transfers 테이블은 transfer_id(INT, PRIMARY KEY), player_id(INT, FOREIGN KEY), player_name(VARCHAR, NOT NULL), from_team(INT), to_team(INT), transfer_fee(INT, CHECK(transfer_fee >= 0)) 속성으로 구성됩니다.
선수의 이적 정보를 저장하며, player_id는 Player 테이블과 연결되고 1:N 관계입니다.

➤ 정규화 요약 (최소 3NF): 모든 테이블은 반복 속성을 제거하고, 각 속성은 기본키에만 종속되어 있으며 이행적 종속도 제거되어 있어 3NF를 만족합니다. 이는 데이터 중복 방지 및 무결성 유지를 위함입니다.




















































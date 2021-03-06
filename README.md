# LoL-Match-Prediction
롤 승부 예측 프로젝트입니다.

프로젝트 진행 기간 : 2021-06-29 ~ 2021-07-02

AI 부트캠프 3기 백경렬의 두번째 프로젝트입니다.

section2에서는 롤 승패 데이터들을 분석하였습니다.

팀 1, 팀 2 각각 5개의 챔피언들에 따른 승 패를 예측 하였습니다.

챔피언의 역할군에 따른 가중치도 추가하여 분석 하였습니다.

챔피언의 선택만으로도 승과 패에 영향을 미친다는 분석을 하였습니다.

영상 : https://youtu.be/w9T9M1Ygbnw

영상 속 내용은 아래 내용과 같습니다.
#

안녕하세요, 리그 오브 레전드 챔피언 선택에 따른 승패 예측으로 두번째 섹션 프로젝트를 발표 할 코드스테이츠 3기 백경렬 입니다.

이번 발표의 목차는 데이터 선정, 베이스라인 선택, 데이터 모델 분석, Q & A 로 이루어져 있습니다.

첫번째로 데이터의 선정과 데이터 셋을 선택한 이유에 대해 알아보겠습니다.

롤에 관한 데이터를 찾는 도중 챔피언 선택에 대한 승패 데이터가 있기에 챔피언 선택에서부터 승패가 어느정도 결정이 되는지 확인해보기 위해 위의 데이터를 선정 하였습니다.

첫번째로 찾은 데이터는 150개의 챔피언 중 Team1, Team2에 각각 5개의 챔피언 선택 한 후 어느 팀이 승리하는지를 담은 데이터고,

이 데이터만으로는 유의미한 결과가 나오지 않기에 각 챔피언의 역할군 어쎄신, 파이터, 메이지, 마크맨, 서포터, 탱커로 이루어진 데이터를 추가로 넣었습니다.

데이터 타겟에 따른 베이스라인을 구축해보겠습니다.

![image](https://user-images.githubusercontent.com/40240766/166125960-e07bbea4-0373-4122-90ce-a6f10c0d9c18.png)

이번 프로젝트의 타겟은 승 패를 0, 1로 분류한 값들을 타겟으로 설정 하겠습니다. 데이터 셋 안의 승이 17466번, 패가 17212 번으로 승이 조금 더 많습니다. 

승을 기준으로 베이스 라인을 구축하여 모두 1로 예측 했을 때 정확도를 확인해본 결과 트레이닝 정확도는 50.3 % 가 나왔습니다.

이 모델보다 더 좋은 결과를 도출 해내면 우리가 선택한 데이터들이 어느정도 승패에 영향이 있음을 알 수 있습니다.

데이터 모델에 따른 결과들을 보도록 하겠습니다.

![image](https://user-images.githubusercontent.com/40240766/166125972-44e1c390-e04c-4b6b-8a66-e0979e040ac0.png)

두번째 데이터 셋을 추가 하지 않고,

150개의 챔피언 중 팀1이 5개의 챔피언을 선택했을 때 승 패를 예측 하는 모델을 만들어 테스트 해봤습니다.

랜덤포레스트를 사용하였고, 랜더마이즈 서치 시브이로 최적화 하였습니다. 

베이스 라인 모델보단 정확도가 4퍼센트 올랐지만, 이정도 예측으로는 별로 의미가 없어 보입니다.

데이터가 너무 단조로운 탓이 아닐까 싶어 추가 데이터를 가져와 첫번째 데이터와 합쳐 다시 진행해 보았습니다.

![image](https://user-images.githubusercontent.com/40240766/166125984-4a3d7b21-9dc2-4928-9cce-9cb4ec09e6e4.png)

첫번째 데이터와 두번째 데이터를 같은 곳에서 받아온 것이 아니여서 챔피언을 부르는 명칭이 차이가 있어서 오공을 몽키킹으로 수정 하였고, 표기에도 따옴표나 중간 중간 공백의 차이가 있어서 이를 수정 해주었습니다.

새로 업데이트 된 챔피언들이 두번째 데이터셋에는 추가가 되어 있지 않아, 릴리아와 요네를 추가해주었습니다. 역할군도 릴리아는 메이지, 서포터, 요네는 파이터 어쌔신으로 추가를 해주었습니다.

![image](https://user-images.githubusercontent.com/40240766/166125989-53dcc94a-df38-480f-9748-d9ec3a09fe6a.png)

위에서 전처리한 데이터를 첫번째 데이터셋과 두번째 데이터셋을 합쳐

원핫인코딩과 XGBoost를 사용하여 예측한 결과 64%로 승패를 맞췄으며, 베이스 모델과, 첫번째 데이터 셋만으로 예측을 한 결과보다 무려 14% 더 높은 정확도로 승패를 예측을 했습니다.

![image](https://user-images.githubusercontent.com/40240766/166125992-e815c43d-4427-4da4-8b1b-d169a0a1f635.png)

이 모델에 승패에 가장 영향을 많이 준 15개의 챔피언을 찾아보았습니다.

럭스, 케이틀린, 진, 세트, 이즈리얼을 선택했을 때 게임승리에 영향을 주는 가중치가 높아졌고,

다이에나, 카서스, 트위스트페이트, 코르키, 엘리스를 선택했을 때 패배에 가중치를 주어 예측 하였습니다.

![image](https://user-images.githubusercontent.com/40240766/166125995-b3d0d4c0-4ed7-4c01-8083-4955188c58de.png)

다음은 승에 영향을 많이 준 럭스와 케이틀린을 선택했을 때의 승률 입니다.

케이틀린만 선택 되었을 때는 54퍼센트의 승률을 가지고, 두 챔피언이 다 선택 되었을 때는 55.3퍼센트의 승률을 가집니다.

둘다 선택 되지 않았을 때는 49.9퍼센트 확률의 승률을 가지는 것을 보면 두 챔피언을 선택하는게 승에 영향을 더 많이 미치는 것으로 확인 됩니다.

![image](https://user-images.githubusercontent.com/40240766/166126000-54a11750-8591-41ae-bc0b-d12afa903379.png)

승패에 영향을 주는 챔피언을 골라 봤습니다.

카타리나, 리신, 트위치, 요네, 젝스, 드레이븐, 이즈리얼은 승과 패에 어느정도 영향을 미치는 챔피언으로 확인되었습니다.

위의 영향력에 따라 경기에 따른 분석을 해 보았습니다.

이 경기의 경우 나미가 있다는 것이 승에 요인을 주었지만, 리신과 나르가 있고, 진이 없다는 이유로 패배를 예측 하였습니다.

데이터들로 예측해본 결과 챔피언의 선택에 따라서도 승패가 어느정도 결정됨을 확인 하였습니다.

추가적으로 게임 내에서 구입한 아이템에 따른 승패도 예측을 해보고 싶었지만, 시간이 부족하여 여기까지 분석 후 발표를 마치겠습니다 ! 

그 외 질문이 있으면 메일로 보내주시면 답변해 드리겠습니다 !

이상 코드스테이츠 3기 백경렬의 데이터 분석을 마치겠습니다. 감사합니다 !

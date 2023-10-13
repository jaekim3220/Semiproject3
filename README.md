# 세미프로젝트3

# Members
- TeamMate1 : 김재현, https://github.com/jaekim3220
- TeamMate2 : 김정훈, https://github.com/jagara101
- TeamMate3 : 하진석, https://github.com/hajinseok11


## 데이터 분석을 위한 (종속/독립)변수를 추출하고 전처리(결측치, 이상치 정제)와 다양한 가설을 검정하고 시각화를 진행

# 필수
- 데이터 수집
- Data 타입 확인
- 기초통계량 확인(describe)
- 결측치/이상치 확인 및 정제
    - 레그플롯(이상치확인)
    - 박스플롯(이상치확인)
    - 히스토그램(이상치확인 및 도수 분포표 확인)
- 신뢰구간 확인
- 표준화(scaling)
- 주성분분석(PCA)
- 데이터 분석(상관분석, 회귀분석 등)
    - 데이터의 관계를 파악하고 해석


!SemiProject_01 -> !SemiProject
### #결측치 처리 - 0값으로 대체
데이터프레임으로 출력

### #왜도/첨도
왜도와 첨도 결과물을 데이터프레임으로 출력

### #잔차의 선형성/정규성 확인
- 선형성 : 종속변수와 독립변수 간의 선형 관계
- 정규성 : 잔차들의 분포가 정규 분포를 이룸

평균 제곱 오차를 사용해 잔차도를 그려 Q-Q Plot보다 자세히 잔차의 정규분포를 판별 가능

# 분석 설명

```
데이터 분포(도수분포, 히스토)
D. 탐색적 데이터 분석(EDA)/02. 기술통계/2-데이터분포.ipynb

이원분산분석
E. 확증적 데이터 분석(CDA)/02. 두 변수간의 차이 분석/08-Two-way-ANOVA.ipynb

사후분석
E. 확증적 데이터 분석(CDA)/02. 두 변수간의 차이 분석/09-사후분석.ipynb

다변수의 상관분석
E. 확증적 데이터 분석(CDA)/03. 연관성 분석/03-여러_변수의_상관분석.ipynb
스피어만 상관분석
E. 확증적 데이터 분석(CDA)/03. 연관성 분석/04-스피어만_상관분석.ipynb


E. 확증적 데이터 분석(CDA)\06. 시계열 분석\09-네이버_검색어_트렌드_복수단어.ipynb
```


# 신뢰수준

```
clevel = 0.95
(# 샘플 사이즈)
n = len(df['총생활비'])
(# 자유도)
dof = n - 1
(# 평균)
sample_mean = df2['총생활비'].mean()
(# 표본 표준 편차)
sample_std = df2['총생활비'].std(ddof=1)
(# 표본 표준오차)
sample_std_error = sample_std / sqrt(n)
(# 신뢰구간)
cmin, cmax = t.interval(clevel, dof, loc=sample_mean, scale=sample_std_error)

sb.kdeplot(data=df2, x='총생활비')
(# 신뢰구간 min 설정)
sb.lineplot(x=[cmin, cmax], y=[0,0.1], color='red')
(# 신뢰구간 max 설정)
sb.lineplot(x=[cmax, cmin], y=[0,0.1], color='blue')
(# -> 붉은선, 파란선 구간이 신뢰 구간 95% 지점)
plt.xlim(-20, 500)
plt.ylim(0, 0.01)
plt.show()
plt.close()
```



# 분석 순서

```
회귀분석
결과보고
잔차분석
- R-squared, pvalue, Durbuin-Watson 값으로 독립성 확인(1.5 ~ 2.5 사이)
잔차의 정규성
- Q-Q Plot
정규성 판단
- 정규성 판단을 위한 Kolmogorov Smirnov 검정
샤피로 검정은 표본이 50개 미만
- 잔차의 등분산성 
브로이슈 패건 검정
- 탐색적 데이터 분석
범주형 데이터는 category 형태로 변환, 탐색적 데이터 분석에서 제외하도록 설정
- PCA 분석
회귀분석에 필요한 요인들을 선정하기 위해`주성분 분석을 수행
```
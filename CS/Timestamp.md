# Prisma Timezone Issue
프리즈마에서 시간 값을 저장할때, KST 시간이 아닌 UTC 시간이 저장됨.
ex)(현재 시간) : 21.5.13시 -> (프리즈마를 통해 DB에 저장되는 시간 ) 21.5.04시 (UTC : KTC-9hour)

## 해결법 : middleware 사용
DB에 넣을 때와 빼올 때 -9, +9 시간을 적용하는 미들웨어를 사용하여 현재 시간으로 저장 / 출력할 수 있다.

## middleware 중복 이슈
create 한 date 값을 받아 update를 수행하니 middleware를 두번 거쳐서 18시간 차이가 나게 됨

# Timestamp
1970년 1월 1일 기준으로 얼마만큼의 시간이(밀리초) 지났는지 나타냄

현재 날짜로 Timestamp를 찍어낸 후 create, update 시 해당 timestamp를 전달해 date를 생성하면 해결된다.

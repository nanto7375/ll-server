# ll-server

NestJS · TypeORM · PostgreSQL 기반 학습 앱 서버입니다.

Node.js 24 LTS와 Yarn 4.18.1을 사용합니다.
패키지는 `node_modules` 방식으로 설치합니다.

## 로컬 PostgreSQL

Docker Desktop을 실행한 상태에서 서버 폴더에서 시작합니다.

```bash
corepack enable
yarn install --immutable
cp -n .env.example .env
```

`.env`의 `POSTGRES_PASSWORD`를 정한 후 실행합니다. 이미 `.env`가 있으면 해당 파일을 그대로 사용합니다.

```bash
yarn db:up
yarn db:status
```

공식 `postgres:18.6` 이미지와 Docker 볼륨을 사용합니다.
PostgreSQL 18 이미지의 데이터 볼륨은 `/var/lib/postgresql`에 연결합니다.

## DBeaver 접속

새 연결에서 PostgreSQL을 선택하고 다음 값을 입력합니다.

| 항목 | 기본값 |
| --- | --- |
| Host | `127.0.0.1` |
| Port | `5432` (`POSTGRES_PORT`) |
| Database | `ll_server` (`POSTGRES_DB`) |
| Username | `ll_user` (`POSTGRES_USER`) |
| Password | `.env`의 `POSTGRES_PASSWORD` |

## 종료 및 로그

```bash
yarn db:logs
yarn db:down
```

`db:down`은 컨테이너를 종료하고 데이터 볼륨은 유지합니다.
환경 변수의 DB 이름·사용자·비밀번호는 빈 볼륨을 처음 초기화할 때 적용됩니다.

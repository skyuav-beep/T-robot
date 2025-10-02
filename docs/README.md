# T_Robot
# Trading Bot – Overview


## Purpose
- Open API 기반 체결/매수/매도 자동화
- Admin/User/Operator 분리, 곡선 목표 기반 노출 관리


## Architecture (High-level)
- apps/gw: API Gateway (NestJS)
- apps/bots: Bot Runtime (NestJS/Worker)
- packages/shared: 공통 유틸(정밀도/레이트리밋)
- Postgres (Docker): 영속 데이터
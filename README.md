# OKI Circuit — AI Server PCB (Vercel deploy)

힉스필드 CDN에 있던 이미지/영상을 로컬(`assets/`)로 내려받아 자체 호스팅하는 정적 사이트입니다.

## 배포 순서

```bash
# 1) 이 폴더로 이동
cd oki-vercel

# 2) CDN 에셋 다운로드 (인터넷 되는 본인 PC 터미널에서)
bash download_assets.sh        # assets/ 에 16개 파일(png 9 / mp4 7) 생성

# 3) 로컬 미리보기 (선택) — 아무 정적 서버나 사용
python3 -m http.server 8080    # http://localhost:8080

# 4) Vercel 배포
npm i -g vercel                # 최초 1회
vercel                         # 프리뷰 배포
vercel --prod                  # 프로덕션 배포
```

Vercel은 루트의 `index.html`을 자동으로 정적 사이트로 인식합니다.
빌드 설정 불필요(Framework Preset: **Other**, Build Command 비움, Output Directory 비움/루트).

## 구성
- `index.html` — 메인 페이지 (에셋 경로가 모두 `assets/...` 로컬 상대경로)
- `download_assets.sh` — 힉스필드 CDN → `assets/` 다운로드 스크립트
- `assets/` — 다운로드된 이미지·영상 (스크립트 실행 후 생성)
- `vercel.json` — 정적 설정 + 에셋 장기 캐시 헤더

## 참고
- 에셋 파일명은 의미 기반으로 정리됨 (예: `vid-hero.mp4`, `img-futuristic-board.png`).
- 다운로드가 막히면(회사 방화벽 등) VPN 해제/개인 네트워크에서 재시도하세요.

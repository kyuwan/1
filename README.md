<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>🚀 GitHub Actions 오픈 안내</title>
  <style>
    :root{
      --bg1:#0f1020; /* 메인 배경 */
      --bg2:#1a1b33; /* 카드 배경 */
      --accent:#6ee7f3; /* 포인트 */
      --accent-2:#a78bfa; /* 포인트 2 */
      --ok:#34d399; /* 그린 */
      --warn:#f59e0b; /* 옐로 */
      --text:#e6e6f0; /* 본문 */
      --muted:#b8b9c9; /* 서브 텍스트 */
      --code-bg:#0b0c19; /* 코드 배경 */
      --shadow: 0 10px 30px rgba(0,0,0,.35);
      --radius: 18px;
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0; color:var(--text); font-family: ui-sans-serif, -apple-system, Segoe UI, Roboto, "Apple SD Gothic Neo", Noto Sans KR, Arial, "Helvetica Neue", sans-serif;
      background: radial-gradient(1200px 600px at 10% -10%, rgba(167,139,250,.18), transparent 60%),
                  radial-gradient(1000px 500px at 110% 10%, rgba(110,231,243,.14), transparent 60%),
                  linear-gradient(180deg, #0b0c19 0%, #121326 60%, #0f1020 100%);
      overflow-x:hidden;
    }
    /* 은은한 격자 배경 */
    .grid-overlay{
      position:fixed; inset:0; pointer-events:none; opacity:.12;
      background-image: linear-gradient(to right, rgba(255,255,255,.08) 1px, transparent 1px),
                        linear-gradient(to bottom, rgba(255,255,255,.08) 1px, transparent 1px);
      background-size: 40px 40px;
      mask-image: radial-gradient(1000px 600px at 70% -20%, rgba(0,0,0,1), rgba(0,0,0,0.1));
    }

    .container{ max-width:1100px; margin:0 auto; padding:40px 20px 80px; position:relative; }

    header.hero{
      position:relative; border-radius: var(--radius); padding:56px 28px; overflow:hidden;
      background: linear-gradient(135deg, rgba(110,231,243,.18), rgba(167,139,250,.22));
      box-shadow: var(--shadow);
    }
    .hero .badge{ display:inline-flex; align-items:center; gap:8px; padding:8px 12px; border-radius:999px; background:rgba(255,255,255,.08); backdrop-filter: blur(6px); font-weight:600; letter-spacing:.2px;}
    .hero h1{ font-size: clamp(28px, 5vw, 46px); line-height:1.1; margin:14px 0 12px; }
    .hero p{ color:var(--muted); max-width:740px; margin:0; font-size: clamp(14px, 2.3vw, 18px)}

    /* 장식용 SVG */
    .hero-illust{ position:absolute; right:-10px; bottom:-34px; width:min(42vw, 460px); opacity:.85; filter: drop-shadow(0 10px 24px rgba(0,0,0,.35)); }

    .actions{ display:flex; gap:12px; margin-top:22px; flex-wrap:wrap }
    .btn{ appearance:none; border:0; border-radius:12px; padding:12px 16px; color:#0b0c19; background: white; font-weight:700; cursor:pointer; box-shadow: var(--shadow); text-decoration:none; display:inline-flex; align-items:center; gap:10px }
    .btn.secondary{ background:transparent; color:var(--text); border:1px solid rgba(255,255,255,.22)}
    .btn .dot{ width:10px; height:10px; border-radius:999px; background: var(--ok) }

    section{ margin-top:38px }

    .card{ background: var(--bg2); border:1px solid rgba(255,255,255,.06); border-radius: var(--radius); box-shadow: var(--shadow); padding:22px }

    .grid{ display:grid; gap:16px }
    .grid.features{ grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); }

    .feature{ position:relative; padding:18px; border-radius:16px; background:linear-gradient(180deg, rgba(255,255,255,.04), rgba(255,255,255,.02));
      border:1px solid rgba(255,255,255,.06)
    }
    .feature h3{ margin:10px 0 6px; font-size:18px }
    .feature p{ margin:0; color:var(--muted); font-size:14px; line-height:1.6 }
    .icon{
      width:34px; height:34px; border-radius:10px; display:grid; place-items:center; background:rgba(255,255,255,.09);
      box-shadow: inset 0 0 0 1px rgba(255,255,255,.08);
    }

    .steps{ counter-reset: step; display:grid; grid-template-columns:repeat(auto-fit, minmax(270px, 1fr)); gap:14px }
    .step{ position:relative; padding:18px 16px 18px 54px; border-radius:14px; border:1px dashed rgba(255,255,255,.18); background:linear-gradient(180deg, rgba(255,255,255,.03), rgba(255,255,255,.02)); }
    .step::before{ counter-increment: step; content: counter(step); position:absolute; left:14px; top:14px; width:28px; height:28px; border-radius:9px; display:grid; place-items:center; background:rgba(167,139,250,.26); color:white; font-weight:800; border:1px solid rgba(255,255,255,.18) }
    .step strong{ display:block; margin-bottom:8px }
    .step p{ margin:0; color:var(--muted); font-size:14px; line-height:1.6 }

    .code{ background:var(--code-bg); border:1px solid rgba(255,255,255,.08); border-radius:14px; padding:18px; overflow:auto; font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace; font-size: 13px; line-height:1.6; position:relative }
    .code .hint{ position:absolute; right:12px; top:8px; color:var(--muted); font-size:12px }
    .kbd{ font-family:inherit; font-weight:700; padding:2px 8px; border-radius:8px; border:1px solid rgba(255,255,255,.25); background:rgba(255,255,255,.06) }

    details{ background:linear-gradient(180deg, rgba(255,255,255,.03), rgba(255,255,255,.02)); border:1px solid rgba(255,255,255,.08); border-radius:14px; padding:14px 16px; }
    details + details{ margin-top:12px }
    summary{ cursor:pointer; font-weight:700 }
    summary span{ color:var(--muted); font-weight:500 }

    .footer-note{ color:var(--muted); font-size:13px }

    /* 반응형 */
    @media (max-width:720px){
      .hero{ padding-bottom: 240px }
      .hero-illust{ right:-30px; bottom:-140px; width: 360px }
    }
  </style>
</head>
<body>
  <div class="grid-overlay"></div>
  <div class="container">
    <header class="hero">
      <div class="badge">✨ 신규 기능 오픈 · <span class="kbd">GitHub Actions</span></div>
      <h1>사내 GitHub Actions 오픈 안내</h1>
      <p>
        그동안 많은 분들이 요청해주신 <strong>GitHub Actions</strong> 기능이 사내 저장소에서 공식 지원됩니다.
        이제 <strong>빌드 · 테스트 · 배포</strong> 등 반복 업무를 자동화하여 개발 효율과 안정성을 높여보세요!
      </p>
      <div class="actions">
        <a class="btn" href="#apply"><span class="dot"></span> Jira SR로 신청하기</a>
        <a class="btn secondary" href="#docs">가이드 & 예시 보기</a>
      </div>

      <!-- 장식용 일러스트: 로켓 + 구름 (SVG) -->
      <svg class="hero-illust" viewBox="0 0 500 320" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
        <defs>
          <linearGradient id="g1" x1="0" y1="0" x2="1" y2="1">
            <stop offset="0%" stop-color="#a78bfa" stop-opacity="0.9" />
            <stop offset="100%" stop-color="#6ee7f3" stop-opacity="0.9" />
          </linearGradient>
          <filter id="glow" x="-50%" y="-50%" width="200%" height="200%">
            <feGaussianBlur stdDeviation="6" result="blur"/>
            <feMerge><feMergeNode in="blur"/><feMergeNode in="SourceGraphic"/></feMerge>
          </filter>
        </defs>
        <!-- 구름 -->
        <g opacity=".55">
          <ellipse cx="90" cy="240" rx="90" ry="36" fill="url(#g1)" opacity=".25"/>
          <ellipse cx="180" cy="240" rx="120" ry="42" fill="url(#g1)" opacity=".18"/>
          <ellipse cx="300" cy="250" rx="140" ry="48" fill="url(#g1)" opacity=".16"/>
        </g>
        <!-- 로켓 -->
        <g transform="translate(220,60) rotate(-12)" filter="url(#glow)">
          <path d="M60 0 C 20 40 8 110 18 150 l84 0 C112 110 100 40 60 0z" fill="url(#g1)"/>
          <rect x="40" y="90" width="40" height="24" rx="6" fill="#0b0c19"/>
          <circle cx="60" cy="62" r="14" fill="#0b0c19"/>
          <path d="M18 150 l84 0 l-12 26 l-60 0 z" fill="#fb7185" opacity=".85"/>
          <path d="M30 176 q30 30 5 60" stroke="#fb7185" stroke-width="4" fill="none" opacity=".6"/>
          <path d="M76 176 q-30 30 -5 60" stroke="#fb7185" stroke-width="4" fill="none" opacity=".6"/>
        </g>
      </svg>
    </header>

    <section id="about">
      <div class="card">
        <h2>🔎 GitHub Actions란?</h2>
        <p>
          GitHub 저장소 이벤트(<em>push, pull_request</em> 등)를 트리거로 하여, 
          <strong>빌드·테스트·배포</strong> 같은 작업을 <strong>자동화</strong>할 수 있는 CI/CD 플랫폼입니다. 
          워크플로우 파일(<code>.github/workflows/*.yml</code>)로 파이프라인을 선언적으로 구성합니다.
        </p>
      </div>
    </section>

    <section id="features">
      <h2>✨ 주요 특징</h2>
      <div class="grid features">
        <div class="feature">
          <div class="icon">🛠️</div>
          <h3>빌드·테스트 자동화</h3>
          <p>PR 생성/업데이트 시 자동으로 빌드와 테스트를 실행하고 결과를 확인합니다.</p>
        </div>
        <div class="feature">
          <div class="icon">🚀</div>
          <h3>브랜치/태그 배포</h3>
          <p>메인 브랜치 머지, 태그 푸시 등 원하는 조건에 맞춰 배포 파이프라인을 구동합니다.</p>
        </div>
        <div class="feature">
          <div class="icon">🔗</div>
          <h3>광범위한 연동</h3>
          <p>Docker, Kubernetes, 패키지 레지스트리, 클라우드 등과 손쉽게 연계됩니다.</p>
        </div>
        <div class="feature">
          <div class="icon">📊</div>
          <h3>가시성 & 감사로그</h3>
          <p>실행 이력/로그/아티팩트로 문제를 빠르게 파악하고 재현할 수 있습니다.</p>
        </div>
      </div>
    </section>

    <section id="apply">
      <h2>📝 이용 방법 (Jira SR)</h2>
      <div class="steps">
        <div class="step">
          <strong>Jira Service Request 접속</strong>
          <p>포털에서 <em>GitHub Actions 활성화 요청</em>을 선택합니다.</p>
        </div>
        <div class="step">
          <strong>필수 정보 입력</strong>
          <p>저장소 이름, 사용 목적, 예상 트리거(<code>push</code>/<code>pull_request</code>), 필요한 권한/시크릿 등을 기재합니다.</p>
        </div>
        <div class="step">
          <strong>승인 & 적용</strong>
          <p>승인 후 저장소에서 <code>.github/workflows/</code>에 워크플로우 파일을 추가하면 바로 사용 가능합니다.</p>
        </div>
      </div>
    </section>

    <section id="docs">
      <h2>📚 빠른 시작 예시 (Node.js)</h2>
      <div class="code">
        <div class="hint">.github/workflows/ci.yml</div>
<pre><code>name: CI
on:
  pull_request:
    branches: [ main ]
  push:
    branches: [ main ]

jobs:
  build-test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'

      - name: Install
        run: npm ci

      - name: Lint & Test
        run: |
          npm run lint --if-present
          npm test -- --ci

      - name: Build
        run: npm run build --if-present

      # 예: 테스트 커버리지 아티팩트 업로드
      - name: Upload coverage
        uses: actions/upload-artifact@v4
        with:
          name: coverage
          path: coverage/**
</code></pre>
      </div>
    </section>

    <section>
      <div class="grid" style="grid-template-columns: 1.2fr .8fr; gap:16px">
        <div class="card">
          <h2>🔐 시크릿 & 권한</h2>
          <p><strong>저장소 → Settings → Secrets and variables</strong>에서 시크릿을 등록하고, 필요한 권한만 최소화하세요(<em>least privilege</em> 원칙).</p>
          <p class="footer-note">배포 키/토큰은 개인 계정이 아닌 조직(봇) 토큰 사용을 권장합니다.</p>
        </div>
        <div class="card">
          <h2>⚠️ 유의 사항</h2>
          <ul>
            <li>불필요한 워크플로우 반복 실행 방지를 위해 <code>paths</code>, <code>concurrency</code> 규칙을 설정하세요.</li>
            <li>조직 정책에 따라 외부 액션 사용이 제한될 수 있습니다(내부 검증 버전 우선).</li>
            <li>장시간 러너 점유 작업은 팀 협의 후 예약 실행을 권장합니다.</li>
          </ul>
        </div>
      </div>
    </section>

    <section>
      <h2>🙋 자주 묻는 질문 (FAQ)</h2>
      <details>
        <summary>러너(Runner)는 어디서 실행되나요? <span>— 호스티드/셀프호스티드 정책</span></summary>
        <p>기본은 GitHub 호스티드 러너를 사용합니다. 보안/네트워크 이슈로 내부망 접근이 필요하면 셀프호스티드 러너 사용을 요청하세요.</p>
      </details>
      <details>
        <summary>요금/쿼터 제약이 있나요? <span>— 팀별 할당 정책</span></summary>
        <p>조직 정책에 따라 팀별 분 단위 할당이 있으며, 과다 사용 시 사전 안내 후 조정됩니다.</p>
      </details>
      <details>
        <summary>외부 액션 사용이 막혀요. <span>— 승인 절차</span></summary>
        <p>보안 검토를 거친 내부 미러/고정 버전을 우선 사용합니다. 신규 액션이 필요하면 Jira SR에 액션 URL/버전과 목적을 첨부해주세요.</p>
      </details>
    </section>

    <section class="card" style="margin-top:28px">
      <h2>✅ 요약</h2>
      <ul>
        <li><strong>GitHub Actions</strong>로 빌드·테스트·배포 자동화</li>
        <li><strong>Jira SR</strong>로 활성화 요청 → 승인 후 즉시 사용</li>
        <li>샘플 워크플로우 제공, 시크릿/권한 최소화 권장</li>
      </ul>
      <div class="actions">
        <a class="btn" href="#apply">지금 신청</a>
        <a class="btn secondary" href="#features">특징 다시 보기</a>
      </div>
    </section>

    <p class="footer-note" style="margin-top:22px">문의: DevOps/플랫폼팀 · 내부 채널 #devops-support</p>
  </div>
</body>
</html>

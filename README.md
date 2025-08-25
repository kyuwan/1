<div style="background-color:#f4f6fa; padding:20px; border-radius:10px; border:1px solid #ccc; font-family:Arial, sans-serif;">
  <h2 style="color:#333;">🚀 GitHub Actions 오픈 안내</h2>
  <p>그동안 요청이 많았던 <b>GitHub Actions</b> 기능이 사내 GitHub에서 오픈되었습니다! 🎉</p>

  <table border="0" cellpadding="10" cellspacing="0" width="100%" style="background:#fff; border:1px solid #ddd; border-radius:6px;">
    <tr>
      <td style="font-size:14px; color:#333;">
        <b>🔎 GitHub Actions란?</b><br>
        코드 <b>빌드(Build)</b>, <b>테스트(Test)</b>, <b>배포(Deploy)</b> 작업을 자동화하는 GitHub의 CI/CD 기능입니다.
      </td>
    </tr>
  </table>

  <h3 style="margin-top:20px; color:#444;">✨ 주요 특징</h3>
  <ul style="line-height:1.6; color:#333;">
    <li>🛠️ 빌드/테스트 자동화</li>
    <li>🚀 배포 파이프라인 구성</li>
    <li>🔗 다양한 서비스 연동</li>
    <li>📊 실행 로그 및 가시성 제공</li>
  </ul>

  <h3 style="margin-top:20px; color:#444;">📝 신청 방법</h3>
  <ol style="line-height:1.6; color:#333;">
    <li><b>Jira SR</b> → <i>GitHub Actions 활성화 요청</i> 선택</li>
    <li>저장소 이름 / 사용 목적 기재</li>
    <li>승인 완료 후 <code>.github/workflows/</code>에 파일 추가</li>
  </ol>

  <div style="margin-top:20px; background:#fff; border:1px solid #ddd; padding:10px; border-radius:6px;">
    <b>예시 워크플로우 (Node.js)</b>
    <pre style="font-size:12px; background:#f9f9f9; border:1px solid #ccc; padding:10px; overflow:auto;">
name: CI
on:
  push:
    branches: [ main ]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
      - run: npm ci
      - run: npm test
    </pre>
  </div>

  <p style="margin-top:20px; font-size:12px; color:#555;">
    문의: DevOps/플랫폼팀 · 내부 채널 #devops-support
  </p>
</div>

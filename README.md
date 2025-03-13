<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="utf-8" />
  <title>NTB 19기 챌린지 학습초대코드 확인</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      background-color: #f0f8ff; /* 옅은 파란 배경 */
      font-family: 'Malgun Gothic', sans-serif;
      color: #003366; /* 진한 파랑 계열 글자색 */
      text-align: center; /* 전체 가운데 정렬 */
    }
    .container {
      max-width: 600px;
      margin: 0 auto;
      padding: 40px 20px;
    }
    h1 {
      font-size: 2em;
      margin-bottom: 0.5em;
    }
    .description {
      font-size: 1.1em;
      margin-bottom: 30px;
    }
    .search-box {
      margin-bottom: 20px;
    }
    .search-box input {
      width: 60%;
      padding: 10px;
      font-size: 1em;
      border: 2px solid #1E90FF;
      border-radius: 4px;
      margin-right: 5px;
    }
    .search-box button {
      background-color: #1E90FF;
      color: #fff;
      padding: 11px 20px;
      border: none;
      border-radius: 4px;
      font-size: 1em;
      cursor: pointer;
    }
    .search-box button:hover {
      background-color: #005DB3;
    }
    .letter {
      margin-top: 30px;
      font-size: 1.2em;
      line-height: 1.6em;
      white-space: pre-wrap;
    }
    .highlight {
      font-weight: bold;
      color: #0066cc;
    }
    .link a {
      color: #1E90FF;
      text-decoration: none;
      font-weight: bold;
    }
    .link a:hover {
      text-decoration: underline;
    }

    /* 관리자 모드 섹션 */
    .admin-button {
      background-color: #1E90FF;
      color: #fff;
      padding: 8px 16px;
      border: none;
      border-radius: 4px;
      font-size: 1em;
      cursor: pointer;
    }
    .admin-button:hover {
      background-color: #005DB3;
    }

    /* 비밀번호 입력 모달/영역 스타일 */
    .admin-login {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.5);
      justify-content: center;
      align-items: center;
    }
    .admin-login-content {
      background: #fff;
      padding: 20px;
      border-radius: 8px;
      text-align: center;
      max-width: 300px;
      margin: 0 auto;
    }
    .admin-login-content h2 {
      margin-bottom: 1em;
      font-size: 1.2em;
      color: #333;
    }
    .admin-login-content input {
      width: 80%;
      padding: 8px;
      margin-bottom: 10px;
      font-size: 1em;
    }

    .admin-section {
      margin-top: 40px;
      border-top: 2px solid #1E90FF;
      padding-top: 20px;
      display: none; /* 처음에는 숨김 */
      text-align: left;
    }
    .admin-section h2 {
      font-size: 1.5em;
      margin-bottom: 1em;
      text-align: center;
    }
    .admin-section label {
      font-weight: bold;
    }
    .paste-area {
      width: 100%;
      height: 120px;
      margin-bottom: 10px;
      font-size: 0.9em;
    }
    .btn-group {
      margin-bottom: 20px;
      text-align: center;
    }
    .preview-table {
      border-collapse: collapse;
      width: 100%;
    }
    .preview-table th,
    .preview-table td {
      border: 1px solid #ccc;
      padding: 4px 8px;
      font-size: 0.9em;
    }
  </style>
</head>
<body>
  <div class="container">
    <!-- 타이틀 -->
    <h1>NTB 19기 챌린지 학습초대코드 확인</h1>
    <!-- 설명 -->
    <div class="description">
      학습 초대코드는 28일부터 검색이 가능합니다.^^<br/>
      학습은 매월 1일 진행됩니다.(시작일이 다른 경우 별도공지)
    </div>

    <!-- 검색 영역 -->
    <div class="search-box">
      <input type="text" id="phoneInput" placeholder="000-0000-0000 형식으로 입력" />
      <button onclick="searchCode()">검색</button>
    </div>

    <!-- 결과 표시 영역 -->
    <div id="resultArea"></div>

    <!-- 관리자 모드 진입 버튼 -->
    <div style="margin-top: 40px;">
      <button class="admin-button" onclick="openAdminLogin()">관리자 모드</button>
    </div>

    <!-- 관리자 모드 섹션 (초기에 숨김) -->
    <div class="admin-section" id="adminSection">
      <h2>엑셀 형식 데이터 입력/수정</h2>
      <p style="text-align:center;">
        <strong>엑셀에서 원하는 셀 범위를 복사(Ctrl+C) 후,<br/>
        아래 영역에 붙여넣기(Ctrl+V) 하세요.</strong>
      </p>

      <!-- 붙여넣기 영역 -->
      <textarea class="paste-area" id="pasteArea" placeholder="엑셀 데이터를 붙여넣으세요"></textarea>

      <!-- 버튼들 -->
      <div class="btn-group">
        <button class="admin-button" onclick="parsePastedData()">미리 보기</button>
        <button class="admin-button" onclick="saveSheetData()">저장</button>
      </div>

      <!-- 미리보기 테이블 -->
      <table class="preview-table" id="previewTable"></table>
    </div>
  </div>

  <!-- 관리자 비밀번호 입력 모달/영역 -->
  <div class="admin-login" id="adminLogin">
    <div class="admin-login-content">
      <h2>관리자 모드 비밀번호</h2>
      <input type="password" id="adminPasswordInput" placeholder="비밀번호 입력" />
      <br/>
      <button class="admin-button" onclick="checkAdminPassword()">확인</button>
      <button class="admin-button" onclick="closeAdminLogin()">취소</button>
    </div>
  </div>

  <script>
    // 관리자 비밀번호
    const ADMIN_PASSWORD = "@ntb307030405";

    // 검색 기능
    async function searchCode() {
      const phone = document.getElementById('phoneInput').value.trim();
      const resultArea = document.getElementById('resultArea');
      resultArea.innerHTML = ''; // 기존 내용 초기화

      if (!phone) {
        alert('전화번호를 입력하세요!');
        return;
      }

      try {
        // /search?phone=... API 요청 (서버 구현 필요)
        const response = await fetch(`/search?phone=${encodeURIComponent(phone)}`);
        const data = await response.json();

        if (data.success && data.code) {
          // 엑셀에서 찾은 초대코드
          const inviteCode = data.code;

          // 편지 형식으로 출력
          resultArea.innerHTML = `
            <div class="letter">
              안녕하세요!<br/>
              고객님 전화번호 <span class="highlight">${phone}</span> 로 조회한 결과<br/>
              <span class="highlight">클래스카드 초대코드</span>는<br/><br/>
              <span class="highlight">${inviteCode}</span><br/><br/>
              입니다. ^^<br/>
              <br/>
              챌린지 참여 감사드리며, 즐거운 학습 되세요!
            </div>
          `;
        } else {
          // 검색 결과가 없을 때
          resultArea.innerHTML = `
            <div class="letter">
              반갑습니다.^^ 엔티비챌린지 구매해주셔서 감사합니다.<br/>
              매월 1일 챌린지가 시작됩니다.<br/>
              구매 후 1~2일 이내로 학습초대코드를 확인하실 수 있습니다.<br/>
              1~2일 이내 초대 코드를 확인할 수 없거나 오류가 있다면<br/>
              엔티비카카오채널 고객센터로 연락주세요.<br/><br/>
              <span class="link">
                <a href="https://center-pf.kakao.com/_GltxfG" target="_blank">
                  카카오 채널 바로가기
                </a>
              </span>
            </div>
          `;
        }
      } catch (err) {
        console.error(err);
        alert('검색 중 오류가 발생했습니다.');
      }
    }

    // 관리자 모드 로그인 창 열기
    function openAdminLogin() {
      document.getElementById('adminLogin').style.display = 'flex';
    }

    // 관리자 모드 로그인 창 닫기
    function closeAdminLogin() {
      document.getElementById('adminLogin').style.display = 'none';
    }

    // 비밀번호 확인
    function checkAdminPassword() {
      const inputPass = document.getElementById('adminPasswordInput').value;
      if (inputPass === ADMIN_PASSWORD) {
        // 비밀번호가 맞으면 모달 닫고 adminSection 보이기
        closeAdminLogin();
        document.getElementById('adminSection').style.display = 'block';
      } else {
        alert("비밀번호가 올바르지 않습니다.");
      }
    }

    // 붙여넣은 데이터를 행/열로 파싱 후 테이블에 표시
    function parsePastedData() {
      const pasteArea = document.getElementById('pasteArea');
      const previewTable = document.getElementById('previewTable');

      // 붙여넣은 문자열
      const rawText = pasteArea.value.trim();
      if (!rawText) {
        alert("붙여넣은 데이터가 없습니다.");
        previewTable.innerHTML = "";
        return;
      }

      // 행 단위로 나누기 (줄바꿈 기준)
      const rows = rawText.split(/\r?\n/);

      // 각 행을 탭(\t)으로 나누어 2차원 배열 형태 구성
      const dataMatrix = rows.map(row => {
        return row.split(/\t/);
      });

      // 테이블 표시
      let html = "";
      dataMatrix.forEach((cols) => {
        html += "<tr>";
        cols.forEach(cell => {
          html += `<td>${cell}</td>`;
        });
        html += "</tr>";
      });
      previewTable.innerHTML = html;
    }

    // 테이블 데이터를 서버로 전송하여 저장 (POST /saveSheet)
    async function saveSheetData() {
      const pasteArea = document.getElementById('pasteArea');
      const rawText = pasteArea.value.trim();
      if (!rawText) {
        alert("붙여넣은 데이터가 없습니다.");
        return;
      }

      // 행 단위로 나누기
      const rows = rawText.split(/\r?\n/);
      // 2차원 배열
      const dataMatrix = rows.map(row => row.split(/\t/));

      try {
        const response = await fetch('/saveSheet', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({ data: dataMatrix })
        });
        if (response.ok) {
          alert("데이터가 성공적으로 저장되었습니다.");
        } else {
          alert("서버에서 오류가 발생했습니다.");
        }
      } catch (error) {
        console.error(error);
        alert("업로드 중 오류가 발생했습니다.");
      }
    }
  </script>
</body>
</html>


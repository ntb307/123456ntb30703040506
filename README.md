<!DOCTYPE html>
<html lang="ko">
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
  <link type="text/css" rel="stylesheet" href="resources/sheet.css" >
  <style type="text/css">
    .ritz .waffle a { color: inherit; }
    .ritz .waffle .s0{
      background-color:#ffffff;text-align:left;color:#000000;font-family:Arial;font-size:10pt;vertical-align:bottom;white-space:nowrap;direction:ltr;padding:2px 3px 2px 3px;
    }
    .ritz .waffle .s2{
      background-color:#ffffff;text-align:center;color:#000000;font-family:Arial;font-size:12pt;vertical-align:bottom;white-space:nowrap;direction:ltr;padding:2px 3px 2px 3px;
    }
    .ritz .waffle .s1{
      background-color:#ffffff;text-align:left;color:#000000;font-family:Arial;font-size:12pt;vertical-align:bottom;white-space:nowrap;direction:ltr;padding:2px 3px 2px 3px;
    }

    body {
      margin: 0;
      padding: 0;
      background-color: #f0f8ff; /* 옅은 파란 배경 */
      font-family: 'Malgun Gothic', sans-serif;
      color: #003366; /* 진한 파랑 계열 글자색 */
      text-align: center; /* 전체 가운데 정렬 */
      position: relative;
    }
    .container {
      max-width: 800px;
      margin: 0 auto;
      padding: 40px 20px;
      position: relative;
    }
    h1 {
      font-size: 2rem;
      margin-bottom: 0.5em;
    }
    .description {
      font-size: 1.1rem;
      margin-bottom: 30px;
      white-space: pre-wrap;
      line-height: 1.4rem;
    }
    .search-box {
      margin-bottom: 20px;
    }
    .search-box input {
      width: 60%;
      padding: 10px;
      font-size: 1rem;
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
      font-size: 1rem;
      cursor: pointer;
    }
    .search-box button:hover {
      background-color: #005DB3;
    }
    .letter {
      margin-top: 30px;
      font-size: 1.2rem;
      line-height: 1.6rem;
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

    /* 관리자 모드 아이콘 (top-right corner) */
    .admin-icon {
      position: absolute;
      top: 10px;
      right: 10px;
      cursor: pointer;
      width: 36px;
      height: 36px;
      border-radius: 50%;
      background-color: #1E90FF;
      color: #fff;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: bold;
      font-size: 1.2rem;
    }
    .admin-icon:hover {
      background-color: #005DB3;
    }

    /* 비밀번호 입력 모달 */
    .admin-login {
      display: none;
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: rgba(0, 0, 0, 0.5);
      justify-content: center; align-items: center;
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

    /* 메인 검색 화면 */
    #searchSection {
      display: block;
    }

    /* 관리자 모드 화면 */
    #adminSection {
      display: none;
      margin-top: 40px;
    }
  </style>

  <title>NTB 19기 챌린지 학습초대코드 확인</title>
</head>
<body>
  <!-- 관리자 모드 아이콘 (우측 상단) -->
  <div class="admin-icon" onclick="openAdminLogin()">A</div>

  <!-- 관리자 비밀번호 입력 모달 (비밀번호 마스킹) -->
  <div class="admin-login" id="adminLogin">
    <div class="admin-login-content">
      <h2>관리자 모드 비밀번호</h2>
      <input type="password" id="adminPasswordInput" placeholder="비밀번호 입력" />
      <br/>
      <button onclick="checkAdminPassword()">확인</button>
      <button onclick="closeAdminLogin()">취소</button>
    </div>
  </div>

  <div class="container">
    <!-- 검색 섹션 -->
    <div id="searchSection">
      <h1>NTB 19기(4월) 챌린지 학습초대코드 확인</h1>
      <div class="description">
        학습 초대코드는 28일부터 검색이 가능합니다.^^<br/>
        학습은 매월 1일 진행됩니다.(시작일이 다른 경우 별도공지)
      </div>

      <div class="search-box">
        <input type="text" id="phoneInput" placeholder="000-0000-0000 형식으로 입력" />
        <button onclick="searchCode()">검색</button>
      </div>

      <div id="resultArea"></div>
    </div>

    <!-- 관리자 모드: 구글 시트 HTML 코드 + 돌아가기 아이콘 -->
    <div id="adminSection">
      <h1>관리자 모드</h1>
      <p>뒤로가기/새로고침 시 비밀번호를 다시 입력해야 합니다.</p>
      <button
        style="background-color:#1E90FF; color:#fff; padding:8px 14px; border:none; border-radius:4px; cursor:pointer; font-size:1rem;"
        onclick="goSearchMode()"
      >
        학습코드 확인창으로
      </button>

      <!-- 구글 시트 HTML 코드 (A=과목, B=결제자, C=연락처, D=안내 내용) -->
      <div class="ritz grid-container" dir="ltr" id="myWaffle">
        <table class="waffle" cellspacing="0" cellpadding="0">
          <thead>
            <tr>
              <th class="row-header freezebar-origin-ltr"></th>
              <th id="0C0" style="width:217px;" class="column-headers-background">A</th>
              <th id="0C1" style="width:120px;" class="column-headers-background">B</th>
              <th id="0C2" style="width:167px;" class="column-headers-background">C</th>
              <th id="0C3" style="width:100px;" class="column-headers-background">D</th>
            </tr>
          </thead>
          <tbody>
            <tr style="height: 20px">
              <th id="0R0" style="height: 20px;" class="row-headers-background">
                <div class="row-header-wrapper" style="line-height: 20px">1</div>
              </th>
              <td class="s0" dir="ltr">과목</td>
              <td class="s0" dir="ltr">결제자</td>
              <td class="s0" dir="ltr">연락처</td>
              <td class="s0" dir="ltr">안내 내용</td>
            </tr>
            <tr style="height: 20px">
              <th id="0R1" style="height: 20px;" class="row-headers-background">
                <div class="row-header-wrapper" style="line-height: 20px">2</div>
              </th>
              <td class="s1">바베쌤-중등영단어순한맛</td>
              <td class="s2">체링</td>
              <td class="s2">010-2741-8264</td>
              <td class="s0" dir="ltr">안내1-<br>챌린지안내<br>
                <span style="text-decoration:underline;text-decoration-skip-ink:none;-webkit-text-decoration-skip:none;color:#1155cc;">
                  <a target="_blank" href="http://ntb307.co/">ntb307.co</a>
                </span>.kr/90<br>초대코드 1234<br><br>
              </td>
            </tr>
            <tr style="height: 20px">
              <th id="0R2" style="height: 20px;" class="row-headers-background">
                <div class="row-header-wrapper" style="line-height: 20px">3</div>
              </th>
              <td class="s1">바베쌤-초등영단어400</td>
              <td class="s2">사유</td>
              <td class="s2">010-9361-0977</td>
              <td class="s0" dir="ltr">
                안내2-<br>챌린지안내<br>ntb307.co.kr/90<br>초대코드 1234<br><br>
              </td>
            </tr>
            <tr style="height: 20px">
              <th id="0R3" style="height: 20px;" class="row-headers-background">
                <div class="row-header-wrapper" style="line-height: 20px">4</div>
              </th>
              <td class="s1">바베쌤-초등영단어매운맛</td>
              <td class="s2">박진희</td>
              <td class="s2">010-2619-9241</td>
              <td class="s0" dir="ltr">
                안내3<br>챌린지안내<br>ntb307.co.kr/90<br>초대코드 1234<br><br>
              </td>
            </tr>
            <tr style="height: 20px">
              <th id="0R4" style="height: 20px;" class="row-headers-background">
                <div class="row-header-wrapper" style="line-height: 20px">5</div>
              </th>
              <td class="s1">젬쌤-미드영쉘든</td>
              <td class="s2">김하나</td>
              <td class="s2">010-5156-9599</td>
              <td class="s0" dir="ltr">
                안내4<br>챌린지안내<br>ntb307.co.kr/90<br>초대코드 1234<br><br>
              </td>
            </tr>
            <tr style="height: 20px">
              <th id="0R5" style="height: 20px;" class="row-headers-background">
                <div class="row-header-wrapper" style="line-height: 20px">6</div>
              </th>
              <td class="s1">젬쌤-여행영어</td>
              <td class="s2">김슬기</td>
              <td class="s2">010-3726-1486</td>
              <td class="s0" dir="ltr">
                안내5<br>챌린지안내<br>ntb307.co.kr/90<br>초대코드 1234<br><br>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>

  <script>
    // 관리자 비밀번호
    const ADMIN_PASSWORD = '@ntb307030405';

    // phone->info (연락처->안내내용) 매핑을 저장할 배열
    // We'll parse from the Google sheet snippet on page load
    let tableData = [];

    window.addEventListener('DOMContentLoaded', () => {
      parseSheetData();
      // 엔터키 검색 지원
      const phoneInput = document.getElementById('phoneInput');
      phoneInput.addEventListener('keyup', (e) => {
        if (e.key === 'Enter') {
          searchCode();
        }
      });
    });

    function parseSheetData() {
      // #myWaffle table => row[0] is header row
      // phone is col C => index=2, info is col D => index=3
      const waffle = document.getElementById('myWaffle');
      if (!waffle) return;

      const rows = waffle.querySelectorAll('tbody tr');
      // skip the header row (index=0) because it says "과목, 결제자, 연락처, 안내 내용"
      tableData = [];
      for (let i = 1; i < rows.length; i++) {
        const cells = rows[i].querySelectorAll('td');
        // col2 => phone, col3 => info
        const phone = cells[2]?.innerText.trim() || '';
        const info  = cells[3]?.innerHTML.trim() || '';
        tableData.push({ phone, info });
      }
    }

    // 관리자 모드 아이콘
    function openAdminLogin() {
      document.getElementById('adminLogin').style.display = 'flex';
    }
    function closeAdminLogin() {
      document.getElementById('adminLogin').style.display = 'none';
    }

    // 비밀번호 확인
    function checkAdminPassword() {
      const inputPass = document.getElementById('adminPasswordInput').value.trim();
      if (inputPass === ADMIN_PASSWORD) {
        closeAdminLogin();
        document.getElementById('searchSection').style.display = 'none';
        document.getElementById('adminSection').style.display = 'block';
      } else {
        alert('비밀번호가 올바르지 않습니다.');
      }
    }

    // 관리자 모드에서 '학습코드 확인창으로' 버튼
    function goSearchMode() {
      document.getElementById('adminSection').style.display = 'none';
      document.getElementById('searchSection').style.display = 'block';
    }

    // 전화번호 검색
    // user enters phone => find matching row in tableData
    // show D열 content as message
    function searchCode() {
      const phoneInput = document.getElementById('phoneInput').value.trim();
      const resultArea = document.getElementById('resultArea');
      resultArea.innerHTML = '';

      if (!phoneInput) {
        alert('전화번호를 입력하세요!');
        return;
      }

      // find phone in tableData
      let foundInfo = '';
      for (const row of tableData) {
        if (row.phone === phoneInput) {
          foundInfo = row.info;
          break;
        }
      }

      if (foundInfo) {
        resultArea.innerHTML = `
          <div class="letter">
            안녕하세요!<br/>
            고객님 전화번호 <span class="highlight">${phoneInput}</span> 로 조회한 결과<br/>
            <span class="highlight">안내 내용</span>은<br/><br/>
            <span class="highlight">${foundInfo}</span><br/><br/>
            입니다. ^^<br/><br/>
            챌린지 참여 감사드리며, 즐거운 학습 되세요!
          </div>
        `;
      } else {
        // not found => default message
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
    }
  </script>
</body>
</html>

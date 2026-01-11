<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>게임 대미지 계산기</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      max-width: 900px;
      margin: 30px auto;
      padding: 0 20px;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      min-height: 100vh;
      overflow-x: hidden;
    }
    .container {
      background: white;
      border-radius: 15px;
      padding: 25px;
      box-shadow: 0 20px 60px rgba(0,0,0,0.3);
      overflow: hidden;
    }
    h1, h2, h3 {
      color: #333;
      text-align: center;
      margin-top: 0;
    }
    h1 {
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      font-size: 26px;
      margin-bottom: 15px;
      padding: 0 10px;
    }
    
    .alert-section {
      background: #fff9e6;
      border-left: 4px solid #ff9800;
      padding: 15px;
      margin: 15px 0 25px 0;
      border-radius: 8px;
      font-size: 14px;
      line-height: 1.5;
    }
    .alert-section strong {
      color: #e65100;
    }
    .alert-section ul {
      margin: 8px 0;
      padding-left: 20px;
    }
    .alert-section li {
      margin-bottom: 5px;
    }
    
    .sections-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 20px;
      margin: 25px 0;
    }
    .section {
      background: white;
      border: 2px solid #ddd;
      border-radius: 10px;
      padding: 18px;
      transition: all 0.3s;
      box-sizing: border-box;
    }
    .section:hover {
      border-color: #667eea;
      transform: translateY(-5px);
      box-shadow: 0 10px 20px rgba(102, 126, 234, 0.1);
    }
    .section h3 {
      text-align: left;
      margin-bottom: 15px;
      padding-bottom: 10px;
      border-bottom: 2px solid;
      font-size: 17px;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }
    .section-1 h3 { color: #667eea; border-color: #667eea; }
    .section-2 h3 { color: #4CAF50; border-color: #4CAF50; }
    .section-3 h3 { color: #FF9800; border-color: #FF9800; }
    .input-group {
      margin-bottom: 12px;
    }
    label {
      display: inline-block;
      width: 70px;
      font-weight: 500;
      color: #555;
      font-size: 14px;
    }
    .input-row {
      display: flex;
      gap: 8px;
      align-items: center;
      margin-top: 5px;
    }
    .value-input {
      flex: 1;
      padding: 8px 10px;
      border: 2px solid #ddd;
      border-radius: 6px;
      font-size: 13px;
      transition: border 0.3s;
      min-width: 0;
      box-sizing: border-box;
    }
    .value-input:focus {
      outline: none;
      border-color: #667eea;
    }
    .add-btn {
      padding: 8px 12px;
      background: #4CAF50;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      font-weight: bold;
      transition: all 0.3s;
      font-size: 13px;
      white-space: nowrap;
    }
    .add-btn:hover {
      background: #45a049;
      transform: scale(1.05);
    }
    .add-btn-special {
      background: #667eea;
    }
    .add-btn-special:hover {
      background: #5a67d8;
    }
    .negative-btn {
      background: #f44336;
      padding: 8px 10px;
    }
    .negative-btn:hover {
      background: #d32f2f;
    }
    .added-value {
      min-width: 60px;
      font-weight: bold;
      font-size: 12px;
      padding: 5px 8px;
      border-radius: 20px;
      text-align: center;
      white-space: nowrap;
    }
    .section-1 .added-value { background: #e8f0fe; color: #667eea; }
    .section-2 .added-value { background: #e8f5e8; color: #4CAF50; }
    .section-3 .added-value { background: #fff3e0; color: #FF9800; }
    
    .calculate-section {
      text-align: center;
      margin: 30px 0;
    }
    .calculate-btn {
      padding: 14px 25px;
      font-size: 16px;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      color: white;
      border: none;
      border-radius: 30px;
      cursor: pointer;
      font-weight: bold;
      transition: all 0.3s;
      min-width: 180px;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
    }
    .calculate-btn:hover {
      transform: translateY(-3px);
      box-shadow: 0 10px 20px rgba(102, 126, 234, 0.3);
    }
    .result {
      background: #f8f9fa;
      border-radius: 10px;
      padding: 20px;
      margin-top: 20px;
      border: 2px solid #e9ecef;
    }
    .final-stats {
      background: white;
      border-radius: 8px;
      padding: 18px;
      margin: 20px 0;
      border: 2px solid #e3f2fd;
    }
    .final-stats h4 {
      color: #667eea;
      margin-top: 0;
      display: flex;
      align-items: center;
      gap: 10px;
      font-size: 16px;
    }
    .stats-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
      gap: 10px;
      margin-top: 15px;
    }
    .stat-item {
      padding: 10px;
      background: #f5f7ff;
      border-radius: 6px;
      text-align: center;
    }
    .stat-label {
      font-size: 12px;
      color: #666;
      margin-bottom: 5px;
    }
    .stat-value {
      font-size: 15px;
      font-weight: bold;
      color: #333;
    }
    .damage-result {
      text-align: center;
      padding: 20px;
      background: white;
      border-radius: 10px;
      border: 3px solid;
      border-image: linear-gradient(135deg, #667eea 0%, #764ba2 100%) 1;
    }
    .damage-item {
      margin: 15px 0;
      padding: 15px;
      background: #f8f9fa;
      border-radius: 8px;
      border-left: 4px solid;
    }
    .damage-main { border-left-color: #667eea; }
    .damage-plus5 { border-left-color: #4CAF50; }
    .damage-minus5 { border-left-color: #f44336; }
    .damage-label {
      font-size: 14px;
      color: #666;
      margin-bottom: 5px;
    }
    .damage-value {
      font-size: 22px;
      font-weight: bold;
      color: #333;
    }
    @media (max-width: 768px) {
      .sections-grid {
        grid-template-columns: 1fr;
      }
      .container {
        padding: 15px;
      }
      h1 {
        font-size: 22px;
      }
      .calculate-btn {
        min-width: 140px;
        padding: 12px 20px;
        font-size: 14px;
      }
    }
    
    .reset-btn {
      padding: 8px 10px;
      background: #9e9e9e;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      font-weight: bold;
      transition: all 0.3s;
      margin-left: 5px;
      font-size: 12px;
    }
    .reset-btn:hover {
      background: #757575;
    }
    
    .formula-section {
      background: #f5f7ff;
      padding: 12px;
      border-radius: 8px;
      margin: 15px 0;
      font-size: 13px;
      text-align: center;
    }
    
    /* 모바일 최적화 */
    @media (max-width: 480px) {
      .input-row {
        flex-wrap: wrap;
      }
      .value-input {
        min-width: 100%;
        order: 0;
      }
      .add-btn, .negative-btn, .reset-btn {
        order: 1;
        flex: 1;
        padding: 8px;
      }
      .added-value {
        order: 2;
        min-width: 100%;
        margin-top: 5px;
      }
      body {
        padding: 0 10px;
        margin: 15px auto;
      }
    }
  </style>
  <!-- Font Awesome -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
</head>
<body>

<div class="container">
  <h1><i class="fas fa-calculator"></i> 게임 대미지 계산기</h1>
  
  <!-- 추가 확인 요소 안내 메시지 -->
  <div class="alert-section">
    <strong><i class="fas fa-exclamation-triangle"></i> 계산 전 확인 사항:</strong>
    <p>다음 요소들이 계산에 포함되었는지 확인해 주세요:</p>
    <ul>
      <li>보스에 적용된 디버프 (방어율 감소, 방어력 감소 등)</li>
      <li>V매트릭스 (코어 강화, 스킬 효과 등)</li>
      <li>헥사 스킬 (추가효가, 종댐 등)</li>
      <li>시아링크 </li>
      <li>보슬 방뿌 등 특코</li>
      <li>기타 등등</li>
    </ul>
    <p>위 요소들이 잘 기입되었는지 확인하세요</p>
  </div>
  
  <div class="formula-section">
    <strong>계산식:</strong> 깡공 × (물공% + 스댐% × (1 + 보공%)) × (1 + 물댐%) × (1.2 + 치피%) × (1 + 종댐%)  +-5%(최대 최소댐)
  </div>

  <div class="sections-grid">
    <!-- 기본스텟 섹션 -->
    <div class="section section-1">
      <h3><i class="fas fa-user"></i> 기본스텟</h3>
      <div class="input-group">
        <label>깡공</label>
        <div class="input-row">
          <input id="a-base" type="number" step="any" value="0" class="value-input">
          <button class="add-btn add-btn-special" onclick="addValue('a', 100, 'base')">+100</button>
          <button class="add-btn negative-btn" onclick="addValue('a', -100, 'base')">-100</button>
          <span class="added-value" id="a-base-added">+0</span>
        </div>
      </div>
      <div class="input-group">
        <label>물공%</label>
        <div class="input-row">
          <input id="b-base" type="number" step="any" value="100" class="value-input">
          <button class="add-btn" onclick="addValue('b', 5, 'base')">+5</button>
          <button class="add-btn negative-btn" onclick="addValue('b', -5, 'base')">-5</button>
          <button class="reset-btn" onclick="resetValue('b', 'base')">초기화</button>
          <span class="added-value" id="b-base-added">+0</span>
        </div>
      </div>
      <div class="input-group">
        <label>스댐%</label>
        <div class="input-row">
          <input id="c-base" type="number" step="any" value="0" class="value-input">
          <button class="add-btn" onclick="addValue('c', 5, 'base')">+5</button>
          <button class="add-btn negative-btn" onclick="addValue('c', -5, 'base')">-5</button>
          <button class="reset-btn" onclick="resetValue('c', 'base')">초기화</button>
          <span class="added-value" id="c-base-added">+0</span>
        </div>
      </div>
      <div class="input-group">
        <label>보공%</label>
        <div class="input-row">
          <input id="d-base" type="number" step="any" value="0" class="value-input">
          <button class="add-btn" onclick="addValue('d', 5, 'base')">+5</button>
          <button class="add-btn negative-btn" onclick="addValue('d', -5, 'base')">-5</button>
          <button class="reset-btn" onclick="resetValue('d', 'base')">초기화</button>
          <span class="added-value" id="d-base-added">+0</span>
        </div>
      </div>
      <div class="input-group">
        <label>물댐%</label>
        <div class="input-row">
          <input id="e-base" type="number" step="any" value="0" class="value-input">
          <button class="add-btn" onclick="addValue('e', 5, 'base')">+5</button>
          <button class="add-btn negative-btn" onclick="addValue('e', -5, 'base')">-5</button>
          <button class="reset-btn" onclick="resetValue('e', 'base')">초기화</button>
          <span class="added-value" id="e-base-added">+0</span>
        </div>
      </div>
      <div class="input-group">
        <label>치피%</label>
        <div class="input-row">
          <input id="f-base" type="number" step="any" value="0" class="value-input">
          <button class="add-btn" onclick="addValue('f', 5, 'base')">+5</button>
          <button class="add-btn negative-btn" onclick="addValue('f', -5, 'base')">-5</button>
          <button class="reset-btn" onclick="resetValue('f', 'base')">초기화</button>
          <span class="added-value" id="f-base-added">+0</span>
        </div>
      </div>
      <div class="input-group">
        <label>종댐%</label>
        <div class="input-row">
          <input id="g-base" type="number" step="any" value="0" class="value-input">
          <button class="add-btn" onclick="addValue('g', 5, 'base')">+5</button>
          <button class="add-btn negative-btn" onclick="addValue('g', -5, 'base')">-5</button>
          <button class="reset-btn" onclick="resetValue('g', 'base')">초기화</button>
          <span class="added-value" id="g-base-added">+0</span>
        </div>
      </div>
    </div>

    <!-- 도핑 섹션 -->
    <div class="section section-2">
      <h3><i class="fas fa-flask"></i> 도핑</h3>
      <div class="input-group">
        <label>깡공</label>
        <div class="input-row">
          <input id="a-doping" type="number" step="any" value="0" class="value-input">
          <button class="add-btn add-btn-special" onclick="addValue('a', 100, 'doping')">+100</button>
          <button class="add-btn negative-btn" onclick="addValue('a', -100, 'doping')">-100</button>
          <span class="added-value" id="a-doping-added">+0</span>
        </div>
      </div>
      <div class="input-group">
        <label>물공%</label>
        <div class="input-row">
          <input id="b-doping" type="number" step="any" value="0" class="value-input">
          <button class="add-btn" onclick="addValue('b', 5, 'doping')">+5</button>
          <button class="add-btn negative-btn" onclick="addValue('b', -5, 'doping')">-5</button>
          <button class="reset-btn" onclick="resetValue('b', 'doping')">초기화</button>
          <span class="added-value" id="b-doping-added">+0</span>
        </div>
      </div>
      <div class="input-group">
        <label>스댐%</label>
        <div class="input-row">
          <input id="c-doping" type="number" step="any" value="0" class="value-input">
          <button class="add-btn" onclick="addValue('c', 5, 'doping')">+5</button>
          <button class="add-btn negative-btn" onclick="addValue('c', -5, 'doping')">-5</button>
          <button class="reset-btn" onclick="resetValue('c', 'doping')">초기화</button>
          <span class="added-value" id="c-doping-added">+0</span>
        </div>
      </div>
      <div class="input-group">
        <label>보공%</label>
        <div class="input-row">
          <input id="d-doping" type="number" step="any" value="0" class="value-input">
          <button class="add-btn" onclick="addValue('d', 5, 'doping')">+5</button>
          <button class="add-btn negative-btn" onclick="addValue('d', -5, 'doping')">-5</button>
          <button class="reset-btn" onclick="resetValue('d', 'doping')">초기화</button>
          <span class="added-value" id="d-doping-added">+0</span>
        </div>
      </div>
      <div class="input-group">
        <label>물댐%</label>
        <div class="input-row">
          <input id="e-doping" type="number" step="any" value="0" class="value-input">
          <button class="add-btn" onclick="addValue('e', 5, 'doping')">+5</button>
          <button class="add-btn negative-btn" onclick="addValue('e', -5, 'doping')">-5</button>
          <button class="reset-btn" onclick="resetValue('e', 'doping')">초기화</button>
          <span class="added-value" id="e-doping-added">+0</span>
        </div>
      </div>
      <div class="input-group">
        <label>치피%</label>
        <div class="input-row">
          <input id="f-doping" type="number" step="any" value="0" class="value-input">
          <button class="add-btn" onclick="addValue('f', 5, 'doping')">+5</button>
          <button class="add-btn negative-btn" onclick="addValue('f', -5, 'doping')">-5</button>
          <button class="reset-btn" onclick="resetValue('f', 'doping')">초기화</button>
          <span class="added-value" id="f-doping-added">+0</span>
        </div>
      </div>
      <div class="input-group">
        <label>종댐%</label>
        <div class="input-row">
          <input id="g-doping" type="number" step="any" value="0" class="value-input">
          <button class="add-btn" onclick="addValue('g', 5, 'doping')">+5</button>
          <button class="add-btn negative-btn" onclick="addValue('g', -5, 'doping')">-5</button>
          <button class="reset-btn" onclick="resetValue('g', 'doping')">초기화</button>
          <span class="added-value" id="g-doping-added">+0</span>
        </div>
      </div>
    </div>

    <!-- 버프 섹션 -->
    <div class="section section-3">
      <h3><i class="fas fa-fire"></i> 버프</h3>
      <div class="input-group">
        <label>깡공</label>
        <div class="input-row">
          <input id="a-buff" type="number" step="any" value="0" class="value-input">
          <button class="add-btn add-btn-special" onclick="addValue('a', 100, 'buff')">+100</button>
          <button class="add-btn negative-btn" onclick="addValue('a', -100, 'buff')">-100</button>
          <span class="added-value" id="a-buff-added">+0</span>
        </div>
      </div>
      <div class="input-group">
        <label>물공%</label>
        <div class="input-row">
          <input id="b-buff" type="number" step="any" value="0" class="value-input">
          <button class="add-btn" onclick="addValue('b', 5, 'buff')">+5</button>
          <button class="add-btn negative-btn" onclick="addValue('b', -5, 'buff')">-5</button>
          <button class="reset-btn" onclick="resetValue('b', 'buff')">초기화</button>
          <span class="added-value" id="b-buff-added">+0</span>
        </div>
      </div>
      <div class="input-group">
        <label>스댐%</label>
        <div class="input-row">
          <input id="c-buff" type="number" step="any" value="0" class="value-input">
          <button class="add-btn" onclick="addValue('c', 5, 'buff')">+5</button>
          <button class="add-btn negative-btn" onclick="addValue('c', -5, 'buff')">-5</button>
          <button class="reset-btn" onclick="resetValue('c', 'buff')">초기화</button>
          <span class="added-value" id="c-buff-added">+0</span>
        </div>
      </div>
      <div class="input-group">
        <label>보공%</label>
        <div class="input-row">
          <input id="d-buff" type="number" step="any" value="0" class="value-input">
          <button class="add-btn" onclick="addValue('d', 5, 'buff')">+5</button>
          <button class="add-btn negative-btn" onclick="addValue('d', -5, 'buff')">-5</button>
          <button class="reset-btn" onclick="resetValue('d', 'buff')">초기화</button>
          <span class="added-value" id="d-buff-added">+0</span>
        </div>
      </div>
      <div class="input-group">
        <label>물댐%</label>
        <div class="input-row">
          <input id="e-buff" type="number" step="any" value="0" class="value-input">
          <button class="add-btn" onclick="addValue('e', 5, 'buff')">+5</button>
          <button class="add-btn negative-btn" onclick="addValue('e', -5, 'buff')">-5</button>
          <button class="reset-btn" onclick="resetValue('e', 'buff')">초기화</button>
          <span class="added-value" id="e-buff-added">+0</span>
        </div>
      </div>
      <div class="input-group">
        <label>치피%</label>
        <div class="input-row">
          <input id="f-buff" type="number" step="any" value="0" class="value-input">
          <button class="add-btn" onclick="addValue('f', 5, 'buff')">+5</button>
          <button class="add-btn negative-btn" onclick="addValue('f', -5, 'buff')">-5</button>
          <button class="reset-btn" onclick="resetValue('f', 'buff')">초기화</button>
          <span class="added-value" id="f-buff-added">+0</span>
        </div>
      </div>
      <div class="input-group">
        <label>종댐%</label>
        <div class="input-row">
          <input id="g-buff" type="number" step="any" value="0" class="value-input">
          <button class="add-btn" onclick="addValue('g', 5, 'buff')">+5</button>
          <button class="add-btn negative-btn" onclick="addValue('g', -5, 'buff')">-5</button>
          <button class="reset-btn" onclick="resetValue('g', 'buff')">초기화</button>
          <span class="added-value" id="g-buff-added">+0</span>
        </div>
      </div>
    </div>
  </div>

  <div class="calculate-section">
    <button class="calculate-btn" onclick="calculate()">
      <i class="fas fa-bolt"></i> 대미지 계산하기
    </button>
    <button class="calculate-btn" onclick="clearAll()" style="background: #f44336; margin-left: 10px;">
      <i class="fas fa-trash"></i> 모두 초기화
    </button>
  </div>

  <div class="result">
    <div class="final-stats">
      <h4><i class="fas fa-chart-bar"></i> 최종 스텟</h4>
      <div class="stats-grid" id="final-stats"></div>
    </div>
    
    <div id="damage-output">
      <h3><i class="fas fa-bullseye"></i> 대미지 계산 결과</h3>
      <p style="text-align: center; color: #666;">계산 버튼을 눌러 결과를 확인하세요</p>
    </div>
  </div>
</div>

<script>
// 각 섹션별 추가된 누적값을 저장할 객체
const addedValues = {
  base: { a: 0, b: 0, c: 0, d: 0, e: 0, f: 0, g: 0 },
  doping: { a: 0, b: 0, c: 0, d: 0, e: 0, f: 0, g: 0 },
  buff: { a: 0, b: 0, c: 0, d: 0, e: 0, f: 0, g: 0 }
};

// 기본값 가져오기
function getDefaultValue(type, section) {
  const defaults = {
    base: { a: 0, b: 100, c: 0, d: 0, e: 0, f: 0, g: 0 },
    doping: { a: 0, b: 0, c: 0, d: 0, e: 0, f: 0, g: 0 },
    buff: { a: 0, b: 0, c: 0, d: 0, e: 0, f: 0, g: 0 }
  };
  return defaults[section][type] || 0;
}

// + 버튼 함수
function addValue(type, amount, section) {
  const inputId = `${type}-${section}`;
  const input = document.getElementById(inputId);
  const addedDisplay = document.getElementById(`${inputId}-added`);
  
  const currentValue = Number(input.value) || 0;
  const newValue = currentValue + amount;
  input.value = newValue < 0 ? 0 : newValue;
  
  const defaultValue = getDefaultValue(type, section);
  addedValues[section][type] = (Number(input.value) || 0) - defaultValue;
  addedDisplay.textContent = `${addedValues[section][type] > 0 ? '+' : ''}${addedValues[section][type]}`;
  
  updateTotalAdded();
}

// 값 초기화 함수
function resetValue(type, section) {
  const inputId = `${type}-${section}`;
  const input = document.getElementById(inputId);
  const addedDisplay = document.getElementById(`${inputId}-added`);
  
  const defaultValue = getDefaultValue(type, section);
  input.value = defaultValue;
  addedValues[section][type] = 0;
  addedDisplay.textContent = '+0';
  
  updateTotalAdded();
}

// 모두 초기화
function clearAll() {
  if (!confirm('모든 입력값을 초기화하시겠습니까?')) return;
  
  const sections = ['base', 'doping', 'buff'];
  sections.forEach(section => {
    Object.keys(addedValues[section]).forEach(type => {
      const inputId = `${type}-${section}`;
      const input = document.getElementById(inputId);
      const addedDisplay = document.getElementById(`${inputId}-added`);
      
      const defaultValue = getDefaultValue(type, section);
      input.value = defaultValue;
      addedValues[section][type] = 0;
      addedDisplay.textContent = '+0';
    });
  });
  
  document.getElementById('damage-output').innerHTML = `
    <h3><i class="fas fa-bullseye"></i> 대미지 계산 결과</h3>
    <p style="text-align: center; color: #666;">계산 버튼을 눌러 결과를 확인하세요</p>
  `;
  
  document.getElementById('final-stats').innerHTML = '';
  
  updateTotalAdded();
}

// 추가된 수치 요약 업데이트
function updateTotalAdded() {
  // 섹션별 시각적 피드백 업데이트
  const sections = [
    { id: 'base', element: '.section-1' },
    { id: 'doping', element: '.section-2' },
    { id: 'buff', element: '.section-3' }
  ];
  
  sections.forEach(({ id, element }) => {
    const sectionData = addedValues[id];
    const hasChanges = Object.values(sectionData).some(value => value !== 0);
    const sectionEl = document.querySelector(element);
    
    if (sectionEl) {
      if (hasChanges) {
        const color = id === 'base' ? '#667eea' : id === 'doping' ? '#4CAF50' : '#FF9800';
        sectionEl.style.boxShadow = `0 0 0 3px ${color}`;
      } else {
        sectionEl.style.boxShadow = '';
      }
    }
  });
}

// 계산 함수
function calculate() {
  const sections = ['base', 'doping', 'buff'];
  const values = {};
  
  ['a', 'b', 'c', 'd', 'e', 'f', 'g'].forEach(type => {
    values[type] = 0;
    sections.forEach(section => {
      const inputId = `${type}-${section}`;
      const inputValue = Number(document.getElementById(inputId).value) || 0;
      values[type] += inputValue;
    });
  });
  
  displayFinalStats(values);
  
  // 계산식 (퍼센트 값을 100으로 나누어 계산)
  const result = values.a * 
                (values.b/100 + values.c/100 * (1 + values.d/100)) * 
                (1 + values.e/100) * 
                (1.2 + values.f/100) * 
                (1 + values.g/100);

  const plus5 = result * 1.05;
  const minus5 = result * 0.95;

  const damageOutput = `
    <div class="damage-result">
      <h3><i class="fas fa-bullseye"></i> 대미지 계산 결과</h3>
      
      <div class="damage-item damage-main">
        <div class="damage-label">최종 대미지</div>
        <div class="damage-value">${result.toLocaleString(undefined, {maximumFractionDigits: 0})}</div>
      </div>
      
      <div class="damage-item damage-plus5">
        <div class="damage-label">+5% 대미지</div>
        <div class="damage-value">${plus5.toLocaleString(undefined, {maximumFractionDigits: 0})}</div>
      </div>
      
      <div class="damage-item damage-minus5">
        <div class="damage-label">-5% 대미지</div>
        <div class="damage-value">${minus5.toLocaleString(undefined, {maximumFractionDigits: 0})}</div>
      </div>
      
      <div style="margin-top: 20px; font-size: 14px; color: #666;">
        <i class="fas fa-info-circle"></i> 대미지 편차: ±${((plus5 - result)/result*100).toFixed(1)}%
      </div>
    </div>
  `;
  
  document.getElementById("damage-output").innerHTML = damageOutput;
  updateTotalAdded();
}

// 최종 스텟 표시 함수
function displayFinalStats(values) {
  const statsHtml = `
    <div class="stat-item">
      <div class="stat-label">깡공</div>
      <div class="stat-value">${values.a.toLocaleString()}</div>
    </div>
    <div class="stat-item">
      <div class="stat-label">물공%</div>
      <div class="stat-value">${values.b}%</div>
    </div>
    <div class="stat-item">
      <div class="stat-label">스댐%</div>
      <div class="stat-value">${values.c}%</div>
    </div>
    <div class="stat-item">
      <div class="stat-label">보공%</div>
      <div class="stat-value">${values.d}%</div>
    </div>
    <div class="stat-item">
      <div class="stat-label">물댐%</div>
      <div class="stat-value">${values.e}%</div>
    </div>
    <div class="stat-item">
      <div class="stat-label">치피%</div>
      <div class="stat-value">${values.f}%</div>
    </div>
    <div class="stat-item">
      <div class="stat-label">종댐%</div>
      <div class="stat-value">${values.g}%</div>
    </div>
  `;
  document.getElementById("final-stats").innerHTML = statsHtml;
}

// 페이지 로드 시 초기화
window.onload = function() {
  const defaultValues = {
    base: { a: 0, b: 100, c: 0, d: 0, e: 0, f: 0, g: 0 },
    doping: { a: 0, b: 0, c: 0, d: 0, e: 0, f: 0, g: 0 },
    buff: { a: 0, b: 0, c: 0, d: 0, e: 0, f: 0, g: 0 }
  };
  
  Object.keys(defaultValues).forEach(section => {
    Object.keys(defaultValues[section]).forEach(type => {
      const inputId = `${type}-${section}`;
      const input = document.getElementById(inputId);
      if (input) {
        input.value = defaultValues[section][type];
      }
    });
  });
  
  updateTotalAdded();
};
</script>

</body>
</html>

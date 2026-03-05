# QC_dashboard-1.0
Dashboard, содержащий в себе базу данных ("правила игры"), материал для тактических инструментов и операционные данные сотрудников (операторов) Soft Collection.

out = open(r"d:\Doc\Doc\Doc\Оценка качества звонков\Отчеты\Итоговый отчет\Dashboard_SC\index.html", "a", encoding="utf-8")

out.write("""
<script>
// ===================== DATA =====================
const PERIODS = ['01–08 фев','09–15 фев','16–22 фев','23–28 фев'];

const EMPLOYEES = {
  'Абдувалиева Зарифа':    {scores:[79.75,74,null,null],   risk:{manip:'0,5 (01,05)',itog:'нет',req:'0,5 (3 зв.)'},   rec:'Переход к нормативной аргументации (ст.236 ГК РУз)', status:'yellow'},
  'Боборахматов Санъатбек':{scores:[80.25,70.75,64.75,83.5],risk:{manip:'«0» (25.02)',itog:'«0» (03.02)',req:'«0» (09.02)'},rec:'Структура легенды + тактики «Выбор без выбора»', status:'yellow'},
  'Каюмова Сония':         {scores:[64.75,69.25,62,76.5],  risk:{manip:'«0» (3 зв.)',itog:'«0» (03.02)',req:'0,5 (все)'},rec:'Тактика «Выбор без выбора», правовая база (ст.333)',status:'red'},
  'Тоштемиров Мухаммадали':{scores:[62.75,null,null,51.5], risk:{manip:'«0» (все)',itog:'«0» (все)',req:'«0» (04.02)'},  rec:'Полный инструктаж по Якунлаш + тактики давления',   status:'red'},
  'Тожиев Шохрух':         {scores:[71.75,69.75,61.5,69],  risk:{manip:'«0» 16–22',itog:'«0» (3 зв.)',req:'«0» (19.02)'},rec:'Обучение: ст.236,237 ГК РУз + манипуляция',         status:'yellow'},
  'Шавкатов Гофур':        {scores:[54.5,57.25,61.25,60.5],risk:{manip:'«0» (22.02)',itog:'«0» (все)',req:'«0» (02.02)'},rec:'Жёсткий контроль блока Якунлаш',                    status:'red'},
  'Бахромова Нозима':      {scores:[63,null,61.75,61],      risk:{manip:'«0» (3 зв.)',itog:'«0» (2 зв.)',req:'«0» (24,28)'},rec:'Цитирование ст.333 ГК РУз в каждом звонке',      status:'red'},
  'Абдуллаева Севинч':     {scores:[59,67.75,78.5,62],      risk:{manip:'«0» (24,28)',itog:'«0» (01.02)',req:'0,5 (все)'},rec:'Исключить односторонний сброс звонка',              status:'yellow'},
  'Шамиев Фаррух':         {scores:[67.75,72,76.5,73.25],   risk:{manip:'«0» (18.02)',itog:'«0» (05.02)',req:'«0» (24,05)'},rec:'Техники перехвата инициативы, ст.236',           status:'yellow'},
  'Шохназарова Сабрина':   {scores:[74,62.75,66.75,58.5],   risk:{manip:'«0» (2 зв.)',itog:'«0» (05.02)',req:'«0» (14.02)'},rec:'Разбор провала CRM 26,28.02',                  status:'red'},
  'Хакимов Умид':          {scores:[65.25,59.5,77,66.5],    risk:{manip:'«0» (02.02)',itog:'«0» (01.02)',req:'0,5 (все)'},rec:'Ст.421 ГК РУз для усиления позиции',              status:'yellow'},
  'Надруллаева Рухсона':   {scores:[75,67.75,66.5,72],      risk:{manip:'«0» (09.02)',itog:'«0» (3 зв.)',req:'0,5 (все)'},rec:'Техники «взрослый–взрослый», сжатие диалога',     status:'yellow'},
  'Сабуров Огабек':        {scores:[52,68.5,65.75,54],      risk:{manip:'«0» (3 зв.)',itog:'«0» (3 зв.)',req:'«0» (2 зв.)'},rec:'Ст.421 ГК РУз + разбор системных провалов',    status:'red'},
  'Алкаров Жамшид':        {scores:[60.25,72.25,56.7,46.5], risk:{manip:'«0» (3 зв.)',itog:'«0» (05.02)',req:'«0» (05.02)'},rec:'ЗАПРЕТ дезинформации (МИБ/блокировка)! Полный пересмотр навыков', status:'red'},
  'Низомиддинов Аслиддин': {scores:[68.5,61,67.25,63.25],   risk:{manip:'«0» (3 зв.)',itog:'нет',req:'«0» (11.02)'},   rec:'Тактики «Выбор без выбора», ст.333 ГК РУз',      status:'yellow'},
  'Исаков Даврон':         {scores:[56.5,50.75,66.5,81.5],  risk:{manip:'«0» (2 зв.)',itog:'«0» (3 зв.)',req:'«0» (2 зв.)'},rec:'🌟 Лучший рост! Сократить время звонков',      status:'green'},
  'Сабитова Навруза':      {scores:[64.75,74.25,66.5,67.5], risk:{manip:'«0» (02.02)',itog:'«0» (24.02)',req:'«0» (2 зв.)'},rec:'Разбор провала 02.02, ст.324 ГК РУз',          status:'yellow'},
  'Куролбоев Жавохир':     {scores:[61.75,65.25,66.5,64],   risk:{manip:'«0» (3 зв.)',itog:'нет',req:'«0» (12.02)'},   rec:'Манипуляция «Давление сроком», ст.236+237',      status:'red'},
  'Мусаев Хуршид':         {scores:[57.25,57.5,54.3,72.75], risk:{manip:'«0» (2 зв.)',itog:'«0» (3 зв.)',req:'0,5 (все)'},rec:'Жёсткий контроль блока Якунлаш (75% «0»)',     status:'red'},
};

const CRITERIA = [
  {n:1,name:'Приветствие, идентификация и прощание',weight:5,color:'#6366f1',
   desc:'Соблюдение официального протокола входа в контакт. Три обязательных компонента.'},
  {n:2,name:'Этика общения',weight:5,color:'#8b5cf6',
   desc:'Отсутствие конфликтогенов, соблюдение норм делового этикета. Удержание инициативы.'},
  {n:3,name:'Работа в системе (CRM)',weight:10,color:'#a78bfa',
   desc:'Соответствие статуса в CRM фактическому итогу. Целостность данных.'},
  {n:4,name:'Легендирование',weight:15,color:'#7c3aed',
   desc:'Тактическое использование сценариев: «компетенция» + «эскалация». Оба компонента обязательны.'},
  {n:5,name:'Информирование о задолженности',weight:10,color:'#4f46e5',
   desc:'Точность и полнота данных о суммах, сроках DPD и последствиях.'},
  {n:6,name:'Аргументация',weight:20,color:'#ec4899',
   desc:'Глубина и логика работы с отказами. Нормативная аргументация (НПА РУз) > стандартной.'},
  {n:7,name:'Манипуляция',weight:10,color:'#f59e0b',
   desc:'Применение психологических триггеров давления. Развёрнутая > формальной.'},
  {n:8,name:'Выставление требований',weight:15,color:'#10b981',
   desc:'Чёткость формулировок: конкретный срок, сумма, способ оплаты. Без компромисса.'},
  {n:9,name:'Подведение итогов (Якунлаш)',weight:10,color:'#06b6d4',
   desc:'Резюмирование договорённостей + упоминание фиксации разговора. «Ждём оплату» не засчитывается.'},
];

const SVP_STAGES = [
  {num:'Этап 1',title:'Фаза входа в контакт',
   desc:'Приветствие · Идентификация · Легендирование',
   detail:'Установление стандартов приветствия. Разделение протоколов: исходящий (устное подтверждение) / входящий (4-факторная верификация). Тактическое легендирование: «компетенция» (роль) + «эскалация» (техн. часть).'},
  {num:'Этап 2',title:'Информационный блок',
   desc:'Информирование о долге · DPD · Открытые вопросы',
   detail:'Озвучивание суммы актуальной задолженности и срока просрочки. Работа с первичными возражениями. Диагностика ситуации через открытые вопросы: «Что помешало оплатить?», «Каким образом планируете распределить бюджет?»'},
  {num:'Этап 3',title:'Блок активного взыскания',
   desc:'Аргументация · Манипуляция · РсВ',
   detail:'Переход от стандартных логических доводов к нормативной аргументации (ссылки на НПА и условия Оферты). Манипуляция: от формальных триггеров к развёрнутой проработке последствий и данности.'},
  {num:'Этап 4',title:'Фиксация обязательств',
   desc:'Требования · Итоги (Якунлаш) · Прощание',
   detail:'Стандартизация требований: конкретный срок PTP, полная сумма (не компромисс), способы оплаты. Обязательное резюмирование + предупреждение о документировании и фиксации разговора.'},
  {num:'Этап 5',title:'Интеграция в систему QC',
   desc:'Весовые коэффициенты · Ответственность · TQS',
   detail:'Увязка каждого этапа СВП с весовыми коэффициентами (5–20%) в оценочном листе QC. Персональная ответственность сотрудника за отклонение от СВП. Стратифицированная рандомная выборка.'},
];

const LAWS = [
  {art:'Ст. 236',name:'Надлежащее исполнение',
   text:'Обязательства должны исполняться надлежащим образом в соответствии с условиями договора.',
   use:'«Согласно ст. 236 ГК РУз, Вы обязаны исполнить обязательства в точном соответствии с условиями оферты...»'},
  {art:'Ст. 237',name:'Запрет одностороннего отказа',
   text:'Односторонний отказ от исполнения обязательства и одностороннее изменение его условий не допускаются.',
   use:'«Согласно ст. 237 ГК РУз, Вы не вправе в одностороннем порядке отказаться от исполнения договорных обязательств...»'},
  {art:'Ст. 333',name:'Ответственность за неисполнение',
   text:'Отсутствие у должника денежных средств само по себе не освобождает его от ответственности.',
   use:'«Ст. 333 ГК РУз прямо указывает: отсутствие денег не снимает с Вас обязательств. Ответственность наступает в любом случае...»'},
  {art:'Ст. 421',name:'Залог до полной оплаты',
   text:'Товар, проданный в кредит, находится в залоге у продавца до момента его полной оплаты.',
   use:'«В соответствии со ст. 421 ГК РУз приобретённый Вами товар является залоговым имуществом VRF до полного погашения задолженности...»'},
];

// ===================== RENDER CRITERIA =====================
function renderCriteria() {
  const g = document.getElementById('criteriaGrid');
  CRITERIA.forEach(c => {
    const pct = c.weight;
    const col = c.color;
    g.innerHTML += `
    <div class="crit-card" style="border-top:3px solid ${col}">
      <div class="crit-num">${c.n}</div>
      <div class="crit-weight" style="color:${col}">${pct}%</div>
      <div class="crit-name">${c.name}</div>
      <div class="crit-desc">${c.desc}</div>
      <div class="crit-bar" style="background:linear-gradient(90deg,${col},${col}44);width:${pct*5}%"></div>
    </div>`;
  });
}

// ===================== RENDER SVP =====================
function renderSVP() {
  const c = document.getElementById('svpContainer');
  SVP_STAGES.forEach((s,i) => {
    const el = document.createElement('div');
    el.className = 'svp-stage' + (i===0?' active':'');
    el.innerHTML = `<div class="svp-num">${s.num}</div>
      <div class="svp-title">${s.title}</div>
      <div class="svp-desc">${s.desc}</div>
      <div class="svp-detail">${s.detail}</div>`;
    el.onclick = () => { document.querySelectorAll('.svp-stage').forEach(x=>x.classList.remove('active')); el.classList.add('active'); };
    c.appendChild(el);
  });
}

// ===================== RENDER LAWS =====================
function renderLaws() {
  const g = document.getElementById('lawGrid');
  LAWS.forEach((l,i) => {
    g.innerHTML += `<div class="law-card" onclick="openLawModal(${i})">
      <div class="law-art">${l.art}</div>
      <div class="law-name">${l.name}</div>
      <div class="law-text">${l.text.substring(0,80)}...</div>
    </div>`;
  });
}
let currentLaw = null;
function openLawModal(i) {
  const l = LAWS[i];
  document.getElementById('lawModalContent').innerHTML = `
    <div style="font-size:22px;font-weight:800;color:#a78bfa;margin-bottom:4px">${l.art}</div>
    <div style="font-size:15px;font-weight:700;color:#f1f5f9;margin-bottom:12px">${l.name}</div>
    <div style="font-size:12px;color:#94a3b8;line-height:1.6;margin-bottom:16px">${l.text}</div>
    <div style="background:rgba(167,139,250,0.1);border:1px solid #4c1d95;border-radius:8px;padding:14px;">
      <div style="font-size:10px;font-weight:700;color:#a78bfa;text-transform:uppercase;letter-spacing:1px;margin-bottom:8px">💬 Пример цитирования</div>
      <div style="font-size:12px;color:#c4b5fd;line-height:1.6;font-style:italic">"${l.use}"</div>
    </div>`;
  document.getElementById('lawModal').classList.add('open');
}
function closeLawModal() { document.getElementById('lawModal').classList.remove('open'); }

// ===================== RENDER RISK TABLE =====================
function renderRisk() {
  const tb = document.getElementById('riskTableBody');
  const sorted = Object.entries(EMPLOYEES).sort((a,b)=>{
    const avgA = a[1].scores.filter(x=>x!==null).reduce((s,v)=>s+v,0)/a[1].scores.filter(x=>x!==null).length;
    const avgB = b[1].scores.filter(x=>x!==null).reduce((s,v)=>s+v,0)/b[1].scores.filter(x=>x!==null).length;
    return avgA-avgB;
  });
  sorted.forEach(([name,data]) => {
    const valid = data.scores.filter(x=>x!==null);
    const avg = (valid.reduce((s,v)=>s+v,0)/valid.length).toFixed(1);
    const sc = data.status;
    const col = sc==='green'?'#4ade80':sc==='yellow'?'#facc15':'#f87171';
    const bgc = sc==='green'?'badge-green':sc==='yellow'?'badge-yellow':'badge-red';
    const icon = sc==='green'?'🟢':sc==='yellow'?'🟡':'🔴';
    tb.innerHTML += `<tr>
      <td style="font-weight:600;color:#e2e8f0">${name}</td>
      <td style="color:${col};font-weight:700">${avg}%</td>
      <td style="color:#f87171;font-size:11px">${data.risk.manip}</td>
      <td style="color:#f87171;font-size:11px">${data.risk.itog}</td>
      <td style="color:#f87171;font-size:11px">${data.risk.req}</td>
      <td><span class="kpi-badge ${bgc}">${icon} ${sc==='green'?'Рост':sc==='yellow'?'Внимание':'Критично'}</span></td>
      <td style="font-size:11px;color:#94a3b8;max-width:220px">${data.rec}</td>
    </tr>`;
  });
}

// ===================== CHART =====================
let trendChart = null;
const COLORS = ['#a78bfa','#4ade80','#f87171','#facc15','#60a5fa','#fb923c','#34d399','#e879f9','#94a3b8','#ffba08'];

function buildChart(selectedNames) {
  const ctx = document.getElementById('trendChart').getContext('2d');
  if (trendChart) trendChart.destroy();
  const datasets = selectedNames.map((name,i) => {
    const d = EMPLOYEES[name];
    return {
      label: name.split(' ')[0],
      data: d.scores,
      borderColor: COLORS[i % COLORS.length],
      backgroundColor: COLORS[i % COLORS.length] + '22',
      borderWidth: 2.5,
      pointRadius: 5,
      pointHoverRadius: 8,
      tension: 0.4,
      spanGaps: true,
    };
  });
  trendChart = new Chart(ctx, {
    type:'line',
    data:{ labels: PERIODS, datasets },
    options:{
      responsive:true, maintainAspectRatio:false,
      plugins:{
        legend:{labels:{color:'#94a3b8',font:{size:11,family:'Inter'}}},
        tooltip:{
          backgroundColor:'#1e2435',borderColor:'#2d3748',borderWidth:1,
          titleColor:'#f1f5f9',bodyColor:'#94a3b8',
          callbacks:{ label: ctx=>`${ctx.dataset.label}: ${ctx.parsed.y !== null ? ctx.parsed.y+'%' : '—'}` }
        }
      },
      scales:{
        x:{ grid:{color:'#1e2435'}, ticks:{color:'#64748b',font:{size:11}} },
        y:{ min:40, max:100, grid:{color:'#232b3e'}, ticks:{color:'#64748b',font:{size:11},callback:v=>v+'%'},
            title:{display:true,text:'Средний балл TQS',color:'#4a5568',font:{size:11}} }
      }
    }
  });
}

// ===================== FILTER =====================
const KEY_EMPLOYEES = ['Исаков Даврон','Боборахматов Санъатбек','Шавкатов Гофур','Абдуллаева Севинч','Каюмова Сония'];
let selected = [...KEY_EMPLOYEES];

function renderFilter() {
  const f = document.getElementById('employeeFilter');
  const names = Object.keys(EMPLOYEES);
  // "Все" button
  const allBtn = document.createElement('div');
  allBtn.className = 'filter-btn' + (selected.length===names.length?' active':'');
  allBtn.textContent = 'Все';
  allBtn.onclick = () => {
    selected = [...names];
    document.querySelectorAll('.filter-btn').forEach(b=>b.classList.remove('active'));
    allBtn.classList.add('active');
    buildChart(selected);
  };
  f.appendChild(allBtn);

  names.forEach(name => {
    const btn = document.createElement('div');
    btn.className = 'filter-btn' + (selected.includes(name)?' active':'');
    btn.textContent = name.split(' ')[0] + ' ' + name.split(' ')[1].charAt(0) + '.';
    btn.onclick = () => {
      if (selected.includes(name)) {
        if (selected.length===1) return;
        selected = selected.filter(n=>n!==name);
        btn.classList.remove('active');
      } else {
        selected.push(name);
        btn.classList.add('active');
      }
      allBtn.classList.remove('active');
      buildChart(selected);
    };
    f.appendChild(btn);
  });
}

// ===================== NAV =====================
function showSection(id) {
  document.querySelectorAll('.section').forEach(s=>s.classList.remove('active'));
  document.querySelectorAll('.nav-item').forEach(n=>n.classList.remove('active'));
  document.getElementById('section-'+id).classList.add('active');
  event.currentTarget.classList.add('active');
  if (id==='operations' && !trendChart) buildChart(selected);
}

// ===================== INIT =====================
renderCriteria();
renderSVP();
renderLaws();
renderRisk();
renderFilter();

// Pre-init hidden chart after slight delay
setTimeout(() => buildChart(selected), 100);
</script>
</body>
</html>""")

print("Part 3 done — HTML complete!")
out.close()

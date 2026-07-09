[index (1).html](https://github.com/user-attachments/files/29834562/index.1.html)
<!doctype html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>日程总结工具 - 手机电脑同步版</title>
  <style>
    :root {
      --bg: #f6f7fb;
      --card: #ffffff;
      --text: #172033;
      --muted: #64748b;
      --line: #e2e8f0;
      --primary: #2563eb;
      --primary-dark: #1d4ed8;
      --success: #16a34a;
      --danger: #dc2626;
      --shadow: 0 10px 30px rgba(15, 23, 42, 0.08);
      --radius: 18px;
    }

    * { box-sizing: border-box; }

    body {
      margin: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Microsoft YaHei", sans-serif;
      background: radial-gradient(circle at top left, #dbeafe, transparent 35%), var(--bg);
      color: var(--text);
    }

    header {
      padding: 34px 18px 18px;
      text-align: center;
    }

    header h1 {
      margin: 0;
      font-size: clamp(26px, 5vw, 40px);
      letter-spacing: -0.04em;
    }

    header p {
      max-width: 780px;
      margin: 12px auto 0;
      color: var(--muted);
      line-height: 1.7;
    }

    main {
      width: min(1180px, calc(100% - 28px));
      margin: 0 auto 38px;
      display: grid;
      grid-template-columns: 400px 1fr;
      gap: 18px;
    }

    .card {
      background: rgba(255, 255, 255, 0.94);
      border: 1px solid rgba(226, 232, 240, 0.9);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      padding: 20px;
    }

    .full { grid-column: 1 / -1; }

    h2 {
      margin: 0 0 14px;
      font-size: 20px;
    }

    label {
      display: block;
      margin: 12px 0 6px;
      color: #334155;
      font-weight: 700;
      font-size: 14px;
    }

    input, select, textarea {
      width: 100%;
      padding: 12px 13px;
      border: 1px solid var(--line);
      border-radius: 12px;
      font: inherit;
      color: var(--text);
      background: #fff;
      outline: none;
    }

    input:focus, select:focus, textarea:focus {
      border-color: var(--primary);
      box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.12);
    }

    textarea {
      min-height: 88px;
      resize: vertical;
    }

    button {
      border: 0;
      border-radius: 12px;
      padding: 11px 14px;
      font: inherit;
      font-weight: 800;
      cursor: pointer;
      background: #e2e8f0;
      color: #0f172a;
    }

    button:hover { transform: translateY(-1px); }
    button:disabled { opacity: 0.55; cursor: not-allowed; transform: none; }

    .primary { background: var(--primary); color: #fff; }
    .primary:hover { background: var(--primary-dark); }
    .danger { background: #fee2e2; color: var(--danger); }
    .success { background: #dcfce7; color: #166534; }

    .row {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
    }

    .actions {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin-top: 16px;
    }

    .notice {
      margin-top: 12px;
      padding: 12px 14px;
      background: #eff6ff;
      color: #1e40af;
      border: 1px solid #bfdbfe;
      border-radius: 14px;
      line-height: 1.6;
      font-size: 14px;
    }

    .error {
      background: #fef2f2;
      color: #991b1b;
      border-color: #fecaca;
    }

    .muted {
      color: var(--muted);
      font-size: 14px;
      line-height: 1.6;
    }

    .hidden { display: none !important; }

    .stats {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 12px;
      margin-bottom: 18px;
    }

    .stat {
      background: #f8fafc;
      border: 1px solid var(--line);
      border-radius: 16px;
      padding: 14px;
    }

    .stat b {
      display: block;
      font-size: 26px;
      margin-bottom: 4px;
    }

    .toolbar {
      display: grid;
      grid-template-columns: 150px 1fr 150px;
      gap: 10px;
      margin-bottom: 14px;
    }

    .schedule-list {
      display: grid;
      gap: 10px;
      max-height: 430px;
      overflow: auto;
      padding-right: 4px;
    }

    .schedule-item {
      border: 1px solid var(--line);
      border-radius: 16px;
      padding: 13px;
      background: #fff;
      display: grid;
      gap: 8px;
    }

    .schedule-top {
      display: flex;
      justify-content: space-between;
      gap: 10px;
      align-items: flex-start;
    }

    .schedule-title {
      font-weight: 900;
      font-size: 16px;
      line-height: 1.4;
    }

    .schedule-title.done {
      color: var(--muted);
      text-decoration: line-through;
    }

    .meta {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      color: var(--muted);
      font-size: 13px;
    }

    .tag {
      display: inline-flex;
      align-items: center;
      width: fit-content;
      padding: 4px 9px;
      border-radius: 999px;
      color: #fff;
      font-size: 12px;
      font-weight: 800;
      white-space: nowrap;
    }

    .item-actions {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
    }

    .item-actions button {
      padding: 7px 10px;
      border-radius: 10px;
      font-size: 13px;
    }

    .tabs {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      margin: 4px 0 14px;
    }

    .tabs button.active {
      background: var(--primary);
      color: #fff;
    }

    .report-box {
      min-height: 320px;
      white-space: pre-wrap;
      background: #0f172a;
      color: #e2e8f0;
      border-radius: 16px;
      padding: 18px;
      line-height: 1.75;
      overflow: auto;
      font-family: "Consolas", "SFMono-Regular", monospace;
    }

    @media (max-width: 900px) {
      main { grid-template-columns: 1fr; }
      .stats { grid-template-columns: repeat(2, 1fr); }
      .toolbar, .row { grid-template-columns: 1fr; }
    }
  </style>
</head>
<body>
  <header>
    <h1>日程总结工具 - 手机电脑同步版</h1>
    <p>使用 Supabase 保存数据。电脑和手机打开这个页面，登录同一个账号，就能同步日程并生成日报、周报、月报。</p>
  </header>

  <main>
    <section id="authCard" class="card full">
      <h2>登录 / 注册</h2>
      <p class="muted">第一次使用请先注册账号。以后电脑和手机都用同一个邮箱和密码登录，就能看到同一份日程。</p>
      <div class="row">
        <div>
          <label for="email">邮箱</label>
          <input id="email" type="email" placeholder="例如：you@example.com" />
        </div>
        <div>
          <label for="password">密码</label>
          <input id="password" type="password" placeholder="至少 6 位" />
        </div>
      </div>
      <div class="actions">
        <button class="primary" id="loginBtn" type="button">登录</button>
        <button id="signupBtn" type="button">注册</button>
      </div>
      <div id="authMessage" class="notice hidden"></div>
    </section>

    <section id="appPanel" class="hidden" style="display: contents;">
      <section class="card">
        <h2 id="formTitle">新增日程</h2>
        <p class="muted">当前账号：<span id="userEmail"></span></p>
        <form id="scheduleForm">
          <input type="hidden" id="editingId" />

          <label for="title">日程标题</label>
          <input id="title" required placeholder="例如：完成客户方案、复习英语、整理房间" />

          <div class="row">
            <div>
              <label for="date">日期</label>
              <input id="date" type="date" required />
            </div>
            <div>
              <label for="category">分类</label>
              <select id="category"></select>
            </div>
          </div>

          <div class="row">
            <div>
              <label for="startTime">开始时间</label>
              <input id="startTime" type="time" />
            </div>
            <div>
              <label for="endTime">结束时间</label>
              <input id="endTime" type="time" />
            </div>
          </div>

          <label for="description">备注</label>
          <textarea id="description" placeholder="可以写目标、结果、遇到的问题、下一步计划"></textarea>

          <div class="actions">
            <button class="primary" type="submit">保存日程</button>
            <button type="button" id="resetForm">清空表单</button>
            <button type="button" id="logoutBtn">退出登录</button>
          </div>
        </form>

        <div id="syncMessage" class="notice hidden"></div>
      </section>

      <section class="card">
        <h2>日程列表</h2>
        <div class="stats">
          <div class="stat"><b id="totalCount">0</b><span>总日程</span></div>
          <div class="stat"><b id="doneCount">0</b><span>已完成</span></div>
          <div class="stat"><b id="todoCount">0</b><span>未完成</span></div>
          <div class="stat"><b id="rateCount">0%</b><span>完成率</span></div>
        </div>

        <div class="toolbar">
          <input id="filterDate" type="date" />
          <input id="keyword" placeholder="搜索标题或备注" />
          <select id="filterCategory">
            <option value="">全部分类</option>
          </select>
        </div>

        <div id="scheduleList" class="schedule-list"></div>
      </section>

      <section class="card full">
        <h2>自动总结报告</h2>
        <div class="row">
          <div>
            <label for="reportDate">选择报告日期</label>
            <input id="reportDate" type="date" />
          </div>
          <div>
            <label for="reportType">报告类型</label>
            <select id="reportType">
              <option value="day">日报</option>
              <option value="week">周报</option>
              <option value="month">月报</option>
            </select>
          </div>
        </div>

        <div class="tabs">
          <button type="button" data-report="day" class="active">日报</button>
          <button type="button" data-report="week">周报</button>
          <button type="button" data-report="month">月报</button>
        </div>

        <div class="actions">
          <button class="primary" id="generateReport" type="button">生成报告</button>
          <button class="success" id="copyReport" type="button">复制报告</button>
          <button id="downloadReport" type="button">下载报告</button>
          <button id="refreshBtn" type="button">刷新同步</button>
        </div>

        <label for="reportOutput">报告内容</label>
        <div id="reportOutput" class="report-box"></div>
      </section>
    </section>
  </main>

  <script type="module">
    import { createClient } from "https://esm.sh/@supabase/supabase-js@2";

    const SUPABASE_URL = "https://xvhpxhjyszrrfbyuaozb.supabase.co";
    const SUPABASE_ANON_KEY = "sb_publishable_RWO4RqhxpD02NC6e4Y890Q_w1dlNnnp";
    const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);

    const $ = (id) => document.getElementById(id);
    const defaultCategories = [
      { id: "", name: "工作", color: "#3b82f6" },
      { id: "", name: "学习", color: "#8b5cf6" },
      { id: "", name: "生活", color: "#10b981" },
      { id: "", name: "会议", color: "#f59e0b" },
      { id: "", name: "其他", color: "#6b7280" }
    ];

    let currentUser = null;
    let schedules = [];
    let categories = [...defaultCategories];

    function today() {
      const date = new Date();
      const offset = date.getTimezoneOffset();
      return new Date(date.getTime() - offset * 60000).toISOString().slice(0, 10);
    }

    $("date").value = today();
    $("filterDate").value = today();
    $("reportDate").value = today();

    function showMessage(id, text, isError = false) {
      const box = $(id);
      box.textContent = text;
      box.className = `notice ${isError ? "error" : ""}`;
      box.classList.remove("hidden");
    }

    function hideMessage(id) {
      $(id).classList.add("hidden");
    }

    async function init() {
      const { data } = await supabase.auth.getSession();
      currentUser = data.session?.user || null;
      await renderAuthState();

      supabase.auth.onAuthStateChange(async (_event, session) => {
        currentUser = session?.user || null;
        await renderAuthState();
      });
    }

    async function renderAuthState() {
      if (!currentUser) {
        $("authCard").classList.remove("hidden");
        $("appPanel").classList.add("hidden");
        return;
      }

      $("authCard").classList.add("hidden");
      $("appPanel").classList.remove("hidden");
      $("userEmail").textContent = currentUser.email || "";
      await loadAllData();
    }

    $("signupBtn").addEventListener("click", async () => {
      hideMessage("authMessage");
      const email = $("email").value.trim();
      const password = $("password").value;
      if (!email || !password) {
        showMessage("authMessage", "请填写邮箱和密码。", true);
        return;
      }

      const { error } = await supabase.auth.signUp({ email, password });
      if (error) {
        showMessage("authMessage", `注册失败：${error.message}`, true);
        return;
      }
      showMessage("authMessage", "注册成功。如果 Supabase 开启了邮箱确认，请先去邮箱点击确认链接，然后再登录。");
    });

    $("loginBtn").addEventListener("click", async () => {
      hideMessage("authMessage");
      const email = $("email").value.trim();
      const password = $("password").value;
      if (!email || !password) {
        showMessage("authMessage", "请填写邮箱和密码。", true);
        return;
      }

      const { error } = await supabase.auth.signInWithPassword({ email, password });
      if (error) {
        showMessage("authMessage", `登录失败：${error.message}`, true);
      }
    });

    $("logoutBtn").addEventListener("click", async () => {
      await supabase.auth.signOut();
      schedules = [];
      renderList();
    });

    async function loadAllData() {
      showMessage("syncMessage", "正在从 Supabase 同步数据...");
      await loadCategories();
      await loadSchedules();
      renderCategoryOptions();
      renderList();
      generateReport();
      showMessage("syncMessage", "同步完成。电脑和手机登录同一个账号即可看到这些日程。");
    }

    async function loadCategories() {
      const { data, error } = await supabase
        .from("categories")
        .select("id,name,color")
        .order("created_at", { ascending: true });

      if (error) {
        categories = [...defaultCategories];
        showMessage("syncMessage", `分类读取失败：${error.message}`, true);
        return;
      }

      categories = data?.length ? data : [...defaultCategories];
    }

    async function loadSchedules() {
      const { data, error } = await supabase
        .from("schedules")
        .select("id,user_id,title,category_id,description,start_time,end_time,date,completed,created_at,updated_at")
        .order("date", { ascending: true })
        .order("start_time", { ascending: true });

      if (error) {
        schedules = [];
        showMessage("syncMessage", `日程读取失败：${error.message}`, true);
        return;
      }

      schedules = data || [];
    }

    function renderCategoryOptions() {
      const options = categories.map((item) => `<option value="${item.id || item.name}">${escapeHtml(item.name)}</option>`).join("");
      $("category").innerHTML = options;
      $("filterCategory").innerHTML = `<option value="">全部分类</option>${options}`;
    }

    function getCategoryById(categoryId) {
      return categories.find((item) => item.id === categoryId || item.name === categoryId) || defaultCategories.find((item) => item.name === "其他");
    }

    function getFilteredSchedules() {
      const filterDate = $("filterDate").value;
      const keyword = $("keyword").value.trim().toLowerCase();
      const categoryValue = $("filterCategory").value;

      return schedules
        .filter((item) => !filterDate || item.date === filterDate)
        .filter((item) => !categoryValue || item.category_id === categoryValue || getCategoryById(item.category_id)?.name === categoryValue)
        .filter((item) => {
          if (!keyword) return true;
          return item.title.toLowerCase().includes(keyword) || (item.description || "").toLowerCase().includes(keyword);
        });
    }

    function renderStats() {
      const filtered = getFilteredSchedules();
      const total = filtered.length;
      const done = filtered.filter((item) => item.completed).length;
      const todo = total - done;
      const rate = total ? Math.round((done / total) * 100) : 0;
      $("totalCount").textContent = total;
      $("doneCount").textContent = done;
      $("todoCount").textContent = todo;
      $("rateCount").textContent = `${rate}%`;
    }

    function renderList() {
      renderStats();
      const list = $("scheduleList");
      const filtered = getFilteredSchedules();
      if (!currentUser) return;

      if (!filtered.length) {
        list.innerHTML = `<p class="muted">当前没有日程。可以新增一条，或调整日期和筛选条件。</p>`;
        return;
      }

      list.innerHTML = filtered.map((item) => {
        const category = getCategoryById(item.category_id);
        const time = item.start_time || item.end_time ? `${item.start_time || "未填"} - ${item.end_time || "未填"}` : "未设置时间";
        return `
          <article class="schedule-item">
            <div class="schedule-top">
              <div>
                <div class="schedule-title ${item.completed ? "done" : ""}">${escapeHtml(item.title)}</div>
                <div class="meta">
                  <span>${item.date}</span>
                  <span>${time}</span>
                  <span>${item.completed ? "已完成" : "未完成"}</span>
                </div>
              </div>
              <span class="tag" style="background:${category?.color || "#6b7280"}">${escapeHtml(category?.name || "其他")}</span>
            </div>
            ${item.description ? `<div class="muted">${escapeHtml(item.description)}</div>` : ""}
            <div class="item-actions">
              <button class="success" data-action="toggle" data-id="${item.id}">${item.completed ? "标为未完成" : "标为完成"}</button>
              <button data-action="edit" data-id="${item.id}">编辑</button>
              <button class="danger" data-action="delete" data-id="${item.id}">删除</button>
            </div>
          </article>
        `;
      }).join("");
    }

    $("scheduleList").addEventListener("click", async (event) => {
      const button = event.target.closest("button");
      if (!button) return;

      const id = button.dataset.id;
      const action = button.dataset.action;
      if (action === "toggle") await toggleDone(id);
      if (action === "edit") editSchedule(id);
      if (action === "delete") await deleteSchedule(id);
    });

    async function toggleDone(id) {
      const item = schedules.find((schedule) => schedule.id === id);
      if (!item) return;
      const { error } = await supabase
        .from("schedules")
        .update({ completed: !item.completed, updated_at: new Date().toISOString() })
        .eq("id", id);

      if (error) {
        showMessage("syncMessage", `更新失败：${error.message}`, true);
        return;
      }
      await loadAllData();
    }

    function editSchedule(id) {
      const item = schedules.find((schedule) => schedule.id === id);
      if (!item) return;
      $("editingId").value = item.id;
      $("formTitle").textContent = "编辑日程";
      $("title").value = item.title;
      $("date").value = item.date;
      $("category").value = item.category_id || "";
      $("startTime").value = item.start_time || "";
      $("endTime").value = item.end_time || "";
      $("description").value = item.description || "";
      window.scrollTo({ top: 0, behavior: "smooth" });
    }

    async function deleteSchedule(id) {
      if (!confirm("确定要删除这条日程吗？")) return;
      const { error } = await supabase.from("schedules").delete().eq("id", id);
      if (error) {
        showMessage("syncMessage", `删除失败：${error.message}`, true);
        return;
      }
      await loadAllData();
    }

    $("scheduleForm").addEventListener("submit", async (event) => {
      event.preventDefault();
      if (!currentUser) return;

      const id = $("editingId").value;
      const payload = {
        user_id: currentUser.id,
        title: $("title").value.trim(),
        category_id: $("category").value || null,
        description: $("description").value.trim() || null,
        start_time: $("startTime").value || null,
        end_time: $("endTime").value || null,
        date: $("date").value,
        updated_at: new Date().toISOString()
      };

      if (!payload.title) {
        showMessage("syncMessage", "请填写日程标题。", true);
        return;
      }

      const result = id
        ? await supabase.from("schedules").update(payload).eq("id", id)
        : await supabase.from("schedules").insert(payload);

      if (result.error) {
        showMessage("syncMessage", `保存失败：${result.error.message}`, true);
        return;
      }

      resetForm();
      await loadAllData();
    });

    function resetForm() {
      $("editingId").value = "";
      $("formTitle").textContent = "新增日程";
      $("title").value = "";
      $("date").value = today();
      $("startTime").value = "";
      $("endTime").value = "";
      $("description").value = "";
      if (categories[0]) $("category").value = categories[0].id || categories[0].name;
    }

    $("resetForm").addEventListener("click", resetForm);
    $("refreshBtn").addEventListener("click", loadAllData);
    $("filterDate").addEventListener("input", renderList);
    $("keyword").addEventListener("input", renderList);
    $("filterCategory").addEventListener("input", renderList);

    function dateRangeFor(type, dateString) {
      const date = new Date(`${dateString}T00:00:00`);
      if (type === "day") return { start: dateString, end: dateString, title: `${dateString} 日报` };
      if (type === "week") {
        const day = date.getDay() || 7;
        const monday = new Date(date);
        monday.setDate(date.getDate() - day + 1);
        const sunday = new Date(monday);
        sunday.setDate(monday.getDate() + 6);
        return { start: formatDate(monday), end: formatDate(sunday), title: `${formatDate(monday)} 至 ${formatDate(sunday)} 周报` };
      }
      const first = new Date(date.getFullYear(), date.getMonth(), 1);
      const last = new Date(date.getFullYear(), date.getMonth() + 1, 0);
      return { start: formatDate(first), end: formatDate(last), title: `${date.getFullYear()}年${date.getMonth() + 1}月月报` };
    }

    function formatDate(date) {
      const offset = date.getTimezoneOffset();
      return new Date(date.getTime() - offset * 60000).toISOString().slice(0, 10);
    }

    function generateReport() {
      const type = $("reportType").value;
      const range = dateRangeFor(type, $("reportDate").value || today());
      const items = schedules
        .filter((item) => item.date >= range.start && item.date <= range.end)
        .sort((a, b) => `${a.date} ${a.start_time || ""}`.localeCompare(`${b.date} ${b.start_time || ""}`));

      const total = items.length;
      const done = items.filter((item) => item.completed).length;
      const todo = total - done;
      const rate = total ? Math.round((done / total) * 100) : 0;
      const byCategory = items.reduce((acc, item) => {
        const name = getCategoryById(item.category_id)?.name || "其他";
        acc[name] = (acc[name] || 0) + 1;
        return acc;
      }, {});

      const lines = [];
      lines.push(`# ${range.title}`);
      lines.push("");
      lines.push(`报告范围：${range.start} 至 ${range.end}`);
      lines.push("");
      lines.push("## 一、整体情况");
      lines.push(`- 总日程：${total} 项`);
      lines.push(`- 已完成：${done} 项`);
      lines.push(`- 未完成：${todo} 项`);
      lines.push(`- 完成率：${rate}%`);
      lines.push("");
      lines.push("## 二、分类统计");
      Object.keys(byCategory).length
        ? Object.entries(byCategory).forEach(([category, count]) => lines.push(`- ${category}：${count} 项`))
        : lines.push("- 暂无数据");
      lines.push("");
      lines.push("## 三、已完成事项");
      appendItems(lines, items.filter((item) => item.completed), "暂无已完成事项");
      lines.push("");
      lines.push("## 四、未完成事项");
      appendItems(lines, items.filter((item) => !item.completed), "暂无未完成事项");
      lines.push("");
      lines.push("## 五、总结建议");
      if (!total) lines.push("本周期还没有记录日程。建议先添加要做的事情，再生成报告。");
      else if (rate >= 80) lines.push("整体完成情况较好，可以继续保持当前节奏，并复盘哪些安排最有效。");
      else if (rate >= 50) lines.push("完成情况中等，建议把未完成事项拆小，并优先处理最重要的任务。");
      else lines.push("完成率偏低，建议减少同一周期内的任务数量，先保证核心事项完成。");

      $("reportOutput").textContent = lines.join("\n");
    }

    function appendItems(lines, items, emptyText) {
      if (!items.length) {
        lines.push(`- ${emptyText}`);
        return;
      }
      items.forEach((item) => {
        const category = getCategoryById(item.category_id)?.name || "其他";
        const time = item.start_time || item.end_time ? `${item.start_time || "未填"}-${item.end_time || "未填"} ` : "";
        lines.push(`- [${item.date}] ${time}${item.title}（${category}）${item.description ? `：${item.description}` : ""}`);
      });
    }

    $("generateReport").addEventListener("click", generateReport);
    $("reportDate").addEventListener("input", generateReport);
    $("reportType").addEventListener("input", syncReportTabs);

    document.querySelectorAll("[data-report]").forEach((button) => {
      button.addEventListener("click", () => {
        $("reportType").value = button.dataset.report;
        syncReportTabs();
      });
    });

    function syncReportTabs() {
      document.querySelectorAll("[data-report]").forEach((button) => {
        button.classList.toggle("active", button.dataset.report === $("reportType").value);
      });
      generateReport();
    }

    $("copyReport").addEventListener("click", async () => {
      const text = $("reportOutput").textContent;
      if (!text.trim()) {
        alert("请先生成报告");
        return;
      }
      try {
        await navigator.clipboard.writeText(text);
        alert("报告已复制。");
      } catch {
        alert("复制失败，请手动选中报告内容复制。");
      }
    });

    $("downloadReport").addEventListener("click", () => {
      const text = $("reportOutput").textContent;
      if (!text.trim()) {
        alert("请先生成报告");
        return;
      }
      const range = dateRangeFor($("reportType").value, $("reportDate").value || today());
      const blob = new Blob([text], { type: "text/markdown;charset=utf-8" });
      const url = URL.createObjectURL(blob);
      const link = document.createElement("a");
      link.href = url;
      link.download = `${range.title}.md`;
      document.body.appendChild(link);
      link.click();
      link.remove();
      URL.revokeObjectURL(url);
    });

    function escapeHtml(text) {
      return String(text)
        .replaceAll("&", "&amp;")
        .replaceAll("<", "&lt;")
        .replaceAll(">", "&gt;")
        .replaceAll('"', "&quot;")
        .replaceAll("'", "&#039;");
    }

    init();
  </script>
</body>
</html>

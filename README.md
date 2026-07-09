# 增强版升级说明

这个增强版在原有日程管理的基础上，新增了三大功能：

- **灵感记录**：随时记录想法，支持分类标签
- **项目管理**：每个项目可添加多个任务/流程，可视化进度条
- **智能提醒**：设置时间提醒，到点浏览器自动弹窗通知

手机和电脑都打开同一个网址，登录同一个账号即可同步全部数据。

---

## 一、升级前确认

你之前已经在 Supabase 里创建过这两张表：

```text
categories
schedules
```

这次增强版需要**再新增 4 张表**：

```text
inspirations    灵感记录
projects        项目管理
project_tasks   项目流程/任务
reminders       提醒
```

## 二、升级数据库

1. 打开 [Supabase Dashboard](https://supabase.com/dashboard)
2. 进入你的项目
3. 左侧点击 **SQL Editor**
4. 点击 **New query**
5. 打开这个文件：

```text
schedule-report-tool-enhanced/supabase-upgrade.sql
```

6. 把里面的内容全部复制到 SQL Editor
7. 点击 **Run**

执行成功后，左侧 **Table Editor** 应该能看到 6 张表：

```text
categories
schedules
inspirations
projects
project_tasks
reminders
```

## 三、更新网站文件

这个增强版的网页文件是：

```text
schedule-report-tool-enhanced/index.html
```

### 如果你用 GitHub Pages

1. 打开你的 GitHub 仓库
2. 点击 `index.html`
3. 点击右上角 **Edit this file**（铅笔图标）
4. 删除原来所有内容
5. 把增强版 `index.html` 的内容全部复制进去
6. 页面底部点击 **Commit changes**
7. 等待 1 到 3 分钟，GitHub Pages 自动更新

### 如果你用 Netlify

1. 打开 [Netlify](https://www.netlify.com)
2. 进入你的站点
3. 点击 **Deploys**
4. 把新的 `index.html` 重新拖拽上传

### 如果你还没发布过

可以把整个文件夹上传：

```text
schedule-report-tool-enhanced
```

参考之前的发布教程，发布到 GitHub Pages 或 Netlify。

## 四、各功能介绍

### 1. 日程（原有功能）

- 新增日程、分类、日期、时间
- 筛选：全部 / 今天 / 本周 / 本月 / 已完成
- 生成日报 / 周报 / 月报
- 复制报告、下载报告

### 2. 灵感（新增）

- 快速记录想法，不用纠结格式
- 支持分类标签：创意、问题、想法、待研究等
- 按时间筛选和搜索
- 统计总灵感数、今日新增、分类数

### 3. 项目（新增）

- 创建项目，填写名称和描述
- 每个项目有 4 个状态：规划中 / 进行中 / 审核中 / 已完成
- 点击"管理流程"进入项目详情，添加具体任务
- 勾选完成任务，进度条自动更新
- 支持设置项目截止日期

### 4. 提醒（新增）

- 填写提醒标题和时间
- 打开页面后会弹出横幅请求浏览器通知权限
- 点击"开启提醒"允许后，到时间会弹窗通知
- 支持筛选：即将到期 / 全部 / 已过期

## 五、数据说明

- 所有数据保存在 Supabase 云端
- 登录同一个账号，手机电脑自动同步
- 不需要手动导出导入备份

## 六、常见问题

| 问题 | 处理 |
|---|---|
| 打开页面看不到新功能 | 刷新网页，或清理浏览器缓存 |
| 新增灵感报错 | 确认 SQL 脚本已执行，inspirations 表已创建 |
| 提醒不弹窗 | 确认浏览器已允许通知权限 |
| 项目进度不更新 | 检查 project_tasks 表是否已创建 |

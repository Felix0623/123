# LinkedIn酒店一线员工招聘信息类别梳理与字段归纳

## ——面向文本挖掘研究设计的系统化框架

---

# 第一部分：研究范围说明

## 1.1 酒店一线员工的纳入口径

本研究中"酒店一线员工"（Hotel Frontline Employees）的定义为：**直接参与宾客服务交付、客房维护、餐饮服务、礼宾接待、现场运营支持等面向顾客的岗位人员**。具体包括：

- **严格一线岗位**：直接与宾客互动或提供现场服务的岗位（如前台接待、客房服务员、餐厅服务员、礼宾员等）
- **一线基层管理岗**：直接管理一线员工且通常仍参与现场服务的督导岗位（如Front Office Supervisor、Housekeeping Supervisor），**单独标注，与纯一线岗位区分**
- **边缘纳入岗位**：如Security Officer、Spa Attendant等，视研究口径可纳入或排除，需在研究设计中明确说明

**排除范围**：中高层管理岗（如General Manager、Director of Operations）、纯后台岗位（如HR、Finance、IT）、非酒店行业的同名岗位（如写字楼Receptionist）。

## 1.2 国家/地区范围

- **全球覆盖**：本框架适用于LinkedIn全球平台上的酒店招聘信息
- **重点关注**：中国（含港澳）、美国、英国、阿联酋（迪拜）、东南亚（新加坡、泰国）、澳大利亚等酒店业发达地区
- **中国特殊说明**：LinkedIn已于2023年8月关闭中国区InCareer服务（来源：Tech Wire Asia, https://techwireasia.com/2023/05/after-a-long-struggle-linkedin-gives-up-on-china/ ），中国大陆酒店一线岗位招聘主要通过51Job、智联招聘、Boss直聘等本地平台进行。本研究如涉及中国酒店招聘，需特别注明数据来源平台并讨论LinkedIn数据的中国代表性局限。

## 1.3 LinkedIn页面与外部招聘页的区别

| 维度 | LinkedIn原生发布职位 | 第三方ATS同步职位 | 外部跳转（公司官网）|
|------|-------------------|-----------------|------------------|
| 数据来源 | 雇主直接在LinkedIn发布 | 通过Workday/Taleo等ATS自动同步至LinkedIn | LinkedIn仅显示摘要，点击跳转至公司官网 |
| 字段完整度 | LinkedIn标准字段齐全 | 部分字段可能缺失或格式不一 | LinkedIn页面字段精简，详细信息在外部页 |
| 申请方式 | Easy Apply（站内完成）| 可能Easy Apply或外部跳转 | 外部跳转至公司ATS |
| 文本挖掘影响 | 字段规范，适合自动化采集 | 需注意格式差异 | 需同时采集LinkedIn页面+外部页面 |

**来源**：LinkedIn官方Job Posting API Schema文档 (https://learn.microsoft.com/en-us/linkedin/talent/job-postings/api/job-posting-api-schema?view=li-lts-2025-10)；LinkedIn XML Feeds Development Guide (https://learn.microsoft.com/en-us/linkedin/talent/job-postings/xml-feeds-development-guide?view=li-lts-2025-10)

## 1.4 数据真实性边界说明

- 本文档中所有岗位名称、信息字段的归纳均基于：①LinkedIn官方帮助文档与API文档；②公开可访问的LinkedIn职位搜索结果页；③大型酒店集团官方招聘页面（Marriott、Hilton、IHG等）；④行业权威参考资源
- **凡无法通过上述来源验证的信息，均明确标注"需人工核查"**
- LinkedIn页面布局和字段显示可能随平台更新而变化，本文档基于截至2025年的公开信息
- 部分字段的显示取决于：雇主是否填写、地区法律要求（如薪资透明法）、用户登录状态、LinkedIn会员等级

---

# 第二部分：岗位类别名称总表

## 模块A：酒店一线岗位"类别名称体系"

### A1. 前厅/接待类（Front Office / Reception）

| 一级岗位类别 | 二级岗位类别 | LinkedIn常见英文岗位名 | 常见变体/别称 | 常见中文名称 | 所属部门 | 是否一线岗位 | 说明 | 来源链接 |
|------------|------------|---------------------|-------------|-----------|---------|-----------|------|---------|
| 前厅/接待类 | 前台接待 | Front Desk Agent | Front Desk Associate, Front Desk Clerk, Front Desk Representative | 前台接待员、前台 | Front Office | ✅ 严格一线 | 最常见的酒店前台岗位名称；Marriott/Hilton/IHG均使用 | https://careers.marriott.com/ ; https://jobs.hilton.com/ |
| 前厅/接待类 | 前台接待 | Front Office Agent | Front Office Associate, Front Office Clerk | 前厅接待员 | Front Office | ✅ 严格一线 | 与Front Desk Agent同义，部分酒店集团偏好此称呼 | https://careers.ihg.com/en/career-paths/hotel-jobs/front-of-house-jobs/ |
| 前厅/接待类 | 宾客服务 | Guest Service Agent | Guest Services Representative, Guest Service Associate, Guest Experience Agent, Guest Relations Agent | 宾客服务员、客户服务专员 | Front Office / Guest Services | ✅ 严格一线 | 强调服务导向；部分高端酒店使用"Guest Experience"强调体验 | https://www.siteminder.com/r/job-positions-hotel/ ; https://hospitalityinsights.ehl.edu/hospitality-manager |
| 前厅/接待类 | 前台接待 | Receptionist | Hotel Receptionist, Reception Agent | 接待员（仅酒店语境） | Front Office | ✅ 严格一线 | ⚠️ 该名称跨行业（写字楼、诊所等均使用），**仅在酒店/住宿场景下纳入研究** | https://www.shms.com/en/news/hotel-staff-positions/ |
| 前厅/接待类 | 迎宾/大堂 | Lobby Host | Lobby Ambassador, Lobby Attendant | 大堂迎宾、大堂服务员 | Front Office | ✅ 严格一线 | 高端/精品酒店可能使用；非所有酒店设此岗 | 综合归纳，非单一来源固定字段；需人工核查具体职位页面 |
| 前厅/接待类 | 夜间审计 | Night Auditor | Night Front Desk Agent, Night Audit Agent | 夜审、夜班前台 | Front Office / Accounting | ✅ 严格一线 | 负责夜间前台运营及日审核账务；在中小型酒店兼具前台职能 | https://www.siteminder.com/r/job-positions-hotel/ |
| 前厅/接待类 | 前厅督导 | Front Office Supervisor | Front Desk Supervisor, Guest Service Supervisor | 前厅主管、前台主管 | Front Office | ⚠️ 一线管理岗 | 属于基层管理，通常仍参与现场服务，单独标注 | https://hospitalityinsights.ehl.edu/hospitality-manager |

### A2. 礼宾/行李/迎宾类（Concierge / Bell / Door）

| 一级岗位类别 | 二级岗位类别 | LinkedIn常见英文岗位名 | 常见变体/别称 | 常见中文名称 | 所属部门 | 是否一线岗位 | 说明 | 来源链接 |
|------------|------------|---------------------|-------------|-----------|---------|-----------|------|---------|
| 礼宾类 | 礼宾 | Concierge | Hotel Concierge, Guest Concierge, Chief Concierge（管理级） | 礼宾员、礼宾师 | Concierge / Front Office | ✅ 严格一线 | 中高端酒店标配岗位；为宾客提供信息咨询、预订、推荐等服务 | https://climbtheladder.com/what-are-hotel-workers-called-job-titles-list/ ; https://www.shms.com/en/news/hotel-staff-positions/ |
| 礼宾类 | 行李服务 | Bell Attendant | Bellman, Bellperson, Bellhop, Bell Captain（管理级） | 行李员、门童 | Bell Services / Front Office | ✅ 严格一线 | Bellman/Bellhop为美式传统称呼；Bellperson为性别中立表达；Bell Captain属一线管理 | https://www.indeed.com/career-advice/finding-a-job/what-are-the-different-jobs-in-a-hotel |
| 礼宾类 | 搬运服务 | Porter | Luggage Porter, Hotel Porter | 行李搬运员、搬运工 | Bell Services | ✅ 严格一线 | 英式/欧洲酒店更常用Porter一词 | https://www.siteminder.com/r/job-positions-hotel/ |
| 礼宾类 | 门迎服务 | Doorman | Doorperson, Door Attendant | 门迎、门童 | Bell Services / Front Office | ✅ 严格一线 | 高端酒店设置；负责迎送宾客、车辆管理协调 | https://mundurek.com/article/list-of-restaurant-hotel-and-other-hospitality-industry-job-titles |
| 礼宾类 | 泊车服务 | Valet Attendant | Valet Parking Attendant, Valet Runner | 泊车员 | Valet / Front Office | ✅ 严格一线 | 部分酒店外包此岗位；在美国/中东较常见 | 综合归纳；需人工核查具体酒店LinkedIn页面 |
| 礼宾类 | 宾客迎宾 | Guest Arrival Ambassador | Arrival Experience Host | 迎宾大使 | Front Office / Guest Services | ✅ 严格一线 | 高端/奢华酒店品牌使用（如St. Regis, Ritz-Carlton等）；非标准化称呼 | 综合归纳，基于高端酒店品牌招聘页；需人工核查 |

### A3. 客房/保洁类（Housekeeping）

| 一级岗位类别 | 二级岗位类别 | LinkedIn常见英文岗位名 | 常见变体/别称 | 常见中文名称 | 所属部门 | 是否一线岗位 | 说明 | 来源链接 |
|------------|------------|---------------------|-------------|-----------|---------|-----------|------|---------|
| 客房类 | 客房清洁 | Room Attendant | Housekeeper, Housekeeping Attendant, Guest Room Attendant, Chambermaid（已较少使用） | 客房服务员、楼层服务员 | Housekeeping | ✅ 严格一线 | 最核心的客房岗位；Room Attendant和Housekeeper在LinkedIn上均高频出现 | https://careers.marriott.com/ ; https://www.siteminder.com/r/job-positions-hotel/ |
| 客房类 | 客房清洁 | Housekeeper | Hotel Housekeeper, Executive Housekeeper（管理级，非一线） | 保洁员、客房保洁 | Housekeeping | ✅ 严格一线 | ⚠️ "Executive Housekeeper"是管理岗，不纳入一线；"Housekeeper"在酒店语境指一线清洁 | https://www.shms.com/en/news/hotel-staff-positions/ |
| 客房类 | 公区清洁 | Public Area Attendant | Public Space Attendant, Public Area Cleaner, Lobby Attendant（清洁职能） | 公区保洁员 | Housekeeping | ✅ 严格一线 | 负责大堂、走廊、公共卫生间等区域清洁 | https://www.indeed.com/career-advice/finding-a-job/what-are-the-different-jobs-in-a-hotel |
| 客房类 | 布草服务 | Laundry Attendant | Linen Attendant, Laundry Operator | 布草/洗衣房服务员 | Housekeeping / Laundry | ✅ 严格一线 | 部分大型酒店设独立洗衣部门 | https://climbtheladder.com/what-are-hotel-workers-called-job-titles-list/ |
| 客房类 | 夜床服务 | Turndown Attendant | Evening Attendant, Turndown Housekeeper | 夜床服务员 | Housekeeping | ✅ 严格一线 | 高端酒店提供夜床服务；部分酒店由Room Attendant兼任 | 综合归纳，非单一来源固定字段；高端酒店品牌网站可见 |
| 客房类 | 客房督导 | Housekeeping Supervisor | Floor Supervisor, Housekeeping Team Leader | 客房主管、楼层主管 | Housekeeping | ⚠️ 一线管理岗 | 检查房间质量、分配任务；仍参与现场操作 | https://www.siteminder.com/r/job-positions-hotel/ |

### A4. 餐饮服务类（Food & Beverage Service）

| 一级岗位类别 | 二级岗位类别 | LinkedIn常见英文岗位名 | 常见变体/别称 | 常见中文名称 | 所属部门 | 是否一线岗位 | 说明 | 来源链接 |
|------------|------------|---------------------|-------------|-----------|---------|-----------|------|---------|
| 餐饮服务类 | 餐厅服务 | Server | Waiter, Waitress, Food & Beverage Server, F&B Attendant, Restaurant Server, Dining Room Server | 餐厅服务员 | F&B / Restaurant | ✅ 严格一线 | Server是LinkedIn上最通用的餐饮服务称呼；Waiter/Waitress为传统称呼，性别化表达正减少 | https://www.indeed.com/career-advice/finding-a-job/what-are-the-different-jobs-in-a-hotel |
| 餐饮服务类 | 传菜 | Food Runner | Expo, Food Expeditor | 传菜员 | F&B / Kitchen | ✅ 严格一线 | 连接厨房与餐厅的桥梁岗位 | https://mundurek.com/article/list-of-restaurant-hotel-and-other-hospitality-industry-job-titles |
| 餐饮服务类 | 清桌 | Busser | Bus Person, Bus Boy/Girl（已较少使用）, Dining Room Attendant | 清桌员、餐厅杂务 | F&B / Restaurant | ✅ 严格一线 | 美式酒店/餐厅更常用此称呼 | https://mundurek.com/article/list-of-restaurant-hotel-and-other-hospitality-industry-job-titles |
| 餐饮服务类 | 迎宾/领位 | Host / Hostess | Restaurant Host, Hostess, Greeter, Maître d'（高端） | 迎宾员、领位员 | F&B / Restaurant | ✅ 严格一线 | Hostess为传统称呼；现代趋向使用Host作为性别中立表达 | https://www.indeed.com/career-advice/finding-a-job/what-are-the-different-jobs-in-a-hotel |
| 餐饮服务类 | 餐厅通用 | Restaurant Attendant | F&B Attendant, Dining Attendant | 餐饮服务员 | F&B | ✅ 严格一线 | 通用性较强的称呼，涵盖多种餐饮服务职能 | 综合归纳 |
| 餐饮服务类 | 酒吧服务 | Bartender | Barista（仅咖啡）, Bar Attendant, Mixologist（高端） | 调酒师、酒吧服务员 | F&B / Bar | ✅ 严格一线 | Bartender在LinkedIn上频率最高；Bar Attendant更偏辅助性 | https://www.indeed.com/career-advice/finding-a-job/what-are-the-different-jobs-in-a-hotel |
| 餐饮服务类 | 酒吧辅助 | Bar Attendant | Bar Back, Bar Helper | 酒吧服务员（辅助） | F&B / Bar | ✅ 严格一线 | 协助调酒师，准备原材料、清洁吧台 | 综合归纳 |
| 餐饮服务类 | 宴会服务 | Banquet Server | Banquet Attendant, Banquet Waiter, Conference & Banqueting Server | 宴会服务员 | F&B / Banquet | ✅ 严格一线 | 大型酒店/会议中心必备岗位 | https://careers.marriott.com/ |
| 餐饮服务类 | 送餐服务 | Room Service Attendant | In-Room Dining Attendant, Room Service Server, IRD Attendant | 送餐员、客房送餐服务员 | F&B / Room Service | ✅ 严格一线 | 高端酒店更倾向使用"In-Room Dining"称呼 | 综合归纳 |
| 餐饮服务类 | 自助餐服务 | Buffet Attendant | Cafeteria Attendant, Breakfast Attendant | 自助餐服务员 | F&B | ✅ 严格一线 | 负责自助餐台补充、清洁、服务 | 综合归纳 |

### A5. 厨房辅助类（Kitchen Support）

| 一级岗位类别 | 二级岗位类别 | LinkedIn常见英文岗位名 | 常见变体/别称 | 常见中文名称 | 所属部门 | 是否一线岗位 | 说明 | 来源链接 |
|------------|------------|---------------------|-------------|-----------|---------|-----------|------|---------|
| 厨房辅助类 | 管事 | Steward | Kitchen Steward, Dishwasher Steward | 管事员、厨房管事 | Kitchen / Stewarding | ⚠️ 视口径 | 负责餐具清洗、厨房清洁；不直接面客但属于一线运营支持 | https://www.siteminder.com/r/job-positions-hotel/ |
| 厨房辅助类 | 洗碗 | Dishwasher | Dish Machine Operator, Kitchen Helper（部分重叠） | 洗碗工 | Kitchen / Stewarding | ⚠️ 视口径 | 基础厨房辅助岗位 | https://www.indeed.com/career-advice/finding-a-job/what-are-the-different-jobs-in-a-hotel |
| 厨房辅助类 | 厨房助手 | Kitchen Helper | Kitchen Assistant, Kitchen Porter, Commis（初级厨师，视口径） | 厨房助手 | Kitchen | ⚠️ 视口径 | Kitchen Porter为英式称呼；Commis属于初级厨师而非辅助，研究口径需明确 | https://climbtheladder.com/what-are-hotel-workers-called-job-titles-list/ |

### A6. 休闲与宾客服务类（Leisure & Guest Services）

| 一级岗位类别 | 二级岗位类别 | LinkedIn常见英文岗位名 | 常见变体/别称 | 常见中文名称 | 所属部门 | 是否一线岗位 | 说明 | 来源链接 |
|------------|------------|---------------------|-------------|-----------|---------|-----------|------|---------|
| 休闲服务类 | SPA服务 | Spa Attendant | Spa Therapist（如含技术操作）, Spa Host | SPA服务员 | Spa / Recreation | ✅ 严格一线 | 度假型酒店核心岗位；Spa Therapist可能需要专业证书 | 综合归纳 |
| 休闲服务类 | SPA接待 | Spa Receptionist | Spa Front Desk, Wellness Receptionist | SPA接待员 | Spa / Recreation | ✅ 严格一线 | 负责SPA区域的预约和接待 | 综合归纳 |
| 休闲服务类 | 泳池服务 | Pool Attendant | Lifeguard（如有救生职责）, Pool Host | 泳池服务员 | Recreation | ✅ 严格一线 | 度假酒店常见；可能需要救生资质 | 综合归纳 |
| 休闲服务类 | 健身服务 | Fitness Attendant | Gym Attendant, Fitness Center Attendant | 健身中心服务员 | Recreation / Fitness | ✅ 严格一线 | 大型酒店/度假村设置 | 综合归纳 |
| 休闲服务类 | 康乐通用 | Recreation Attendant | Activities Attendant, Activities Coordinator（偏管理） | 康乐服务员 | Recreation | ✅ 严格一线 | 度假村类酒店更常见 | 综合归纳 |
| 休闲服务类 | 儿童服务 | Kids Club Attendant | Children's Activity Host, Kid's Club Counselor | 儿童俱乐部服务员 | Recreation | ✅ 严格一线 | 家庭度假型酒店/度假村设置 | 综合归纳 |

### A7. 安保与现场服务类（Security & On-site Services）

| 一级岗位类别 | 二级岗位类别 | LinkedIn常见英文岗位名 | 常见变体/别称 | 常见中文名称 | 所属部门 | 是否一线岗位 | 说明 | 来源链接 |
|------------|------------|---------------------|-------------|-----------|---------|-----------|------|---------|
| 安保类 | 安全保卫 | Security Officer | Hotel Security, Security Guard | 保安员 | Security / Loss Prevention | ⚠️ 视口径 | 不直接提供"酒店服务"但属于现场运营一线；视研究口径纳入 | https://www.indeed.com/career-advice/finding-a-job/what-are-the-different-jobs-in-a-hotel |
| 安保类 | 损失预防 | Loss Prevention Officer | Loss Prevention Agent, Asset Protection Officer | 损失预防员 | Security / Loss Prevention | ⚠️ 视口径 | 大型酒店集团（Marriott, Hilton）设有专门LP部门 | 综合归纳 |

### A8. 中国及亚洲语境下的特殊岗位名称对照

| 中文常见岗位名 | 对应英文名称 | LinkedIn搜索建议关键词 | 备注 |
|-------------|-----------|---------------------|------|
| 酒店前台 | Front Desk Agent, Receptionist | "front desk" AND "hotel" | 中国本地平台更常用"酒店前台"而非"前厅接待" |
| 前厅接待 | Front Office Agent | "front office" AND "hotel" | 正式称呼，培训教材常用 |
| 宾客服务员 | Guest Service Agent | "guest service" AND "hotel" | 高端酒店品牌在中国也使用英文称呼 |
| 礼宾员 | Concierge | "concierge" AND "hotel" | 国际品牌酒店在中国保留英文称呼 |
| 行李员 | Bell Attendant, Bellman | "bell" AND "hotel" | — |
| 客房服务员 | Room Attendant, Housekeeper | "room attendant" OR "housekeeper" AND "hotel" | — |
| 保洁员 | Housekeeper, Public Area Attendant | "housekeeper" AND "hotel" | "保洁员"在中国可能泛指非酒店清洁 |
| 餐厅服务员 | Server, Waiter/Waitress | "server" OR "waiter" AND "hotel" | — |
| 迎宾员 | Host/Hostess, Greeter | "host" AND "restaurant" AND "hotel" | — |
| 宴会服务员 | Banquet Server | "banquet" AND "server" AND "hotel" | — |
| 酒吧服务员 | Bartender, Bar Attendant | "bartender" AND "hotel" | — |
| 客服专员（仅酒店） | Guest Service Representative | "guest service" AND "hotel" | ⚠️ 需限定酒店语境，否则与电商/电信客服混淆 |
| 康乐服务员 | Recreation Attendant | "recreation" AND "hotel" | 度假型酒店 |
| 温泉/SPA接待 | Spa Receptionist, Spa Attendant | "spa" AND "hotel" | — |
| 楼层服务员 | Floor Attendant, Room Attendant | "floor attendant" OR "room attendant" | 中国酒店行业特有分层称呼 |

**来源说明**：中文岗位名称的对照基于国际酒店集团中国区招聘页面惯例（如Marriott中国、Hilton中国、IHG中国官方招聘页面）以及行业培训标准的综合归纳。具体对应关系可能因酒店品牌不同而有差异。

---

# 第三部分：招聘网页信息类别总表

## 模块B：LinkedIn酒店招聘网页"全部信息类别体系"

### B1. 职位基础标识信息

| 一级类别 | 二级类别 | 字段/信息类别名称 | 中文说明 | 典型页面表现 | 是否LinkedIn标准字段 | 出现频率 | 文本挖掘价值 | 适合编码方式 | 来源链接 | 备注 |
|---------|---------|----------------|---------|-----------|-------------------|---------|-----------|-----------|---------|------|
| 职位基础标识 | 职位名称 | Job Title | 职位名称 | 页面顶部最大字体显示，如"Front Desk Agent" | ✅ 必有标准字段 | 100% | 🔴 核心 | 结构化提取 + 文本分类 | LinkedIn API Schema (https://learn.microsoft.com/en-us/linkedin/talent/job-postings/api/job-posting-api-schema?view=li-lts-2025-10) | XML feed中对应`<title>`字段，最多200字符 |
| 职位基础标识 | 公司名称 | Company Name | 发布招聘的公司名称 | 职位名称下方，带公司logo和LinkedIn公司页链接 | ✅ 必有标准字段 | 100% | 🔴 核心 | 结构化提取 | 同上 | 必须为真实公司名称，不允许"Confidential"等占位符 |
| 职位基础标识 | 公司Logo | Company Logo | 公司品牌标识图片 | 职位名称左侧或上方 | ✅ 标准字段 | 约95%+ | 🟡 低 | 图像识别（超出文本挖掘范围） | 综合归纳 | 来自公司LinkedIn主页 |
| 职位基础标识 | LinkedIn职位URL | Job Posting URL | 职位在LinkedIn上的唯一链接 | 浏览器地址栏，格式如linkedin.com/jobs/view/XXXXXXXXX | ✅ 平台生成 | 100% | 🔴 核心 | 结构化提取（作为唯一标识符） | 综合归纳 | URL中包含LinkedIn内部Job ID |
| 职位基础标识 | 职位ID | Job ID / Partner Job ID | LinkedIn内部或ATS同步的职位编号 | 部分页面在URL或页面底部可见；API中为`partnerJobId` | ✅ 标准字段（API层） | 页面层不一定可见 | 🟡 中 | 结构化提取 | LinkedIn XML Feeds Guide (https://learn.microsoft.com/en-us/linkedin/talent/job-postings/xml-feeds-development-guide?view=li-lts-2025-10) | ATS同步时必须提供 |
| 职位基础标识 | 发布时间 | Posted Date / Date Posted | 职位发布或最后更新的时间 | "Posted X days/weeks ago" 或 "Reposted X days ago" | ✅ 标准字段 | 100% | 🔴 核心 | 结构化提取（时间戳） | 综合归纳，基于LinkedIn职位搜索页面通用显示 | LinkedIn显示相对时间而非绝对日期 |
| 职位基础标识 | 申请方式 | Apply Method | Easy Apply（站内申请）或外部申请 | 绿色"Easy Apply"按钮 或 "Apply"按钮跳转外部 | ✅ 标准字段 | 100% | 🟠 中高 | 二分类结构化变量 | https://www.autoapplymax.com/blog/linkedin-easy-apply-guide ; https://www.jobscan.co/blog/linkedin-easy-apply-employers/ | Easy Apply岗位信息更完整，外部申请需跳转 |
| 职位基础标识 | 申请人数 | Number of Applicants | 已申请该职位的人数 | "X applicants" 显示在职位标题附近 | ✅ 标准字段（Easy Apply更常显示） | 60-80%（估计） | 🟠 中高 | 结构化提取（数值） | https://itentio.com/blog/linkedin-number-of-applicants/ ; https://www.clrn.org/how-does-linkedin-know-how-many-applicants/ | Easy Apply岗位通常显示；外部申请可能不显示或显示"High applicant volume" |
| 职位基础标识 | 推广标识 | Promoted / Sponsored | 是否为付费推广职位 | 可能显示"Promoted"标签 | ✅ 标准字段 | 部分职位 | 🟡 低-中 | 二分类结构化变量 | 综合归纳 | 影响职位排序和可见度 |

### B2. 工作地点与用工形式

| 一级类别 | 二级类别 | 字段/信息类别名称 | 中文说明 | 典型页面表现 | 是否LinkedIn标准字段 | 出现频率 | 文本挖掘价值 | 适合编码方式 | 来源链接 | 备注 |
|---------|---------|----------------|---------|-----------|-------------------|---------|-----------|-----------|---------|------|
| 工作地点 | 地点 | Location | 工作所在地（国家、州/省、城市） | 职位名称下方，如"New York, NY, United States" | ✅ 必有标准字段 | 100% | 🔴 核心 | 结构化提取（地理编码） | LinkedIn API Schema | XML feed要求格式："City, State"(US) 或 "City, Country"(非US) |
| 工作地点 | 多地点 | Alternate Locations | 多个工作地点 | 部分职位显示多个可选地点 | ✅ 可选标准字段 | 低频 | 🟡 中 | 结构化提取 | LinkedIn API Schema | API支持`alternateLocations`字段 |
| 工作地点 | 工作模式 | Workplace Type | 现场/混合/远程 | 标签形式显示"On-site"/"Hybrid"/"Remote" | ✅ 标准字段 | 90%+ | 🔴 核心 | 分类结构化变量 | 综合归纳，LinkedIn职位搜索筛选器标准选项 | 酒店一线岗位几乎全部为"On-site" |
| 工作地点 | 详细地址 | Specific Address | 更精确的工作地址（酒店名称+地址） | 部分出现在职位描述正文中 | ❌ 非标准字段 | 部分职位 | 🟡 中 | NLP提取（从描述文本中识别地址） | 综合归纳 | LinkedIn标准仅显示到城市级别 |
| 用工形式 | 住宿/派遣 | Relocation / Housing | 是否提供员工住宿或异地派遣支持 | 出现在职位描述或福利部分，如"Staff accommodation provided" | ❌ 非标准字段 | 低-中频 | 🟠 中高 | NLP提取（关键词/正则匹配） | 综合归纳 | 度假村/偏远地区酒店更常出现 |

### B3. 职位属性字段

| 一级类别 | 二级类别 | 字段/信息类别名称 | 中文说明 | 典型页面表现 | 是否LinkedIn标准字段 | 出现频率 | 文本挖掘价值 | 适合编码方式 | 来源链接 | 备注 |
|---------|---------|----------------|---------|-----------|-------------------|---------|-----------|-----------|---------|------|
| 职位属性 | 雇佣类型 | Employment Type | 全职/兼职/合同/临时/实习/志愿者 | 职位详情区域标签显示，如"Full-time" | ✅ 标准字段 | 90%+ | 🔴 核心 | 分类结构化变量 | LinkedIn API Schema: employmentType字段，枚举值包括FULL_TIME, PART_TIME, CONTRACT, TEMPORARY, VOLUNTEER, INTERNSHIP | 酒店一线以Full-time和Part-time为主 |
| 职位属性 | 资历级别 | Seniority Level | 入门/初级/中级/高级/总监/高管 | 职位详情区域标签显示，如"Entry level" | ✅ 标准字段 | 85%+ | 🔴 核心 | 有序分类变量 | LinkedIn API Schema: seniorityLevel字段，枚举值包括ENTRY_LEVEL, ASSOCIATE, MID_SENIOR, DIRECTOR, EXECUTIVE | 酒店一线岗位主要为Entry level或Associate |
| 职位属性 | 职能类别 | Job Function | 职位所属职能领域 | 职位详情区域，如"Hospitality" | ✅ 标准字段 | 80%+ | 🟠 中高 | 分类结构化变量 | LinkedIn API Schema: jobFunction字段，可为数组 | 酒店一线通常为"Hospitality""Food Service""Customer Service"等 |
| 职位属性 | 所属行业 | Industry | 公司/职位所属行业 | 职位详情区域，如"Hospitality" | ✅ 标准字段 | 80%+ | 🟠 中高 | 分类结构化变量 | LinkedIn API Schema: industry字段 | 酒店通常为"Hospitality""Hotels & Resorts" |
| 职位属性 | 排班/轮班 | Shift / Schedule | 工作班次要求（早班/晚班/夜班/轮班/周末） | 出现在职位描述正文中，如"Must be available to work weekends and holidays" | ❌ 非标准字段 | 中-高频 | 🟠 中高 | NLP提取（关键词匹配/主题分析） | 综合归纳 | 酒店一线岗位高频出现排班要求 |
| 职位属性 | 部门归属 | Department | 岗位所属酒店部门 | 部分出现在职位描述中，如"Front Office Department" | ❌ 非标准字段 | 中频 | 🟡 中 | NLP提取 | 综合归纳 | — |
| 职位属性 | 汇报对象 | Reports To | 该岗位的直接上级 | 部分出现在职位描述中，如"Reports to Front Office Manager" | ❌ 非标准字段 | 低-中频 | 🟡 中 | NLP提取 | 综合归纳 | 有助于理解组织层级 |

### B4. 薪酬与福利信息

| 一级类别 | 二级类别 | 字段/信息类别名称 | 中文说明 | 典型页面表现 | 是否LinkedIn标准字段 | 出现频率 | 文本挖掘价值 | 适合编码方式 | 来源链接 | 备注 |
|---------|---------|----------------|---------|-----------|-------------------|---------|-----------|-----------|---------|------|
| 薪酬信息 | 薪资范围 | Salary Range | 薪资的最低和最高范围 | 职位标题下方或详情区域，如"$15.00/hr - $18.00/hr" | ✅ 标准字段（雇主选填或平台估算） | 地区差异大 | 🔴 核心 | 结构化提取（数值+单位） | https://fantastic.jobs/article/salary-transparency ; LinkedIn职位页面通用显示 | 美国CO/NY/CA/WA等州法律要求披露；中国仅约4%职位披露薪资 |
| 薪酬信息 | 薪资来源标识 | Salary Source Indicator | 薪资数据来源（雇主提供 vs. LinkedIn估算） | 可能标注"Employer-provided salary" 或 "Estimated salary" | ✅ 标准字段 | 有薪资显示时出现 | 🟠 中高 | 二分类结构化变量 | 综合归纳 | 区分"真实薪资"和"估算薪资"对研究至关重要 |
| 薪酬信息 | 薪资单位 | Pay Period | 按小时/日/周/月/年计薪 | "$15.00/hr" 或 "$32,000/yr" | ✅ 随薪资字段 | 有薪资时出现 | 🔴 核心 | 分类结构化变量 | 综合归纳 | 酒店一线岗位（美国）多为时薪制 |
| 薪酬信息 | 币种 | Currency | 薪资的货币单位 | "$"（美元）、"£"（英镑）、"AED"等 | ✅ 随薪资字段 | 有薪资时出现 | 🟡 中 | 结构化提取 | 综合归纳 | 跨国比较研究时需统一币种 |
| 福利信息 | 福利概述 | Benefits | 标准福利信息 | 标签或列表形式，如"Health insurance, 401(k), Paid time off" | ✅ 标准字段（部分） | 50-70% | 🟠 中高 | 结构化提取 + NLP分类 | 综合归纳，基于LinkedIn职位页面通用显示 | LinkedIn可能以标签形式显示常见福利 |
| 福利信息 | 酒店特色福利 | Hotel-Specific Benefits | 酒店行业特有福利（员工折扣、免费住宿、员工餐等） | 出现在职位描述正文中，如"Associate discount at hotel properties" | ❌ 非标准字段 | 中-高频 | 🟠 中高 | NLP提取（关键词/正则） | 综合归纳 | 酒店行业特色——员工住宿折扣、免费员工餐等 |
| 福利信息 | 小费/服务费 | Tips / Service Charge / Gratuity | 是否涉及小费收入 | 出现在职位描述中，如"Tips included" 或 薪资注明"plus tips" | ❌ 非标准字段 | 部分职位（餐饮类更多） | 🟠 中高 | NLP提取 | 综合归纳 | 美国餐饮服务类岗位常见；中国几乎不涉及 |
| 福利信息 | 签证支持 | Visa Sponsorship / Relocation Support | 是否提供工作签证或搬迁支持 | 出现在职位描述中，如"Visa sponsorship available" 或 "Must be authorized to work in the US" | ❌ 非标准字段 | 低-中频 | 🟠 中高 | NLP提取（关键词匹配） | 综合归纳 | 中东（迪拜）酒店较常见签证支持说明 |

### B5. 岗位职责信息

| 一级类别 | 二级类别 | 字段/信息类别名称 | 中文说明 | 典型页面表现 | 是否LinkedIn标准字段 | 出现频率 | 文本挖掘价值 | 适合编码方式 | 来源链接 | 备注 |
|---------|---------|----------------|---------|-----------|-------------------|---------|-----------|-----------|---------|------|
| 岗位职责 | 职位描述正文 | Job Description (Full Text) | 职位的完整描述文本 | 页面主体区域，可能包含HTML格式（项目符号列表、段落等） | ✅ 必有标准字段 | 100% | 🔴🔴 最核心 | 全文本NLP分析（主题模型/情感分析/语义分析） | LinkedIn API Schema: description字段，100-25,000字符，支持部分HTML | **这是文本挖掘的核心对象**——所有非结构化信息均嵌入其中 |
| 岗位职责 | 核心职责 | Key Responsibilities / Duties | 岗位主要职责列表 | 通常以"Responsibilities"或"What you'll do"为小标题，项目符号列出 | ❌ 非标准字段（嵌入职位描述） | 90%+ | 🔴 核心 | NLP提取（段落分割+主题分析） | 综合归纳 | 结构通常为项目符号列表 |
| 岗位职责 | 服务对象 | Service Target | 服务的对象类型（住客、餐厅客人、会议客人等） | 嵌入职位描述，如"Provide exceptional service to guests" | ❌ 非标准字段 | 高频 | 🟠 中高 | NLP提取 | 综合归纳 | — |
| 岗位职责 | 服务标准 | Service Standards | 服务品质标准（如Forbes五星标准、品牌标准等） | 嵌入职位描述，如"Maintain Forbes Five-Star standards" | ❌ 非标准字段 | 中频（高端酒店更多） | 🟠 中高 | NLP提取 | 综合归纳 | 品牌差异比较的重要文本 |
| 岗位职责 | KPI/绩效 | Performance Metrics | 绩效考核要求 | 嵌入职位描述，如"Achieve guest satisfaction scores above 90%" | ❌ 非标准字段 | 低-中频 | 🟠 中高 | NLP提取 | 综合归纳 | 部分职位明确列出 |
| 岗位职责 | 设备/系统 | Systems / Technology Used | 需使用的系统或设备（Opera PMS, Micros等） | 嵌入职位描述或要求，如"Experience with Opera PMS preferred" | ❌ 非标准字段 | 中频 | 🟡 中 | NLP提取（命名实体识别） | 综合归纳 | 酒店特有PMS系统为重要技能指标 |
| 岗位职责 | 安全/卫生 | Health & Safety Duties | 清洁、卫生、安全相关职责 | 嵌入职位描述，如"Adhere to all health and safety protocols" | ❌ 非标准字段 | 高频 | 🟡 中 | NLP提取 | 综合归纳 | COVID后此类要求显著增加 |
| 岗位职责 | 跨部门协作 | Cross-departmental Collaboration | 与其他部门的协作要求 | 嵌入职位描述，如"Coordinate with housekeeping and engineering teams" | ❌ 非标准字段 | 中频 | 🟡 中 | NLP提取 | 综合归纳 | — |

### B6. 任职资格与招聘要求

| 一级类别 | 二级类别 | 字段/信息类别名称 | 中文说明 | 典型页面表现 | 是否LinkedIn标准字段 | 出现频率 | 文本挖掘价值 | 适合编码方式 | 来源链接 | 备注 |
|---------|---------|----------------|---------|-----------|-------------------|---------|-----------|-----------|---------|------|
| 任职资格 | 学历要求 | Education Requirements | 最低学历要求 | 嵌入职位描述，如"High school diploma or equivalent required" | ❌ 非标准字段 | 中-高频 | 🔴 核心 | NLP提取 + 有序分类编码 | 综合归纳 | 酒店一线通常要求高中/同等学历 |
| 任职资格 | 工作经验 | Experience Requirements | 所需工作经验年限 | 嵌入职位描述，如"Minimum 1 year of hotel front desk experience" | ❌ 非标准字段 | 高频 | 🔴 核心 | NLP提取 + 数值编码 | 综合归纳 | — |
| 任职资格 | 行业经验 | Hospitality Experience | 酒店/餐饮行业特定经验 | 嵌入职位描述，如"Prior hotel experience preferred" | ❌ 非标准字段 | 高频 | 🟠 中高 | NLP提取 | 综合归纳 | — |
| 任职资格 | 语言要求 | Language Requirements | 所需语言能力 | 嵌入职位描述，如"Bilingual English/Spanish preferred" | ❌ 非标准字段 | 中-高频 | 🔴 核心 | NLP提取 + 多标签分类 | 综合归纳 | 跨国酒店多语言要求突出 |
| 任职资格 | 证书/执照 | Certifications / Licenses | 专业证书或执照要求 | 嵌入职位描述，如"Food Handler's Certificate required" | ❌ 非标准字段 | 中频 | 🟠 中高 | NLP提取（命名实体） | 综合归纳 | 餐饮类（Food Handler）、酒水类（TIPS certified）、安保类等 |
| 任职资格 | 技能要求 | Skills Requirements | 硬技能要求（软件、工具等） | 嵌入职位描述 + LinkedIn技能标签 | 部分为LinkedIn标准技能标签 | 高频 | 🔴 核心 | 结构化（标签）+ NLP提取（描述文本） | 综合归纳 | LinkedIn自动从描述中提取技能标签 |
| 任职资格 | 软技能 | Soft Skills | 人际沟通、团队合作、服务意识等 | 嵌入职位描述，如"Excellent communication and interpersonal skills" | ❌ 非标准字段 | 高频 | 🔴 核心 | NLP提取 + 分类编码 | 综合归纳 | 酒店一线岗位软技能要求突出 |
| 任职资格 | 体能要求 | Physical Requirements | 体力/体能要求 | 嵌入职位描述，如"Ability to stand for extended periods" "Lift up to 50 lbs" | ❌ 非标准字段 | 中-高频 | 🟠 中高 | NLP提取 | 综合归纳 | 客房/行李/厨房类岗位更常见 |
| 任职资格 | 仪容仪表 | Grooming / Appearance Standards | 仪容仪表要求 | 嵌入职位描述，如"Professional appearance and grooming standards" | ❌ 非标准字段 | 中频 | 🟡 中 | NLP提取 | 综合归纳 | 高端酒店更为强调 |
| 任职资格 | 排班可用性 | Availability / Scheduling Flexibility | 班次灵活性要求 | 嵌入职位描述，如"Must be available to work flexible hours including weekends, holidays, and evenings" | ❌ 非标准字段 | 高频 | 🟠 中高 | NLP提取 | 综合归纳 | 酒店一线几乎必有此要求 |
| 任职资格 | 法律合规 | Legal / Work Authorization | 工作许可、年龄限制等 | 嵌入职位描述，如"Must be at least 18 years old" "Legally authorized to work in the US" | ❌ 非标准字段 | 中-高频 | 🟡 中 | NLP提取 | 综合归纳 | 酒水服务可能有年龄要求 |
| 任职资格 | 优先条件 | Preferred Qualifications | 加分项/优先条件 | 通常以"Preferred"或"Nice to have"小标题，与"Required"分开 | ❌ 非标准字段 | 高频 | 🟠 中高 | NLP提取（区分Required vs. Preferred） | 综合归纳 | 区分"必备"和"优先"对研究设计重要 |

### B7. 公司与雇主信息

| 一级类别 | 二级类别 | 字段/信息类别名称 | 中文说明 | 典型页面表现 | 是否LinkedIn标准字段 | 出现频率 | 文本挖掘价值 | 适合编码方式 | 来源链接 | 备注 |
|---------|---------|----------------|---------|-----------|-------------------|---------|-----------|-----------|---------|------|
| 公司信息 | 公司简介 | Company Description / About | 公司概况 | 页面侧边栏或底部，来自公司LinkedIn主页 | ✅ 标准字段 | 90%+ | 🟠 中高 | 雇主品牌话语分析 | 综合归纳 | 部分内容也嵌入职位描述正文开头 |
| 公司信息 | 公司规模 | Company Size | 员工人数范围 | 侧边栏，如"10,001+ employees" | ✅ 标准字段 | 85%+ | 🟡 中 | 结构化分类变量 | 综合归纳 | 来自公司LinkedIn主页 |
| 公司信息 | 公司行业 | Company Industry | 公司所属行业 | 侧边栏，如"Hospitality" | ✅ 标准字段 | 85%+ | 🟡 中 | 结构化分类变量 | 综合归纳 | — |
| 公司信息 | 公司类型 | Company Type | 上市/私营/非营利等 | 侧边栏 | ✅ 标准字段 | 部分显示 | 🟡 低-中 | 结构化分类变量 | 综合归纳 | — |
| 公司信息 | 公司总部 | Headquarters Location | 总部所在地 | 侧边栏 | ✅ 标准字段 | 80%+ | 🟡 中 | 结构化提取 | 综合归纳 | — |
| 公司信息 | 品牌/集团 | Brand / Parent Company | 酒店品牌及母公司 | 嵌入职位描述或公司简介中 | ❌ 非标准字段 | 中-高频 | 🟠 中高 | NLP提取 + 人工映射 | 综合归纳 | 如"Courtyard by Marriott"——品牌为Courtyard，集团为Marriott |
| 公司信息 | 公司价值观/文化 | Company Values / Culture | 企业文化、价值观描述 | 嵌入职位描述或公司简介，如"We are committed to..." | ❌ 非标准字段（嵌入描述） | 中-高频 | 🔴 核心 | NLP雇主品牌话语分析 + 情感分析 | 综合归纳 | **雇主品牌研究的核心文本** |
| 公司信息 | DEI声明 | DEI / Diversity & Inclusion Statement | 多样性、公平与包容声明 | 通常在职位描述末尾，如"We celebrate diversity and are committed to creating an inclusive environment" | ❌ 非标准字段（嵌入描述） | 中-高频（欧美更常见） | 🟠 中高 | NLP提取 + 话语分析 | 综合归纳 | 地区差异大——美国/英国/澳洲高频，亚洲相对低频 |
| 公司信息 | 雇主品牌宣传 | Employer Branding Content | 雇主品牌营销文案 | 嵌入职位描述开头或结尾，如"Join our award-winning team..." | ❌ 非标准字段 | 中-高频 | 🔴 核心 | NLP情感分析 + 话语分析 | 综合归纳 | **适合做雇主品牌话语分析** |

### B8. 招聘流程与申请信息

| 一级类别 | 二级类别 | 字段/信息类别名称 | 中文说明 | 典型页面表现 | 是否LinkedIn标准字段 | 出现频率 | 文本挖掘价值 | 适合编码方式 | 来源链接 | 备注 |
|---------|---------|----------------|---------|-----------|-------------------|---------|-----------|-----------|---------|------|
| 招聘流程 | 申请方式 | Application Method | Easy Apply或外部申请 | 申请按钮 | ✅ 标准字段 | 100% | 见B1 | 见B1 | 见B1 | — |
| 招聘流程 | 申请截止日期 | Application Deadline | 申请截止时间 | 部分职位在描述中提及 | ❌ 非标准字段（LinkedIn不强制） | 低频 | 🟡 低 | 结构化提取（日期） | 综合归纳 | Colorado州法律要求列明关闭日期 |
| 招聘流程 | 筛选问题 | Screening Questions | 雇主设置的预筛选问题 | Easy Apply流程中出现（申请者可见，采集侧不一定可见） | ✅ 标准字段（Easy Apply功能） | 仅Easy Apply | 🟡 中 | 结构化分类 | https://www.autoapplymax.com/blog/linkedin-easy-apply-guide | 采集者可能无法获取此信息 |
| 招聘流程 | 面试流程 | Interview Process | 面试步骤说明 | 嵌入职位描述中 | ❌ 非标准字段 | 低频 | 🟡 低-中 | NLP提取 | 综合归纳 | — |
| 招聘流程 | 招聘负责人 | Job Poster / Recruiter | 发布职位的招聘人员信息 | 页面显示职位发布者姓名、头像、职称 | ✅ 标准字段（部分可见） | 中-高频 | 🟡 低 | 结构化提取 | 综合归纳 | 登录状态下通常可见 |
| 招聘流程 | 背景调查 | Background Check Requirements | 是否需要背景调查/体检 | 嵌入职位描述，如"Background check required" | ❌ 非标准字段 | 中频 | 🟡 中 | NLP提取 | 综合归纳 | — |

### B9. 合规与声明信息

| 一级类别 | 二级类别 | 字段/信息类别名称 | 中文说明 | 典型页面表现 | 是否LinkedIn标准字段 | 出现频率 | 文本挖掘价值 | 适合编码方式 | 来源链接 | 备注 |
|---------|---------|----------------|---------|-----------|-------------------|---------|-----------|-----------|---------|------|
| 合规声明 | EEO声明 | Equal Opportunity Employer Statement | 平等就业机会声明 | 职位描述末尾，标准化法律文本 | ❌ 非标准字段（嵌入描述） | 高频（欧美） | 🟡 中 | NLP提取 + 存在/不存在编码 | 综合归纳 | 美国联邦法律建议但不强制；大公司几乎必有 |
| 合规声明 | 隐私声明 | Privacy Notice | 数据使用与隐私声明 | 部分出现在职位描述末尾或链接跳转 | ❌ 非标准字段 | 低-中频 | 🟡 低 | 存在/不存在编码 | 综合归纳 | GDPR相关地区更常见 |
| 合规声明 | 薪资透明声明 | Pay Transparency Statement | 薪资透明法合规声明 | 部分美国州（CO/NY/CA/WA）的职位描述中 | ❌ 非标准字段 | 地区性（美国特定州） | 🟠 中高 | NLP提取 + 编码 | https://salarytransparencycheck.com/state-laws ; https://www.forbes.com/sites/alonzomartinez/2024/06/14/2024-state-by-state-pay-transparency-laws-key-insights-for-employers/ | **中外差异比较的重要字段** |
| 合规声明 | 无障碍声明 | Accessibility Statement | 残障人士无障碍声明 | 部分出现在职位描述末尾 | ❌ 非标准字段 | 低-中频 | 🟡 低-中 | 存在/不存在编码 | 综合归纳 | — |
| 合规声明 | 安全审查声明 | Security Clearance / Drug Testing | 安全审查/药物检测声明 | 嵌入职位描述，如"Pre-employment drug screening required" | ❌ 非标准字段 | 低-中频 | 🟡 中 | NLP提取 | 综合归纳 | 美国酒店部分岗位要求 |

### B10. 平台侧附加信息

| 一级类别 | 二级类别 | 字段/信息类别名称 | 中文说明 | 典型页面表现 | 是否LinkedIn标准字段 | 出现频率 | 文本挖掘价值 | 适合编码方式 | 来源链接 | 备注 |
|---------|---------|----------------|---------|-----------|-------------------|---------|-----------|-----------|---------|------|
| 平台信息 | 技能标签 | Skills Tags | LinkedIn自动提取的技能标签 | 职位详情区域，如蓝色标签"Customer Service""Hospitality" | ✅ LinkedIn生成 | 80%+ | 🟠 中高 | 结构化提取 | https://www.clrn.org/how-does-linkedin-know-how-many-applicants/ | LinkedIn NLP自动从描述中提取 |
| 平台信息 | 技能匹配 | Skill Match Indicator | 用户技能与职位要求的匹配提示 | 登录状态下显示"You have X of Y skills" | ✅ LinkedIn生成（个人化） | 登录时显示 | 🟡 低 | 不适合采集（个人化内容） | 综合归纳 | 因人而异，不适合大规模采集 |
| 平台信息 | 相似职位 | Similar Jobs | LinkedIn推荐的相似职位 | 页面底部模块 | ✅ LinkedIn生成 | 高频 | 🟡 低 | — | 综合归纳 | — |
| 平台信息 | 校友信息 | Alumni at Company | 同校校友在该公司的人数 | 登录状态下侧边栏，如"12 alumni from your school work here" | ✅ LinkedIn生成（个人化） | 登录时显示 | 🟡 低 | 不适合大规模采集 | https://www.clrn.org/how-does-linkedin-know-how-many-applicants/ | 个人化信息 |
| 平台信息 | 公司洞察 | Company Insights | 公司员工分布、增长趋势、部门构成 | 侧边栏"Insights"模块 | ✅ LinkedIn生成 | 中-高频 | 🟡 中 | 可辅助采集公司维度数据 | https://blog.hootsuite.com/linkedin-analytics/ | 来自LinkedIn aggregated数据 |
| 平台信息 | 招聘方活跃度 | Recruiter Activity | 招聘方是否活跃（如"Actively recruiting"徽章） | 职位标题附近或招聘者名片 | ✅ LinkedIn生成 | 部分职位 | 🟡 中 | 二分类编码 | 综合归纳 | — |
| 平台信息 | 申请人数 | Applicant Count | 见B1详述 | 见B1 | ✅ | 见B1 | 见B1 | 见B1 | 见B1 | — |

### B11. 文本挖掘编码建议汇总

| 信息类别 | 更适合结构化变量 | 更适合文本主题分析 | 更适合情感/语气分析 | 更适合招聘要求强度分析 | 更适合中外差异比较 | 更适合雇主品牌话语分析 |
|---------|---------------|----------------|------------------|-------------------|-----------------|-------------------|
| 职位名称 | ✅ | | | | ✅ | |
| 公司名称 | ✅ | | | | | |
| 发布时间 | ✅ | | | | | |
| 地点 | ✅ | | | | ✅ | |
| 工作模式 | ✅ | | | | | |
| 雇佣类型 | ✅ | | | | | |
| 资历级别 | ✅ | | | | | |
| 薪资范围 | ✅ | | | | ✅ | |
| 职位描述全文 | | ✅ | ✅ | ✅ | ✅ | ✅ |
| 核心职责 | | ✅ | | ✅ | ✅ | |
| 服务标准 | | ✅ | | ✅ | ✅ | |
| 学历要求 | ✅（有序） | | | ✅ | ✅ | |
| 工作经验 | ✅（数值） | | | ✅ | ✅ | |
| 语言要求 | ✅（多标签） | | | | ✅ | |
| 软技能要求 | | ✅ | | ✅ | ✅ | |
| 体能要求 | | | | ✅ | ✅ | |
| 排班要求 | | | | ✅ | ✅ | |
| 公司价值观 | | ✅ | ✅ | | ✅ | ✅ |
| DEI声明 | ✅（有/无） | | ✅ | | ✅ | ✅ |
| 雇主品牌文案 | | ✅ | ✅ | | ✅ | ✅ |
| EEO声明 | ✅（有/无） | | | | ✅ | |
| 薪资透明声明 | ✅（有/无） | | | | ✅ | |
| 福利信息 | ✅（标签）| ✅（描述部分） | | | ✅ | ✅ |
| 酒店特色福利 | | ✅ | | | ✅ | ✅ |
| 技能标签 | ✅ | | | | | |
| 申请方式 | ✅ | | | | | |
| 申请人数 | ✅ | | | | | |

---

# 第四部分：中外招聘页面差异提示

> ⚠️ **重要声明**：以下差异总结仅基于本文档引用的实际来源归纳，不代表所有情况。具体差异需研究者在数据采集后通过实证分析验证。

| 差异维度 | 国外（欧美澳为主）LinkedIn页面 | 中国相关情况 | 来源依据 |
|---------|---------------------------|-----------|---------|
| **平台可用性** | LinkedIn为主要招聘平台之一 | LinkedIn已于2023年8月关闭中国区InCareer服务；中国酒店招聘主要通过51Job、智联招聘、Boss直聘 | https://techwireasia.com/2023/05/after-a-long-struggle-linkedin-gives-up-on-china/ ; https://hrone.com/blog/do-people-use-linkedin-in-china-the-surprising-truth/ ; https://teamedupchina.com/ultimate-guide-to-chinese-job-boards/ |
| **薪资公开程度** | 高——美国特定州（CO/NY/CA/WA）法律要求披露薪资范围；英国/澳洲亦趋向透明；奥地利高达86%职位公开薪资 | 极低——中国仅约4%的职位公开薪资信息；文化上薪资属于私人话题 | https://fantastic.jobs/article/salary-transparency |
| **岗位名称语言** | 英文为主；部分非英语国家使用当地语言 | 国际品牌酒店可能同时使用中英文岗位名称；本土酒店以中文为主 | 综合归纳 |
| **EEO/合规声明** | 高频出现——美国联邦建议，大公司几乎必有EEO声明、DEI声明 | 中国招聘广告中几乎不出现EEO相关声明；劳动合规表述方式不同 | 综合归纳 |
| **语言要求** | 英语为基本要求；双语/多语言为加分项（西班牙语、法语等） | 普通话为基本要求；英语为加分项（国际品牌酒店可能要求英语） | 综合归纳 |
| **公司介绍长度** | 中-长；通常包含品牌故事、文化价值观、发展历史 | 相对简短；更侧重实际岗位信息 | 综合归纳，需人工核查 |
| **福利描述** | 详细列举——保险、401(k)/养老金、带薪休假、员工折扣等 | 较简略——可能提及五险一金、餐补、住宿，但描述粒度通常较低 | 综合归纳，需人工核查 |
| **体能要求** | 明确列出——如"stand for 8 hours""lift 50 lbs"等 | 较少明确列出体能要求 | 综合归纳，需人工核查 |
| **薪资透明法声明** | CO/NY/CA/WA等州要求在招聘广告中披露薪资范围和福利 | 无对应法律要求 | https://salarytransparencycheck.com/state-laws |

---

# 第五部分：适合后续文本挖掘的字段优先级建议

## 5.1 核心必抓字段（所有研究场景均需）

| 字段 | 理由 | 采集方式 |
|------|------|---------|
| Job Title（职位名称） | 岗位分类的基础 | 结构化提取 |
| Company Name（公司名称） | 雇主识别 | 结构化提取 |
| Location（工作地点） | 地理分析的基础 | 结构化提取 |
| Full Job Description（职位描述全文） | **文本挖掘的核心对象** | 全文本采集 |
| Employment Type（雇佣类型） | 基础分类变量 | 结构化提取 |
| Seniority Level（资历级别） | 岗位层级筛选 | 结构化提取 |
| Posted Date（发布时间） | 时间序列分析 | 结构化提取 |
| Job URL / Job ID（职位链接/ID） | 唯一标识符，去重必需 | 结构化提取 |
| Apply Method（申请方式） | Easy Apply vs. 外部申请区分 | 结构化提取 |

## 5.2 建议抓取字段（丰富研究维度）

| 字段 | 理由 | 采集方式 |
|------|------|---------|
| Salary Range（薪资范围） | 薪酬研究核心 | 结构化提取（如有） |
| Workplace Type（工作模式） | On-site/Hybrid/Remote分类 | 结构化提取 |
| Job Function（职能类别） | 辅助岗位分类 | 结构化提取 |
| Industry（行业） | 确认酒店行业 | 结构化提取 |
| Skills Tags（技能标签） | LinkedIn自动提取的技能 | 结构化提取 |
| Company Size（公司规模） | 组织层面变量 | 结构化提取 |
| Number of Applicants（申请人数） | 岗位吸引力指标 | 结构化提取（如有） |

## 5.3 低频但高价值字段（提升研究深度）

| 字段 | 理由 | 采集方式 |
|------|------|---------|
| 服务标准描述 | 品牌服务水平研究 | NLP从描述文本提取 |
| 系统/设备要求（如Opera PMS） | 技术能力需求分析 | NLP命名实体识别 |
| 酒店品牌/集团信息 | 品牌层面比较 | NLP提取 + 人工映射 |
| DEI声明内容 | 多样性话语分析 | NLP提取 |
| 雇主品牌宣传文案 | 雇主品牌研究 | NLP情感/话语分析 |
| 签证支持/搬迁支持 | 国际劳动力流动研究 | NLP关键词匹配 |
| 小费/服务费信息 | 薪酬结构研究 | NLP关键词匹配 |

## 5.4 仅在部分地区抓取字段

| 字段 | 适用地区 | 理由 |
|------|---------|------|
| Pay Transparency Statement（薪资透明声明） | 美国CO/NY/CA/WA等州 | 法规驱动字段 |
| Application Closing Date（申请截止日） | 美国Colorado州 | CO法律要求 |
| Drug Testing Statement（药物检测声明） | 美国 | 美国法律/行业惯例 |
| 员工住宿提供 | 度假村/偏远地区/中东 | 地理特殊性 |
| 工会相关说明 | 美国/欧洲特定地区 | 劳动关系研究相关 |

---

# 第六部分：参考来源清单

以下为本文档引用的全部来源，按类别整理：

## LinkedIn官方/微软官方文档

| 编号 | 来源名称 | URL | 用途 |
|------|---------|-----|------|
| S1 | LinkedIn Job Posting API Schema - Microsoft Learn | https://learn.microsoft.com/en-us/linkedin/talent/job-postings/api/job-posting-api-schema?view=li-lts-2025-10 | API字段定义 |
| S2 | LinkedIn XML Feeds Development Guide - Microsoft Learn | https://learn.microsoft.com/en-us/linkedin/talent/job-postings/xml-feeds-development-guide?view=li-lts-2025-10 | XML Feed必需/可选字段 |
| S3 | LinkedIn Third-Party Job Listing Guidelines - Microsoft Learn | https://learn.microsoft.com/en-us/linkedin/talent/job-postings/xml-feeds-job-posting-guidelines?view=li-lts-2025-10 | 职位发布规则 |
| S4 | LinkedIn Create Jobs API - Microsoft Learn | https://learn.microsoft.com/en-us/linkedin/talent/job-postings/api/create-jobs?view=li-lts-2025-10 | 创建职位API |

## 酒店集团官方招聘页面

| 编号 | 来源名称 | URL | 用途 |
|------|---------|-----|------|
| S5 | Marriott International Careers | https://careers.marriott.com/ | 岗位名称核验 |
| S6 | Marriott Hotel Career Journeys | https://careers.marriott.com/career-journeys/hotel/ | 酒店岗位分类 |
| S7 | Hilton Careers | https://jobs.hilton.com/us/en | 岗位名称核验 |
| S8 | Hilton Hotel Career Areas | https://jobs.hilton.com/us/en/career-areas-hotel | 酒店岗位分类 |
| S9 | IHG Hotel Jobs & Hospitality Careers | https://careers.ihg.com/en/ | 岗位名称核验 |
| S10 | IHG Front of House Jobs | https://careers.ihg.com/en/career-paths/hotel-jobs/front-of-house-jobs/ | 一线岗位分类 |
| S11 | IHG Hotel Jobs | https://careers.ihg.com/en/career-paths/hotel-jobs/ | 酒店岗位分类 |

## 酒店行业参考资源

| 编号 | 来源名称 | URL | 用途 |
|------|---------|-----|------|
| S12 | SiteMinder - Hotel Positions: Types of Jobs in the Hotel Industry | https://www.siteminder.com/r/job-positions-hotel/ | 酒店岗位分类参考 |
| S13 | EHL Hospitality Insights - Hotel Staff Positions | https://hospitalityinsights.ehl.edu/hospitality-manager | 酒店岗位管理参考 |
| S14 | SHMS - Hotel Staff Positions: Roles, Qualifications, and Growth | https://www.shms.com/en/news/hotel-staff-positions/ | 酒店岗位列表 |
| S15 | CLIMB - What Are Hotel Workers Called: Job Titles List | https://climbtheladder.com/what-are-hotel-workers-called-job-titles-list/ | 岗位名称变体 |
| S16 | Indeed - 38 Types of Hotel Jobs You Can Pursue | https://www.indeed.com/career-advice/finding-a-job/what-are-the-different-jobs-in-a-hotel | 酒店岗位列表 |
| S17 | Mundurek - List of Restaurant, Hotel, and Other Hospitality Industry Job Titles | https://mundurek.com/article/list-of-restaurant-hotel-and-other-hospitality-industry-job-titles | 酒店/餐饮岗位名称 |
| S18 | HotelTalk - Main Positions and Titles in Hotels & Resorts | https://hoteltalk.app/hotel-positions-and-titles/ | 岗位分类参考 |
| S19 | TTEC Jobs - Hospitality Job Description: Titles & Skill Sets | https://www.ttecjobs.com/en/hospitality-job-description-titles-and-skill-sets | 酒店岗位技能描述 |

## LinkedIn使用指南与分析资源

| 编号 | 来源名称 | URL | 用途 |
|------|---------|-----|------|
| S20 | Breezy HR - LinkedIn Job Posting: A Complete Guide | https://breezy.hr/blog/linkedin-job-posting | LinkedIn职位发布字段说明 |
| S21 | Recooty - How to Post a Job on LinkedIn (2025) | https://recooty.com/blog/how-to-post-a-job-on-linkedin/ | LinkedIn发布流程 |
| S22 | Bardeen - LinkedIn Job Posting Guide 2024 | https://www.bardeen.ai/answers/how-to-post-a-job-on-linkedin | LinkedIn发布字段 |
| S23 | AutoApplyMax - LinkedIn Easy Apply: Complete Guide | https://www.autoapplymax.com/blog/linkedin-easy-apply-guide | Easy Apply机制 |
| S24 | JobScan - Everything You Need to Know About LinkedIn Easy Apply | https://www.jobscan.co/blog/linkedin-easy-apply-employers/ | Easy Apply与外部申请差异 |
| S25 | LinkedHelper - LinkedIn Easy Apply: How It Works | https://www.linkedhelper.com/blog/linkedin-easy-apply/ | Easy Apply流程 |
| S26 | ATSCVChecker - LinkedIn Easy Apply vs Direct Apply | https://www.atscvchecker.pro/blog/linkedin-easy-apply-ats-guide/ | Easy Apply与ATS关系 |
| S27 | Vettio - How Does LinkedIn Easy Apply Work | https://vettio.com/blog/how-does-linkedin-easy-apply-work/ | Easy Apply机制 |
| S28 | itentio - How Accurate is LinkedIn Number of Applicants | https://itentio.com/blog/linkedin-number-of-applicants/ | 申请人数显示机制 |
| S29 | CLRN - How Does LinkedIn Know How Many Applicants | https://www.clrn.org/how-does-linkedin-know-how-many-applicants/ | 申请人数与技能标签 |
| S30 | Hootsuite - How to Use LinkedIn Analytics (2024) | https://blog.hootsuite.com/linkedin-analytics/ | LinkedIn公司洞察功能 |

## 中国LinkedIn与本地招聘平台

| 编号 | 来源名称 | URL | 用途 |
|------|---------|-----|------|
| S31 | Tech Wire Asia - LinkedIn Gives Up on China | https://techwireasia.com/2023/05/after-a-long-struggle-linkedin-gives-up-on-china/ | LinkedIn中国退出背景 |
| S32 | HROne - Do People Use LinkedIn in China? | https://hrone.com/blog/do-people-use-linkedin-in-china-the-surprising-truth/ | LinkedIn中国使用情况 |
| S33 | TeamedUp China - Ultimate Guide to Chinese Job Boards | https://teamedupchina.com/ultimate-guide-to-chinese-job-boards/ | 中国本地招聘平台 |

## 薪资透明法律

| 编号 | 来源名称 | URL | 用途 |
|------|---------|-----|------|
| S34 | fantastic.jobs - Global Salary Transparency in Job Postings 2025 | https://fantastic.jobs/article/salary-transparency | 全球薪资透明率对比 |
| S35 | Salary Transparency Check - State Laws | https://salarytransparencycheck.com/state-laws | 美国各州薪资透明法 |
| S36 | Forbes - 2024 State-By-State Pay Transparency Laws | https://www.forbes.com/sites/alonzomartinez/2024/06/14/2024-state-by-state-pay-transparency-laws-key-insights-for-employers/ | 美国薪资透明法 |
| S37 | Mosey - Salary Transparency Laws by State (2024) | https://mosey.com/blog/salary-transparency-laws-by-state-best-practices/ | 美国薪资透明法 |
| S38 | ADP - Complying with Colorado Pay Transparency Law | https://www.adp.com/spark/articles/2024/04/complying-with-the-colorado-pay-transparency-law.aspx | CO州具体要求 |
| S39 | Diversity Employment - Pay Transparency Laws by State | https://diversityemployment.com/legal-government-economic-news/pay-transparency-laws-by-state-current-rules-and-whats-next/ | 美国薪资透明法综述 |

## LinkedIn API与技术文档

| 编号 | 来源名称 | URL | 用途 |
|------|---------|-----|------|
| S40 | Postman - LinkedIn Talent Solutions Job Posting API | https://www.postman.com/linkedin-developer-apis/linkedin-talent-solutions/documentation/ycpzuyn/job-posting | API字段验证 |
| S41 | DEV Community - LinkedIn Jobs API | https://dev.to/eunit/linkedin-jobs-api-36m7 | API字段参考 |
| S42 | LinkedIn API Overview - Microsoft Learn | https://learn.microsoft.com/en-us/linkedin/talent/job-postings/api/sync-job-postings?view=li-lts-2025-10 | API同步机制 |

---

# 附录：研究设计建议

## 数据采集策略建议

1. **优先采集LinkedIn原生页面结构化字段**（Job Title, Company, Location, Employment Type, Seniority Level, Workplace Type, Salary Range等）——这些字段格式规范，适合批量结构化处理
2. **全文本采集Job Description字段**——这是文本挖掘的核心对象，包含职责、要求、福利、合规声明等全部非结构化信息
3. **区分Easy Apply与外部申请职位**——两类职位的信息完整度不同，分析时需作为控制变量或分层变量
4. **建立岗位名称标准化映射表**——根据本文第二部分的岗位名称变体表，将采集到的Job Title统一映射为标准化岗位类别
5. **记录采集时间戳**——LinkedIn显示的是相对发布时间（"X days ago"），采集时需记录实际采集日期以推算绝对发布日期

## 文本挖掘分析路径建议

| 分析目标 | 推荐方法 | 适用字段 |
|---------|---------|---------|
| 岗位职责主题结构 | LDA主题模型 / BERTopic | 职位描述全文 - 职责部分 |
| 技能需求分类 | 命名实体识别(NER) + 技能分类器 | 任职资格部分 + 技能标签 |
| 招聘要求强度 | 关键词频率 + 强度词典(Required/Preferred/Must/Should) | 任职资格部分 |
| 雇主品牌话语 | 情感分析 + 话语分析框架 | 公司价值观 + 雇主品牌文案 |
| 中外差异比较 | 交叉分类 + 文本统计特征比较 | 所有字段（以国家为分组变量） |
| 薪酬透明度分析 | 二分类 + 回归分析 | 薪资范围有/无 × 地区 × 公司规模 |
| DEI话语分析 | 词典法 + 主题模型 | DEI声明 + EEO声明 |

---

> **免责声明**：本文档为学术研究设计参考框架，所有信息基于公开可访问的来源整理。LinkedIn平台字段和页面布局可能随时更新，研究者在正式采集数据前应进行最新的人工核验。所有标注"综合归纳"的内容系基于多个来源的综合判断，非单一页面固定显示内容。标注"需人工核查"的内容表示存在不确定性，建议在实际采集中验证。

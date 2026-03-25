<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>故土与新途</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        
        :root {
            --primary: #1a1a1a;
            --accent: #b83a3a;
            --gold: #c9a962;
            --gray: #888;
            --light: #fafafa;
            --beige: #f7f5f0;
        }
        
        html { scroll-behavior: smooth; }
        
        body {
            font-family: "Noto Serif SC", "Songti SC", "SimSun", serif;
            background: #fff;
            color: var(--primary);
            line-height: 2;
            overflow-x: hidden;
        }
        
        /* 动画定义 */
        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(60px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        @keyframes scaleIn {
            from { opacity: 0; transform: scale(0.8); }
            to { opacity: 1; transform: scale(1); }
        }
        
        @keyframes slideInLeft {
            from { opacity: 0; transform: translateX(-100px); }
            to { opacity: 1; transform: translateX(0); }
        }
        
        @keyframes slideInRight {
            from { opacity: 0; transform: translateX(100px); }
            to { opacity: 1; transform: translateX(0); }
        }
        
        @keyframes countUp {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }
        
        @keyframes lineGrow {
            from { width: 0; }
            to { width: 100%; }
        }
        
        .animate { opacity: 0; }
        .animate.show { animation: fadeInUp 1s ease forwards; }
        .animate-delay-1 { animation-delay: 0.2s; }
        .animate-delay-2 { animation-delay: 0.4s; }
        .animate-delay-3 { animation-delay: 0.6s; }
        
        /* 首屏 */
        .hero {
            min-height: 100vh;
            background: linear-gradient(135deg, #1a1a1a 0%, #2d2d2d 50%, #1a1a1a 100%);
            color: #fff;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 60px 40px;
            position: relative;
            overflow: hidden;
        }
        
        .hero::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url("data:image/svg+xml,%3Csvg width='60' height='60' viewBox='0 0 60 60' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='none' fill-rule='evenodd'%3E%3Cg fill='%23ffffff' fill-opacity='0.03'%3E%3Cpath d='M36 34v-4h-2v4h-4v2h4v4h2v-4h4v-2h-4zm0-30V0h-2v4h-4v2h4v4h2V6h4V4h-4zM6 34v-4H4v4H0v2h4v4h2v-4h4v-2H6zM6 4V0H4v4H0v2h4v4h2V6h4V4H6z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
            opacity: 0.5;
        }
        
        .hero-content {
            position: relative;
            z-index: 1;
        }
        
        .hero-subtitle {
            font-size: 14px;
            letter-spacing: 8px;
            color: var(--gold);
            margin-bottom: 30px;
            animation: fadeIn 2s ease;
        }
        
        .hero h1 {
            font-size: clamp(48px, 12vw, 120px);
            font-weight: 700;
            letter-spacing: 20px;
            margin-bottom: 40px;
            animation: scaleIn 1.5s ease;
        }
        
        .hero-line {
            width: 100px;
            height: 2px;
            background: var(--gold);
            margin: 0 auto 40px;
            animation: lineGrow 2s ease forwards;
        }
        
        .hero-desc {
            font-size: 18px;
            color: #aaa;
            max-width: 600px;
            line-height: 2;
            animation: fadeInUp 2s ease 0.5s both;
        }
        
        .scroll-indicator {
            position: absolute;
            bottom: 40px;
            left: 50%;
            transform: translateX(-50%);
            animation: pulse 2s infinite;
        }
        
        /* 章节通用 */
        .section {
            padding: 120px 40px;
            max-width: 900px;
            margin: 0 auto;
        }
        
        .section-dark {
            background: var(--primary);
            color: #fff;
        }
        
        .section-beige {
            background: var(--beige);
        }
        
        .section-header {
            text-align: center;
            margin-bottom: 80px;
        }
        
        .section-num {
            font-size: 12px;
            color: var(--accent);
            letter-spacing: 4px;
            margin-bottom: 20px;
        }
        
        .section-title {
            font-size: 42px;
            font-weight: 700;
            margin-bottom: 20px;
            line-height: 1.3;
        }
        
        .section-subtitle {
            font-size: 16px;
            color: var(--gray);
            max-width: 600px;
            margin: 0 auto;
        }
        
        /* 数据展示 */
        .data-showcase {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 60px;
            margin: 100px 0;
        }
        
        .data-item {
            text-align: center;
            position: relative;
        }
        
        .data-item::after {
            content: '';
            position: absolute;
            right: -30px;
            top: 50%;
            transform: translateY(-50%);
            width: 1px;
            height: 60px;
            background: #ddd;
        }
        
        .data-item:last-child::after {
            display: none;
        }
        
        .data-number {
            font-size: 72px;
            font-weight: 700;
            color: var(--accent);
            line-height: 1;
            margin-bottom: 16px;
            font-family: -apple-system, sans-serif;
        }
        
        .data-label {
            font-size: 14px;
            color: var(--gray);
            margin-bottom: 8px;
        }
        
        .data-source {
            font-size: 12px;
            color: #bbb;
        }
        
        /* 时间轴图表 */
        .timeline-chart {
            margin: 80px 0;
            position: relative;
        }
        
        .timeline-line {
            position: absolute;
            left: 0;
            right: 0;
            top: 50%;
            height: 2px;
            background: linear-gradient(90deg, var(--accent) 0%, transparent 100%);
        }
        
        .timeline-items {
            display: flex;
            justify-content: space-between;
            position: relative;
        }
        
        .timeline-node {
            text-align: center;
            flex: 1;
            position: relative;
        }
        
        .timeline-dot {
            width: 16px;
            height: 16px;
            background: var(--accent);
            border-radius: 50%;
            margin: 0 auto 20px;
            position: relative;
            z-index: 1;
            box-shadow: 0 0 0 6px rgba(184, 58, 58, 0.2);
        }
        
        .timeline-year {
            font-size: 24px;
            font-weight: 700;
            margin-bottom: 8px;
        }
        
        .timeline-value {
            font-size: 14px;
            color: var(--gray);
        }
        
        /* 地图区域 */
        .map-section {
            background: var(--light);
            padding: 120px 40px;
        }
        
        .map-container {
            max-width: 800px;
            margin: 0 auto;
        }
        
        .map-visual {
            background: #fff;
            border-radius: 16px;
            padding: 60px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.08);
        }
        
        /* 故事卡片 */
        .story-grid {
            display: grid;
            gap: 60px;
        }
        
        .story-card {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 60px;
            align-items: center;
        }
        
        .story-card.reverse {
            direction: rtl;
        }
        
        .story-card.reverse > * {
            direction: ltr;
        }
        
        .story-visual {
            background: var(--beige);
            border-radius: 12px;
            padding: 60px;
            text-align: center;
        }
        
        .story-big-num {
            font-size: 120px;
            font-weight: 700;
            color: var(--accent);
            line-height: 1;
            margin-bottom: 20px;
        }
        
        .story-content {
            padding: 20px 0;
        }
        
        .story-location {
            font-size: 12px;
            color: var(--accent);
            letter-spacing: 3px;
            margin-bottom: 16px;
        }
        
        .story-title {
            font-size: 28px;
            font-weight: 700;
            margin-bottom: 24px;
            line-height: 1.4;
        }
        
        .story-text {
            font-size: 16px;
            color: #444;
            margin-bottom: 20px;
        }
        
        blockquote {
            border-left: 3px solid var(--accent);
            padding: 20px 24px;
            background: var(--light);
            margin: 30px 0;
            font-style: italic;
        }
        
        blockquote p {
            font-size: 18px;
            margin-bottom: 12px;
        }
        
        blockquote cite {
            font-size: 14px;
            color: var(--gray);
            font-style: normal;
        }
        
        /* 数据对比 */
        .compare-table {
            width: 100%;
            border-collapse: collapse;
            margin: 60px 0;
            font-size: 15px;
        }
        
        .compare-table th {
            background: var(--primary);
            color: #fff;
            padding: 20px;
            text-align: left;
            font-weight: 600;
            letter-spacing: 1px;
        }
        
        .compare-table td {
            padding: 20px;
            border-bottom: 1px solid #eee;
        }
        
        .compare-table tr:hover {
            background: var(--light);
        }
        
        .trend-down {
            color: var(--accent);
            font-weight: 600;
        }
        
        /* 统计条形图 */
        .bar-chart {
            margin: 60px 0;
        }
        
        .bar-item {
            display: flex;
            align-items: center;
            margin: 20px 0;
        }
        
        .bar-label {
            width: 100px;
            font-size: 14px;
            color: var(--gray);
        }
        
        .bar-track {
            flex: 1;
            height: 40px;
            background: #f0f0f0;
            border-radius: 4px;
            overflow: hidden;
            position: relative;
        }
        
        .bar-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--accent) 0%, #d47474 100%);
            border-radius: 4px;
            position: relative;
            transition: width 1.5s ease;
        }
        
        .bar-value {
            position: absolute;
            right: 16px;
            top: 50%;
            transform: translateY(-50%);
            color: #fff;
            font-weight: 600;
            font-size: 14px;
        }
        
        /* 页脚 */
        footer {
            background: var(--primary);
            color: #fff;
            padding: 100px 40px;
            text-align: center;
        }
        
        footer h2 {
            font-size: 48px;
            margin-bottom: 30px;
            letter-spacing: 8px;
        }
        
        footer p {
            color: #888;
            font-size: 14px;
            line-height: 2;
            max-width: 600px;
            margin: 0 auto;
        }
        
        .footer-divider {
            width: 60px;
            height: 1px;
            background: var(--gold);
            margin: 40px auto;
        }
        
        /* 响应式 */
        @media (max-width: 768px) {
            .data-showcase {
                grid-template-columns: 1fr;
                gap: 40px;
            }
            
            .data-item::after {
                display: none;
            }
            
            .story-card {
                grid-template-columns: 1fr;
            }
            
            .story-card.reverse {
                direction: ltr;
            }
            
            .section {
                padding: 80px 24px;
            }
            
            .section-title {
                font-size: 28px;
            }
            
            .hero h1 {
                letter-spacing: 10px;
            }
        }
    </style>
</head>
<body>

<!-- 首屏 -->
<header class="hero">
    <div class="hero-content">
        <div class="hero-subtitle">乡村教育纪实</div>
 <h1>故土与新途</h1>
        <div class="hero-line"></div>
        <p class="hero-desc">
            2011年至2024年，中国乡村小学从12.4万所降至7.8万所。<br>
            我们走访了那些曾经承载几代人记忆的校园，<br>
            记录下撤并浪潮中，学生、教师与乡村的真实故事。
        </p>
    </div>
    <div class="scroll-indicator">
        <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="#666" stroke-width="1">
            <path d="M12 5v14M19 12l-7 7-7-7"/>
        </svg>
    </div>
</header>

<!-- 数据概览 -->
<section class="section">
    <div class="section-header">
        <div class="section-num">01</div>
        <h2 class="section-title">数字的变化</h2>
        <p class="section-subtitle">十三年间，超过4.6万所乡村小学成为历史</p>
    </div>
    
    <div class="data-showcase">
        <div class="data-item animate">
            <div class="data-number" data-count="12.4">12.4万</div>
            <div class="data-label">2011年乡村小学数量</div>
            <div class="data-source">来源：教育部统计公报</div>
        </div>
        <div class="data-item animate animate-delay-1">
            <div class="data-number" data-count="7.8">7.8万</div>
            <div class="data-label">2024年乡村小学数量</div>
            <div class="data-source">来源：教育部统计公报</div>
        </div>
        <div class="data-item animate animate-delay-2">
            <div class="data-number" data-count="37">37%</div>
            <div class="data-label">学校数量降幅</div>
            <div class="data-source">年均减少约3500所</div>
        </div>
    </div>
    
    <!-- 趋势条形图 -->
    <div class="bar-chart">
        <div class="bar-item">
            <div class="bar-label">2011年</div>
            <div class="bar-track">
                <div class="bar-fill" style="width: 100%;">
                    <span class="bar-value">12.4万所</span>
                </div>
            </div>
        </div>
        <div class="bar-item">
            <div class="bar-label">2015年</div>
            <div class="bar-track">
                <div class="bar-fill" style="width: 81%;">
                    <span class="bar-value">10.1万所</span>
                </div>
            </div>
        </div>
 <div class="bar-item">
            <div class="bar-label">2019年</div>
            <div class="bar-track">
                <div class="bar-fill" style="width: 69%;">
                    <span class="bar-value">8.6万所</span>
                </div>
            </div>
        </div>
        <div class="bar-item">
            <div class="bar-label">2024年</div>
            <div class="bar-track">
                <div class="bar-fill" style="width: 63%;">
                    <span class="bar-value">7.8万所</span>
                </div>
            </div>
        </div>
    </div>
    
    <p style="text-align: center; color: #999; font-size: 13px; margin-top: 40px;">
        数据来源：教育部《全国教育事业发展统计公报》（2011-2024年度）
    </p>
</section>

<!-- 对比表格 -->
<section class="section section-beige">
    <div class="section-header">
        <div class="section-num">02</div>
        <h2 class="section-title">各地变迁</h2>
        <p class="section-subtitle">不同地区撤并进程对照</p>
    </div>
    
    <table class="compare-table">
        <thead>
            <tr>
                <th>地区</th>
                <th>时间节点</th>
                <th>变化</th>
                <th>现状</th>
            </tr>
        </thead>
        <tbody>
            <tr class="animate">
                <td><strong>陕西兴平市</strong></td>
                <td>2011-2026</td>
                <td class="trend-down">15所 → 4所</td>
                <td>撤并率73%</td>
            </tr>
            <tr class="animate animate-delay-1">
                <td><strong>湖南娄底市</strong></td>
                <td>2026春</td>
                <td class="trend-down">15人 → 14人</td>
                <td>即将撤并</td>
            </tr>
            <tr class="animate animate-delay-2">
                <td><strong>河北故城县</strong></td>
                <td>2000-2026</td>
                <td class="trend-down">58村小 → 9所</td>
                <td>持续萎缩</td>
            </tr>
            <tr class="animate animate-delay-3">
                <td><strong>山东青岛市</strong></td>
                <td>2022-2024</td>
                <td class="trend-down">22人 → 0人</td>
                <td>改为幼儿园</td>
            </tr>
            <tr class="animate">
                <td><strong>河南开封市</strong></td>
                <td>2026</td>
                <td>最少仅6人</td>
                <td>坚守</td>
            </tr>
        </tbody>
    </table>
    
    <p style="text-align: center; color: #999; font-size: 13px; margin-top: 30px;">
        数据来源：实地采访记录（2026年2-3月）
    </p>
</section>

<!-- 故事1：湖南 -->
<section class="section">
    <div class="story-grid">
        <div class="story-card">
            <div class="story-visual">
                <div class="story-big-num">14</div>
                <div style="color: #666; font-size: 16px;">名学生</div>
            </div>
            <div class="story-content">
                <div class="story-location">湖南 · 娄底</div>
                <h3 class="story-title">云山学校的最后一个学期</h3>
                <p class="story-text">
                    2026年2月，21岁的尹佳琪打开学校大门。她是校长，也是二年级语文老师、三年级英语老师、二三年级音乐老师，还是班主任。
                </p>
                <blockquote>
                    <p>「这个学期只有14个学生，上学期还有15个，转走了一个。应该是今年下半年就撤并了。」</p>
                    <cite>—— 尹佳琪，2005年出生，刚毕业即任校长</cite>
                </blockquote>
            </div>
        </div>
        
        <div class="story-card reverse">
            <div class="story-visual">
                <div class="story-big-num">60</div>
                <div style="color: #666; font-size: 16px;">公里</div>
            </div>
            <div class="story-content">
                <div class="story-location">湖南 · 留守儿童</div>
                <h3 class="story-title">童年的距离</h3>
                <p class="story-text">
                    曾湘欧今年7岁。当被问起家离学校多远，他说：「60米。」然后又说：「走路要一个小时。」最后改口：「60公里。」
                </p>
                <blockquote>
                    <p>「我妈妈跟别的男的跑了，我爸去长沙工作了，差不多一个月才能回来。」</p>
                    <cite>—— 曾湘欧，7岁，每天走6公里上学</cite>
                </blockquote>
            </div>
        </div>
    </div>
</section>

<!-- 故事2：陕西 -->
<section class="section section-beige">
    <div class="story-grid">
        <div class="story-card">
            <div class="story-content">
                <div class="story-location">陕西 · 兴平</div>
                <h3 class="story-title">从380人到空无一人</h3>
                <p class="story-text">
                    丰仪镇中心小学退休校长见证了学校从鼎盛到衰败的全过程。1976年他来这里任教时，学校有380名学生，比全镇其他地方加起来还多。
                </p>
                <blockquote>
                    <p>「过去我们在丰仪村小，有380个娃，全乡才300个，我们村比全乡还多。现在，周围的好像都撤并了。」</p>
                    <cite>—— 退休校长，1976-2015年任教</cite>
                </blockquote>
            </div>
            <div class="story-visual">
                <div style="font-size: 48px; font-weight: 700; color: var(--accent); margin-bottom: 20px;">380 → 0</div>
                <div style="color: #666;">学生的变迁</div>
            </div>
        </div>
        
        <div class="story-card reverse">
            <div class="story-content">
                <div class="story-location">陕西 · 策村小学</div>
                <h3 class="story-title">一人的课堂</h3>
                <p class="story-text">
                    41岁的张娜老师已经教了16年书。她所在的学校现在有80多名学生，但一年级只有6个人，三年级也只有6个人。她教英语，还要教科学。
                </p>
                <blockquote>
                    <p>「家庭条件不太好的才在这上，条件稍微好一些的，娃子都在城里上学了。」</p>
                    <cite>—— 张娜，策村小学教师</cite>
                </blockquote>
            </div>
            <div class="story-visual">
                <div style="font-size: 48px; font-weight: 700; color: var(--accent); margin-bottom: 20px;">6</div>
                <div style="color: #666;">人/班</div>
            </div>
        </div>
    </div>
</section>

<!-- 故事3：河北/河南/山东 -->
<section class="section">
    <div class="section-header">
        <div class="section-num">03</div>
        <h2 class="section-title">更多面孔</h2>
    </div>
    
    <div style="display: grid; gap: 40px; margin-top: 60px;">
        <div class="story-card">
            <div class="story-content">
                <div class="story-location">河北 · 衡水</div>
                <h3 class="story-title">二十年前就开始的撤并</h3>
                <p class="story-text">
                    故城县王志超主任回忆，2000年代初期就开始「合校并点」：58个村每村一所小学，逐步合并为9所。「当时叫合校并点，为了集中资源。没想到现在还要继续撤。」
                </p>
                <blockquote>
                    <p>「2020年我们还有将近4000学生，现在每年流失一百多人。」</p>
                    <cite>—— 王志超，故城县中心校主任</cite>
                </blockquote>
            </div>
            <div class="story-visual">
                <div style="font-size: 48px; font-weight: 700; color: var(--accent); margin-bottom: 20px;">58 → 9</div>
                <div style="color: #666;">村小数量变化</div>
            </div>
        </div>
        
        <div class="story-card reverse">
            <div class="story-content">
                <div class="story-location">河南 · 开封</div>
                <h3 class="story-title">「一人也不停办」</h3>
                <p class="story-text">
                    杞县的乡村小学，「只要有1个学生就不停办」。有的学校只有6名学生，分布在不同年级，必须分开授课。退休教师介绍，这些学生多为留守儿童或残疾儿童。
                </p>
                <blockquote>
                    <p>「正常家庭都把孩子送到县城了，留下的都是没办法的。」</p>
                    <cite>—— 杞县退休教师</cite>
                </blockquote>
            </div>
            <div class="story-visual">
                <div style="font-size: 48px; font-weight: 700; color: var(--accent); margin-bottom: 20px;">1</div>
                <div style="color: #666;">人也不停办</div>
            </div>
        </div>
        
        <div class="story-card">
            <div class="story-content">
                <div class="story-location">山东 · 青岛</div>
                <h3 class="story-title">改为幼儿园之后</h3>
                <p class="story-text">
                    青山小学从200多人减至22人，最终撤并。改为幼儿园后，「家长都把孩子送到黄山幼儿园了」。转型未能留住孩子，曾经的读书声变成了机器的轰鸣。
                </p>
                <blockquote>
                    <p>「青山小学成了辣椒厂。以前这里是我的教室，现在变成工厂了。」</p>
                    <cite>—— 胡涵阳，转学生</cite>
                </blockquote>
            </div>
            <div class="story-visual">
                <div style="font-size: 48px; font-weight: 700; color: var(--accent); margin-bottom: 20px;">22 → 0</div>
                <div style="color: #666;">青山小学</div>
            </div>
        </div>
    </div>
</section>

<!-- 教师群像 -->
<section class="section section-dark">
    <div class="section-header">
        <div class="section-num" style="color: var(--gold);">04</div>
        <h2 class="section-title" style="color: #fff;">坚守者</h2>
        <p class="section-subtitle" style="color: #888;">一个人的全科教学</p>
    </div>
    
    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 40px; margin-top: 60px;">
        <div style="text-align: center; padding: 40px;">
            <div style="font-size: 64px; font-weight: 700; color: var(--gold); margin-bottom: 20px;">4</div>
            <div style="color: #fff; font-size: 18px; margin-bottom: 10px;">门课程</div>
            <div style="color: #888; font-size: 14px;">尹佳琪：语文+英语+音乐+班主任+校长</div>
        </div>
        <div style="text-align: center; padding: 40px;">
            <div style="font-size: 64px; font-weight: 700; color: var(--gold); margin-bottom: 20px;">16</div>
            <div style="color: #fff; font-size: 18px; margin-bottom: 10px;">年教龄</div>
            <div style="color: #888; font-size: 14px;">张娜：英语+科学双科教学</div>
        </div>
        <div style="text-align: center; padding: 40px;">
            <div style="font-size: 64px; font-weight: 700; color: var(--gold); margin-bottom: 20px;">30+</div>
            <div style="color: #fff; font-size: 18px; margin-bottom: 10px;">年坚守</div>
            <div style="color: #888; font-size: 14px;">陈志辉：中文系毕业教数学</div>
        </div>
    </div>
    
    <blockquote style="background: rgba(255,255,255,0.05); border-color: var(--gold); margin-top: 60px;">
        <p style="color: #fff;">「我也尽力而为了，走了这么久，凭良心做事。」</p>
        <cite style="color: #888;">—— 陈志辉</cite>
    </blockquote>
</section>

<!-- 尾声 -->
<section class="section" style="text-align: center; padding: 150px 40px;">
    <div class="section-num">05</div>
    <h2 class="section-title">回声</h2>
    
    <div style="margin: 80px 0;">
        <blockquote style="background: none; border: none; max-width: 600px; margin: 0 auto;">
            <p style="font-size: 22px; line-height: 2;">「刚开始可难受了，后来习惯了，反正大家都差不多，都是被学校赶出来的。」</p>
            <cite>—— 彭旭童，转学生</cite>
        </blockquote>
    </div>
    
    <div style="margin: 100px 0;">
        <div style="font-size: 160px; font-weight: 700; color: var(--accent); line-height: 1;">60</div>
        <div style="font-size: 24px; color: var(--gray); margin: 20px 0;">公里</div>
        <div style="font-size: 16px; color: #999; font-style: italic;">
            是真实的距离，也是童年的比例尺<br>
            —— 曾湘欧，7岁
        </div>
    </div>
</section>

<!-- 页脚 -->
<footer>
    <h2>故土与新途</h2>
    <div class="footer-divider"></div>
    <p>
        本报道基于2026年2月至3月实地采访<br>
        数据来源：教育部统计公报、实地访谈记录<br>
        采访地点：陕西、湖南、河北、河南、山东等地乡村小学
    </p>
</footer>

<script>
    // 滚动动画
    const observerOptions = {
        threshold: 0.2,
        rootMargin: '0px 0px -50px 0px'
    };

    const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.classList.add('show');
                
                // 数字增长动画
                const numbers = entry.target.querySelectorAll('[data-count]');
                numbers.forEach(num => {
                    const target = parseFloat(num.dataset.count);
                    const suffix = num.textContent.replace(/[0-9.]/g, '');
                    let current = 0;
                    const increment = target / 50;
                    const timer = setInterval(() => {
                        current += increment;
                        if (current >= target) {
                            current = target;
                            clearInterval(timer);
                        }
                        num.textContent = current.toFixed(1) + suffix;
                    }, 30);
                });
            }
        });
    }, observerOptions);

    document.querySelectorAll('.animate').forEach(el => {
        observer.observe(el);
    });

    // 条形图动画
    const barObserver = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                const fills = entry.target.querySelectorAll('.bar-fill');
                fills.forEach((fill, index) => {
                    const width = fill.style.width;
                    fill.style.width = '0';
                    setTimeout(() => {
                        fill.style.width = width;
                    }, index * 200);
                });
            }
        });
    }, { threshold: 0.3 });

    document.querySelectorAll('.bar-chart').forEach(chart => {
        barObserver.observe(chart);
    });
</script>

</body>
</html>

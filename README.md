[index.html](https://github.com/user-attachments/files/32083656/index.html)
# 養車成本分析

<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>汽車養車成本與電池壽命詳細分析報告</title>
    <style>
        :root {
            --primary: #1e3a8a;
            --primary-light: #3b82f6;
            --bg-main: #f8fafc;
            --card-bg: #ffffff;
            --text-main: #0f172a;
            --text-muted: #475569;
            --border: #e2e8f0;
            --accent-green: #059669;
            --accent-amber: #d97706;
            --accent-blue: #2563eb;
            --accent-purple: #7c3aed;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, "PingFang TC", "Microsoft JhengHei", sans-serif;
            background-color: var(--bg-main);
            color: var(--text-main);
            line-height: 1.6;
            padding: 2rem 1rem;
        }

        .container {
            max-width: 1100px;
            margin: 0 auto;
        }

        header {
            text-align: center;
            margin-bottom: 2.5rem;
            padding: 2rem;
            background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%);
            color: #ffffff;
            border-radius: 16px;
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1);
        }

        header h1 {
            font-size: 2.2rem;
            font-weight: 700;
            margin-bottom: 0.75rem;
            letter-spacing: -0.02em;
        }

        header p {
            color: #94a3b8;
            font-size: 1.05rem;
        }

        .badge-container {
            display: flex;
            justify-content: center;
            gap: 0.75rem;
            margin-top: 1rem;
            flex-wrap: wrap;
        }

        .badge {
            background: rgba(255, 255, 255, 0.1);
            padding: 0.35rem 0.85rem;
            border-radius: 20px;
            font-size: 0.85rem;
            color: #cbd5e1;
            border: 1px solid rgba(255, 255, 255, 0.15);
        }

        .grid-2 {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 1.5rem;
            margin-bottom: 1.5rem;
        }

        .card {
            background: var(--card-bg);
            border-radius: 12px;
            padding: 1.75rem;
            border: 1px solid var(--border);
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.05);
        }

        .card h2 {
            font-size: 1.35rem;
            color: var(--primary);
            margin-bottom: 1rem;
            padding-bottom: 0.5rem;
            border-bottom: 2px solid #f1f5f9;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .qa-box {
            background-color: #f0fdf4;
            border-left: 4px solid var(--accent-green);
            padding: 1.25rem;
            border-radius: 0 8px 8px 0;
            margin-bottom: 1.5rem;
        }

        .qa-title {
            font-weight: 700;
            color: #166534;
            font-size: 1.1rem;
            margin-bottom: 0.5rem;
        }

        .qa-content {
            color: #15803d;
            font-size: 0.95rem;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin: 1rem 0;
            font-size: 0.95rem;
        }

        th, td {
            padding: 0.85rem 1rem;
            text-align: left;
            border-bottom: 1px solid var(--border);
        }

        th {
            background-color: #f1f5f9;
            color: var(--text-main);
            font-weight: 600;
        }

        tr:last-child td {
            border-bottom: none;
        }

        .highlight-row {
            background-color: #eff6ff;
            font-weight: 600;
        }

        .stat-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 1rem;
            margin-bottom: 2rem;
        }

        .stat-card {
            background: var(--card-bg);
            border-radius: 12px;
            padding: 1.25rem;
            border: 1px solid var(--border);
            border-top: 4px solid var(--primary-light);
            text-align: center;
        }

        .stat-card.green { border-top-color: var(--accent-green); }
        .stat-card.amber { border-top-color: var(--accent-amber); }
        .stat-card.purple { border-top-color: var(--accent-purple); }

        .stat-label {
            font-size: 0.85rem;
            color: var(--text-muted);
            margin-bottom: 0.25rem;
        }

        .stat-value {
            font-size: 1.6rem;
            font-weight: 700;
            color: var(--text-main);
        }

        .stat-sub {
            font-size: 0.8rem;
            color: var(--text-muted);
            margin-top: 0.25rem;
        }

        .chart-container {
            margin-top: 1.5rem;
        }

        .bar-group {
            margin-bottom: 1.25rem;
        }

        .bar-label {
            display: flex;
            justify-content: space-between;
            font-size: 0.9rem;
            margin-bottom: 0.35rem;
            font-weight: 500;
        }

        .bar-track {
            height: 12px;
            background-color: #e2e8f0;
            border-radius: 6px;
            overflow: hidden;
        }

        .bar-fill {
            height: 100%;
            border-radius: 6px;
        }

        .bg-20na { background-color: #ef4444; }
        .bg-15t { background-color: #f59e0b; }
        .bg-hybrid { background-color: #3b82f6; }
        .bg-ev { background-color: #10b981; }

        .section-title {
            font-size: 1.5rem;
            font-weight: 700;
            margin: 2.5rem 0 1.25rem 0;
            color: var(--text-main);
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .note-list {
            list-style-type: none;
        }

        .note-list li {
            position: relative;
            padding-left: 1.5rem;
            margin-bottom: 0.75rem;
            font-size: 0.95rem;
            color: var(--text-muted);
        }

        .note-list li::before {
            content: "•";
            position: absolute;
            left: 0.5rem;
            color: var(--primary-light);
            font-weight: bold;
        }

        footer {
            text-align: center;
            margin-top: 3rem;
            padding: 1.5rem;
            color: var(--text-muted);
            font-size: 0.85rem;
            border-top: 1px solid var(--border);
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>汽車養車成本與電池壽命完整分析</h1>
            <p>車價 105 萬 | 年行駛 10,000 公里 | 10 年長期持有一頁式分析報告</p>
            <div class="badge-container">
                <span class="badge">車價 105 萬元</span>
                <span class="badge">年里程 1 萬公里</span>
                <span class="badge">10 年持有週期</span>
                <span class="badge">含電池壽命評估</span>
            </div>
        </header>

     
        <!-- 核心數據總覽卡片 -->
        <h2 class="section-title">📊 10 年養車總成本概覽 (含車價 105 萬攤提)</h2>
        <div class="stat-grid">
            <div class="stat-card">
                <div class="stat-label">2.0L 汽油自然進氣</div>
                <div class="stat-value" style="color: #ef4444;">$195.2 萬</div>
                <div class="stat-sub">平均每月 $16,268</div>
            </div>
            <div class="stat-card amber">
                <div class="stat-label">1.5T 汽油渦輪增壓</div>
                <div class="stat-value" style="color: #f59e0b;">$184.6 萬</div>
                <div class="stat-sub">平均每月 $15,382 (省 10.6萬)</div>
            </div>
            <div class="stat-card">
                <div class="stat-label">1.8L 油電 (含換電池預算)</div>
                <div class="stat-value" style="color: #3b82f6;">$181.7 萬</div>
                <div class="stat-sub">平均每月 $15,140 (省 13.5萬)</div>
            </div>
            <div class="stat-card green">
                <div class="stat-label">純電車 EV (家充為主)</div>
                <div class="stat-value" style="color: #10b981;">$154.0 萬</div>
                <div class="stat-sub">平均每月 $12,833 (省 41.2萬)</div>
            </div>
        </div>

        <!-- 長期成本可視化圖表 -->
        <div class="card" style="margin-bottom: 2rem;">
            <h2>📈 10 年總養車成本對比條形圖</h2>
            <div class="chart-container">
                <div class="bar-group">
                    <div class="bar-label">
                        <span>2.0L 汽油自然進氣</span>
                        <span>NT$ 1,952,100</span>
                    </div>
                    <div class="bar-track">
                        <div class="bar-fill bg-20na" style="width: 100%;"></div>
                    </div>
                </div>

                <div class="bar-group">
                    <div class="bar-label">
                        <span>1.5T 汽油渦輪增壓</span>
                        <span>NT$ 1,845,870 (可省 NT$ 106,230)</span>
                    </div>
                    <div class="bar-track">
                        <div class="bar-fill bg-15t" style="width: 94.5%;"></div>
                    </div>
                </div>

                <div class="bar-group">
                    <div class="bar-label">
                        <span>1.8L 油電混合 (含 $6萬 電池預留金)</span>
                        <span>NT$ 1,816,800 (可省 NT$ 135,300)</span>
                    </div>
                    <div class="bar-track">
                        <div class="bar-fill bg-hybrid" style="width: 93.0%;"></div>
                    </div>
                </div>

                <div class="bar-group">
                    <div class="bar-label">
                        <span>純電動車 EV (含 $2萬 檢修預備金)</span>
                        <span>NT$ 1,540,000 (可省 NT$ 412,100)</span>
                    </div>
                    <div class="bar-track">
                        <div class="bar-fill bg-ev" style="width: 78.8%;"></div>
                    </div>
                </div>
            </div>
        </div>

        <!-- 詳細數據明細表格 -->
        <div class="card" style="margin-bottom: 2rem;">
            <h2>📋 四種動力型態 10 年詳細費用明細對比表</h2>
            <div style="overflow-x: auto;">
                <table>
                    <thead>
                        <tr>
                            <th>費用項目 (10年累積)</th>
                            <th>2.0L 汽油 NA</th>
                            <th>1.5T 汽油渦輪</th>
                            <th>1.8L 油電 Hybrid</th>
                            <th>純電動車 EV</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td><b>購車成本攤提</b></td>
                            <td>$1,050,000</td>
                            <td>$1,050,000</td>
                            <td>$1,050,000</td>
                            <td>$1,050,000</td>
                        </tr>
                        <tr>
                            <td><b>政府稅金 (牌照+燃料)</b></td>
                            <td>$174,100</td>
                            <td>$119,200</td>
                            <td>$119,200</td>
                            <td>$0 (免徵至2030)</td>
                        </tr>
                        <tr>
                            <td><b>能源費用 (油資/電費)</b></td>
                            <td>$258,000 (12 km/L)</td>
                            <td>$206,670 (15 km/L)</td>
                            <td>$147,600 (21 km/L)</td>
                            <td>$70,000 (家充為主)</td>
                        </tr>
                        <tr>
                            <td><b>基礎定保與耗材</b></td>
                            <td>$150,000</td>
                            <td>$150,000</td>
                            <td>$120,000</td>
                            <td>$60,000</td>
                        </tr>
                        <tr>
                            <td><b>大電池更換/檢修預備金</b></td>
                            <td>$0</td>
                            <td>$0</td>
                            <td><b>$60,000 (預留1次)</b></td>
                            <td><b>$20,000 (檢修/小電瓶)</b></td>
                        </tr>
                        <tr>
                            <td><b>保險費用 (10年均額)</b></td>
                            <td>$200,000</td>
                            <td>$200,000</td>
                            <td>$200,000</td>
                            <td>$220,000 (電車略高)</td>
                        </tr>
                        <tr>
                            <td><b>臨停與國道過路費</b></td>
                            <td>$120,000</td>
                            <td>$120,000</td>
                            <td>$120,000</td>
                            <td>$120,000</td>
                        </tr>
                        <tr class="highlight-row">
                            <td><b>10 年日常總花費 (不含購車)</b></td>
                            <td><b>$902,100</b></td>
                            <td><b>$795,870</b></td>
                            <td><b>$766,800</b></td>
                            <td><b>$490,000</b></td>
                        </tr>
                        <tr class="highlight-row" style="background-color: #dbeafe; color: #1e40af;">
                            <td><b>10 年養車總成本 (含購車)</b></td>
                            <td><b>$1,952,100</b></td>
                            <td><b>$1,845,870</b></td>
                            <td><b>$1,816,800</b></td>
                            <td><b>$1,540,000</b></td>
                        </tr>
                        <tr>
                            <td><b>平均每年負擔</b></td>
                            <td>$195,210</td>
                            <td>$184,587</td>
                            <td>$181,680</td>
                            <td>$154,000</td>
                        </tr>
                        <tr>
                            <td><b>平均每月負擔</b></td>
                            <td><b>$16,268</b></td>
                            <td><b>$15,382</b></td>
                            <td><b>$15,140</b></td>
                            <td><b>$12,833</b></td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>

   <!-- 電池壽命疑問解答卡片 -->
        <div class="card" style="margin-bottom: 2rem;">
            <h2>💡 電池壽命疑問專題分析：「電池真的 5 年就要換嗎？」</h2>
            <div class="qa-box">
                <div class="qa-title">結論摘要：現代車用電池壽命已大幅提升，並非 5 年就必須換新！</div>
                <div class="qa-content">
                    原廠對油電與純電車電池大多提供 <b>8 年或 16 萬公里</b> 的長期保固。在年行駛 1 萬公里的低里程使用條件下，電池衰退幅度小，大電池絕大多數能在 8-10 年間正常運作。
                </div>
            </div>

            <div class="grid-2">
                <div>
                    <h3 style="color: var(--accent-blue); margin-bottom: 0.5rem;">⚡ 油電混合車 (Hybrid) 電池分析</h3>
                    <ul class="note-list">
                        <li><b>原廠保固：</b>通常為 8 年或 16 萬公里（如 Toyota）。</li>
                        <li><b>實際壽命：</b>平均耐用約 7 - 10 年（約 15~20 萬公里）。</li>
                        <li><b>更換費用：</b>若在第 7-8 年過保後更換，大電池費用約 <b>NT$ 50,000 - 70,000</b>。</li>
                        <li><b>本試算納入：</b>已預留 <b>NT$ 60,000</b> 做為 10 年內更換一次大電池的攤提成本。</li>
                    </ul>
                </div>
                <div>
                    <h3 style="color: var(--accent-green); margin-bottom: 0.5rem;">🔋 純電動車 (EV) 電池分析</h3>
                    <ul class="note-list">
                        <li><b>原廠保固：</b>標準為 8 年或 16 萬公里（保證容量 ≥ 70%）。</li>
                        <li><b>實際壽命：</b>具備水冷溫控與 BMS 管理，循環壽命達 1500+ 次。10 年跑 10 萬公里僅衰退約 10-15%。</li>
                        <li><b>更換費用：</b>整組極貴，但保固期長且 10 萬公里內壞掉機率極低；模組修復約 2-5 萬。</li>
                        <li><b>本試算納入：</b>預留 <b>NT$ 20,000</b> 輔助電瓶與系統檢修預備金，整組更換屬低機率事件。</li>
                    </ul>
                </div>
            </div>
        </div>

        <!-- 購車決策建議 -->
        <div class="card">
            <h2>💡 綜合選車建議與結論</h2>
            <ul class="note-list">
                <li><b>如果您在意初期穩定與妥善率：</b>選擇 <b>1.5T 渦輪引擎</b> 車款，相比 2.0L 自然進氣每年現省 $5,490 稅金加上油資，10 年能穩省約 10.6 萬元，且無大電池過保心理負擔。</li>
                <li><b>如果您經常走市區/走走停停：</b>選擇 <b>1.8L 油電 Hybrid</b>。雖然預估在 7-8 年需準備約 6 萬的大電池更換費用，但靠著極佳油耗（20+ km/L），扣除電池費用後 10 年依舊比 2.0L 汽油車省下約 <b>13.5 萬元</b>。</li>
                <li><b>如果您家中有條件安裝充電樁：</b>選擇 <b>純電動車 EV</b> 經濟效益最高。即便考慮到電車保險費用略高，10 年累積仍可比 2.0L 汽油車大幅省下超過 <b>41 萬元</b> 的養車開銷！</li>
            </ul>
        </div>

        <footer>
            <p>※ 本報告依據現行牌照稅、燃料費、油價 ($31/L 95無鉛) 及平均電力成本進行估算。實際費用依個人駕駛習慣與車款原廠規範而定。</p>
        </footer>
    </div>
</body>
</html>

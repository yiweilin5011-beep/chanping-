# chanping-
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>财务分析智能体 - 用户旅程地图</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Microsoft YaHei', sans-serif;
            background: linear-gradient(135deg, #e8f3ff 0%, #f0e6ff 50%, #e8f3ff 100%);
            padding: 40px 20px;
            min-height: 100vh;
            position: relative;
            overflow-x: hidden;
        }

        /* 背景装饰球体 */
        body::before {
            content: '';
            position: fixed;
            top: -200px;
            right: -200px;
            width: 600px;
            height: 600px;
            background: linear-gradient(135deg, rgba(100, 150, 255, 0.1) 0%, rgba(150, 120, 255, 0.05) 100%);
            border-radius: 50%;
            z-index: -1;
        }

        body::after {
            content: '';
            position: fixed;
            bottom: -150px;
            left: -150px;
            width: 400px;
            height: 400px;
            background: linear-gradient(135deg, rgba(100, 200, 255, 0.08) 0%, rgba(150, 120, 255, 0.04) 100%);
            border-radius: 50%;
            z-index: -1;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(59, 130, 246, 0.08),
                        0 0 1px rgba(59, 130, 246, 0.1);
            overflow: hidden;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.7);
        }

        .header {
            background: linear-gradient(135deg, #3b82f6 0%, #6366f1 50%, #8b5cf6 100%);
            color: white;
            padding: 60px 40px;
            text-align: center;
            position: relative;
            overflow: hidden;
        }

        .header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background:
                radial-gradient(circle at 20% 50%, rgba(255, 255, 255, 0.1) 0%, transparent 50%),
                radial-gradient(circle at 80% 80%, rgba(255, 255, 255, 0.05) 0%, transparent 50%);
            pointer-events: none;
        }

        .header h1 {
            font-size: 40px;
            margin-bottom: 15px;
            font-weight: 700;
            position: relative;
            z-index: 1;
            letter-spacing: -0.5px;
        }

        .header p {
            font-size: 16px;
            opacity: 0.95;
            position: relative;
            z-index: 1;
        }

        .content {
            padding: 40px;
            display: flex;
            flex-direction: column;
        }

        /* Section重新排序 */
        .content > .section:nth-child(1) {
            order: 2;
        }

        .content > .section:nth-child(2) {
            order: 1;
        }

        .content > .section:nth-child(3) {
            order: 3;
        }

        .content > .section:nth-child(4) {
            order: 6;
        }

        .content > .section:nth-child(5) {
            order: 5;
        }

        .content > .section:nth-child(6) {
            order: 7;
        }

        .content > .section:nth-child(7) {
            order: 8;
        }

        .content > .section:nth-child(8) {
            order: 9;
        }

        .content > .section:nth-child(9) {
            order: 4;
        }

        .content > .section:nth-child(10) {
            order: 10;
        }

        .section {
            margin-bottom: 50px;
        }

        .section-title {
            font-size: 24px;
            color: #1e3c72;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 3px solid #2a5298;
            display: flex;
            align-items: center;
        }

        .section-title .number {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            width: 35px;
            height: 35px;
            background: #2a5298;
            color: white;
            border-radius: 50%;
            margin-right: 15px;
            font-size: 18px;
            font-weight: 600;
        }

        .journey-stages {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 24px;
            margin-bottom: 30px;
        }

        .stage-card {
            background: linear-gradient(135deg, rgba(255, 255, 255, 0.8) 0%, rgba(248, 250, 255, 0.9) 100%);
            border-left: 4px solid #3b82f6;
            padding: 28px;
            border-radius: 16px;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.6);
            box-shadow: 0 4px 20px rgba(59, 130, 246, 0.08),
                        inset 0 1px 0 rgba(255, 255, 255, 0.5);
        }

        .stage-card:hover {
            box-shadow: 0 12px 40px rgba(59, 130, 246, 0.15),
                        inset 0 1px 0 rgba(255, 255, 255, 0.7);
            transform: translateY(-4px);
            background: linear-gradient(135deg, rgba(255, 255, 255, 0.95) 0%, rgba(250, 252, 255, 0.95) 100%);
        }

        .stage-card.stage-1 {
            border-left-color: #FF6B6B;
        }

        .stage-card.stage-2 {
            border-left-color: #4ECDC4;
        }

        .stage-card.stage-3 {
            border-left-color: #FFD93D;
        }

        .stage-card.stage-4 {
            border-left-color: #6BCB77;
        }

        .stage-card.stage-5 {
            border-left-color: #A78BFA;
        }

        .stage-card h4 {
            color: #1e293b;
            margin-bottom: 12px;
            font-size: 16px;
            font-weight: 700;
        }

        .stage-card p {
            color: #475569;
            font-size: 14px;
            line-height: 1.6;
            margin-bottom: 12px;
        }

        .stage-card .tag {
            display: inline-block;
            padding: 6px 12px;
            background: linear-gradient(135deg, rgba(59, 130, 246, 0.1) 0%, rgba(99, 102, 241, 0.08) 100%);
            border-radius: 8px;
            font-size: 12px;
            margin-right: 6px;
            margin-top: 8px;
            color: #3b82f6;
            border: 1px solid rgba(59, 130, 246, 0.2);
            font-weight: 500;
        }

        .journey-flow {
            background: linear-gradient(135deg, rgba(248, 250, 255, 0.8) 0%, rgba(240, 246, 255, 0.8) 100%);
            padding: 32px;
            border-radius: 16px;
            margin: 30px 0;
            overflow-x: auto;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(59, 130, 246, 0.1);
        }

        .flow-diagram {
            display: flex;
            align-items: center;
            gap: 12px;
            min-width: 1000px;
        }

        .flow-box {
            flex-shrink: 0;
            background: white;
            border: 2px solid rgba(59, 130, 246, 0.3);
            border-radius: 12px;
            padding: 16px 20px;
            min-width: 160px;
            text-align: center;
            font-size: 13px;
            font-weight: 600;
            color: #1e293b;
            box-shadow: 0 2px 8px rgba(59, 130, 246, 0.08);
            transition: all 0.3s ease;
        }

        .flow-box:hover {
            background: linear-gradient(135deg, rgba(59, 130, 246, 0.05) 0%, rgba(99, 102, 241, 0.05) 100%);
            border-color: #3b82f6;
            box-shadow: 0 4px 16px rgba(59, 130, 246, 0.15);
        }

        .flow-arrow {
            flex-shrink: 0;
            font-size: 20px;
            color: #3b82f6;
            font-weight: 600;
        }

        .interaction-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            overflow-x: auto;
        }

        .interaction-table thead {
            background: linear-gradient(135deg, #3b82f6 0%, #6366f1 100%);
            color: white;
        }

        .interaction-table th {
            padding: 16px 15px;
            text-align: left;
            font-weight: 600;
            font-size: 14px;
        }

        .interaction-table td {
            padding: 16px 15px;
            border-bottom: 1px solid rgba(59, 130, 246, 0.08);
            font-size: 13px;
            color: #475569;
        }

        .interaction-table tbody tr {
            transition: all 0.3s ease;
        }

        .interaction-table tbody tr:hover {
            background: rgba(59, 130, 246, 0.04);
        }

        .badge {
            display: inline-block;
            padding: 6px 12px;
            border-radius: 8px;
            font-size: 12px;
            font-weight: 600;
            margin-right: 6px;
            margin-bottom: 6px;
        }

        .badge.success {
            background: linear-gradient(135deg, rgba(34, 197, 94, 0.15) 0%, rgba(74, 222, 128, 0.1) 100%);
            color: #166534;
            border: 1px solid rgba(34, 197, 94, 0.3);
        }

        .badge.info {
            background: linear-gradient(135deg, rgba(6, 182, 212, 0.15) 0%, rgba(34, 211, 238, 0.1) 100%);
            color: #164e63;
            border: 1px solid rgba(6, 182, 212, 0.3);
        }

        .badge.warning {
            background: linear-gradient(135deg, rgba(245, 158, 11, 0.15) 0%, rgba(251, 191, 36, 0.1) 100%);
            color: #92400e;
            border: 1px solid rgba(245, 158, 11, 0.3);
        }

        .badge.danger {
            background: linear-gradient(135deg, rgba(239, 68, 68, 0.15) 0%, rgba(248, 113, 113, 0.1) 100%);
            color: #7f1d1d;
            border: 1px solid rgba(239, 68, 68, 0.3);
        }

        .badge.supplement {
            background: linear-gradient(135deg, rgba(245, 158, 11, 0.15) 0%, rgba(251, 191, 36, 0.1) 100%);
            color: #b45309;
            border: 1px solid rgba(245, 158, 11, 0.3);
        }

        .badge.optimization {
            background: linear-gradient(135deg, rgba(59, 130, 246, 0.15) 0%, rgba(96, 165, 250, 0.1) 100%);
            color: #1e3a8a;
            border: 1px solid rgba(59, 130, 246, 0.3);
        }

        .interaction-detail {
            background: linear-gradient(135deg, rgba(255, 255, 255, 0.8) 0%, rgba(248, 250, 255, 0.8) 100%);
            border: 1px solid rgba(59, 130, 246, 0.1);
            border-radius: 16px;
            padding: 24px;
            margin: 18px 0;
            backdrop-filter: blur(10px);
            transition: all 0.3s ease;
        }

        .interaction-detail:hover {
            box-shadow: 0 8px 24px rgba(59, 130, 246, 0.1);
        }

        .interaction-detail h5 {
            color: #1e293b;
            margin-bottom: 14px;
            font-size: 14px;
            display: flex;
            align-items: center;
            font-weight: 700;
        }

        .interaction-detail h5 .icon {
            margin-right: 10px;
            font-size: 18px;
        }

        .interaction-detail ul {
            margin-left: 20px;
            color: #475569;
            font-size: 13px;
            line-height: 1.8;
        }

        .interaction-detail li {
            margin-bottom: 10px;
        }

        .condition-box {
            background: linear-gradient(135deg, rgba(59, 130, 246, 0.08) 0%, rgba(99, 102, 241, 0.06) 100%);
            border-left: 4px solid #3b82f6;
            padding: 18px;
            margin: 18px 0;
            border-radius: 12px;
            font-size: 13px;
            color: #334155;
            backdrop-filter: blur(4px);
        }

        .condition-box strong {
            color: #3b82f6;
            display: block;
            margin-bottom: 8px;
            font-weight: 700;
        }

        .error-box {
            background: linear-gradient(135deg, rgba(239, 68, 68, 0.08) 0%, rgba(239, 68, 68, 0.06) 100%);
            border-left: 4px solid #ef4444;
            padding: 18px;
            margin: 18px 0;
            border-radius: 12px;
            font-size: 13px;
            color: #334155;
        }

        .error-box strong {
            color: #ef4444;
            display: block;
            margin-bottom: 8px;
            font-weight: 700;
        }

        .success-box {
            background: linear-gradient(135deg, rgba(34, 197, 94, 0.08) 0%, rgba(34, 197, 94, 0.06) 100%);
            border-left: 4px solid #22c55e;
            padding: 18px;
            margin: 18px 0;
            border-radius: 12px;
            font-size: 13px;
            color: #334155;
        }

        .success-box strong {
            color: #22c55e;
            display: block;
            margin-bottom: 8px;
            font-weight: 700;
        }

        .screen-reference {
            background: linear-gradient(135deg, rgba(59, 130, 246, 0.1) 0%, rgba(99, 102, 241, 0.08) 100%);
            padding: 6px 12px;
            border-radius: 8px;
            display: inline-block;
            margin: 8px 0;
            font-size: 12px;
            color: #3b82f6;
            border: 1px solid rgba(59, 130, 246, 0.2);
            font-weight: 600;
        }

        .branch-path {
            margin-left: 20px;
            padding-left: 20px;
            border-left: 3px dashed #06b6d4;
        }

        .branch-path h5 {
            color: #0891b2;
            margin: 16px 0 10px 0;
            font-size: 13px;
            display: flex;
            align-items: center;
            font-weight: 700;
        }

        .branch-path h5 .icon {
            margin-right: 8px;
        }

        .branch-path p {
            color: #475569;
            font-size: 13px;
            line-height: 1.7;
        }

        .footer {
            background: linear-gradient(135deg, rgba(248, 250, 255, 0.8) 0%, rgba(240, 246, 255, 0.8) 100%);
            padding: 40px;
            text-align: center;
            color: #64748b;
            font-size: 13px;
            border-top: 1px solid rgba(59, 130, 246, 0.1);
        }

        .footer p {
            margin-bottom: 12px;
            color: #475569;
        }

        .footer strong {
            color: #1e293b;
            font-weight: 700;
        }

        @media (max-width: 768px) {
            .header h1 {
                font-size: 24px;
            }

            .journey-stages {
                grid-template-columns: 1fr;
            }

            .interaction-table {
                font-size: 12px;
            }

            .interaction-table th,
            .interaction-table td {
                padding: 10px;
            }

            .flow-diagram {
                flex-wrap: wrap;
            }
        }

        /* SVG图标样式 */
        .svg-icon {
            width: 1.2em;
            height: 1.2em;
            display: inline-block;
            margin-right: 0.3em;
            vertical-align: -0.15em;
            flex-shrink: 0;
        }

        .svg-icon-blue {
            color: #3b82f6;
        }

        /* 流程图紧凑样式 */
        .flow-diagram-compact {
            gap: 8px;
        }

        .flow-diagram-compact .flow-box {
            min-width: 120px;
            padding: 10px 14px;
            font-size: 11px;
        }

        .flow-diagram-compact .flow-arrow {
            font-size: 16px;
        }

        /* 五阶段紧凑卡片 */
        .stage-card-compact {
            padding: 16px 12px;
        }

        .stage-card-compact h4 {
            font-size: 13px;
            margin-bottom: 8px;
        }

        .stage-card-compact p {
            font-size: 12px;
            margin-bottom: 8px;
        }

        .stage-card-compact .tag {
            font-size: 11px;
            padding: 4px 8px;
            margin-right: 4px;
            margin-top: 6px;
        }

        /* 图片容器 */
        .stage-image-container {
            width: 100%;
            height: 120px;
            background: linear-gradient(135deg, rgba(59, 130, 246, 0.08), rgba(99, 102, 241, 0.06));
            border-radius: 12px;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
            border: 1px solid rgba(59, 130, 246, 0.15);
        }

        .stage-image-container img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .stage-image-placeholder {
            color: #94a3b8;
            font-size: 12px;
            text-align: center;
        }

        /* 响应式调整 */
        @media (max-width: 1200px) {
            .journey-stages {
                grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            }
        }

        @media (max-width: 768px) {
            .journey-stages {
                grid-template-columns: 1fr;
            }

            .stage-card-compact {
                padding: 14px 10px;
            }

            .stage-card-compact h4 {
                font-size: 12px;
            }

            .stage-card-compact p {
                font-size: 11px;
            }

            .flow-diagram-compact {
                flex-wrap: wrap;
                gap: 6px;
            }

            .flow-diagram-compact .flow-box {
                min-width: 100px;
                font-size: 10px;
                padding: 8px 12px;
            }
        }
    </style>
</head>
<body>
    <!-- SVG图标库 -->
    <svg style="display: none;">
        <defs>
            <!-- 目标图标 -->
            <symbol id="icon-target" viewBox="0 0 24 24">
                <circle cx="12" cy="12" r="10" fill="none" stroke="currentColor" stroke-width="2"/>
                <circle cx="12" cy="12" r="6" fill="none" stroke="currentColor" stroke-width="2"/>
                <circle cx="12" cy="12" r="2" fill="currentColor"/>
            </symbol>
            <!-- 搜索图标 -->
            <symbol id="icon-search" viewBox="0 0 24 24">
                <circle cx="11" cy="11" r="8" fill="none" stroke="currentColor" stroke-width="2"/>
                <path d="m21 21-4.35-4.35" stroke="currentColor" stroke-width="2" fill="none"/>
            </symbol>
            <!-- 齿轮图标 -->
            <symbol id="icon-cog" viewBox="0 0 24 24">
                <circle cx="12" cy="12" r="3" fill="currentColor"/>
                <path d="M12 1v6m0 6v6M4.22 4.22l4.24 4.24m2.12 2.12l4.24 4.24M1 12h6m6 0h6m-17.78 7.78l4.24-4.24m2.12-2.12l4.24-4.24M4.22 19.78l4.24-4.24m2.12-2.12l4.24-4.24" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round"/>
            </symbol>
            <!-- 图表图标 -->
            <symbol id="icon-chart" viewBox="0 0 24 24">
                <path d="M3 3v18h18" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M6 14l4-4 4 4 7-7" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>
                <circle cx="6" cy="14" r="1.5" fill="currentColor"/>
                <circle cx="14" cy="6" r="1.5" fill="currentColor"/>
                <circle cx="19" cy="1" r="1.5" fill="currentColor"/>
            </symbol>
            <!-- 用户图标 -->
            <symbol id="icon-users" viewBox="0 0 24 24">
                <path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>
                <circle cx="9" cy="7" r="4" stroke="currentColor" stroke-width="2" fill="none"/>
                <path d="M23 21v-2a4 4 0 0 0-3-3.87" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M16 3.13a4 4 0 0 1 0 7.75" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>
            </symbol>
            <!-- 锁图标 -->
            <symbol id="icon-lock" viewBox="0 0 24 24">
                <rect x="3" y="11" width="18" height="11" rx="2" ry="2" stroke="currentColor" stroke-width="2" fill="none"/>
                <path d="M7 11V7a5 5 0 0 1 10 0v4" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round"/>
                <circle cx="12" cy="16" r="1" fill="currentColor"/>
            </symbol>
            <!-- 信息图标 -->
            <symbol id="icon-info" viewBox="0 0 24 24">
                <circle cx="12" cy="12" r="10" stroke="currentColor" stroke-width="2" fill="none"/>
                <path d="M12 16v-4M12 8h.01" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round"/>
            </symbol>
            <!-- 警告图标 -->
            <symbol id="icon-warning" viewBox="0 0 24 24">
                <path d="M10.29 3.86L1.82 18a2 2 0 0 0 1.71 3.05h16.94a2 2 0 0 0 1.71-3.05L13.71 3.86a2 2 0 0 0-3.42 0z" stroke="currentColor" stroke-width="2" fill="none" stroke-linejoin="round"/>
                <line x1="12" y1="9" x2="12" y2="13" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
                <line x1="12" y1="17" x2="12.01" y2="17" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
            </symbol>
            <!-- 成功/检查图标 -->
            <symbol id="icon-check" viewBox="0 0 24 24">
                <polyline points="20 6 9 17 4 12" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>
            </symbol>
            <!-- 分支图标 -->
            <symbol id="icon-branch" viewBox="0 0 24 24">
                <circle cx="6" cy="3" r="2" stroke="currentColor" stroke-width="2" fill="none"/>
                <circle cx="6" cy="21" r="2" stroke="currentColor" stroke-width="2" fill="none"/>
                <circle cx="18" cy="21" r="2" stroke="currentColor" stroke-width="2" fill="none"/>
                <path d="M6 5v6a4 4 0 0 0 4 4h4" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M14 15v6" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round"/>
            </symbol>
            <!-- 文档图标 -->
            <symbol id="icon-document" viewBox="0 0 24 24">
                <path d="M13 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V9z" stroke="currentColor" stroke-width="2" fill="none" stroke-linejoin="round"/>
                <polyline points="13 2 13 9 20 9" stroke="currentColor" stroke-width="2" fill="none" stroke-linejoin="round"/>
                <line x1="9" y1="13" x2="15" y2="13" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
                <line x1="9" y1="17" x2="15" y2="17" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
            </symbol>
            <!-- 闪电/加载图标 -->
            <symbol id="icon-lightning" viewBox="0 0 24 24">
                <polygon points="13 2 3 14 12 14 11 22 21 10 12 10 13 2" stroke="currentColor" stroke-width="2" fill="none" stroke-linejoin="round"/>
            </symbol>
            <!-- 评论图标 -->
            <symbol id="icon-comment" viewBox="0 0 24 24">
                <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z" stroke="currentColor" stroke-width="2" fill="none" stroke-linejoin="round"/>
            </symbol>
        </defs>
    </svg>
    <div class="container">
        <!-- 页头 -->
        <div class="header">
            <h1><svg class="svg-icon svg-icon-blue"><use xlink:href="#icon-chart"></use></svg>财务分析智能体用户旅程地图</h1>
            <p>企业级AI数据平台 · 数据洞察报告生成流程</p>
        </div>

        <!-- 主内容 -->
        <div class="content">
            <!-- 第一部分：用户旅程五大阶段 -->
            <div class="section">
                <div class="section-title">
                    <span class="number">2</span>
                    用户旅程五大阶段
                </div>
                <div class="journey-stages">
                    <div class="stage-card stage-1 stage-card-compact">
                        <div class="stage-image-container">
                            <img src="../../产品经理/财务分析智能体原型/数据洞察界面1.png" alt="数据洞察界面1">
                        </div>
                        <h4><svg class="svg-icon svg-icon-blue"><use xlink:href="#icon-target"></use></svg>第一阶段：需求初始化</h4>
                        <p>用户进入应用，通过AI对话式交互提出数据分析需求</p>
                        <span class="tag">对应界面：数据洞察界面1</span>
                    </div>
                    <div class="stage-card stage-2 stage-card-compact">
                        <div class="stage-image-container">
                            <img src="../../产品经理/财务分析智能体原型/数据洞察界面2.png" alt="数据洞察界面2">
                        </div>
                        <h4><svg class="svg-icon svg-icon-blue"><use xlink:href="#icon-search"></use></svg>第二阶段：AI引导分析</h4>
                        <p>AI助手提供分析指引，展示诊断、归因、建议框架</p>
                        <span class="tag">对应界面：数据洞察界面2</span>
                    </div>
                    <div class="stage-card stage-3 stage-card-compact">
                        <div class="stage-image-container">
                            <img src="../../产品经理/财务分析智能体原型/执行规划1.png" alt="执行规划1">
                        </div>
                        <h4><svg class="svg-icon svg-icon-blue"><use xlink:href="#icon-cog"></use></svg>第三阶段：执行规划</h4>
                        <p>可视化展示数据流转过程，多维度分析逻辑配置</p>
                        <span class="tag">对应界面：执行规划1</span>
                    </div>
                    <div class="stage-card stage-4 stage-card-compact">
                        <div class="stage-image-container">
                            <img src="../../产品经理/财务分析智能体原型/报告生成1.png" alt="报告生成1">
                        </div>
                        <h4><svg class="svg-icon svg-icon-blue"><use xlink:href="#icon-chart"></use></svg>第四阶段：报告生成</h4>
                        <p>异步生成详细分析报告，展示KPI、图表、数据表格</p>
                        <span class="tag">对应界面：报告生成1</span>
                    </div>
                    <div class="stage-card stage-5 stage-card-compact">
                        <div class="stage-image-container">
                            <img src="../../产品经理/财务分析智能体原型/任务下发1.png" alt="任务下发1">
                        </div>
                        <h4><svg class="svg-icon svg-icon-blue"><use xlink:href="#icon-users"></use></svg>第五阶段：任务分配</h4>
                        <p>将分析结果转化为团队任务，支持多人协作</p>
                        <span class="tag">对应界面：任务下发1</span>
                    </div>
                </div>
            </div>

            <!-- 第二部分：核心用户路径流程 -->
            <div class="section">
                <div class="section-title">
                    <span class="number">1</span>
                    核心用户路径流程
                </div>
                <div class="journey-flow">
                    <div class="flow-diagram flow-diagram-compact">
                        <div class="flow-box">发起新对话</div>
                        <div class="flow-arrow">→</div>
                        <div class="flow-box">选择分析类型</div>
                        <div class="flow-arrow">→</div>
                        <div class="flow-box">配置数据源</div>
                        <div class="flow-arrow">→</div>
                        <div class="flow-box">生成报告</div>
                        <div class="flow-arrow">→</div>
                        <div class="flow-box">查看结果</div>
                        <div class="flow-arrow">→</div>
                        <div class="flow-box">分配任务</div>
                    </div>
                </div>

                <h4 style="margin-top: 24px; color: #1e293b; margin-bottom: 12px; font-weight: 700;"><svg class="svg-icon svg-icon-blue" style="margin-right: 0.5em;"><use xlink:href="#icon-info"></use></svg>关键路径触发条件</h4>
                <div class="condition-box">
                    <strong>条件1：功能卡片的解锁状态</strong>
                    用户首次进入应用时，仅「客户收益诊断洞察」卡片可点击（其他卡片显示<svg class="svg-icon" style="width: 1em; height: 1em; vertical-align: -0.1em; margin: 0 0.2em;"><use xlink:href="#icon-lock"></use></svg>锁定状态），用户需完成此分析后方可解锁下一个功能
                </div>

                <div class="condition-box">
                    <strong>条件2：数据源关联</strong>
                    点击「生成数据洞察」按钮的前置条件：必须至少选择1个数据源（左侧数据源面板中的数据集）
                </div>

                <div class="condition-box">
                    <strong>条件3：进度条显示机制</strong>
                    报告生成时，当加载时间≥3秒时自动显示进度条（含思考过程、多维分析、提示词加载、汇总4个子步骤）
                </div>

                <div class="condition-box">
                    <strong>条件4：任务分配权限</strong>
                    用户仅在报告生成成功后，才可使用「转任务」功能；转任务需选择≥1个目标联系人或部门
                </div>
            </div>

            <!-- 第三部分：交互详细表格 -->
            <div class="section">
                <div class="section-title">
                    <span class="number">3</span>
                    交互节点详细说明
                </div>
                <table class="interaction-table">
                    <thead>
                        <tr>
                            <th style="width: 12%;">界面</th>
                            <th style="width: 18%;">交互动作</th>
                            <th style="width: 20%;">触发条件</th>
                            <th style="width: 20%;">系统反馈</th>
                            <th style="width: 30%;">特殊说明</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td><span class="screen-reference">数据洞察界面1</span></td>
                            <td>点击「客户收益诊断洞察」卡片</td>
                            <td>用户进入新对话</td>
                            <td>界面跳转至数据洞察界面2，卡片展开显示详细内容</td>
                            <td>其他卡片为锁定状态，需标注🔒图标</td>
                        </tr>
                        <tr>
                            <td rowspan="3"><span class="screen-reference">数据洞察界面2</span></td>
                            <td>点击「生成数据洞察」按钮</td>
                            <td>至少选择1个数据源</td>
                            <td>跳转至执行规划界面，显示数据流转图</td>
                            <td>按钮默认禁用（灰色），选择数据源后变活跃（蓝色）</td>
                        </tr>
                        <tr>
                            <td>上传附件/编辑提示词</td>
                            <td>用户主动操作</td>
                            <td>弹出文件选择框或编辑窗口</td>
                            <td><span class="badge optimization">优化建议：</span>支持拖拽上传，减少操作步骤</td>
                        </tr>
                        <tr>
                            <td>点击数据洞察卡片中的数据源</td>
                            <td>鼠标hover卡片</td>
                            <td>显示详细数据源说明（表名、文件路径、大小）</td>
                            <td>支持点击查看完整数据源信息</td>
                        </tr>
                        <tr>
                            <td rowspan="2"><span class="screen-reference">执行规划1</span></td>
                            <td>浏览分析思路/数据流转图</td>
                            <td>用户查看页面内容</td>
                            <td>展示数据→维度→算子→输出矩阵的完整链路</td>
                            <td><span class="badge supplement">原型补充：</span>建议增加流程图中各节点的展开/收起功能</td>
                        </tr>
                        <tr>
                            <td>点击「生成数据洞察」确认</td>
                            <td>用户确认分析参数</td>
                            <td>提交任务至后端，跳转至报告生成界面</td>
                            <td>此步为原型补充路径，连接执行规划与报告生成</td>
                        </tr>
                        <tr>
                            <td rowspan="4"><span class="screen-reference">报告生成1</span></td>
                            <td>查看思考过程及进度</td>
                            <td>报告生成中（≥3秒）</td>
                            <td>并行显示4个进度步骤：数据加载→多维分析→提示词加载→汇总</td>
                            <td>每个步骤显示耗时（如6s、8s）和当前进度描述</td>
                        </tr>
                        <tr>
                            <td>查看KPI卡片/图表/表格</td>
                            <td>报告生成完成</td>
                            <td>展示销售收入、成本、利润等核心指标及可视化图表</td>
                            <td>数据表格支持排序、搜索；图表支持放大预览</td>
                        </tr>
                        <tr>
                            <td>点击「订阅」按钮</td>
                            <td>用户希望定期接收此报告</td>
                            <td>弹出订阅配置窗口（周期、接收人等）</td>
                            <td><span class="badge supplement">原型补充：</span>需补充订阅管理界面</td>
                        </tr>
                        <tr>
                            <td>点击「转任务」按钮</td>
                            <td>报告生成成功</td>
                            <td>弹出「选择联系人」窗口，进入任务下发界面</td>
                            <td>支持按部门筛选、搜索；支持批量选择（0-200人）</td>
                        </tr>
                        <tr>
                            <td rowspan="3"><span class="screen-reference">任务下发1</span></td>
                            <td>选择目标联系人/部门</td>
                            <td>用户点击「转任务」按钮后进入界面</td>
                            <td>支持单选/多选，显示已选人数（如0/200）</td>
                            <td>部门树状展开，支持「创建新朝天」快捷操作</td>
                        </tr>
                        <tr>
                            <td>点击「确定」按钮</td>
                            <td>选择≥1个联系人</td>
                            <td>任务下发完成，返回报告界面，显示成功提示</td>
                            <td>任务创建后支持实时跟踪（可补充任务追踪界面）</td>
                        </tr>
                        <tr>
                            <td>点击「建议」勾选项</td>
                            <td>用户查看右侧思考过程面板</td>
                            <td>展开相应的建议说明（1、2、3级等）</td>
                            <td><span class="badge optimization">优化建议：</span>建议提供建议的重要性分级展示</td>
                        </tr>
                    </tbody>
                </table>
            </div>

            <!-- 第四部分：微交互说明 -->
            <div class="section">
                <div class="section-title">
                    <span class="number">6</span>
                    关键微交互说明
                </div>

                <div class="interaction-detail">
                    <h5><svg class="svg-icon svg-icon-blue"><use xlink:href="#icon-lightning"></use></svg>微交互1：按钮状态转换</h5>
                    <ul>
                        <li><strong>初始状态：</strong>「生成数据洞察」按钮为禁用状态（灰色背景#CCCCCC，不可点击）</li>
                        <li><strong>触发条件：</strong>用户选择≥1个数据源</li>
                        <li><strong>激活状态：</strong>按钮变为蓝色#2A5298，支持点击；同时按钮下方显示绿色勾选图标<svg class="svg-icon svg-icon-blue" style="width: 0.9em; height: 0.9em; vertical-align: -0.1em; margin: 0 0.2em;"><use xlink:href="#icon-check"></use></svg></li>
                        <li><strong>点击反馈：</strong>按钮显示加载动画（旋转loading圆圈），文字变为「生成中...」</li>
                    </ul>
                </div>

                <div class="interaction-detail">
                    <h5><svg class="svg-icon svg-icon-blue"><use xlink:href="#icon-chart"></use></svg>微交互2：进度条与加载状态</h5>
                    <ul>
                        <li><strong>触发时机：</strong>点击「生成数据洞察」按钮后，系统开始处理数据</li>
                        <li><strong>0-3秒：</strong>显示简单加载动画（无进度条），文本提示「正在加载...」</li>
                        <li><strong>≥3秒：</strong>自动显示详细进度条，并行展示4个子步骤：
                            <ul style="margin-left: 20px; margin-top: 8px;">
                                <li><svg class="svg-icon svg-icon-blue" style="width: 0.9em; height: 0.9em; vertical-align: -0.1em; margin-right: 0.4em;"><use xlink:href="#icon-check"></use></svg>思考过程及进度 (6s)</li>
                                <li>⚙️ 多维度分析 (8s)</li>
                                <li>⏳ 加载提示词 (3s)</li>
                                <li><svg class="svg-icon svg-icon-blue" style="width: 0.9em; height: 0.9em; vertical-align: -0.1em; margin-right: 0.4em;"><use xlink:href="#icon-chart"></use></svg>汇总 (6s)</li>
                            </ul>
                        </li>
                        <li><strong>完成反馈：</strong>所有步骤完成后，进度条消失，报告内容自动渲染（无跳转动画，直接显示）</li>
                    </ul>
                </div>

                <div class="interaction-detail">
                    <h5><svg class="svg-icon svg-icon-blue"><use xlink:href="#icon-document"></use></svg>微交互3：卡片展开与折叠</h5>
                    <ul>
                        <li><strong>默认状态：</strong>功能卡片以紧凑卡片模式显示（标题+2行描述+icon）</li>
                        <li><strong>Hover效果：</strong>卡片边框变为蓝色，背景色变浅，显示「点击了解更多」提示</li>
                        <li><strong>点击后：</strong>卡片高度增加，展开完整描述、建议内容、相关数据源链接</li>
                        <li><strong>二次点击：</strong>卡片收起回紧凑模式</li>
                        <li><strong>锁定卡片：</strong>显示<svg class="svg-icon" style="width: 1em; height: 1em; vertical-align: -0.1em; margin: 0 0.2em;"><use xlink:href="#icon-lock"></use></svg>图标，鼠标hover时提示「此功能正在开发中」</li>
                    </ul>
                </div>

                <div class="interaction-detail">
                    <h5><svg class="svg-icon svg-icon-blue"><use xlink:href="#icon-users"></use></svg>微交互4：多选联系人</h5>
                    <ul>
                        <li><strong>界面形式：</strong>树状结构展示部门+员工，支持多级展开</li>
                        <li><strong>选择交互：</strong>点击部门名称可全选该部门下所有员工；点击员工可单选</li>
                        <li><strong>实时反馈：</strong>顶部显示「已选联系人：X/200」，每次选择都动态更新</li>
                        <li><strong>搜索功能：</strong>支持模糊搜索员工名称，快速定位目标</li>
                        <li><strong>确定按钮：</strong>选择数≥1时按钮为蓝色可点击；选择数=0时按钮灰色禁用</li>
                    </ul>
                </div>

                <div class="interaction-detail">
                    <h5><svg class="svg-icon svg-icon-blue"><use xlink:href="#icon-comment"></use></svg>微交互5：AI对话框输入反馈</h5>
                    <ul>
                        <li><strong>焦点状态：</strong>输入框被点击时，底部边框变为蓝色，显示虚拟键盘</li>
                        <li><strong>字数限制：</strong>支持最多2000字输入，实时显示已输入字数/上限</li>
                        <li><strong>工具栏交互：</strong>
                            <ul style="margin-left: 20px; margin-top: 8px;">
                                <li>附件按钮：点击打开文件选择器，支持pdf、excel、csv格式</li>
                                <li>内容编辑：支持富文本编辑（加粗、斜体、列表等）</li>
                                <li>数据洞察：快速插入常用数据维度（客户、部门、产品等）</li>
                                <li>智能指建：点击显示AI推荐的问题模板</li>
                            </ul>
                        </li>
                        <li><strong>发送按钮：</strong>输入框为空时按钮禁用；有内容时变为蓝色可点击</li>
                    </ul>
                </div>
            </div>

            <!-- 第五部分：异常处理流程 -->
            <div class="section">
                <div class="section-title">
                    <span class="number">5</span>
                    异常处理与分支路径
                </div>

                <div class="error-box">
                    <strong>异常1：数据加载失败</strong>
                    当报告生成过程中，后端数据源无响应或超时（>30秒）时，系统应自动重试2次。若仍失败，显示「数据加载失败，请检查数据源连接」提示，并提供「重新生成」和「反馈问题」两个按钮选项。用户点击「反馈问题」时，自动记录本次生成的sessionId和错误日志。
                </div>

                <div class="error-box">
                    <strong>异常2：未选择数据源</strong>
                    用户未选择任何数据源就点击「生成数据洞察」按钮时，系统应显示红色警告提示：「请至少选择1个数据源」，同时左侧数据源面板高亮闪动（持续2秒），引导用户完成选择。
                </div>

                <div class="error-box">
                    <strong>异常3：报告生成超时</strong>
                    若报告生成时间超过60秒仍未完成，系统应显示「分析耗时较长，您可先进行其他操作，稍后查看报告」的友好提示，同时提供「后台继续分析」和「取消任务」两个选项。用户可返回首页继续新建对话，系统将在后台继续处理。
                </div>

                <div class="error-box">
                    <strong>异常4：任务下发失败</strong>
                    点击「转任务」后，若任务创建失败（如网络错误、权限不足），显示弹窗提示「任务创建失败，请稍后重试」，保留已选联系人列表（不清空），支持用户修改后重新提交。
                </div>

                <div class="branch-path">
                    <h5><svg class="svg-icon svg-icon-blue"><use xlink:href="#icon-branch"></use></svg>分支路径1：用户中途取消分析</h5>
                    <p>若用户在报告生成过程中（进度条显示中）点击「取消」，系统应立即停止后端计算任务，清空进度条，返回到数据洞察界面2，保留用户之前的数据源选择和输入内容（支持快速重新生成）。</p>
                </div>

                <div class="branch-path">
                    <h5><svg class="svg-icon svg-icon-blue"><use xlink:href="#icon-branch"></use></svg>分支路径2：用户重新编辑分析参数</h5>
                    <p>用户在报告生成界面查看结果后，若希望修改分析维度或数据源，可点击「返回编辑」按钮（原型补充），返回执行规划界面，修改后可重新生成报告。系统应保留此前的多个报告版本，用户可在「我的报告」中查看历史版本对比。</p>
                </div>

                <div class="branch-path">
                    <h5><svg class="svg-icon svg-icon-blue"><use xlink:href="#icon-branch"></use></svg>分支路径3：用户仅订阅不转任务</h5>
                    <p>用户可在报告生成界面单独点击「订阅」按钮配置定期报告，而不必同时执行转任务操作。订阅配置应支持：周期选择（日/周/月）、接收人配置、报告模板筛选。订阅成功后，系统在指定时间自动生成并发送报告。</p>
                </div>

                <div class="branch-path">
                    <h5><svg class="svg-icon svg-icon-blue"><use xlink:href="#icon-branch"></use></svg>分支路径4：用户跳过AI建议直接生成报告</h5>
                    <p>虽然规范流程包含「AI引导分析」阶段，但系统应允许高级用户直接跳过此步，在数据洞察界面1中点击「快速生成」（原型补充）直接配置参数并生成报告。此时系统不展示AI诊断/归因/建议框架，仅进行数据处理和报告输出。</p>
                </div>
            </div>

            <!-- 第六部分：原型补充与优化建议 -->
            <div class="section">
                <div class="section-title">
                    <span class="number">7</span>
                    原型补充与优化建议
                </div>

                <div class="interaction-detail">
                    <h5><span class="badge supplement">原型补充</span>界面补充1：报告订阅配置界面</h5>
                    <p>当用户点击「订阅」按钮时，系统应弹出订阅配置窗口，包含以下字段：</p>
                    <ul>
                        <li><strong>订阅周期：</strong>日、周、月、自定义（日期选择器）</li>
                        <li><strong>订阅接收人：</strong>支持多选，可选用户或部门</li>
                        <li><strong>报告模板：</strong>完整版/摘要版/自定义维度</li>
                        <li><strong>发送时间：</strong>时间选择器（精确到小时）</li>
                        <li><strong>启用状态：</strong>订阅开启/关闭切换</li>
                    </ul>
                </div>

                <div class="interaction-detail">
                    <h5><span class="badge supplement">原型补充</span>界面补充2：报告历史版本对比界面</h5>
                    <p>在「我的报告」菜单中，用户应能查看同一分析主题的多个报告版本，支持：</p>
                    <ul>
                        <li>版本时间线展示（按生成时间排序）</li>
                        <li>版本之间的KPI变化对比（△增减百分比）</li>
                        <li>版本删除/导出/分享操作</li>
                        <li>版本详情快速预览</li>
                    </ul>
                </div>

                <div class="interaction-detail">
                    <h5><span class="badge supplement">原型补充</span>界面补充3：任务追踪与反馈界面</h5>
                    <p>任务下发后，系统应提供任务追踪界面，显示：</p>
                    <ul>
                        <li>任务接收人的阅读状态（已读/未读）</li>
                        <li>任务完成情况（进行中/已完成/超期）</li>
                        <li>关联行动项（如「降低成本20%」的具体执行记录）</li>
                        <li>反馈汇总（接收人的完成反馈和补充说明）</li>
                    </ul>
                </div>

                <div class="interaction-detail">
                    <h5><span class="badge optimization">优化建议</span>优化1：提升数据源选择效率</h5>
                    <ul>
                        <li><strong>当前状态：</strong>数据源以列表形式展示，用户需逐个查看和选择</li>
                        <li><strong>优化方案：</strong>
                            <ul style="margin-left: 20px; margin-top: 8px;">
                                <li>添加「数据源搜索框」，支持按表名/库名模糊搜索</li>
                                <li>添加「常用数据源」收藏功能，快速定位高频使用数据</li>
                                <li>支持「预设模板」，将常见分析场景（如「客户收益分析」）的数据源预选，用户可一键应用</li>
                            </ul>
                        </li>
                        <li><strong>预期效果：</strong>减少用户选择时间50%以上</li>
                    </ul>
                </div>

                <div class="interaction-detail">
                    <h5><span class="badge optimization">优化建议</span>优化2：增强流程图交互</h5>
                    <ul>
                        <li><strong>当前状态：</strong>执行规划界面的流程图为静态展示，用户无法与流程节点交互</li>
                        <li><strong>优化方案：</strong>
                            <ul style="margin-left: 20px; margin-top: 8px;">
                                <li>流程节点支持点击展开，显示该步骤的详细配置（如维度选择、算子参数）</li>
                                <li>流程节点支持拖拽调整顺序（高级用户），改变分析维度的执行优先级</li>
                                <li>提供「流程导出」功能，用户可导出为JSON格式配置文件，支持复用和版本控制</li>
                            </ul>
                        </li>
                        <li><strong>预期效果：</strong>提升高级用户的自定义分析能力</li>
                    </ul>
                </div>

                <div class="interaction-detail">
                    <h5><span class="badge optimization">优化建议</span>优化3：改进报告导出格式</h5>
                    <ul>
                        <li><strong>当前状态：</strong>原型中未明确显示报告导出功能（原型缺失）</li>
                        <li><strong>优化方案：</strong>
                            <ul style="margin-left: 20px; margin-top: 8px;">
                                <li>在报告详情页添加「导出」按钮，支持多格式：PDF（保留格式）/ Excel（含数据表）/ PPT（摘要版）/ Markdown（文本版）</li>
                                <li>导出前支持配置：选择包含的章节、数据敏感性设置（脱敏/完整）、接收人限制</li>
                                <li>支持「邮件发送」和「分享链接」两种导出方式，后者应设置有效期和访问权限</li>
                            </ul>
                        </li>
                        <li><strong>预期效果：</strong>提升报告的易用性和传播效率</li>
                    </ul>
                </div>

                <div class="interaction-detail">
                    <h5><span class="badge optimization">优化建议</span>优化4：完善AI对话上下文管理</h5>
                    <ul>
                        <li><strong>当前状态：</strong>AI对话框仅支持当前对话的多轮交互，对话历史管理不明确</li>
                        <li><strong>优化方案：</strong>
                            <ul style="margin-left: 20px; margin-top: 8px;">
                                <li>左侧导航栏的「历史对话」需支持搜索、标签分类、删除等管理操作</li>
                                <li>支持「对话保存为模板」，便于用户复用常见分析场景</li>
                                <li>对话中的AI回复支持「点赞/点踩」反馈机制，优化AI模型训练</li>
                            </ul>
                        </li>
                        <li><strong>预期效果：</strong>提升AI个性化推荐准确度，同时帮助用户更高效地复用历史分析</li>
                    </ul>
                </div>
            </div>

            <!-- 第七部分：触发条件与权限矩阵 -->
            <div class="section">
                <div class="section-title">
                    <span class="number">8</span>
                    功能权限矩阵
                </div>

                <table class="interaction-table">
                    <thead>
                        <tr>
                            <th style="width: 25%;">功能</th>
                            <th style="width: 25%;">权限要求</th>
                            <th style="width: 25%;">可用范围</th>
                            <th style="width: 25%;">特殊限制</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td><strong>新建对话</strong></td>
                            <td>所有登录用户</td>
                            <td>全局可用</td>
                            <td>无限制</td>
                        </tr>
                        <tr>
                            <td><strong>客户收益诊断</strong></td>
                            <td>所有用户（已开放）</td>
                            <td>数据洞察界面</td>
                            <td>无</td>
                        </tr>
                        <tr>
                            <td><strong>网点/区域收益诊断</strong></td>
                            <td>高级用户/管理员</td>
                            <td>数据洞察界面</td>
                            <td>显示<svg class="svg-icon" style="width: 1em; height: 1em; vertical-align: -0.1em; margin: 0 0.2em;"><use xlink:href="#icon-lock"></use></svg>锁定，需升级权限</td>
                        </tr>
                        <tr>
                            <td><strong>生成数据洞察</strong></td>
                            <td>所有用户</td>
                            <td>数据洞察界面2</td>
                            <td>必须选择≥1个数据源</td>
                        </tr>
                        <tr>
                            <td><strong>订阅报告</strong></td>
                            <td>所有用户</td>
                            <td>报告生成界面</td>
                            <td>每用户最多订阅50个报告</td>
                        </tr>
                        <tr>
                            <td><strong>转任务</strong></td>
                            <td>具有任务分配权限的用户</td>
                            <td>报告生成/任务下发界面</td>
                            <td>仅在报告成功生成后可用；必须选择≥1个接收人</td>
                        </tr>
                        <tr>
                            <td><strong>编辑提示词</strong></td>
                            <td>所有用户（基础编辑）/ 管理员（全局编辑）</td>
                            <td>数据洞察界面2</td>
                            <td>基础用户仅可编辑当前对话的提示词</td>
                        </tr>
                        <tr>
                            <td><strong>上传附件</strong></td>
                            <td>所有用户</td>
                            <td>数据洞察界面2</td>
                            <td>单个文件≤50MB，支持pdf/excel/csv格式</td>
                        </tr>
                        <tr>
                            <td><strong>查看分析历史</strong></td>
                            <td>分析创建者本人及授权用户</td>
                            <td>我的报告/洞察菜单</td>
                            <td>保留180天；可设置共享权限</td>
                        </tr>
                    </tbody>
                </table>
            </div>

            <!-- 第八部分：用户角色与能力映射 -->
            <div class="section">
                <div class="section-title">
                    <span class="number">9</span>
                    核心用户角色与能力映射
                </div>

                <div class="interaction-detail">
                    <h5><svg class="svg-icon svg-icon-blue"><use xlink:href="#icon-users"></use></svg>角色1：财务分析人员（主要用户）</h5>
                    <ul>
                        <li><strong>核心用途：</strong>通过AI助手快速生成财务分析报告，支撑管理决策</li>
                        <li><strong>典型旅程：</strong>发起新对话 → 选择「客户收益诊断」 → AI给出诊断结论 → 生成详细报告 → 分享给管理层</li>
                        <li><strong>关键功能：</strong>数据洞察界面、报告生成、订阅报告</li>
                        <li><strong>预期使用频率：</strong>每天2-3次</li>
                    </ul>
                </div>

                <div class="interaction-detail">
                    <h5><svg class="svg-icon svg-icon-blue"><use xlink:href="#icon-users"></use></svg>角色2：部门管理者（二级用户）</h5>
                    <ul>
                        <li><strong>核心用途：</strong>接收财务分析报告和相关任务，追踪执行进展，反馈完成情况</li>
                        <li><strong>典型旅程：</strong>接收「转任务」通知 → 查看报告详情 → 理解分析结论 → 执行关联行动 → 反馈执行结果</li>
                        <li><strong>关键功能：</strong>任务下发、任务追踪、反馈管理</li>
                        <li><strong>预期使用频率：</strong>每周1-2次</li>
                    </ul>
                </div>

                <div class="interaction-detail">
                    <h5><svg class="svg-icon svg-icon-blue"><use xlink:href="#icon-users"></use></svg>角色3：数据科学家/高级分析师（高级用户）</h5>
                    <ul>
                        <li><strong>核心用途：</strong>自定义分析流程，优化数据处理参数，构建分析模板</li>
                        <li><strong>典型旅程：</strong>新对话 → 访问「执行规划」界面 → 自定义数据源与维度 → 调整分析算子 → 生成高阶报告 → 保存为模板</li>
                        <li><strong>关键功能：</strong>执行规划、提示词编辑、流程导出、预设模板管理</li>
                        <li><strong>预期使用频率：</strong>每周2-3次</li>
                    </ul>
                </div>
            </div>

            <!-- 第九部分：页面转换时间线 -->
            <div class="section">
                <div class="section-title">
                    <span class="number">4</span>
                    完整用户操作时间线（理想场景）
                </div>

                <table class="interaction-table">
                    <thead>
                        <tr>
                            <th style="width: 8%;">时刻</th>
                            <th style="width: 20%;">用户操作</th>
                            <th style="width: 25%;">系统反馈</th>
                            <th style="width: 22%;">界面状态</th>
                            <th style="width: 25%;">预计耗时</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>T+0s</td>
                            <td>用户进入应用，发起新对话</td>
                            <td>加载数据洞察界面1</td>
                            <td>显示5个功能卡片（1个激活+4个锁定）</td>
                            <td>0-2s</td>
                        </tr>
                        <tr>
                            <td>T+2s</td>
                            <td>点击「客户收益诊断洞察」卡片</td>
                            <td>卡片展开，跳转至数据洞察界面2</td>
                            <td>显示详细分析指引与AI对话框</td>
                            <td>0-1s</td>
                        </tr>
                        <tr>
                            <td>T+3s</td>
                            <td>用户查看左侧数据源，选择1-2个数据源</td>
                            <td>实时显示已选数据源数量；「生成数据洞察」按钮变蓝</td>
                            <td>数据源面板高亮，按钮激活</td>
                            <td>15-30s</td>
                        </tr>
                        <tr>
                            <td>T+33s</td>
                            <td>点击「生成数据洞察」按钮</td>
                            <td>按钮显示加载动画，跳转至执行规划界面</td>
                            <td>展示分析流程图，可浏览各节点详情</td>
                            <td>1-2s</td>
                        </tr>
                        <tr>
                            <td>T+35s</td>
                            <td>用户在执行规划界面浏览流程图</td>
                            <td>后台异步执行数据处理</td>
                            <td>流程图完全展开，支持交互</td>
                            <td>10-20s</td>
                        </tr>
                        <tr>
                            <td>T+55s</td>
                            <td>用户点击确认或返回</td>
                            <td>跳转至报告生成界面，显示加载进度</td>
                            <td>显示「思考过程及进度」面板（4个子步骤）</td>
                            <td>1s</td>
                        </tr>
                        <tr>
                            <td>T+56s</td>
                            <td>用户查看实时进度条</td>
                            <td>并行处理4个步骤，逐步完成</td>
                            <td>进度条动态更新，显示各步骤状态</td>
                            <td>8-15s</td>
                        </tr>
                        <tr>
                            <td>T+71s</td>
                            <td>报告生成完成，用户查看结果</td>
                            <td>进度条消失，展示KPI卡片、图表、数据表格</td>
                            <td>完整报告内容渲染，支持滚动浏览</td>
                            <td>2-3s</td>
                        </tr>
                        <tr>
                            <td>T+74s</td>
                            <td>用户点击「转任务」按钮</td>
                            <td>弹出「选择联系人」窗口</td>
                            <td>显示部门树状结构和员工列表</td>
                            <td>0.5s</td>
                        </tr>
                        <tr>
                            <td>T+75s</td>
                            <td>用户搜索并选择目标联系人</td>
                            <td>实时更新已选人数显示（如「已选：3/200」）</td>
                            <td>被选项高亮，显示勾选状态</td>
                            <td>20-30s</td>
                        </tr>
                        <tr>
                            <td>T+105s</td>
                            <td>用户点击「确定」完成任务下发</td>
                            <td>窗口关闭，返回报告界面，显示成功提示</td>
                            <td>「转任务」按钮变为「已下发」（禁用状态）</td>
                            <td>1-2s</td>
                        </tr>
                        <tr>
                            <td>T+107s</td>
                            <td>流程结束</td>
                            <td>用户可继续浏览报告、订阅报告或返回首页</td>
                            <td>全流程完成，用户可选择后续操作</td>
                            <td>-</td>
                        </tr>
                    </tbody>
                </table>
                <p style="margin-top: 15px; color: #666; font-size: 13px;">
                    💡 <strong>总耗时：</strong>约107秒（1分47秒）从发起分析到完成任务下发。若用户仅进行分析不下发任务，总耗时约74秒。
                </p>
            </div>

            <!-- 第十部分：总结与关键指标 -->
            <div class="section">
                <div class="section-title">
                    <span class="number">10</span>
                    关键设计指标与成功度量
                </div>

                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-top: 20px;">
                    <div class="stage-card">
                        <h4>📊 用户完成率</h4>
                        <p><strong style="color: #2a5298; font-size: 20px;">≥80%</strong></p>
                        <p style="font-size: 12px; margin-top: 10px;">新用户从「发起对话」到「生成报告」的完成度，目标不低于80%</p>
                    </div>

                    <div class="stage-card">
                        <h4>⏱️ 平均操作时长</h4>
                        <p><strong style="color: #2a5298; font-size: 20px;">≤2分钟</strong></p>
                        <p style="font-size: 12px; margin-top: 10px;">从发起分析到生成报告的平均耗时，目标不超过2分钟</p>
                    </div>

                    <div class="stage-card">
                        <h4>🎯 转任务成功率</h4>
                        <p><strong style="color: #2a5298; font-size: 20px;">≥75%</strong></p>
                        <p style="font-size: 12px; margin-top: 10px;">生成报告的用户中，转任务的比例（反映价值转化）</p>
                    </div>

                    <div class="stage-card">
                        <h4>♻️ 复用率</h4>
                        <p><strong style="color: #2a5298; font-size: 20px;">≥60%</strong></p>
                        <p style="font-size: 12px; margin-top: 10px;">用户基于历史分析再次生成报告的比例，反映工具粘性</p>
                    </div>

                    <div class="stage-card">
                        <h4>😊 用户满意度</h4>
                        <p><strong style="color: #2a5298; font-size: 20px;">≥4.5/5</strong></p>
                        <p style="font-size: 12px; margin-top: 10px;">报告生成后用户对分析质量的评分（5分制）</p>
                    </div>

                    <div class="stage-card">
                        <h4>📈 任务反馈率</h4>
                        <p><strong style="color: #2a5298; font-size: 20px;">≥50%</strong></p>
                        <p style="font-size: 12px; margin-top: 10px;">接收任务的用户完成反馈的比例，反映闭环管理效果</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- 页脚 -->
        <div class="footer">
            <p><strong>文档信息</strong> · 财务分析智能体用户旅程地图</p>
            <p>生成时间：2026年2月9日 | 原型版本：V1.0</p>
            <p style="font-size: 12px; margin-top: 15px; color: #999;">
                <span class="badge supplement">原型补充</span> 标注部分缺失在原型图中的必要界面<br/>
                <span class="badge optimization">优化建议</span> 标注可增强现有交互的改进方案<br/>
                <span class="badge danger">异常处理</span> 标注系统异常时的应对流程
            </p>
        </div>
    </div>
</body>
</html>

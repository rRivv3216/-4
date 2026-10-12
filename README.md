<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>منصة الكيمياء التفاعلية - الاختبارات والمحاكاة</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root {
            --primary: #4a6baf;
            --secondary: #6d28d9;
            --accent: #06d6a0;
            --light: #f8fafc;
            --dark: #1e293b;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #ef4444;
            --card-bg: rgba(255, 255, 255, 0.95);
            --transition: all 0.3s ease;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            min-height: 100vh;
            color: var(--dark);
            overflow-x: hidden;
        }

        .background-animation {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            z-index: -1; overflow: hidden;
            background: linear-gradient(125deg, #0f2b5e 0%, #1e3c72 25%, #2a5298 50%, #3a6bc5 75%, #4a85f2 100%);
        }

        .floating-element {
            position: absolute; border-radius: 50%;
            background: rgba(255, 255, 255, 0.1);
            animation: floatElement 20s infinite linear;
        }
        .floating-element:nth-child(1) { width: 150px; height: 150px; top: 10%; left: 5%; animation-delay: 0s; background: radial-gradient(circle, rgba(74, 107, 175, 0.3) 0%, rgba(74, 107, 175, 0) 70%); }
        .floating-element:nth-child(2) { width: 200px; height: 200px; top: 60%; left: 80%; animation-delay: 5s; background: radial-gradient(circle, rgba(109, 40, 217, 0.3) 0%, rgba(109, 40, 217, 0) 70%); }
        .floating-element:nth-child(3) { width: 100px; height: 100px; top: 80%; left: 20%; animation-delay: 10s; background: radial-gradient(circle, rgba(6, 214, 160, 0.3) 0%, rgba(6, 214, 160, 0) 70%); }
        .floating-element:nth-child(4) { width: 180px; height: 180px; top: 30%; left: 70%; animation-delay: 15s; background: radial-gradient(circle, rgba(245, 158, 11, 0.3) 0%, rgba(245, 158, 11, 0) 70%); }
        .floating-element:nth-child(5) { width: 120px; height: 120px; top: 70%; left: 40%; animation-delay: 20s; background: radial-gradient(circle, rgba(239, 68, 68, 0.3) 0%, rgba(239, 68, 68, 0) 70%); }

        @keyframes floatElement {
            0% { transform: translate(0, 0) rotate(0deg) scale(1); opacity: 0.7; }
            25% { transform: translate(50px, -30px) rotate(90deg) scale(1.1); opacity: 0.5; }
            50% { transform: translate(-20px, 40px) rotate(180deg) scale(0.9); opacity: 0.8; }
            75% { transform: translate(-40px, -20px) rotate(270deg) scale(1.05); opacity: 0.6; }
            100% { transform: translate(0, 0) rotate(360deg) scale(1); opacity: 0.7; }
        }

        .grid-lines {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background-image: 
                linear-gradient(rgba(255, 255, 255, 0.05) 1px, transparent 1px),
                linear-gradient(90deg, rgba(255, 255, 255, 0.05) 1px, transparent 1px);
            background-size: 50px 50px; z-index: -1;
        }

        .app-container { display: flex; min-height: 100vh; }

        .sidebar {
            width: 280px;
            background: linear-gradient(180deg, rgba(74, 107, 175, 0.9), rgba(109, 40, 217, 0.9));
            color: white; padding: 20px 0;
            box-shadow: 5px 0 15px rgba(0, 0, 0, 0.1);
            z-index: 100; position: relative; backdrop-filter: blur(10px);
        }

        .logo { text-align: center; padding: 20px; border-bottom: 1px solid rgba(255, 255, 255, 0.2); margin-bottom: 20px; }
        .logo h1 { font-size: 1.5em; display: flex; align-items: center; justify-content: center; }
        .logo i { margin-left: 10px; font-size: 1.8em; }

        .nav-menu { list-style: none; padding: 0 15px; }
        .nav-item { margin-bottom: 8px; }
        .nav-link {
            display: flex; align-items: center; padding: 15px 20px; color: white;
            text-decoration: none; border-radius: 10px; transition: var(--transition);
        }
        .nav-link:hover, .nav-link.active { background: rgba(255, 255, 255, 0.2); transform: translateX(5px); }
        .nav-link i { margin-left: 15px; font-size: 1.2em; }

        .user-section { padding: 20px; border-top: 1px solid rgba(255, 255, 255, 0.2); margin-top: 20px; }
        .user-info { display: flex; align-items: center; }
        .user-avatar {
            width: 50px; height: 50px; border-radius: 50%; background: var(--accent);
            display: flex; align-items: center; justify-content: center;
            font-size: 1.5em; color: white; margin-left: 15px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
        }

        .team-section { padding: 20px; border-top: 1px solid rgba(255, 255, 255, 0.2); margin-top: 20px; }
        .team-section h3 { margin-bottom: 15px; font-size: 1.1em; display: flex; align-items: center; }
        .team-section h3 i { margin-left: 10px; }
        .team-member {
            display: flex; align-items: center; padding: 10px; margin-bottom: 8px;
            border-radius: 8px; transition: var(--transition); cursor: pointer;
        }
        .team-member:hover { background: rgba(255, 255, 255, 0.1); }
        .team-avatar {
            width: 35px; height: 35px; border-radius: 50%;
            display: flex; align-items: center; justify-content: center;
            margin-left: 10px; font-size: 0.9em; color: white;
        }
        .team-member-info { flex: 1; }
        .team-member-name { font-size: 0.9em; font-weight: bold; }
        .team-member-role { font-size: 0.75em; opacity: 0.8; }

        .main-content { flex: 1; padding: 20px; overflow-y: auto; }

        .header {
            background: var(--card-bg); border-radius: 15px; padding: 20px 30px;
            margin-bottom: 25px; box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            display: flex; justify-content: space-between; align-items: center;
            backdrop-filter: blur(10px); border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .header h2 { color: var(--primary); display: flex; align-items: center; }
        .header h2 i { margin-left: 15px; }
        .user-actions { display: flex; gap: 15px; }

        .login-screen {
            display: flex; flex-direction: column; justify-content: center; align-items: center;
            min-height: 100vh; padding: 20px;
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
        }
        .login-container {
            background: var(--card-bg); border-radius: 20px; padding: 40px;
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
            width: 100%; max-width: 500px; text-align: center;
            backdrop-filter: blur(10px); border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .login-icon { font-size: 4em; color: var(--primary); margin-bottom: 20px; }
        .login-container h1 { color: var(--dark); margin-bottom: 10px; font-size: 2.2em; }
        .login-container p { color: #666; margin-bottom: 30px; font-size: 1.1em; }

        .form-group { margin-bottom: 20px; text-align: right; }
        .form-group label { display: block; margin-bottom: 8px; color: var(--dark); font-weight: bold; }
        .form-control {
            width: 100%; padding: 15px; border: 2px solid #e1e5f1;
            border-radius: 10px; font-size: 1em; background: white; transition: var(--transition);
        }
        .form-control:focus {
            border-color: var(--primary); outline: none;
            box-shadow: 0 0 0 3px rgba(74, 107, 175, 0.3);
        }

        .cards-container {
            display: grid; grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 25px; margin-bottom: 30px;
        }
        .card {
            background: var(--card-bg); border-radius: 15px; padding: 25px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1); transition: var(--transition);
            cursor: pointer; backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            position: relative; overflow: hidden;
        }
        .card::before {
            content: ''; position: absolute; top: 0; left: 0; width: 100%; height: 5px;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
        }
        .card:hover { transform: translateY(-5px); box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15); }
        .card-header { display: flex; align-items: center; margin-bottom: 15px; }
        .card-icon {
            width: 60px; height: 60px; border-radius: 12px;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            display: flex; align-items: center; justify-content: center;
            font-size: 1.8em; color: white; margin-left: 15px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
        }
        .card h3 { color: var(--dark); font-size: 1.3em; }
        .card p { color: #666; line-height: 1.6; margin-bottom: 20px; }

        .btn {
            padding: 12px 25px;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white; border: none; border-radius: 10px; cursor: pointer;
            font-size: 1em; font-weight: bold; transition: var(--transition);
            display: inline-flex; align-items: center; justify-content: center;
            box-shadow: 0 4px 10px rgba(74, 107, 175, 0.3);
            position: relative; overflow: hidden;
        }
        .btn::before {
            content: ''; position: absolute; top: 0; left: -100%;
            width: 100%; height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transition: left 0.5s;
        }
        .btn:hover::before { left: 100%; }
        .btn:hover { transform: translateY(-2px); box-shadow: 0 6px 15px rgba(74, 107, 175, 0.4); }
        .btn i { margin-left: 8px; }
        .btn-success { background: linear-gradient(135deg, var(--success), #059669); }
        .btn-warning { background: linear-gradient(135deg, var(--warning), #d97706); }
        .btn-danger { background: linear-gradient(135deg, var(--danger), #dc2626); }
        .btn-outline {
            background: transparent; border: 2px solid var(--primary);
            color: var(--primary); box-shadow: none;
        }

        .screen { display: none; }
        .screen.active { display: block; animation: fadeIn 0.5s ease; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        .welcome-screen { text-align: center; padding: 40px 20px; }
        .welcome-icon { font-size: 5em; color: var(--primary); margin-bottom: 20px; }
        .welcome-screen h1 { color: var(--dark); margin-bottom: 15px; font-size: 2.5em; }
        .welcome-screen p { color: #666; font-size: 1.2em; max-width: 600px; margin: 0 auto 30px; line-height: 1.6; }

        .settings-container {
            background: var(--card-bg); border-radius: 15px; padding: 30px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(10px); border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .settings-group { margin-bottom: 30px; }
        .settings-group h3 {
            color: var(--primary); margin-bottom: 20px; padding-bottom: 10px;
            border-bottom: 2px solid #f1f5f9; display: flex; align-items: center;
        }
        .settings-group h3 i { margin-left: 10px; }
        .setting-item {
            display: flex; justify-content: space-between; align-items: center;
            padding: 15px 0; border-bottom: 1px solid #f1f5f9;
        }
        .setting-info h4 { color: var(--dark); margin-bottom: 5px; }
        .setting-info p { color: #666; font-size: 0.9em; }

        .quiz-setup {
            background: var(--card-bg); border-radius: 15px; padding: 30px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1); max-width: 600px; margin: 0 auto;
            backdrop-filter: blur(10px); border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .quiz-options { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 30px; }
        .quiz-option {
            padding: 20px; border: 2px solid #e1e5f1; border-radius: 10px;
            cursor: pointer; transition: var(--transition); text-align: center;
            position: relative; overflow: hidden;
        }
        .quiz-option::before {
            content: ''; position: absolute; top: 0; left: 0; width: 100%; height: 100%;
            background: linear-gradient(135deg, rgba(74, 107, 175, 0.1), rgba(109, 40, 217, 0.1));
            opacity: 0; transition: var(--transition);
        }
        .quiz-option:hover { border-color: var(--primary); transform: translateY(-3px); }
        .quiz-option:hover::before { opacity: 1; }
        .quiz-option.selected { border-color: var(--primary); background: rgba(74, 107, 175, 0.1); }
        .quiz-option i { font-size: 2em; margin-bottom: 10px; color: var(--primary); }
        .quiz-controls { display: flex; gap: 15px; margin-top: 30px; }

        .quiz-container { display: flex; gap: 20px; flex-wrap: wrap; }
        .quiz-content {
            flex: 1; min-width: 300px; background: var(--card-bg);
            border-radius: 15px; padding: 30px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(10px); border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .whiteboard-container {
            flex: 1; min-width: 300px; background: var(--card-bg);
            border-radius: 15px; padding: 20px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(10px); border: 1px solid rgba(255, 255, 255, 0.2);
            display: flex; flex-direction: column;
        }
        .whiteboard-header {
            display: flex; justify-content: space-between; align-items: center;
            margin-bottom: 15px; padding-bottom: 10px; border-bottom: 2px solid #f1f5f9;
        }
        .whiteboard-frame {
            width: 100%; height: 500px; border: none; border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        .whiteboard-info { margin-top: 15px; text-align: center; font-size: 0.9em; color: #666; }

        .quiz-header {
            display: flex; justify-content: space-between; align-items: center;
            margin-bottom: 25px; padding-bottom: 15px; border-bottom: 2px solid #f1f5f9;
        }
        .quiz-info { display: flex; gap: 20px; }
        .quiz-timer {
            background: var(--warning); color: white; padding: 8px 15px;
            border-radius: 20px; font-weight: bold;
            box-shadow: 0 4px 10px rgba(245, 158, 11, 0.3);
        }
        .progress-container { margin-bottom: 25px; }
        .progress-bar {
            height: 10px; background: #e0e0e0; border-radius: 5px;
            overflow: hidden; box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.1);
        }
        .progress {
            height: 100%; background: linear-gradient(90deg, var(--primary), var(--secondary));
            width: 0%; transition: width 0.5s ease; border-radius: 5px;
        }

        .question {
            font-size: 1.4em; margin-bottom: 25px; color: var(--dark);
            line-height: 1.6; padding: 20px; background: #f8fafc;
            border-radius: 10px; border-right: 4px solid var(--primary);
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
        }
        .options { display: grid; grid-template-columns: 1fr; gap: 15px; margin-bottom: 30px; }
        .option {
            padding: 18px 20px; background: white; border: 2px solid #e1e5f1;
            border-radius: 10px; cursor: pointer; transition: var(--transition);
            display: flex; align-items: center; position: relative; overflow: hidden;
        }
        .option::before {
            content: ''; position: absolute; top: 0; left: 0; width: 5px; height: 100%;
            background: var(--primary); transform: scaleY(0); transition: var(--transition);
        }
        .option:hover { border-color: var(--primary); transform: translateY(-2px); box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1); }
        .option:hover::before { transform: scaleY(1); }
        .option.selected { background: var(--primary); color: white; border-color: var(--primary); }
        .option.correct { background: var(--success); color: white; border-color: var(--success); }
        .option.wrong { background: var(--danger); color: white; border-color: var(--danger); }
        .option.disabled { cursor: not-allowed; opacity: 0.7; }
        .option-number {
            display: inline-flex; align-items: center; justify-content: center;
            width: 30px; height: 30px; background: rgba(0, 0, 0, 0.1);
            border-radius: 50%; margin-left: 15px; font-weight: bold;
        }
        .selected .option-number, .correct .option-number, .wrong .option-number {
            background: rgba(255, 255, 255, 0.3);
        }
        .explanation {
            background: #e8f5e9; padding: 20px; border-radius: 10px;
            margin-top: 20px; border-right: 4px solid var(--success);
            display: none; box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
        }
        .explanation h3 { color: #2e7d32; margin-bottom: 10px; display: flex; align-items: center; }
        .explanation h3 i { margin-left: 10px; }

        .result-container { text-align: center; padding: 30px; }
        .result-score {
            font-size: 4em; font-weight: bold; color: var(--primary);
            margin: 20px 0; text-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        .result-chart { width: 250px; height: 250px; margin: 0 auto; }
        .comparison {
            background: #f5f7ff; padding: 20px; border-radius: 10px;
            margin: 20px 0; box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
        }
        .weak-lessons { text-align: right; margin-top: 30px; }
        .lesson-item {
            background: #ffebee; padding: 15px; margin: 10px 0;
            border-radius: 10px; border-right: 4px solid var(--danger);
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
        }

        .progress-screen { padding: 20px; }
        .progress-stats {
            display: grid; grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px; margin-bottom: 30px;
        }
        .stat-card {
            background: var(--card-bg); border-radius: 15px; padding: 20px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1); text-align: center;
            backdrop-filter: blur(10px); border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .stat-card i { font-size: 2.5em; color: var(--primary); margin-bottom: 15px; }
        .stat-card h3 { color: var(--dark); margin-bottom: 10px; }
        .stat-card .stat-value { font-size: 2em; font-weight: bold; color: var(--primary); }

        .progress-history {
            background: var(--card-bg); border-radius: 15px; padding: 30px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(10px); border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .history-table { width: 100%; border-collapse: collapse; margin-top: 20px; }
        .history-table th, .history-table td {
            padding: 15px; text-align: right; border-bottom: 1px solid #e1e5f1;
        }
        .history-table th { background: #f8fafc; color: var(--dark); font-weight: bold; }
        .history-table tr:last-child td { border-bottom: none; }
        .score-badge { padding: 5px 10px; border-radius: 20px; font-weight: bold; color: white; }
        .score-high { background: var(--success); }
        .score-medium { background: var(--warning); }
        .score-low { background: var(--danger); }

        .leaderboard-screen { padding: 20px; }
        .leaderboard-container {
            background: var(--card-bg); border-radius: 15px; padding: 30px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(10px); border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .leaderboard-list { margin-top: 20px; }
        .leaderboard-item {
            display: flex; align-items: center; padding: 15px;
            border-radius: 10px; margin-bottom: 10px;
            background: #f8fafc; transition: var(--transition);
        }
        .leaderboard-item:hover { transform: translateY(-2px); box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1); }
        .leaderboard-item.current-user {
            background: linear-gradient(135deg, rgba(74, 107, 175, 0.1), rgba(109, 40, 217, 0.1));
            border: 1px solid var(--primary);
        }
        .leaderboard-rank {
            width: 40px; height: 40px; border-radius: 50%; background: var(--primary);
            color: white; display: flex; align-items: center; justify-content: center;
            font-weight: bold; margin-left: 15px; box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
        }
        .leaderboard-user { flex: 1; }
        .leaderboard-user h4 { color: var(--dark); margin-bottom: 5px; }
        .leaderboard-user p { color: #666; font-size: 0.9em; }
        .leaderboard-score { font-weight: bold; color: var(--primary); font-size: 1.2em; }

        .toggle-switch { position: relative; display: inline-block; width: 60px; height: 30px; }
        .toggle-switch input { opacity: 0; width: 0; height: 0; }
        .slider {
            position: absolute; cursor: pointer; top: 0; left: 0; right: 0; bottom: 0;
            background-color: #ccc; transition: .4s; border-radius: 34px;
        }
        .slider:before {
            position: absolute; content: ""; height: 22px; width: 22px; left: 4px; bottom: 4px;
            background-color: white; transition: .4s; border-radius: 50%;
        }
        input:checked + .slider { background-color: var(--success); }
        input:checked + .slider:before { transform: translateX(30px); }

        select, input[type="number"], input[type="text"], input[type="email"] {
            padding: 10px 15px; border: 2px solid #e1e5f1;
            border-radius: 8px; font-size: 1em; background: white;
        }
        select:focus, input:focus { border-color: var(--primary); outline: none; }

        .chemistry-elements {
            position: fixed; width: 100%; height: 100%; top: 0; left: 0;
            pointer-events: none; z-index: -1;
        }
        .element {
            position: absolute; font-size: 1.5em; opacity: 0.03;
            animation: floatElement 20s infinite linear;
        }
        .element:nth-child(1) { top: 10%; left: 5%; animation-duration: 25s; }
        .element:nth-child(2) { top: 20%; right: 10%; animation-duration: 30s; }
        .element:nth-child(3) { bottom: 15%; left: 15%; animation-duration: 20s; }
        .element:nth-child(4) { bottom: 25%; right: 5%; animation-duration: 35s; }
        .element:nth-child(5) { top: 50%; left: 20%; animation-duration: 28s; }
        .element:nth-child(6) { top: 60%; right: 20%; animation-duration: 32s; }

        .video-section {
            margin: 40px 0; padding: 30px; background: #f8f9fa;
            border-radius: 20px; box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        .video-container {
            position: relative; width: 100%; height: 0; padding-bottom: 56.25%;
            margin: 25px 0; border-radius: 15px; overflow: hidden;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
        }
        .video-container iframe {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;
        }
        .video-info { margin-top: 20px; }

        .simulation-container {
            display: flex; flex-direction: column; align-items: center;
            padding: 30px; background: var(--card-bg); border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1); margin-top: 20px;
            backdrop-filter: blur(10px); border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .simulation-frame {
            width: 100%; height: 600px; border: none; border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        .simulation-info { margin-top: 20px; text-align: center; max-width: 800px; }

        @media (max-width: 768px) {
            .app-container { flex-direction: column; }
            .sidebar { width: 100%; height: auto; }
            .nav-menu { display: flex; overflow-x: auto; padding-bottom: 10px; }
            .nav-item { flex-shrink: 0; margin-bottom: 0; margin-left: 10px; }
            .cards-container { grid-template-columns: 1fr; }
            .header { flex-direction: column; gap: 15px; text-align: center; }
            .user-actions { justify-content: center; }
            .quiz-options { grid-template-columns: 1fr; }
            .quiz-controls { flex-direction: column; }
            .login-container { padding: 20px; }
            .progress-stats { grid-template-columns: 1fr; }
            .quiz-container { flex-direction: column; }
        }

        .pulse { animation: pulse 2s infinite; }
        @keyframes pulse { 0% { transform: scale(1); } 50% { transform: scale(1.05); } 100% { transform: scale(1); } }

        .student-info { margin-top: 10px; padding-top: 10px; border-top: 1px solid rgba(255, 255, 255, 0.2); }
        .student-info p { font-size: 0.9em; margin-bottom: 5px; }

        .rank-badge {
            display: inline-flex; align-items: center; padding: 5px 12px;
            border-radius: 20px; font-weight: bold; font-size: 0.9em;
            margin-right: 10px; box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }
        .rank-inert { background: #9ca3af; color: white; }
        .rank-active { background: #f59e0b; color: white; }
        .rank-good { background: #10b981; color: white; }
        .rank-genius {
            background: linear-gradient(135deg, #8b5cf6, #6366f1);
            color: white; animation: glow 2s infinite alternate;
        }
        @keyframes glow { from { box-shadow: 0 0 5px #8b5cf6; } to { box-shadow: 0 0 15px #6366f1; } }

        .notifications-container {
            background: var(--card-bg); border-radius: 15px; padding: 30px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(10px); border: 1px solid rgba(255, 255, 255, 0.2);
            max-height: 500px; overflow-y: auto;
        }
        .notification-item {
            padding: 15px; border-bottom: 1px solid #e1e5f1;
            display: flex; align-items: flex-start;
        }
        .notification-item:last-child { border-bottom: none; }
        .notification-icon { margin-left: 15px; font-size: 1.2em; color: var(--primary); }
        .notification-content { flex: 1; }
        .notification-title { font-weight: bold; margin-bottom: 5px; }
        .notification-time { font-size: 0.8em; color: #666; }

        .profile-container {
            background: var(--card-bg); border-radius: 15px; padding: 30px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(10px); border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .profile-header { display: flex; align-items: center; margin-bottom: 30px; }
        .profile-avatar {
            width: 100px; height: 100px; border-radius: 50%;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            display: flex; align-items: center; justify-content: center;
            font-size: 2.5em; color: white; margin-left: 20px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }
        .profile-info { flex: 1; }
        .profile-name {
            font-size: 1.5em; font-weight: bold; margin-bottom: 10px;
            display: flex; align-items: center;
        }
        .profile-stats {
            display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 20px; margin-top: 30px;
        }
        .profile-stat {
            background: #f8fafc; padding: 20px; border-radius: 10px; text-align: center;
        }
        .profile-stat-value {
            font-size: 2em; font-weight: bold; color: var(--primary); margin-bottom: 10px;
        }
        .profile-stat-label { color: #666; font-size: 0.9em; }

        .advanced-report {
            background: var(--card-bg); border-radius: 15px; padding: 30px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(10px); border: 1px solid rgba(255, 255, 255, 0.2);
            margin-top: 30px;
        }
        .report-section { margin-bottom: 30px; }
        .report-section h3 {
            color: var(--primary); margin-bottom: 15px; padding-bottom: 10px;
            border-bottom: 2px solid #f1f5f9; display: flex; align-items: center;
        }
        .report-section h3 i { margin-left: 10px; }
        .report-chart { width: 100%; height: 300px; margin: 20px 0; }
        .improvement-tips {
            background: #e8f5e9; padding: 20px; border-radius: 10px;
            margin-top: 20px; border-right: 4px solid var(--success);
        }
        .improvement-tips h4 { color: #2e7d32; margin-bottom: 10px; display: flex; align-items: center; }
        .improvement-tips h4 i { margin-left: 10px; }
        .improvement-tips ul { padding-right: 20px; }
        .improvement-tips li { margin-bottom: 10px; }

        .url-indicator {
            position: fixed; bottom: 15px; left: 15px;
            background: rgba(0, 0, 0, 0.7); color: #06d6a0;
            padding: 8px 15px; border-radius: 20px;
            font-size: 0.8em; font-family: 'Courier New', monospace;
            z-index: 9999; backdrop-filter: blur(10px);
            border: 1px solid rgba(6, 214, 160, 0.3);
            transition: var(--transition); cursor: pointer; display: none;
        }
        .url-indicator:hover { background: rgba(0, 0, 0, 0.9); }
        .url-indicator.visible { display: block; }

        .logout-btn {
            margin-top: 15px; width: 100%; padding: 10px;
            background: rgba(239, 68, 68, 0.2); color: #ff8a8a;
            border: 1px solid rgba(239, 68, 68, 0.4);
            border-radius: 8px; cursor: pointer;
            font-size: 0.9em; transition: var(--transition);
            display: flex; align-items: center; justify-content: center; gap: 8px;
        }
        .logout-btn:hover { background: rgba(239, 68, 68, 0.4); color: white; }

        /* ============================================
           أنماط صفحة البحث الكيميائي
           ============================================ */
        .research-container { max-width: 1200px; margin: 0 auto; padding: 20px; }

        .research-hero {
            background: linear-gradient(135deg, #4a6baf, #6d28d9);
            border-radius: 20px; padding: 40px 30px; color: white;
            text-align: center; margin-bottom: 30px;
            box-shadow: 0 10px 30px rgba(74, 107, 175, 0.3);
            position: relative; overflow: hidden;
        }
        .research-hero::before {
            content: ''; position: absolute; top: -50%; right: -50%;
            width: 200%; height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.1) 0%, transparent 70%);
            animation: rotateBg 20s linear infinite;
        }
        @keyframes rotateBg { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }

        .research-hero h1 { font-size: 2.2em; margin-bottom: 15px; position: relative; z-index: 1; }
        .research-hero p { font-size: 1.1em; opacity: 0.95; max-width: 700px; margin: 0 auto; position: relative; z-index: 1; line-height: 1.7; }

        .research-elements-showcase {
            display: flex; justify-content: center; gap: 20px;
            flex-wrap: wrap; margin-top: 25px; position: relative; z-index: 1;
        }
        .element-chip {
            background: rgba(255, 255, 255, 0.2); backdrop-filter: blur(10px);
            padding: 12px 20px; border-radius: 30px; font-weight: bold;
            border: 2px solid rgba(255, 255, 255, 0.3);
            display: flex; align-items: center; gap: 8px; transition: all 0.3s ease;
        }
        .element-chip:hover { background: rgba(255, 255, 255, 0.35); transform: translateY(-3px); }
        .element-chip .symbol { font-size: 1.3em; }

        .research-toc {
            background: var(--card-bg); border-radius: 15px; padding: 25px;
            margin-bottom: 30px; box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(10px); border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .research-toc h3 {
            color: var(--primary); margin-bottom: 20px; padding-bottom: 12px;
            border-bottom: 2px solid #f1f5f9; display: flex; align-items: center; gap: 10px;
        }
        .toc-grid {
            display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 12px;
        }
        .toc-link {
            display: flex; align-items: center; gap: 10px; padding: 12px 15px;
            background: #f8fafc; border-radius: 10px; color: var(--dark);
            text-decoration: none; transition: all 0.3s ease;
            border-right: 4px solid var(--primary); font-size: 0.95em;
        }
        .toc-link:hover {
            background: linear-gradient(135deg, rgba(74, 107, 175, 0.15), rgba(109, 40, 217, 0.15));
            transform: translateX(-5px); color: var(--primary);
        }
        .toc-link i { color: var(--primary); font-size: 1.1em; }

        .research-section {
            background: var(--card-bg); border-radius: 15px; padding: 30px;
            margin-bottom: 25px; box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(10px); border: 1px solid rgba(255, 255, 255, 0.2);
            scroll-margin-top: 20px; transition: all 0.3s ease;
        }
        .research-section:hover { box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15); }

        .section-header-element {
            display: flex; align-items: center; gap: 20px;
            padding: 20px; border-radius: 15px; margin-bottom: 25px;
            color: white; position: relative; overflow: hidden;
        }
        .section-header-element::before {
            content: ''; position: absolute; top: 0; right: 0;
            width: 200px; height: 100%;
            background: radial-gradient(circle, rgba(255,255,255,0.15) 0%, transparent 70%);
        }
        .element-badge {
            width: 80px; height: 80px; border-radius: 50%;
            background: rgba(255, 255, 255, 0.25);
            display: flex; align-items: center; justify-content: center;
            font-size: 2.2em; font-weight: bold; backdrop-filter: blur(10px);
            border: 3px solid rgba(255, 255, 255, 0.4);
            flex-shrink: 0; box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }
        .element-info-title h2 { font-size: 1.6em; margin-bottom: 5px; }
        .element-info-title p { opacity: 0.95; font-size: 0.95em; }

        .element-fe { background: linear-gradient(135deg, #b91c1c, #7f1d1d); }
        .element-zn { background: linear-gradient(135deg, #0891b2, #155e75); }
        .element-mg { background: linear-gradient(135deg, #16a34a, #15803d); }
        .element-i  { background: linear-gradient(135deg, #7c3aed, #5b21b6); }
        .element-se { background: linear-gradient(135deg, #ea580c, #c2410c); }
        .element-intro { background: linear-gradient(135deg, #4a6baf, #6d28d9); }

        .subsection { margin-bottom: 25px; padding-bottom: 20px; border-bottom: 1px solid #f1f5f9; }
        .subsection:last-child { border-bottom: none; margin-bottom: 0; padding-bottom: 0; }
        .subsection h4 {
            color: var(--primary); font-size: 1.15em; margin-bottom: 15px;
            display: flex; align-items: center; gap: 10px;
            padding-right: 12px; border-right: 4px solid var(--primary);
        }
        .subsection p { line-height: 1.9; color: #334155; margin-bottom: 12px; text-align: justify; }
        .subsection ul { padding-right: 25px; margin-bottom: 15px; }
        .subsection li { line-height: 1.8; color: #334155; margin-bottom: 8px; }
        .subsection strong { color: var(--dark); }

        .formula-box {
            background: linear-gradient(135deg, #1e293b, #0f172a);
            color: #06d6a0; padding: 20px; border-radius: 12px;
            text-align: center; font-family: 'Courier New', monospace;
            font-size: 1.2em; font-weight: bold; margin: 15px 0;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            border: 1px solid rgba(6, 214, 160, 0.3);
            direction: ltr; letter-spacing: 1px;
        }

        .info-box {
            padding: 18px 20px; border-radius: 12px; margin: 15px 0;
            border-right: 4px solid; line-height: 1.8;
        }
        .info-box h5 { margin-bottom: 10px; display: flex; align-items: center; gap: 8px; font-size: 1.05em; }
        .info-box.warning { background: #fff7ed; border-color: #f59e0b; }
        .info-box.warning h5 { color: #92400e; }
        .info-box.danger { background: #fef2f2; border-color: #ef4444; }
        .info-box.danger h5 { color: #991b1b; }
        .info-box.success { background: #f0fdf4; border-color: #10b981; }
        .info-box.success h5 { color: #065f46; }
        .info-box.info { background: #eff6ff; border-color: #3b82f6; }
        .info-box.info h5 { color: #1e40af; }
        .info-box.purple { background: #faf5ff; border-color: #8b5cf6; }
        .info-box.purple h5 { color: #5b21b6; }

        .comparison-table-wrapper {
            overflow-x: auto; border-radius: 12px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08); margin: 20px 0;
        }
        .comparison-table { width: 100%; border-collapse: collapse; background: white; min-width: 800px; }
        .comparison-table th {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white; padding: 15px 12px; text-align: right;
            font-weight: bold; font-size: 0.95em;
        }
        .comparison-table td {
            padding: 15px 12px; border-bottom: 1px solid #f1f5f9;
            text-align: right; line-height: 1.7; font-size: 0.9em;
        }
        .comparison-table tr:hover { background: #f8fafc; }
        .comparison-table tr:last-child td { border-bottom: none; }
        .comparison-table .element-cell {
            font-weight: bold; color: var(--primary);
            display: flex; align-items: center; gap: 8px;
        }
        .comparison-table .element-mini-badge {
            display: inline-flex; align-items: center; justify-content: center;
            width: 30px; height: 30px; border-radius: 50%;
            color: white; font-weight: bold; font-size: 0.85em;
        }

        .references-list { list-style: none; padding: 0; counter-reset: ref-counter; }
        .references-list li {
            counter-increment: ref-counter;
            padding: 15px 20px 15px 60px; margin-bottom: 12px;
            background: #f8fafc; border-radius: 10px; position: relative;
            line-height: 1.7; border-right: 4px solid var(--primary);
            transition: all 0.3s ease; font-size: 0.92em;
            direction: ltr; text-align: left;
        }
        .references-list li:hover { background: #eff6ff; transform: translateX(-5px); }
        .references-list li::before {
            content: counter(ref-counter);
            position: absolute; left: 15px; top: 50%;
            transform: translateY(-50%); width: 30px; height: 30px;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white; border-radius: 50%;
            display: flex; align-items: center; justify-content: center;
            font-weight: bold; font-size: 0.85em;
        }
        .references-list a { color: var(--primary); text-decoration: none; word-break: break-all; }
        .references-list a:hover { text-decoration: underline; }

        .conclusion-box {
            background: linear-gradient(135deg, #f0fdf4, #dcfce7);
            border-radius: 15px; padding: 30px;
            border-right: 5px solid var(--success);
            line-height: 1.9; color: #14532d;
        }
        .conclusion-box h3 {
            color: #065f46; margin-bottom: 15px;
            display: flex; align-items: center; gap: 10px;
        }

        .back-to-top {
            position: fixed; bottom: 70px; left: 30px;
            width: 45px; height: 45px;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white; border: none; border-radius: 50%; cursor: pointer;
            box-shadow: 0 5px 15px rgba(74, 107, 175, 0.4);
            display: none; align-items: center; justify-content: center;
            font-size: 1.1em; z-index: 999; transition: all 0.3s ease;
        }
        .back-to-top.visible { display: flex; }
        .back-to-top:hover { transform: translateY(-3px); box-shadow: 0 8px 20px rgba(74, 107, 175, 0.5); }

        @media (max-width: 768px) {
            .research-hero h1 { font-size: 1.5em; }
            .section-header-element { flex-direction: column; text-align: center; }
            .element-badge { width: 70px; height: 70px; font-size: 1.8em; }
            .subsection h4 { font-size: 1em; }
            .formula-box { font-size: 0.95em; }
        }
    </style>
</head>
<body>
    <div class="background-animation">
        <div class="floating-element"></div>
        <div class="floating-element"></div>
        <div class="floating-element"></div>
        <div class="floating-element"></div>
        <div class="floating-element"></div>
        <div class="grid-lines"></div>
    </div>

    <div class="chemistry-elements">
        <div class="element">H₂O</div>
        <div class="element">CO₂</div>
        <div class="element">NaCl</div>
        <div class="element">CH₄</div>
        <div class="element">C₆H₁₂O₆</div>
        <div class="element">H₂SO₄</div>
    </div>

    <div class="url-indicator" id="url-indicator" title="اضغط لنسخ الرابط"></div>

    <div class="login-screen active" id="login">
        <div class="login-container">
            <div class="login-icon"><i class="fas fa-atom"></i></div>
            <h1>منصة الكيمياء التفاعلية</h1>
            <p>سجل دخولك للبدء في رحلة التعلم التفاعلية</p>
            <form id="login-form">
                <div class="form-group">
                    <label for="student-name">اسم الطالب</label>
                    <input type="text" id="student-name" class="form-control" placeholder="أدخل اسمك" required>
                </div>
                <div class="form-group">
                    <label for="student-section">الشعبة</label>
                    <select id="student-section" class="form-control" required>
                        <option value="" disabled selected>اختر شعبتك</option>
                        <option value="الشعبة 1">الشعبة 1</option>
                        <option value="الشعبة 2">الشعبة 2</option>
                        <option value="الشعبة 3">الشعبة 3</option>
                        <option value="الشعبة 4">الشعبة 4</option>
                        <option value="الشعبة 5">الشعبة 5</option>
                        <option value="الشعبة 6">الشعبة 6</option>
                        <option value="الشعبة 7">الشعبة 7</option>
                    </select>
                </div>
                <button type="submit" class="btn" style="width: 100%;">
                    <i class="fas fa-sign-in-alt"></i> بدء التعلم
                </button>
            </form>
        </div>
    </div>

    <div class="app-container" id="main-app" style="display: none;">
        <div class="sidebar">
            <div class="logo"><h1><i class="fas fa-atom"></i> كيمياء</h1></div>
            
            <ul class="nav-menu">
                <li class="nav-item">
                    <a href="#/welcome" class="nav-link active" data-screen="welcome">
                        <i class="fas fa-home"></i><span>الرئيسية</span>
                    </a>
                </li>
                <li class="nav-item">
                    <a href="#/quiz-setup" class="nav-link" data-screen="quiz-setup">
                        <i class="fas fa-file-alt"></i><span>الاختبارات</span>
                    </a>
                </li>
                <li class="nav-item">
                    <a href="#/chemistry-research" class="nav-link" data-screen="chemistry-research">
                        <i class="fas fa-flask"></i><span>بحث كيمياء 2</span>
                    </a>
                </li>
                <li class="nav-item">
                    <a href="#/simulation" class="nav-link" data-screen="simulation">
                        <i class="fas fa-vial"></i><span>المحاكاة</span>
                    </a>
                </li>
                <li class="nav-item">
                    <a href="#/progress" class="nav-link" data-screen="progress">
                        <i class="fas fa-chart-line"></i><span>التقدم</span>
                    </a>
                </li>
                <li class="nav-item">
                    <a href="#/leaderboard" class="nav-link" data-screen="leaderboard">
                        <i class="fas fa-trophy"></i><span>المتصدرين</span>
                    </a>
                </li>
                <li class="nav-item">
                    <a href="#/settings" class="nav-link" data-screen="settings">
                        <i class="fas fa-cog"></i><span>الإعدادات</span>
                    </a>
                </li>
            </ul>

            <div class="team-section">
                <h3><i class="fas fa-users"></i> فريق العمل</h3>
                <div class="team-member" style="background: rgba(255, 215, 0, 0.2);">
                    <div class="team-avatar" style="background: #FFD700;"><i class="fas fa-crown"></i></div>
                    <div class="team-member-info">
                        <div class="team-member-name">تميم الزهراني</div>
                        <div class="team-member-role">القائد والمبرمج</div>
                    </div>
                </div>
                <div class="team-member" style="background: rgba(192, 192, 192, 0.2);">
                    <div class="team-avatar" style="background: #C0C0C0;"><i class="fas fa-user-tie"></i></div>
                    <div class="team-member-info">
                        <div class="team-member-name">عمار الغامدي</div>
                        <div class="team-member-role">المشرف</div>
                    </div>
                </div>
                <div class="team-member" style="background: rgba(205, 127, 50, 0.2);">
                    <div class="team-avatar" style="background: #CD7F32;"><i class="fas fa-lightbulb"></i></div>
                    <div class="team-member-info">
                        <div class="team-member-name">خالد العتيبي</div>
                        <div class="team-member-role">الأفكار والبحث</div>
                    </div>
                </div>
                <div class="team-member" style="background: rgba(0, 123, 255, 0.2);">
                    <div class="team-avatar" style="background: #007BFF;"><i class="fas fa-pen"></i></div>
                    <div class="team-member-info">
                        <div class="team-member-name">أحمد الصالح</div>
                        <div class="team-member-role">الكاتب</div>
                    </div>
                </div>
                <div class="team-member" style="background: rgba(108, 117, 125, 0.2);">
                    <div class="team-avatar" style="background: #6C757D;"><i class="fas fa-users"></i></div>
                    <div class="team-member-info">
                        <div class="team-member-name">سلطان المطيري</div>
                        <div class="team-member-role">الكاتب</div>
                    </div>
                </div>
                <div class="team-member" style="background: rgba(108, 117, 125, 0.2);">
                    <div class="team-avatar" style="background: #6C757D;"><i class="fas fa-users"></i></div>
                    <div class="team-member-info">
                        <div class="team-member-name">عبدالاله القحطاني</div>
                        <div class="team-member-role">الكاتب</div>
                    </div>
                </div>
                <div class="team-member" style="background: rgba(108, 117, 125, 0.2);">
                    <div class="team-avatar" style="background: #6C757D;"><i class="fas fa-users"></i></div>
                    <div class="team-member-info">
                        <div class="team-member-name">ناصر العقيل</div>
                        <div class="team-member-role">الكاتب</div>
                    </div>
                </div>
            </div>

            <div class="user-section">
                <div class="user-info">
                    <div class="user-avatar"><i class="fas fa-user"></i></div>
                    <div>
                        <h4 id="username-display">طالب كيمياء</h4>
                        <div class="student-info">
                            <p id="section-display">الشعبة: غير محدد</p>
                            <p id="user-level">المستوى: مبتدئ</p>
                        </div>
                    </div>
                </div>
                <button class="logout-btn" id="logout-btn">
                    <i class="fas fa-sign-out-alt"></i> تسجيل الخروج
                </button>
            </div>
        </div>

        <div class="main-content">
            <!-- شاشة الترحيب -->
            <div class="screen active" id="welcome">
                <div class="header">
                    <h2><i class="fas fa-home"></i> الرئيسية</h2>
                    <div class="user-actions">
                        <button class="btn btn-outline" onclick="navigateTo('notifications')">
                            <i class="fas fa-bell"></i> الإشعارات
                        </button>
                        <button class="btn" onclick="navigateTo('profile')">
                            <i class="fas fa-user"></i> الملف الشخصي
                        </button>
                    </div>
                </div>
                <div class="welcome-screen">
                    <div class="welcome-icon"><i class="fas fa-atom"></i></div>
                    <h1>مرحباً بك في منصة الكيمياء التفاعلية</h1>
                    <p>منصة شاملة لتعلم الكيمياء من خلال الاختبارات التفاعلية، المحاكاة، والتجارب الافتراضية</p>
                    <div class="cards-container">
                        <div class="card" onclick="navigateTo('quiz-setup')">
                            <div class="card-header">
                                <div class="card-icon"><i class="fas fa-file-alt"></i></div>
                                <h3>الاختبارات التفاعلية</h3>
                            </div>
                            <p>اختبر معرفتك في الكيمياء من خلال اختبارات تفاعلية مع تصحيح فوري وتحليل مفصل للأداء</p>
                            <button class="btn">ابدأ الاختبار</button>
                        </div>
                        <div class="card" onclick="navigateTo('chemistry-research')">
                            <div class="card-header">
                                <div class="card-icon"><i class="fas fa-flask"></i></div>
                                <h3>بحث كيمياء 2</h3>
                            </div>
                            <p>دراسة كيميائية حيوية شاملة للعناصر المهمة في جسم الإنسان وآليات عملها على المستوى الجزيئي</p>
                            <button class="btn btn-success">اقرأ البحث</button>
                        </div>
                        <div class="card" onclick="navigateTo('simulation')">
                            <div class="card-header">
                                <div class="card-icon"><i class="fas fa-vial"></i></div>
                                <h3>المحاكاة والتجارب</h3>
                            </div>
                            <p>قم بتجربة التفاعلات الكيميائية افتراضياً في مختبر آمن مع شرح مفصل للنتائج</p>
                            <button class="btn btn-success">ابدأ المحاكاة</button>
                        </div>
                        <div class="card" onclick="navigateTo('progress')">
                            <div class="card-header">
                                <div class="card-icon"><i class="fas fa-chart-line"></i></div>
                                <h3>تتبع التقدم</h3>
                            </div>
                            <p>راجع إحصائيات أدائك، تتبع تقدمك التعليمي، واحصل على توصيات مخصصة للتحسين</p>
                            <button class="btn btn-warning">عرض التقارير</button>
                        </div>
                        <div class="card" onclick="navigateTo('leaderboard')">
                            <div class="card-header">
                                <div class="card-icon"><i class="fas fa-trophy"></i></div>
                                <h3>لوحة المتصدرين</h3>
                            </div>
                            <p>تنافس مع زملائك، احصل على نقاط، وارتقِ في لوحة المتصدرين لتصير الأفضل</p>
                            <button class="btn btn-danger">عرض المتصدرين</button>
                        </div>
                    </div>
                </div>
            </div>

            <!-- شاشة إعداد الاختبار -->
            <div class="screen" id="quiz-setup">
                <div class="header">
                    <h2><i class="fas fa-file-alt"></i> إعداد الاختبار</h2>
                    <div class="user-actions">
                        <button class="btn btn-outline" onclick="navigateTo('welcome')">
                            <i class="fas fa-arrow-right"></i> العودة
                        </button>
                    </div>
                </div>
                <div class="quiz-setup">
                    <h3 style="text-align: center; margin-bottom: 25px; color: var(--primary);">اختر نوع الاختبار</h3>
                    <div class="quiz-options">
                        <div class="quiz-option" data-mode="practice">
                            <i class="fas fa-graduation-cap"></i>
                            <h4>وضع الممارسة</h4>
                            <p>تعلم بالسرعة التي تناسبك مع تصحيح فوري للأسئلة</p>
                        </div>
                        <div class="quiz-option" data-mode="exam">
                            <i class="fas fa-clock"></i>
                            <h4>وضع الامتحان</h4>
                            <p>اختبر نفسك في ظروف مشابهة للامتحان مع مؤقت</p>
                        </div>
                    </div>
                    <div class="setting-item">
                        <div class="setting-info">
                            <h4>عدد الأسئلة</h4>
                            <p>اختر عدد الأسئلة في الاختبار</p>
                        </div>
                        <select id="question-count">
                            <option value="10">10 أسئلة</option>
                            <option value="20">20 أسئلة</option>
                            <option value="30">30 أسئلة</option>
                            <option value="50" selected>50 أسئلة (كاملة)</option>
                        </select>
                    </div>
                    <div class="setting-item">
                        <div class="setting-info">
                            <h4>مستوى الصعوبة</h4>
                            <p>اختر مستوى الصعوبة المناسب لك</p>
                        </div>
                        <select id="difficulty">
                            <option value="all">جميع المستويات</option>
                            <option value="easy">سهل</option>
                            <option value="medium" selected>متوسط</option>
                            <option value="hard">صعب</option>
                        </select>
                    </div>
                    <div class="quiz-controls">
                        <button class="btn" id="start-quiz" style="flex: 1;">
                            <i class="fas fa-play"></i> بدء الاختبار
                        </button>
                        <button class="btn btn-outline" onclick="navigateTo('welcome')" style="flex: 1;">
                            <i class="fas fa-times"></i> إلغاء
                        </button>
                    </div>
                </div>
            </div>

            <!-- شاشة الاختبار -->
            <div class="screen" id="quiz">
                <div class="header">
                    <h2><i class="fas fa-file-alt"></i> اختبار الكيمياء</h2>
                    <div class="user-actions">
                        <div class="quiz-timer" id="quiz-timer">30:00</div>
                        <button class="btn btn-danger" id="end-quiz">
                            <i class="fas fa-stop"></i> إنهاء الاختبار
                        </button>
                    </div>
                </div>
                <div class="quiz-container">
                    <div class="quiz-content">
                        <div class="quiz-header">
                            <div class="quiz-info">
                                <div id="question-counter">السؤال 1 من 50</div>
                                <div id="score-display">النقاط: 0</div>
                            </div>
                            <div class="progress-container" style="flex: 1; margin: 0 20px;">
                                <div class="progress-bar">
                                    <div class="progress" id="progress"></div>
                                </div>
                            </div>
                        </div>
                        <div class="question" id="question"></div>
                        <div class="options" id="options"></div>
                        <button class="btn" id="next-btn" disabled>
                            <i class="fas fa-arrow-left"></i> التالي
                        </button>
                        <div class="explanation" id="explanation"></div>
                    </div>
                    <div class="whiteboard-container">
                        <div class="whiteboard-header">
                            <h3><i class="fas fa-chalkboard"></i> السبورة التفاعلية</h3>
                            <button class="btn btn-outline" id="clear-whiteboard">
                                <i class="fas fa-eraser"></i> مسح
                            </button>
                        </div>
                        <iframe src="https://www.canva.com/design/DAG37-MyN6M/31ae22xdkRDIFafdn72jBw/view?embed" 
                                class="whiteboard-frame" 
                                id="whiteboard"
                                allowfullscreen>
                        </iframe>
                        <div class="whiteboard-info">
                            <p>استخدم السبورة لحل المسائل وكتابة الملاحظات أثناء الاختبار</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- شاشة النتائج -->
            <div class="screen" id="results">
                <div class="header">
                    <h2><i class="fas fa-chart-bar"></i> نتائج الاختبار</h2>
                    <div class="user-actions">
                        <button class="btn" onclick="navigateTo('quiz-setup')">
                            <i class="fas fa-redo"></i> اختبار جديد
                        </button>
                        <button class="btn btn-outline" onclick="navigateTo('welcome')">
                            <i class="fas fa-home"></i> الرئيسية
                        </button>
                    </div>
                </div>
                <div class="result-container">
                    <div class="user-info" style="background: #f8f9fa; padding: 20px; border-radius: 15px; margin-bottom: 20px;">
                        <p><i class="fas fa-user-graduate"></i> <strong>الاسم:</strong> <span id="result-username">طالب كيمياء</span></p>
                        <p><i class="fas fa-clock"></i> <strong>الوقت المستغرق:</strong> <span id="time-taken">--:--</span></p>
                        <p><i class="fas fa-chart-bar"></i> <strong>النتيجة:</strong> <span id="result-score">0</span> من <span id="total-questions">50</span></p>
                        <p><i class="fas fa-medal"></i> <strong>رتبتك:</strong> <span id="user-rank">غاز خامل</span></p>
                    </div>
                    <h2><i class="fas fa-trophy"></i> نتيجة الاختبار</h2>
                    <div class="result-score" id="final-score">0%</div>
                    <div class="result-chart">
                        <canvas id="result-chart" width="250" height="250"></canvas>
                    </div>
                    <div class="comparison" id="comparison"></div>
                    <div class="weak-lessons" id="weak-lessons"></div>
                    <div class="advanced-report">
                        <div class="report-section">
                            <h3><i class="fas fa-chart-line"></i> تحليل أدائك</h3>
                            <div class="report-chart">
                                <canvas id="performance-chart"></canvas>
                            </div>
                            <div class="improvement-tips">
                                <h4><i class="fas fa-lightbulb"></i> نصائح للتحسين</h4>
                                <ul id="improvement-tips"></ul>
                            </div>
                        </div>
                    </div>
                    <div class="video-section">
                        <h3><i class="fas fa-video"></i> فيديو تعليمي للمراجعة</h3>
                        <div class="video-container">
                            <iframe src="https://www.youtube.com/embed/i395UdUAOvE" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
                        </div>
                        <div class="video-info">
                            <h3><i class="fas fa-play-circle"></i> شرح التفاعلات الكيميائية - سلسلة شاملة</h3>
                            <p>هذا الفيديو جزء من سلسلة شاملة للكيمياء للمرحلة الثانوية، يقدم شرحاً مفصلاً للتفاعلات الكيميائية بأنواعها المختلفة.</p>
                        </div>
                    </div>
                    <div class="quiz-controls" style="margin-top: 30px;">
                        <button class="btn" onclick="navigateTo('quiz-setup')" style="flex: 1;">
                            <i class="fas fa-redo"></i> اختبار جديد
                        </button>
                        <button class="btn btn-outline" onclick="navigateTo('progress')" style="flex: 1;">
                            <i class="fas fa-chart-line"></i> عرض التقدم
                        </button>
                        <button class="btn btn-outline" onclick="navigateTo('welcome')" style="flex: 1;">
                            <i class="fas fa-home"></i> الرئيسية
                        </button>
                    </div>
                </div>
            </div>

            <!-- شاشة التقدم -->
            <div class="screen" id="progress">
                <div class="header">
                    <h2><i class="fas fa-chart-line"></i> تتبع التقدم</h2>
                    <div class="user-actions">
                        <button class="btn btn-outline" onclick="navigateTo('welcome')">
                            <i class="fas fa-arrow-right"></i> العودة
                        </button>
                    </div>
                </div>
                <div class="progress-screen">
                    <div class="progress-stats">
                        <div class="stat-card">
                            <i class="fas fa-chart-bar"></i>
                            <h3>متوسط النتائج</h3>
                            <div class="stat-value" id="average-score">0%</div>
                        </div>
                        <div class="stat-card">
                            <i class="fas fa-check-circle"></i>
                            <h3>أفضل نتيجة</h3>
                            <div class="stat-value" id="best-score">0%</div>
                        </div>
                        <div class="stat-card">
                            <i class="fas fa-list-ol"></i>
                            <h3>عدد الاختبارات</h3>
                            <div class="stat-value" id="total-quizzes">0</div>
                        </div>
                        <div class="stat-card">
                            <i class="fas fa-clock"></i>
                            <h3>إجمالي الوقت</h3>
                            <div class="stat-value" id="total-time">0 د</div>
                        </div>
                    </div>
                    <div class="progress-history">
                        <h3><i class="fas fa-history"></i> تاريخ الاختبارات</h3>
                        <table class="history-table">
                            <thead>
                                <tr>
                                    <th>التاريخ</th>
                                    <th>نوع الاختبار</th>
                                    <th>النتيجة</th>
                                    <th>الوقت المستغرق</th>
                                    <th>عدد الأسئلة</th>
                                </tr>
                            </thead>
                            <tbody id="quiz-history"></tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- شاشة المتصدرين -->
            <div class="screen" id="leaderboard">
                <div class="header">
                    <h2><i class="fas fa-trophy"></i> لوحة المتصدرين</h2>
                    <div class="user-actions">
                        <button class="btn btn-outline" onclick="navigateTo('welcome')">
                            <i class="fas fa-arrow-right"></i> العودة
                        </button>
                    </div>
                </div>
                <div class="leaderboard-screen">
                    <div class="leaderboard-container">
                        <h3><i class="fas fa-crown"></i> أعلى 10 متصدرين هذا الأسبوع</h3>
                        <div class="leaderboard-list" id="leaderboard-list"></div>
                    </div>
                </div>
            </div>

            <!-- شاشة الإعدادات -->
            <div class="screen" id="settings">
                <div class="header">
                    <h2><i class="fas fa-cog"></i> الإعدادات</h2>
                </div>
                <div class="settings-container">
                    <div class="settings-group">
                        <h3><i class="fas fa-user-cog"></i> إعدادات الحساب</h3>
                        <div class="setting-item">
                            <div class="setting-info">
                                <h4>الاسم</h4>
                                <p>اسم المستخدم المعروض في المنصة</p>
                            </div>
                            <input type="text" id="username" value="طالب كيمياء" class="setting-control">
                        </div>
                        <div class="setting-item">
                            <div class="setting-info">
                                <h4>البريد الإلكتروني</h4>
                                <p>للاستلام الإشعارات والتحديثات</p>
                            </div>
                            <input type="email" id="user-email" value="student@chemistry.com" class="setting-control">
                        </div>
                        <div class="setting-item">
                            <div class="setting-info">
                                <h4>المستوى</h4>
                                <p>مستواك الحالي في الكيمياء</p>
                            </div>
                            <select id="user-level-select" class="setting-control">
                                <option value="beginner">مبتدئ</option>
                                <option value="intermediate">متوسط</option>
                                <option value="advanced">متقدم</option>
                            </select>
                        </div>
                    </div>
                    <div class="settings-group">
                        <h3><i class="fas fa-palette"></i> الإعدادات العامة</h3>
                        <div class="setting-item">
                            <div class="setting-info">
                                <h4>الأصوات</h4>
                                <p>تشغيل أصوات التصحيح والإشعارات</p>
                            </div>
                            <label class="toggle-switch">
                                <input type="checkbox" id="sound-enabled" checked>
                                <span class="slider"></span>
                            </label>
                        </div>
                        <div class="setting-item">
                            <div class="setting-info">
                                <h4>الوضع الليلي</h4>
                                <p>تفعيل الوضع المظلم للراحة البصرية</p>
                            </div>
                            <label class="toggle-switch">
                                <input type="checkbox" id="dark-mode">
                                <span class="slider"></span>
                            </label>
                        </div>
                        <div class="setting-item">
                            <div class="setting-info">
                                <h4>الإشعارات</h4>
                                <p>تلقي إشعارات حول الاختبارات والتحديثات</p>
                            </div>
                            <label class="toggle-switch">
                                <input type="checkbox" id="notifications" checked>
                                <span class="slider"></span>
                            </label>
                        </div>
                        <div class="setting-item">
                            <div class="setting-info">
                                <h4>صعوبة الاختبارات الافتراضية</h4>
                                <p>اختر مستوى الصعوبة الافتراضي للاختبارات</p>
                            </div>
                            <select id="default-difficulty" class="setting-control">
                                <option value="all">جميع المستويات</option>
                                <option value="easy">سهل</option>
                                <option value="medium" selected>متوسط</option>
                                <option value="hard">صعب</option>
                            </select>
                        </div>
                        <div class="setting-item">
                            <div class="setting-info">
                                <h4>عدد الأسئلة الافتراضي</h4>
                                <p>عدد الأسئلة الافتراضي في كل اختبار</p>
                            </div>
                            <input type="number" id="default-question-count" value="20" min="5" max="50" class="setting-control">
                        </div>
                    </div>
                    <div class="settings-group">
                        <h3><i class="fas fa-language"></i> إعدادات اللغة</h3>
                        <div class="setting-item">
                            <div class="setting-info">
                                <h4>لغة الواجهة</h4>
                                <p>اختر اللغة المعروضة في المنصة</p>
                            </div>
                            <select id="interface-language" class="setting-control">
                                <option selected>العربية</option>
                                <option>English</option>
                                <option>Français</option>
                            </select>
                        </div>
                        <div class="setting-item">
                            <div class="setting-info">
                                <h4>لغة المصطلحات العلمية</h4>
                                <p>اختر لغة المصطلحات الكيميائية</p>
                            </div>
                            <select id="terms-language" class="setting-control">
                                <option selected>العربية</option>
                                <option>English</option>
                                <option>مختلط</option>
                            </select>
                        </div>
                    </div>
                    <div class="settings-group">
                        <h3><i class="fas fa-download"></i> البيانات والخصوصية</h3>
                        <div class="setting-item">
                            <div class="setting-info">
                                <h4>حفظ النتائج تلقائياً</h4>
                                <p>حفظ نتائج الاختبارات تلقائياً على الجهاز</p>
                            </div>
                            <label class="toggle-switch">
                                <input type="checkbox" id="auto-save" checked>
                                <span class="slider"></span>
                            </label>
                        </div>
                        <div class="setting-item">
                            <div class="setting-info">
                                <h4>تصدير البيانات</h4>
                                <p>تحميل جميع نتائجك وتقاريرك</p>
                            </div>
                            <button class="btn btn-outline" id="export-data">تصدير البيانات</button>
                        </div>
                        <div class="setting-item">
                            <div class="setting-info">
                                <h4>مسح البيانات</h4>
                                <p>حذف جميع البيانات المحفوظة على الجهاز</p>
                            </div>
                            <button class="btn btn-danger" id="clear-data">مسح البيانات</button>
                        </div>
                    </div>
                    <div class="quiz-controls" style="margin-top: 30px;">
                        <button class="btn" id="save-settings" style="flex: 1;">
                            <i class="fas fa-save"></i> حفظ الإعدادات
                        </button>
                        <button class="btn btn-outline" onclick="navigateTo('welcome')" style="flex: 1;">
                            <i class="fas fa-times"></i> إلغاء
                        </button>
                    </div>
                </div>
            </div>

            <!-- شاشة المحاكاة -->
            <div class="screen" id="simulation">
                <div class="header">
                    <h2><i class="fas fa-vial"></i> المحاكاة</h2>
                    <div class="user-actions">
                        <button class="btn btn-outline" onclick="navigateTo('welcome')">
                            <i class="fas fa-arrow-right"></i> العودة
                        </button>
                    </div>
                </div>
                <div class="simulation-container">
                    <h2>محاكاة موازنة المعادلات الكيميائية</h2>
                    <p>استخدم هذه المحاكاة التفاعلية لموازنة المعادلات الكيميائية واكتشاف مبادئ حفظ الكتلة</p>
                    <iframe src="https://phet.colorado.edu/sims/html/balancing-chemical-equations/latest/balancing-chemical-equations_ar.html" 
                            class="simulation-frame" allowfullscreen></iframe>
                    <div class="simulation-info">
                        <h3><i class="fas fa-info-circle"></i> معلومات عن المحاكاة</h3>
                        <p>هذه المحاكاة مقدمة من مشروع PhET التفاعلي بجامعة كولورادو. يمكنك استخدامها لموازنة المعادلات الكيميائية، ومشاهدة كيفية تفاعل الذرات، وفهم مبدأ حفظ الكتلة في التفاعلات الكيميائية.</p>
                    </div>
                </div>
            </div>

            <!-- شاشة الإشعارات -->
            <div class="screen" id="notifications">
                <div class="header">
                    <h2><i class="fas fa-bell"></i> الإشعارات</h2>
                    <div class="user-actions">
                        <button class="btn btn-outline" onclick="navigateTo('welcome')">
                            <i class="fas fa-arrow-right"></i> العودة
                        </button>
                        <button class="btn btn-danger" id="clear-notifications">
                            <i class="fas fa-trash"></i> مسح الكل
                        </button>
                    </div>
                </div>
                <div class="notifications-container" id="notifications-list"></div>
            </div>

            <!-- شاشة الملف الشخصي -->
            <div class="screen" id="profile">
                <div class="header">
                    <h2><i class="fas fa-user"></i> الملف الشخصي</h2>
                    <div class="user-actions">
                        <button class="btn btn-outline" onclick="navigateTo('welcome')">
                            <i class="fas fa-arrow-right"></i> العودة
                        </button>
                        <button class="btn" id="save-profile">
                            <i class="fas fa-save"></i> حفظ التغييرات
                        </button>
                    </div>
                </div>
                <div class="profile-container">
                    <div class="profile-header">
                        <div class="profile-avatar"><i class="fas fa-user"></i></div>
                        <div class="profile-info">
                            <div class="profile-name">
                                <input type="text" id="profile-username" value="طالب كيمياء" class="form-control" style="display: inline-block; width: auto;">
                                <span id="profile-rank" class="rank-badge rank-inert">غاز خامل</span>
                            </div>
                            <p id="profile-section">الشعبة: غير محدد</p>
                            <p id="profile-level">المستوى: مبتدئ</p>
                        </div>
                    </div>
                    <div class="profile-stats">
                        <div class="profile-stat">
                            <div class="profile-stat-value" id="profile-total-quizzes">0</div>
                            <div class="profile-stat-label">إجمالي الاختبارات</div>
                        </div>
                        <div class="profile-stat">
                            <div class="profile-stat-value" id="profile-average-score">0%</div>
                            <div class="profile-stat-label">متوسط النتائج</div>
                        </div>
                        <div class="profile-stat">
                            <div class="profile-stat-value" id="profile-best-score">0%</div>
                            <div class="profile-stat-label">أفضل نتيجة</div>
                        </div>
                        <div class="profile-stat">
                            <div class="profile-stat-value" id="profile-total-time">0 د</div>
                            <div class="profile-stat-label">إجمالي الوقت</div>
                        </div>
                    </div>
                    <div class="settings-group" style="margin-top: 30px;">
                        <h3><i class="fas fa-pen"></i> السيرة الذاتية</h3>
                        <textarea id="profile-bio" class="form-control" rows="5" placeholder="اكتب عن نفسك..."></textarea>
                    </div>
                </div>
            </div>

            <!-- شاشة بحث كيمياء 2 -->
            <div class="screen" id="chemistry-research">
                <div class="header">
                    <h2><i class="fas fa-flask"></i> بحث كيمياء 2</h2>
                    <div class="user-actions">
                        <button class="btn btn-outline" onclick="navigateTo('welcome')">
                            <i class="fas fa-arrow-right"></i> العودة
                        </button>
                    </div>
                </div>

                <div class="research-container">
                    <div class="research-hero">
                        <h1><i class="fas fa-atom"></i> العناصر الكيميائية المهمة في جسم الإنسان</h1>
                        <p>دراسة كيميائية حيوية شاملة لخصائص العناصر، آليات عملها على المستوى الجزئي، ووظائفها داخل الجسم</p>
                        <div class="research-elements-showcase">
                            <div class="element-chip"><span class="symbol">Fe</span> الحديد</div>
                            <div class="element-chip"><span class="symbol">Zn</span> الزنك</div>
                            <div class="element-chip"><span class="symbol">Mg</span> المغنيسيوم</div>
                            <div class="element-chip"><span class="symbol">I</span> اليود</div>
                            <div class="element-chip"><span class="symbol">Se</span> السيلينيوم</div>
                        </div>
                    </div>

                    <div class="research-toc">
                        <h3><i class="fas fa-list"></i> فهرس البحث</h3>
                        <div class="toc-grid">
                            <a href="#res-intro" class="toc-link"><i class="fas fa-book-open"></i> المقدمة والمبادئ</a>
                            <a href="#res-fe" class="toc-link"><i class="fas fa-fire"></i> الحديد (Fe)</a>
                            <a href="#res-zn" class="toc-link"><i class="fas fa-shield-alt"></i> الزنك (Zn)</a>
                            <a href="#res-mg" class="toc-link"><i class="fas fa-bolt"></i> المغنيسيوم (Mg)</a>
                            <a href="#res-i" class="toc-link"><i class="fas fa-leaf"></i> اليود (I)</a>
                            <a href="#res-se" class="toc-link"><i class="fas fa-umbrella"></i> السيلينيوم (Se)</a>
                            <a href="#res-table" class="toc-link"><i class="fas fa-table"></i> جدول المقارنة</a>
                            <a href="#res-conclusion" class="toc-link"><i class="fas fa-flag-checkered"></i> الخاتمة</a>
                            <a href="#res-refs" class="toc-link"><i class="fas fa-book"></i> المراجع</a>
                        </div>
                    </div>

                    <!-- قسم المقدمة -->
                    <div class="research-section" id="res-intro">
                        <div class="section-header-element element-intro">
                            <div class="element-badge"><i class="fas fa-flask"></i></div>
                            <div class="element-info-title">
                                <h2>المقدمة والمبادئ الكيميائية الحيوية</h2>
                                <p>الأساس الذري لوظائف الجسم الحيوية</p>
                            </div>
                        </div>

                        <div class="subsection">
                            <h4><i class="fas fa-info-circle"></i> المقدمة والأهمية الكيميائية الحيوية</h4>
                            <p>لا تعتمد وظائف جسم الإنسان الحيوية على وجود المركبات العضوية الكبرى وحدها، مثل البروتينات، الكربوهيدرات، والدهون، بل تعتمد اعتماداً كلياً على عناصر كيميائية تمتلك خصائص ذرية وإلكترونية فريدة تجعلها ضرورية لحدوث تفاعلات حيوية محددة لا يمكن بدونها استمرار الحياة.</p>
                            <p>وتكمن أهمية هذه العناصر الكيميائية في قدرتها على تكوين الأيونات النشطة، والارتباط الانتقائي بالجزيئات الحيوية، وتغيير طاقة التنشيط وسرعة التفاعلات الكيميائية عبر التحفيز الإنزيمي، بالإضافة إلى المشاركة المباشرة في سلاسل انتقال الإلكترونات وتثبيت التراكيب الفراغية ثلاثية الأبعاد للبروتينات والأحماض النووية.</p>
                        </div>

                        <div class="subsection">
                            <h4><i class="fas fa-microscope"></i> الرؤية الكيميائية الحيوية للعناصر</h4>
                            <p>من منظور الكيمياء الحيوية، لا تتساوى العناصر في طريقة عملها داخل الجسم؛ فالحديد يستطيع التناوب بين حالات أكسدة متعددة ليشارك في نقل الإلكترونات والأكسجين، بينما يمتاز الزنك بقدرته على تكوين روابط تناسقية ثابتة الجزيئات، ويمتلك المغنيسيوم ألفة عالية لمجموعات الفوسفات السالبة في جزيئات ATP، بينما يدخل اليود بصورة بنيوية دائمة في تركيب الهرمونات، ويشكل السيلينيوم مركزاً حافزاً فريداً في إنزيمات مضادات الأكسدة.</p>
                        </div>

                        <div class="subsection">
                            <h4><i class="fas fa-cogs"></i> المبادئ الكيميائية الحيوية الحاكمة للعناصر</h4>
                            <p>تخضع كافة العناصر الكيميائية في جسم الإنسان لمجموعة من القواعد الفيزيوكيميائية التي تحدد نمط وظيفتها داخل الخلايا، ويمكن تلخيص هذه المبادئ في أربعة محاور أساسية:</p>

                            <div class="info-box info">
                                <h5><i class="fas fa-bolt"></i> 1. جهد الأكسدة والاختزال (Redox Potential)</h5>
                                <p>تحديد قدرة العنصر على اكتساب أو فقد الإلكترونات بمرونة دون إحداث إجهاد تأكسدي عشوائي.</p>
                            </div>

                            <div class="info-box purple">
                                <h5><i class="fas fa-cube"></i> 2. الهندسة التناسقية (Coordination Geometry)</h5>
                                <p>شكل الروابط الفراغية التي يشكلها أيون الفلز مع المجموعات العضوية المحيطة به داخل الموقع النشط.</p>
                            </div>

                            <p><strong>وتُصنَّف العناصر الحيوية تبعاً لوظائفها إلى ثلاث فئات رئيسية:</strong></p>

                            <div class="toc-grid" style="margin-top: 15px;">
                                <div class="toc-link" style="cursor: default;">
                                    <i class="fas fa-fire" style="color: #ef4444;"></i>
                                    <div>
                                        <strong>عناصر التخليق الهرموني</strong>
                                        <div style="font-size: 0.85em; opacity: 0.75; margin-top: 3px;">اليود (I)</div>
                                    </div>
                                </div>
                                <div class="toc-link" style="cursor: default;">
                                    <i class="fas fa-shield-alt" style="color: #10b981;"></i>
                                    <div>
                                        <strong>عناصر التثبيت البنيوي</strong>
                                        <div style="font-size: 0.85em; opacity: 0.75; margin-top: 3px;">الزنك (Zn) والمغنيسيوم (Mg)</div>
                                    </div>
                                </div>
                                <div class="toc-link" style="cursor: default;">
                                    <i class="fas fa-exchange-alt" style="color: #3b82f6;"></i>
                                    <div>
                                        <strong>عناصر نقل الطاقة والإلكترون</strong>
                                        <div style="font-size: 0.85em; opacity: 0.75; margin-top: 3px;">الحديد (Fe) والسيلينيوم (Se)</div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- قسم الحديد -->
                    <div class="research-section" id="res-fe">
                        <div class="section-header-element element-fe">
                            <div class="element-badge">Fe</div>
                            <div class="element-info-title">
                                <h2>أولاً: الحديد (Fe) — كيمياء الأكسجين وانتقال الإلكترونات</h2>
                                <p>العدد الذري: 26 | الوزن الذري: 55.84</p>
                            </div>
                        </div>

                        <div class="subsection">
                            <h4><i class="fas fa-atom"></i> 1. الخصائص الكيميائية والذرية للحديد</h4>
                            <p>الحديد عنصر فلزي انتقالي (Transition Metal) ينتمي للسلسلة الانتقالية الأولى في الجدول الدوري، وعدده الذري 26. يتميز التوزيع الإلكتروني للحديد بقابليته لفقد إلكترونات من المدارين 4s و 3d، مما يمنحه القدرة الفريدة على الوجود في حالتي أكسدة حيوية رئيسيتين ومتوازنتين داخل البيئة المائية للجسم:</p>
                            <ul>
                                <li><strong>الحديد الثنائي - Ferrous (Fe²⁺):</strong> يتميز بزيادة تفاعليته وقابليته للذوبان، ويُعد الصورة الرئيسية في الامتصاص المعوي والارتباط بالأكسجين.</li>
                                <li><strong>الحديد الثلاثي - Ferric (Fe³⁺):</strong> الصورة الأكثر استقراراً في الوسط الأكسجيني، ويشكل الصورة الأساسية للتخزين بروتينياً داخل الخلية.</li>
                            </ul>
                            <p>تسمح هذه الخاصية المزدوجة للحديد بالمشاركة الفعالة والديناميكية في تفاعلات الأكسدة والاختزال (Redox Reactions)، حيث تنتقل الإلكترونات بسلاسة بين المواد المتفاعلة، وعلى خلاف العناصر ذات حالات الأكسدة الثابتة (مثل الزنك 2+)، يعد الحديد بمثابة "مكون إلكتروني" يحرك التفاعلات الحيوية داخل الخلايا.</p>
                        </div>

                        <div class="subsection">
                            <h4><i class="fas fa-lungs"></i> 2. آلية نقل الأكسجين عبر حلقة الهيم والهيموغلوبين</h4>
                            <p>لا يوجد الحديد داخل جسم الإنسان في صورة أيون حر طليق، لأن الأيونات الحرة تمتلك سمية تأكسدية عالية. بدلاً من ذلك، يتم احتجاز الحديد داخل مجموعة كيميائية عضوية معقدة تُعرف بالهيم (Heme). تتكون مجموعة الهيم من حلقة عضوية كبيرة تُعرف باسم البورفيرين (Porphyrin) تتوسطها ذرة حديد مرابطة بأربعة روابط تناسقية مع ذرات نيتروجين الحلقة.</p>

                            <div class="info-box info">
                                <h5><i class="fas fa-droplet"></i> التكامل الجزيئي في نقل الأكسجين</h5>
                                <p>تتيح البيئة الفراغية المنظمة داخل بروتين الهيموغلوبين بذرة الحديد (Fe²⁺) تكوين رابطة سادسة ضعيفة وقابلة للانعكاس مع جزيء الأكسجين (O₂). يتيح هذا التوازن للحديد التقاط الأكسجين في الرئتين حيث يكون الضغط الجزئي للأكسجين مرتفعاً، ثم إطلاقه بسلاسة في الأنسجة التي تعاني من انخفاض الضغط الجزئي.</p>
                            </div>
                        </div>

                        <div class="subsection">
                            <h4><i class="fas fa-charging-station"></i> 3. الحديد في السيتوكرومات وسلاسل نقل الإلكترون</h4>
                            <p>لا تقتصر كيمياء الحديد الحيوية على نقل الغازات كالأكسجين، بل يمتد دوره الكيميائي إلى الميتوكوندريا حيث يشارك في إنتاج الطاقة. يدخل الحديد في تركيب بروتينات متخصصة تسمى السيتوكرومات (Cytochrome)، والتي تشكل المركبات الأساسية في سلسلة التنفس الخلوي ونقل الإلكترونات (Electron Transport Chain).</p>
                            <p>خلال عمليات التنفس الخلوي، تكتسب ذرة الحديد في السيتوكروم إلكتروناً لتحول من الصورة الثلاثية (Fe³⁺) إلى الصورة الثنائية (Fe²⁺)، ثم لا تلبث أن تفقد هذا الإلكترون لتنقله إلى المركب التالي في السلسلة وتعود لـ (Fe³⁺). هذا التأرجح الدوري المستمر يجعل الحديد يعمل كموصل كهربائي جزئي ينقل الطاقة الكيميائية دون أن يتم استهلاكه كمتفاعل نهائي.</p>
                        </div>

                        <div class="subsection">
                            <h4><i class="fas fa-cubes"></i> 4. عناقيد الحديد والكبريت (Iron-Sulfur Clusters)</h4>
                            <p>من التراكيب الجزيئية المتقدمة للحديد دخوله في تراكيب مدمجة تُعرف باسم عناقيد الحديد والكبريت (Fe-S Clusters) مثل [2Fe-2S] و [4Fe-4S]. ترتبط هذه العناقيد ببقايا حمض السيستئين الأميني داخل الإنزيمات الحيوية (مثل إنزيم أكونيتاز وإنزيمات مركب الميتوكوندريا الأول).</p>
                            <p>وتعمل هذه العناقيد كمستشعرات خلوية لمستويات الأكسجين والتأكسد، بالإضافة إلى أداء دور التحفيز الإنزيمي المباشر.</p>
                        </div>

                        <div class="subsection">
                            <h4><i class="fas fa-exclamation-triangle"></i> 5. الخطورة التأكسدية وتفاعل فنتون (Fenton Reaction)</h4>
                            <p>على الرغم من الأهمية المطلقة للحديد، إلا أن وجوده حراً في السيتوبلازم يمثل خطراً جسيماً على سلامة الخلية. يمتلك الحديد الحر القدرة على تحفيز تفاعل كيميائي خطير يُعرف بـ تفاعل فنتون (Fenton Reaction)، حيث يتفاعل الحديد الثنائي مع فوق أكسيد الهيدروجين:</p>

                            <div class="formula-box">
                                Fe²⁺ + H₂O₂ → Fe³⁺ + OH⁻ + •OH
                            </div>

                            <div class="info-box danger">
                                <h5><i class="fas fa-radiation"></i> خطر جذر الهيدروكسيل (•OH)</h5>
                                <p>ينتج عن هذا التفاعل جذر الهيدروكسيل (•OH) وهو أحشى وأقوى الجذور الحرة التأكسدية التي تدمر الأغشية الخلوية والـ DNA. لذلك نظم الجسم آليات صارمة لتخزين الحديد ونقله عبر الترانسفيرين (Transferrin) في الدم والفيريتين (Ferritin) بروتين خلايا.</p>
                            </div>

                            <p><strong>بروتين الفيريتين (Ferritin):</strong> مجمع تخزين كروي مجوف يختزن ما يصل إلى 4500 ذرة حديد داخل نواته البلورية.</p>
                            <p><strong>بروتين الترانسفيرين (Transferrin):</strong> ينقل الحديد في مجرى الدم في حالة الأكسدة Fe³⁺ بأمان تام لمنع تفاعل فنتون.</p>
                        </div>
                    </div>

                    <!-- قسم الزنك -->
                    <div class="research-section" id="res-zn">
                        <div class="section-header-element element-zn">
                            <div class="element-badge">Zn</div>
                            <div class="element-info-title">
                                <h2>ثانياً: الزنك (Zn) — عنصر التثبيت البنيوي والتحفيز الإنزيمي</h2>
                                <p>العدد الذري: 30 | عنصر فلزي انتقالي</p>
                            </div>
                        </div>

                        <div class="subsection">
                            <h4><i class="fas fa-atom"></i> 1. الخصائص الكيميائية والروابط التناسقية للزنك</h4>
                            <p>الزنك عنصر فلزي يقع في المجموعة الثانية عشرة من الجدول الدوري، وعدده الذري 30. يوجد الزنك داخل الأنظمة الحيوية حصرياً على صورة أيون موجب ثنائي الشحنة (Zn²⁺). يمتلك الزنك غلافاً إلكترونياً كاملاً من طراز (d10)، مما جعله خافتاً من الناحية التأكسدية؛ فهو لا يتأرجح بين حالات أكسدة مختلفة كالحديد، ولا يشارك في تفاعلات الأكسدة والاختزال المباشرة.</p>
                        </div>

                        <div class="subsection">
                            <h4><i class="fas fa-fingerprint"></i> 2. تثبيت البنية الفراغية وأصابع الزنك (Zinc Fingers)</h4>
                            <p>تتمثل القوة الكيميائية الفريدة لأيون الزنك في قدرته الفائقة على تكوين روابط تناسقية رباعية مع ذرات النيتروجين في حمض الهيستيدين (Histidine) وذرات الكبريت في حمض السيستين (Cysteine). يتيح هذا الارتباط إنشاء ثنيات بروتينية صلبة تعرف بـ أصابع الزنك (Zinc Finger Motifs).</p>

                            <div class="info-box purple">
                                <h5><i class="fas fa-dna"></i> التحكم في التعبير الجيني بواسطة الزنك</h5>
                                <p>تعمل أصابع الزنك كقوالب هندسية تسمح لبروتينات العوامل النووية (Transcription Factors) بالقبض الدقيق على مجاري الحمض النووي DNA والتلازم مع تسلسلات قواعده النيتروجينية، مما يعطي الخلايا القدرة على تنظيم قراءة الجينات وتفعيلها بحسب الحاجة الحيوية.</p>
                            </div>
                        </div>

                        <div class="subsection">
                            <h4><i class="fas fa-cog"></i> 3. الدور التحفيزي في الإنزيمات: الأنهيدراز الكربوني</h4>
                            <p>يدخل الزنك في تركيب أكثر من 300 إنزيم تحفيزي. يعمل أيون الزنك (Zn²⁺) كحمض لويس (Lewis Acid) قوي يكذب جزيء الماء المترابط معه، مما يقلل القيمة الحمضية pKa للماء ويحوله إلى أيون هيدروكسيل نشط عند الرقم الهيدروجيني الفسيولوجي. وأبرز مثال هو إنزيم الأنهيدراز الكربوني (Carbonic Anhydrase):</p>

                            <div class="formula-box">
                                CO₂ + H₂O ⇌ HCO₃⁻ + H⁺
                            </div>
                        </div>
                    </div>

                    <!-- قسم المغنيسيوم -->
                    <div class="research-section" id="res-mg">
                        <div class="section-header-element element-mg">
                            <div class="element-badge">Mg</div>
                            <div class="element-info-title">
                                <h2>ثالثاً: المغنيسيوم (Mg) — عنصر نقل الطاقة والاستقرار الجيني</h2>
                                <p>العدد الذري: 12 | الوزن الذري: 24.30</p>
                            </div>
                        </div>

                        <div class="subsection">
                            <h4><i class="fas fa-atom"></i> 1. الخصائص الكيميائية والشحنة الأيونية للمغنيسيوم</h4>
                            <p>المغنيسيوم عنصر فلزي من الفلزات القلوية الترابية (Group 2)، وعدده الذري 12. يوجد في البيئة الخلوية على هيئة أيون موجب ثنائي الشحنة (Mg²⁺). يمتلك أيون المغنيسيوم كثافة شحنة عالية جداً بفضل صغر حجمه الأيوني، مما يجعله محاطاً بغلاف تميه كيميائي مائي كثيف، ويمنحه جلي الألفة الكيميائية للارتباط بالمجموعات الكيميائية سالبة الشحنة، وعلى رأسها مجموعات الفوسفات (Phosphate Groups).</p>
                        </div>

                        <div class="subsection">
                            <h4><i class="fas fa-bolt"></i> 2. معقد المغنيسيوم وجزيء ATP</h4>
                            <p>يُعد جزيء أدينوسين ثالثي الفوسفات (ATP) العملة الأساسية لنقل الطاقة داخل الخلايا. يحمل هذا الجزيء أربع شحنات سالبة كيميائية في الظروف الفسيولوجية، مما يجعل مجموعات الفوسفات تتنافر وتتأثر بالاضطراب الفراغي، وهذا يأتي الدور الكيميائي الحاسم للمغنيسيوم؛ حيث يندمج مع جزيء ATP ليشكل معقداً مخلبياً يعرف بـ [Mg-ATP]²⁻.</p>
                        </div>

                        <div class="subsection">
                            <h4><i class="fas fa-key"></i> 3. المغنيسيوم كالمفتاح الحقيقي لاستخدام الطاقة</h4>
                            <p>إن أغلب الإنزيمات المستهلكة للطاقة (مثل الكاينازات Kinases) لا تتفاعل إطلاقاً مع جزيء ATP الحر؛ بل تعرف حصرياً معقد Mg-ATP. يعمل المغنيسيوم على الجانب الإلكترونية للمجموعات، مما يجعل الفوسفات الطرفية (γ-phosphate) محبة للهجوم النيكلوفيلي وسهلة الانفصال والنقل الطاقة.</p>
                        </div>

                        <div class="subsection">
                            <h4><i class="fas fa-dna"></i> 4. تثبيت الهياكل الجينية والريبوسومات</h4>
                            <p>يمتد دور المغنيسيوم الكيميائي ليشكل الدعامة الأساسية للأحماض النووية (DNA و RNA). يعمل المغنيسيوم على التعادل الكهرومغناطيسي مع مصفوفة الفوسفات ثنائية السلسلة في الـ DNA، مما يمنع تفكك السلسلتين المزدوجتين تحت تأثير التنافر الكهربائي السالب. كما يعد المغنيسيوم شرطاً لتماسك وحدات الريبوسومات (Ribosomal Subunits) لتخليق وتصنيع البروتينات.</p>
                        </div>
                    </div>

                    <!-- قسم اليود -->
                    <div class="research-section" id="res-i">
                        <div class="section-header-element element-i">
                            <div class="element-badge">I</div>
                            <div class="element-info-title">
                                <h2>رابعاً: اليود (I) — عنصر يدخل في بناء الهرمونات ببراعة تساهمية</h2>
                                <p>العدد الذري: 53 | الوزن الذري: 126.90</p>
                            </div>
                        </div>

                        <div class="subsection">
                            <h4><i class="fas fa-atom"></i> 1. الخصائص الكيميائية والامتصاص النسيجي لليود</h4>
                            <p>اليود عنصر لا فلزي قلوي ينتمي لعائلة الهالوجينات (Group 17) بالجدول الدوري، وعدده الذري 53. يتمتع اليود بنصف قطر ذري كبير وقابلية للاستقطاب الإلكتروني، يُلتقط اليود الغذائي في القناة الهضمية على صورة أيون يوديد (I⁻)، حيث يتم ضخه بنشاط إلى داخل خلايا الغدة الدرقية عبر ناقل اليوديد والصوديوم (NIS Membrane Pump) بكفاءة تزيد مئات المرات عن مستواه في الدم.</p>
                        </div>

                        <div class="subsection">
                            <h4><i class="fas fa-flask"></i> 2. الآلية الإنزيمية لبناء هرمونات الغدة الدرقية</h4>
                            <p>على عكس المعادن الأخرى التي تؤدي دور المساعد الإنزيمي المؤقت، يدخل اليود في روابط تساهمية كربونية-يودية (C-I Bonds) دائمة داخل بنية المركب العضوي. تتضمن هذه العملية خطوات كيميائية متعاقبة تحت إشراف إنزيم بيروكسيداز الغدة الدرقية (TPO):</p>
                            <ul>
                                <li>أكسدة أيون اليوديد (I⁻) باستخدام فوق أكسيد الهيدروجين إلى صورة يودية نشطة.</li>
                                <li>إدراج اليود تساهمياً في الحلقات العطرية لحمض التيروزين (Tyrosine) الأميني داخل بروتين الثايروغلوبولين.</li>
                                <li>اقتران حلقة أحادي يودوتيروزين (MIT) مع ثنائي يودوتيروزين (DIT) لتشكيل هرمون T₃، أو اقتران حلقتين ثنائيتين لتشكيل هرمون T₄.</li>
                            </ul>
                        </div>

                        <div class="subsection">
                            <h4><i class="fas fa-balance-scale"></i> 3. الفارق الذري بين هرموني T3 و T4</h4>
                            <p>يحمل هرمون الثيروكسين (T₄) أربع ذرات يود وهو الهرمون الرئيسي المفرز في الدم، بينما يحمل هرمون ثلاثي يودوثايرونين (T₃) ثلاث ذرات يود فقط. وعلى الرغم من حقيقة أن T₄ أكثر وفرة، فإن T₃ يمتلك ألفة ارتباط بالمستقبلات النووية تزيد بمقدار 10 إلى 15 ضعفاً عن T₄، مما يبرز الأثر الفائق لنزع ذرة يود واحدة على الفعالية الفسيولوجية.</p>
                        </div>
                    </div>

                    <!-- قسم السيلينيوم -->
                    <div class="research-section" id="res-se">
                        <div class="section-header-element element-se">
                            <div class="element-badge">Se</div>
                            <div class="element-info-title">
                                <h2>خامساً: السيلينيوم (Se) — درع مضاد الأكسدة الحيوي</h2>
                                <p>العدد الذري: 34 | الوزن الذري: 78.96</p>
                            </div>
                        </div>

                        <div class="subsection">
                            <h4><i class="fas fa-atom"></i> 1. الخصائص الكيميائية وحمض السيلينوسيستين النادر</h4>
                            <p>السيلينيوم عنصر لا فلزي يقع في المجموعة السادسة عشرة (الكالكوجينات Chalcogens) بالجدول الدوري أسفل عنصر الكبريت مباشرة، وعدده الذري 34. يتشابه السيلينيوم كيميائياً مع الكبريت، ولكنه يمتاز بكثافة إلكترونية ونصف قطر ذري أكبر، مما يجعل رابطة (Se-H) أكثر حامضية وأسهل في التأين مقارنة برابطة (S-H). يدمج الجسم السيلينيوم في الحمض الأميني الخاص رقم 21 (سيلينوسيستين).</p>
                        </div>

                        <div class="subsection">
                            <h4><i class="fas fa-shield-virus"></i> 2. إنزيمات السيلينوبروتين والدفاع المضاد للأكسدة</h4>
                            <p>يُشفَّر حمض السيلينوسيستين جينياً عبر شفرة خاصة (UGA Stop Codon) بمساعدة تراكيب SECIS المتقدمة في الـ mRNA. يدخل هذا الحمض في بروتينات حيوية تسمى (Selenoproteins)، وعلى رأسها مجموعة إنزيمات الجلوتاثيون بيروكسيداز (Glutathione Peroxidase - GPx).</p>

                            <div class="formula-box">
                                H₂O₂ + 2GSH → 2H₂O + GSSG
                            </div>

                            <p>يعمل السيلينيوم في هذا الإنزيم على التفكيك المباشر والآمن لمركبات بيروكسيد الهيدروجين والبيروكسيدات العضوية، وتحويلها إلى ماء وكحول دون إطلاق أي جذور حرة ثانوية، مما يحمي الغشاء الخلوية والدهون الفسفورية من التلف.</p>
                        </div>

                        <div class="subsection">
                            <h4><i class="fas fa-handshake"></i> 3. التكامل الكيميائي الحيوي بين السيلينيوم واليود</h4>
                            <p>يمتد التكامل الكيميائي بين العناصر عبر إنزيمات نازعات اليود (Deiodinases)، وهي إنزيمات سيلينوبروتينية تحتوي على السيلينيوم في مواقعها النشطة. تقوم هذه الإنزيمات بنزع ذرة يود من هرمون T₄ الخامل لتحويله إلى T₃ النشط. وبذلك، فإن بناء هرمون الغدة الدرقية يتطلب اليود، بينما تفعيله النسيجي يتطلب السيلينيوم.</p>
                        </div>
                    </div>

                    <!-- جدول المقارنة -->
                    <div class="research-section" id="res-table">
                        <div class="section-header-element element-intro">
                            <div class="element-badge"><i class="fas fa-table"></i></div>
                            <div class="element-info-title">
                                <h2>جدول المقارنة الشامل للخصائص والوظائف</h2>
                                <p>ملخص الخصائص الكيميائية والوظائف الحيوية للعناصر الخمسة</p>
                            </div>
                        </div>

                        <div class="comparison-table-wrapper">
                            <table class="comparison-table">
                                <thead>
                                    <tr>
                                        <th>العنصر</th>
                                        <th>الصورة الأيونية الحيوية</th>
                                        <th>الخاصية الكيميائية المعززة</th>
                                        <th>الوظيفة الجزئية الرئيسية</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>
                                            <div class="element-cell">
                                                <span class="element-mini-badge" style="background: #b91c1c;">Fe</span>
                                                الحديد
                                            </div>
                                        </td>
                                        <td>Fe²⁺ / Fe³⁺</td>
                                        <td>التناوب بين حالات الأكسدة وتكوين الهيم</td>
                                        <td>نقل O₂ عبر الهيموغلوبين ونقل الإلكترونات في السيتوكرومات</td>
                                    </tr>
                                    <tr>
                                        <td>
                                            <div class="element-cell">
                                                <span class="element-mini-badge" style="background: #0891b2;">Zn</span>
                                                الزنك
                                            </div>
                                        </td>
                                        <td>Zn²⁺ (ثابتة)</td>
                                        <td>روابط تناسقية رباعية مع Cys/His (حمض لويس)</td>
                                        <td>تثبيت أشكال أصابع الزنك للـ DNA وتحفيز الأنهيدراز الكربوني</td>
                                    </tr>
                                    <tr>
                                        <td>
                                            <div class="element-cell">
                                                <span class="element-mini-badge" style="background: #16a34a;">Mg</span>
                                                المغنيسيوم
                                            </div>
                                        </td>
                                        <td>Mg²⁺</td>
                                        <td>الألفة العالية لشحنات الفوسفات الكثيفة</td>
                                        <td>تكوين معقد [Mg-ATP]²⁻ وترتيب الـ DNA والريبوسومات</td>
                                    </tr>
                                    <tr>
                                        <td>
                                            <div class="element-cell">
                                                <span class="element-mini-badge" style="background: #7c3aed;">I</span>
                                                اليود
                                            </div>
                                        </td>
                                        <td>I⁻ / يود عضوي</td>
                                        <td>تكوين روابط تساهمية كربونية-يودية دائمة</td>
                                        <td>بناء الهرمونات الدرقية (T₃ & T₄) للتحكم بالمستقلب الخلوي</td>
                                    </tr>
                                    <tr>
                                        <td>
                                            <div class="element-cell">
                                                <span class="element-mini-badge" style="background: #ea580c;">Se</span>
                                                السيلينيوم
                                            </div>
                                        </td>
                                        <td>سيلينوسيستين</td>
                                        <td>حمض أميني نادر ذو قدرة اختزال فائقة</td>
                                        <td>الموقع النشط لإنزيم GPx لمكافحة التأكسد وإنزيمات Deiodinases</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>

                    <!-- الخاتمة -->
                    <div class="research-section" id="res-conclusion">
                        <div class="section-header-element element-intro">
                            <div class="element-badge"><i class="fas fa-flag-checkered"></i></div>
                            <div class="element-info-title">
                                <h2>الخاتمة والتوصيات العلمية</h2>
                                <p>ملخص النتائج والتوصيات البحثية</p>
                            </div>
                        </div>

                        <div class="conclusion-box">
                            <h3><i class="fas fa-lightbulb"></i> الخاتمة</h3>
                            <p>تكشف هذه الدراسة الكيميائية الحيوية الموسعة للعناصر الخمسة (الحديد، الزنك، المغنيسيوم، اليود، والسيلينيوم) عن حقيقة جوهرية: إن المظاهر الفسيولوجية المعقدة لجسم الإنسان تستند كلياً إلى سلوكيات تفاعلية دقيقة تحدث على المستوى الذري والإلكتروني.</p>
                            <p>فالتوازنات الدقيقة بين هذه العناصر، وتوافق هندستها التناسقية مع الجزيئات الحيوية الكبرى، هي ما يضمن كفاءة تحويل الطاقة، حماية الخلايا من التلف التأكسدي، والتعبير الجيني المضبوط.</p>

                            <h3 style="margin-top: 20px;"><i class="fas fa-bullseye"></i> التوصيات</h3>
                            <p>نوصي بالتوسع في أبحاث علم الكيمياء التناسقية الحيوية (Bioinorganic Chemistry) لفهم التدخلات المباشرة بين النقص الغذائي لهذه العناصر والاضطرابات الجزئية الناتجة عنها.</p>
                        </div>
                    </div>

                    <!-- المراجع -->
                    <div class="research-section" id="res-refs">
                        <div class="section-header-element element-intro">
                            <div class="element-badge"><i class="fas fa-book"></i></div>
                            <div class="element-info-title">
                                <h2>المراجع العلمية الأصلية</h2>
                                <p>المصادر والدراسات المعتمدة في البحث</p>
                            </div>
                        </div>

                        <ol class="references-list">
                            <li>Rolić, T., et al. (2025). Iron Metabolism, Calcium, Magnesium and Trace Elements: A Review. <em>Biological Trace Element Research</em>. <a href="https://doi.org/10.1007/s12011-024-04289-z" target="_blank">https://doi.org/10.1007/s12011-024-04289-z</a></li>
                            <li>Teaching the Chemical Elements in Biochemistry: Elemental Biology and Metallomics. <a href="https://pmc.ncbi.nlm.nih.gov/articles/PMC9303777" target="_blank">https://pmc.ncbi.nlm.nih.gov/articles/PMC9303777</a></li>
                            <li>Trace Elements in Human Nutrition (II) – An Update. <a href="https://pmc.ncbi.nlm.nih.gov/articles/6993532" target="_blank">https://pmc.ncbi.nlm.nih.gov/articles/6993532</a></li>
                            <li>Biochemistry, Nutrients. NCBI Bookshelf. <a href="https://www.ncbi.nlm.nih.gov/books/NBK554545" target="_blank">https://www.ncbi.nlm.nih.gov/books/NBK554545</a></li>
                            <li>Essential Metals in Health and Disease. <em>Chemico-Biological Interactions</em>. <a href="https://doi.org/10.1016/j.cbi.2022.110173" target="_blank">https://doi.org/10.1016/j.cbi.2022.110173</a></li>
                        </ol>
                    </div>

                    <button class="back-to-top" id="back-to-top" title="العودة للأعلى">
                        <i class="fas fa-chevron-up"></i>
                    </button>
                </div>
            </div>
        </div>
    </div>

    <audio id="correct-sound" preload="auto">
        <source src="https://assets.mixkit.co/active_storage/sfx/257/257-preview.mp3" type="audio/mp3">
    </audio>
    <audio id="wrong-sound" preload="auto">
        <source src="https://assets.mixkit.co/active_storage/sfx/258/258-preview.mp3" type="audio/mp3">
    </audio>
    <audio id="complete-sound" preload="auto">
        <source src="https://assets.mixkit.co/active_storage/sfx/255/255-preview.mp3" type="audio/mp3">
    </audio>
    <audio id="fail-sound" preload="auto">
        <source src="https://assets.mixkit.co/active_storage/sfx/250/250-preview.mp3" type="audio/mp3">
    </audio>

    <script>
        const VALID_SCREENS = [
            'login', 'welcome', 'quiz-setup', 'quiz', 'results',
            'progress', 'leaderboard', 'settings', 'simulation',
            'notifications', 'profile', 'chemistry-research'
        ];

        function getScreenFromHash() {
            let hash = window.location.hash.replace(/^#\/?/, '');
            if (!hash) return 'login';
            hash = hash.replace(/^\//, '');
            return VALID_SCREENS.includes(hash) ? hash : 'welcome';
        }

        function navigateTo(screenId, replace = false) {
            if (!VALID_SCREENS.includes(screenId)) screenId = 'welcome';
            const newHash = '#/' + screenId;
            if (replace) {
                history.replaceState(null, '', newHash);
                handleRoute();
            } else {
                if (window.location.hash === newHash) {
                    handleRoute();
                } else {
                    window.location.hash = newHash;
                }
            }
        }

        function handleRoute() {
            const screenId = getScreenFromHash();
            const user = getLoggedInUser();
            
            if (!user && screenId !== 'login') {
                navigateTo('login', true);
                return;
            }
            if (user && screenId === 'login') {
                navigateTo('welcome', true);
                return;
            }
            if (screenId === 'login') {
                showLoginScreen();
            } else {
                showMainApp();
                showScreenInternal(screenId);
            }
            updateUrlIndicator(screenId);
        }

        function showLoginScreen() {
            document.getElementById('login').classList.add('active');
            document.getElementById('main-app').style.display = 'none';
        }

        function showMainApp() {
            document.getElementById('login').classList.remove('active');
            document.getElementById('main-app').style.display = 'flex';
            const user = getLoggedInUser();
            if (user) {
                studentName = user.name;
                studentSection = user.section;
                document.getElementById('username-display').textContent = user.name;
                document.getElementById('section-display').textContent = `الشعبة: ${user.section}`;
                document.getElementById('result-username').textContent = user.name;
                document.getElementById('profile-section').textContent = `الشعبة: ${user.section}`;
            }
        }

        function showScreenInternal(screenId) {
            document.querySelectorAll('.screen').forEach(screen => screen.classList.remove('active'));
            document.querySelectorAll('.nav-link').forEach(link => link.classList.remove('active'));
            
            const targetScreen = document.getElementById(screenId);
            if (targetScreen) targetScreen.classList.add('active');
            
            const navLink = document.querySelector(`.nav-link[data-screen="${screenId}"]`);
            if (navLink) navLink.classList.add('active');
            
            if (screenId === 'progress') updateProgressScreen();
            if (screenId === 'leaderboard') updateLeaderboard();
            if (screenId === 'notifications') updateNotifications();
            if (screenId === 'profile') updateProfile();
            if (screenId === 'chemistry-research') setupResearchScrollBehavior();
        }

        function updateUrlIndicator(screenId) {
            const indicator = document.getElementById('url-indicator');
            indicator.textContent = '🔗 ' + window.location.href;
            indicator.classList.add('visible');
        }

        document.getElementById('url-indicator').addEventListener('click', function() {
            navigator.clipboard.writeText(window.location.href).then(() => {
                const original = this.textContent;
                this.textContent = '✅ تم نسخ الرابط!';
                setTimeout(() => { this.textContent = original; }, 1500);
            });
        });

        function saveLoggedInUser(name, section) {
            const user = { name, section, loginTime: Date.now() };
            localStorage.setItem('chemistryCurrentUser', JSON.stringify(user));
        }

        function getLoggedInUser() {
            const data = localStorage.getItem('chemistryCurrentUser');
            if (!data) return null;
            try { return JSON.parse(data); } catch { return null; }
        }

        function logoutUser() {
            if (confirm('هل أنت متأكد من تسجيل الخروج؟')) {
                localStorage.removeItem('chemistryCurrentUser');
                navigateTo('login', true);
                document.getElementById('student-name').value = '';
                document.getElementById('student-section').value = '';
            }
        }

        // ============================================
        // وظائف صفحة البحث الكيميائي
        // ============================================
        function setupResearchScrollBehavior() {
            const backToTop = document.getElementById('back-to-top');
            if (!backToTop) return;
            
            window.removeEventListener('scroll', handleResearchScroll);
            window.addEventListener('scroll', handleResearchScroll);
            
            document.querySelectorAll('.research-toc .toc-link[href^="#"]').forEach(link => {
                link.addEventListener('click', function(e) {
                    e.preventDefault();
                    const targetId = this.getAttribute('href').substring(1);
                    const target = document.getElementById(targetId);
                    if (target) {
                        const mainContent = document.querySelector('.main-content');
                        const targetTop = target.offsetTop - 20;
                        mainContent.scrollTo({ top: targetTop, behavior: 'smooth' });
                    }
                });
            });
            
            backToTop.onclick = () => {
                document.querySelector('.main-content').scrollTo({ top: 0, behavior: 'smooth' });
            };
        }

        function handleResearchScroll() {
            const backToTop = document.getElementById('back-to-top');
            if (backToTop) {
                const mainContent = document.querySelector('.main-content');
                if (mainContent && mainContent.scrollTop > 300) {
                    backToTop.classList.add('visible');
                } else {
                    backToTop.classList.remove('visible');
                }
            }
        }

        // بيانات الأسئلة
        const allQuestions = [
            { question: "العملية التي يعاد فيها ترتيب الذرات في مادة أو أكثر لتكوين مواد جديدة تسمى:", options: ["التغير الفيزيائي", "التفاعل النووي", "التفاعل الكيميائي"], correct: 2, explanation: "التعريف المباشر للتفاعل الكيميائي هو عملية يعاد فيها ترتيب الذرات لتكوين مواد جديدة", lesson: "التفاعلات والمعادلات", difficulty: "easy" },
            { question: "المعادلة التي توضح الجسيمات (الذرات أو الأيونات) المشاركة في التفاعل بشكل مفصل تسمى:", options: ["المعادلة الكيميائية", "المعادلة الأيونية", "المعادلة الموزونة"], correct: 1, explanation: "المعادلة الأيونية تمثل المواد في المحاليل المائية على شكل أيونات", lesson: "التفاعلات والمعادلات", difficulty: "medium" },
            { question: "ما هو العدد الأقصى من الإلكترونات الذي يستوعبه مستوى الطاقة الرئيسي الرابع (n=4)?", options: ["18", "8", "32"], correct: 2, explanation: "حسب قاعدة 2n²: 2 × (4)² = 32 إلكترون", lesson: "الترتيب الإلكتروني", difficulty: "medium" },
            { question: "أي من الرموز التالية يمثل الصيغة الأيونية الصحيحة لكلوريد الصوديوم?", options: ["Na²⁺ Cl⁻", "Na⁺ Cl⁻", "Na²⁺ Cl²⁻"], correct: 1, explanation: "الصوديوم يفقد إلكترون ليصبح Na⁺ والكلور يكتسب ليصبح Cl⁻", lesson: "التفاعلات والمعادلات", difficulty: "easy" },
            { question: "الأيون OH⁻ يسمى أيون:", options: ["الكربوكسيل", "الهيدروكسيد", "الكربونات"], correct: 1, explanation: "الاسم الشائع لأيون الهيدروكسيد", lesson: "التفاعلات والمعادلات", difficulty: "easy" },
            { question: "التفاعل الذي تكون نواتجه مادة واحدة فقط يُصنف على أنه تفاعل:", options: ["احتراق", "إحلال بسيط", "تكوين"], correct: 2, explanation: "يتحد متفاعلان أو أكثر لتكوين مادة واحدة", lesson: "التفاعلات والمعادلات", difficulty: "easy" },
            { question: "إذا انتهى التوزيع الإلكتروني بـ 3p⁶، فإن العدد الذري هو:", options: ["10", "12", "18"], correct: 2, explanation: "1s² 2s² 2p⁶ 3s² 3p⁶ = 18 إلكترون", lesson: "الترتيب الإلكتروني", difficulty: "medium" },
            { question: "الرمز المستخدم للفصل بين المواد المتفاعلة والنواتج هو:", options: ["+", "→", "(s)"], correct: 1, explanation: "السهم يشير لاتجاه التفاعل", lesson: "التفاعلات والمعادلات", difficulty: "easy" },
            { question: "تفاعل مادة مع الأكسجين ينتج ضوء أو حرارة هو تفاعل:", options: ["تكوين", "احتراق", "إحلال مزدوج"], correct: 1, explanation: "التعريف المباشر لتفاعل الاحتراق", lesson: "التفاعلات والمعادلات", difficulty: "easy" },
            { question: "الصيغة الصحيحة لهيدروكسيد الألومنيوم هي:", options: ["AlOH", "Al(OH)₂", "Al(OH)₃"], correct: 2, explanation: "شحنة Al هي 3+ وشحنة OH هي 1-", lesson: "التفاعلات والمعادلات", difficulty: "medium" },
            { question: "كم عدد المستويات الثانوية في n=3?", options: ["2", "3", "4"], correct: 1, explanation: "s, p, d", lesson: "الترتيب الإلكتروني", difficulty: "medium" },
            { question: "أي توزيع إلكتروني صحيح للكلور (17)?", options: ["1s² 2s² 2p⁶ 3s² 3p⁵", "1s² 2s² 2p⁶ 3s² 3p⁶", "1s² 2s² 2p⁶ 3s¹ 3p⁶"], correct: 0, explanation: "التوزيع الصحيح وفقاً لمبدأ البناء التصاعدي", lesson: "الترتيب الإلكتروني", difficulty: "hard" },
            { question: "ما المستويات الثانوية التي يحتويها n=5?", options: ["s, p", "s, p, d", "s, p, d, f"], correct: 2, explanation: "المستوى الخامس يحتوي على s, p, d, f, g", lesson: "الترتيب الإلكتروني", difficulty: "hard" },
            { question: "أي مما يلي ليس من أدلة حدوث التفاعل الكيميائي?", options: ["تصاعد غاز", "تغير اللون", "تغير الشكل"], correct: 2, explanation: "تغير الشكل تغير فيزيائي", lesson: "التفاعلات والمعادلات", difficulty: "easy" },
            { question: "في N₂ + 3H₂ → 2NH₃، ما معامل H₂?", options: ["1", "2", "3"], correct: 2, explanation: "3 جزئيات من H₂", lesson: "التفاعلات والمعادلات", difficulty: "medium" },
            { question: "عدد الأكسدة للأكسجين في معظم مركباته:", options: ["+1", "-1", "-2"], correct: 2, explanation: "-2 في معظم الأكاسيد", lesson: "التفاعلات والمعادلات", difficulty: "medium" },
            { question: "التوزيع الإلكتروني الصحيح للبورون (5):", options: ["1s² 2s³", "1s² 2s² 2p¹", "1s² 2p³"], correct: 1, explanation: "1s² 2s² 2p¹", lesson: "الترتيب الإلكتروني", difficulty: "medium" },
            { question: "الصيغة الصحيحة للناتج من Mg²⁺ مع NO₃⁻:", options: ["MgNO₃", "Mg(NO₃)₂", "Mg₂NO₃"], correct: 1, explanation: "شحنة Mg 2+ وشحنة NO₃ 1-", lesson: "التفاعلات والمعادلات", difficulty: "medium" },
            { question: "الصيغة الكيميائية لأكسيد الحديد الثنائي:", options: ["FeO₂", "Fe₂O", "FeO"], correct: 2, explanation: "نسبة 1:1 لمعادلة الشحنة", lesson: "التفاعلات والمعادلات", difficulty: "medium" },
            { question: "المعادلة الأيونية الكاملة للتفاعل AgNO₃ + KI:", options: ["Ag⁺ + NO₃⁻ + K⁺ + I⁻ → AgI + K⁺ + NO₃⁻", "Ag⁺ + I⁻ → AgI", "AgNO₃ + KI → AgI + KNO₃"], correct: 0, explanation: "جميع المواد الذائبة تتفكك", lesson: "التفاعلات والمعادلات", difficulty: "hard" },
            { question: "المعادلة الأيونية النهائية للتفاعل AgNO₃ + KI:", options: ["Ag⁺ + NO₃⁻ + K⁺ + I⁻ → AgI + K⁺ + NO₃⁻", "Ag⁺ + I⁻ → AgI", "K⁺ + NO₃⁻ → KNO₃"], correct: 1, explanation: "الأيونات المتفرجة تحذف", lesson: "التفاعلات والمعادلات", difficulty: "hard" },
            { question: "قانون حفظ الكتلة ينص على:", options: ["كتلة المتفاعلة = كتلة الناتجة", "فقدان كتلة", "زيادة كتلة"], correct: 0, explanation: "المادة لا تفنى ولا تستحدث", lesson: "التفاعلات والمعادلات", difficulty: "easy" },
            { question: "الغرض من المعاملات في المعادلة:", options: ["توضيح النسب بحيث يتساوى عدد الذرات", "سهولة القراءة", "زيادة السرعة"], correct: 0, explanation: "لتحقيق قانون حفظ الكتلة", lesson: "التفاعلات والمعادلات", difficulty: "easy" },
            { question: "تفاعل CH₄ مع O₂ لإنتاج CO₂ و H₂O هو:", options: ["تكوين", "إحلال بسيط", "احتراق"], correct: 2, explanation: "احتراق المركبات العضوية", lesson: "التفاعلات والمعادلات", difficulty: "medium" },
            { question: "لماذا يحل Mg محل H في HCl?", options: ["أكثر لمعاناً", "أكثر نشاطاً في سلسلة النشاط", "أرخص"], correct: 1, explanation: "سلسلة النشاط الكيميائي", lesson: "التفاعلات والمعادلات", difficulty: "medium" },
            { question: "أي التفاعلات التالية إحلال مزدوج?", options: ["Na + Cl₂ → 2NaCl", "Zn + 2HCl → ZnCl₂ + H₂", "AgNO₃ + NaCl → AgCl + NaNO₃"], correct: 2, explanation: "تبادل الأيونات", lesson: "التفاعلات والمعادلات", difficulty: "medium" },
            { question: "الخطأ في H₂ + O₂ = H₂O:", options: ["الصيغ خاطئة", "غير موزونة", "اتجاه السهم"], correct: 1, explanation: "عدد ذرات الأكسجين غير متساو", lesson: "التفاعلات والمعادلات", difficulty: "easy" },
            { question: "الرمز (s) يدل على:", options: ["محلول مائي", "غاز", "صلب"], correct: 2, explanation: "(s) للصلب", lesson: "التفاعلات والمعادلات", difficulty: "easy" },
            { question: "أي التغيرات التالية كيميائي؟", options: ["ذوبان السكر", "صدأ الحديد", "تجمّد الماء"], correct: 1, explanation: "صدأ الحديد تفاعل كيميائي", lesson: "التفاعلات والمعادلات", difficulty: "easy" },
            { question: "النسبة بين H₂ و O₂ في 2H₂ + O₂ → 2H₂O:", options: ["1:1", "2:1", "1:2"], correct: 1, explanation: "المعاملات 2:1", lesson: "التفاعلات والمعادلات", difficulty: "medium" },
            { question: "الصيغة الصحيحة لكبريتات الألومنيوم:", options: ["AlSO₄", "Al₂(SO₄)₃", "Al₃(SO₄)₂"], correct: 1, explanation: "شحنة Al 3+ و SO₄ 2-", lesson: "التفاعلات والمعادلات", difficulty: "hard" },
            { question: "4غ هيدروجين + 32غ أكسجين = ؟ ماء:", options: ["28غ", "32غ", "36غ"], correct: 2, explanation: "قانون حفظ الكتلة: 4 + 32 = 36غ", lesson: "التفاعلات والمعادلات", difficulty: "medium" },
            { question: "المعادلة الصحيحة لاحتراق المغنيسيوم:", options: ["Mg + O → MgO", "Mg + O₂ → 2MgO", "2Mg + O₂ → 2MgO"], correct: 2, explanation: "موزونة وصحيحة", lesson: "التفاعلات والمعادلات", difficulty: "medium" },
            { question: "هل تغير حالة المادة دليل على تفاعل كيميائي؟", options: ["صحيحة تماماً", "خاطئة تماماً", "غير دقيقة"], correct: 2, explanation: "قد يكون تغير فيزيائي", lesson: "التفاعلات والمعادلات", difficulty: "easy" },
            { question: "الرمز (g) يدل على:", options: ["صلب", "سائل", "غاز"], correct: 2, explanation: "(g) للغاز", lesson: "التفاعلات والمعادلات", difficulty: "easy" },
            { question: "لماذا لا يحل Cu محل Fe?", options: ["أقل لمعاناً", "أقل نشاطاً", "أكثر تكلفة"], correct: 1, explanation: "سلسلة النشاط", lesson: "التفاعلات والمعادلات", difficulty: "medium" },
            { question: "عدد ذرات الأكسجين في Al₂(SO₄)₃:", options: ["4", "7", "12"], correct: 2, explanation: "3 × 4 = 12", lesson: "التفاعلات والمعادلات", difficulty: "hard" },
            { question: "أي التفاعلات إحلال مزدوج؟", options: ["CaCO₃ → CaO + CO₂", "Zn + 2HCl → ZnCl₂ + H₂", "AgNO₃ + NaCl → AgCl + NaNO₃"], correct: 2, explanation: "تبادل الأيونات", lesson: "التفاعلات والمعادلات", difficulty: "medium" },
            { question: "المعادلة الموزونة لـ HCl + NaOH:", options: ["HCl + NaOH → NaCl + H₂O", "2HCl + NaOH → 2NaCl + H₂O", "HCl + 2NaOH → NaCl + 2H₂O"], correct: 0, explanation: "موزونة أصلاً", lesson: "التفاعلات والمعادلات", difficulty: "medium" },
            { question: "سبب استخدام السهم في المعادلات:", options: ["اتجاه التفاعل", "سرعة التفاعل", "التمييز"], correct: 0, explanation: "يرمز لـ 'ينتج'", lesson: "التفاعلات والمعادلات", difficulty: "easy" },
            { question: "عدد الإلكترونات التي يفقدها Mg (12):", options: ["إلكترون واحد", "إلكترونان", "ثلاثة"], correct: 1, explanation: "3s² يفقد إلكترونين", lesson: "الترتيب الإلكتروني", difficulty: "medium" },
            { question: "أيون توزيعه 1s² 2s² 2p⁶:", options: ["Na⁺", "F⁻", "O²⁻", "جميعها صحيحة"], correct: 3, explanation: "كلها لها 10 إلكترونات", lesson: "الترتيب الإلكتروني", difficulty: "hard" },
            { question: "المعادلة اللفظية لنترات الفضة + كلوريد الصوديوم:", options: ["→ كلوريد الفضة (راسب) + نترات الصوديوم", "→ نترات الصوديوم + كلوريد الفضة", "كلاهما صحيح"], correct: 2, explanation: "كلا الوصفين صحيح", lesson: "التفاعلات والمعادلات", difficulty: "easy" },
            { question: "أي المشاهدات تدل على تفاعل كيميائي؟", options: ["ذوبان السكر", "تغير لون عباد الشمس", "تكوين راسب"], correct: 2, explanation: "الراسب دليل قوي", lesson: "التفاعلات والمعادلات", difficulty: "medium" },
            { question: "الغرض من وزن المعادلات:", options: ["سهولة القراءة", "تطبيق حفظ الكتلة", "زيادة السرعة"], correct: 1, explanation: "تحقيق قانون حفظ الكتلة", lesson: "التفاعلات والمعادلات", difficulty: "easy" },
            { question: "معامل النيتروجين في 4NH₃ + 5O₂ → 4NO + 6H₂O:", options: ["4", "5", "1"], correct: 2, explanation: "معامل ضمني", lesson: "التفاعلات والمعادلات", difficulty: "hard" },
            { question: "لماذا نكتب حالة المادة في المعادلة؟", options: ["اللون", "تؤثر على المعادلة الأيونية", "الصيغة"], correct: 1, explanation: "مهمة للمعادلة الأيونية", lesson: "التفاعلات والمعادلات", difficulty: "medium" },
            { question: "المعادلة الموزونة لـ Ca + H₂O:", options: ["Ca + H₂O → Ca(OH)₂ + H₂", "Ca + 2H₂O → Ca(OH)₂ + H₂", "2Ca + 2H₂O → 2Ca(OH)₂ + H₂"], correct: 1, explanation: "موزونة بشكل صحيح", lesson: "التفاعلات والمعادلات", difficulty: "medium" },
            { question: "هل H₂ + Cl₂ → 2HCl موزونة؟", options: ["نعم", "لا", "لا، الناتج خطأ"], correct: 0, explanation: "عدد الذرات متساو", lesson: "التفاعلات والمعادلات", difficulty: "easy" },
            { question: "المعادلة الموزونة لتفاعل Na مع Cl₂:", options: ["Na + Cl → NaCl", "2Na + Cl₂ → 2NaCl", "2Na + 2Cl → 2NaCl"], correct: 1, explanation: "الكلور ثنائي الذرة", lesson: "التفاعلات والمعادلات", difficulty: "medium" }
        ];

        let currentQuestion = 0;
        let score = 0;
        let userAnswers = [];
        let weakLessons = {};
        let quizMode = "practice";
        let quizTime = 1800;
        let timerInterval;
        let currentQuestions = [];
        let soundEnabled = true;
        let studentName = "";
        let studentSection = "";
        let notifications = [];

        const correctSound = document.getElementById('correct-sound');
        const wrongSound = document.getElementById('wrong-sound');
        const completeSound = document.getElementById('complete-sound');
        const failSound = document.getElementById('fail-sound');

        const defaultLeaderboard = [
            { name: "أحمد محمد", score: 98, section: "الشعبة 1" },
            { name: "خالد إبراهيم", score: 95, section: "الشعبة 3" },
            { name: "يوسف حسن", score: 92, section: "الشعبة 2" },
            { name: "محمد عبدالرحمن", score: 90, section: "الشعبة 4" },
            { name: "عمر ناصر", score: 88, section: "الشعبة 5" },
            { name: "سعيد علي", score: 85, section: "الشعبة 6" },
            { name: "محمود خالد", score: 82, section: "الشعبة 7" },
            { name: "حسن سليمان", score: 80, section: "الشعبة 1" },
            { name: "فيصل عبدالله", score: 78, section: "الشعبة 3" },
            { name: "ناصر راشد", score: 75, section: "الشعبة 2" }
        ];

        function handleLogin(event) {
            event.preventDefault();
            studentName = document.getElementById('student-name').value;
            studentSection = document.getElementById('student-section').value;
            if (!studentName || !studentSection) {
                alert('يرجى إدخال اسمك واختيار الشعبة');
                return;
            }
            saveLoggedInUser(studentName, studentSection);
            document.getElementById('username-display').textContent = studentName;
            document.getElementById('section-display').textContent = `الشعبة: ${studentSection}`;
            document.getElementById('result-username').textContent = studentName;
            document.getElementById('profile-section').textContent = `الشعبة: ${studentSection}`;
            initializeSettings();
            addNotification('مرحباً بك!', `مرحباً ${studentName} في منصة الكيمياء التفاعلية. نتمنى لك تجربة تعليمية ممتعة!`, 'info');
            navigateTo('welcome', true);
        }

        function initializeSettings() {
            const savedSettings = localStorage.getItem('chemistryAppSettings');
            if (savedSettings) {
                const settings = JSON.parse(savedSettings);
                document.getElementById('username').value = settings.username || studentName;
                document.getElementById('user-email').value = settings.email || 'student@chemistry.com';
                document.getElementById('user-level-select').value = settings.userLevel || 'beginner';
                document.getElementById('sound-enabled').checked = settings.soundEnabled !== false;
                document.getElementById('dark-mode').checked = settings.darkMode || false;
                document.getElementById('notifications').checked = settings.notifications !== false;
                document.getElementById('default-difficulty').value = settings.defaultDifficulty || 'medium';
                document.getElementById('default-question-count').value = settings.defaultQuestionCount || 20;
                document.getElementById('interface-language').value = settings.interfaceLanguage || 'العربية';
                document.getElementById('terms-language').value = settings.termsLanguage || 'العربية';
                document.getElementById('auto-save').checked = settings.autoSave !== false;
                updateUserInterface();
            }
            const savedNotifications = localStorage.getItem('chemistryAppNotifications');
            if (savedNotifications) notifications = JSON.parse(savedNotifications);
            soundEnabled = document.getElementById('sound-enabled').checked;
        }

        function saveSettings() {
            const settings = {
                username: document.getElementById('username').value,
                email: document.getElementById('user-email').value,
                userLevel: document.getElementById('user-level-select').value,
                soundEnabled: document.getElementById('sound-enabled').checked,
                darkMode: document.getElementById('dark-mode').checked,
                notifications: document.getElementById('notifications').checked,
                defaultDifficulty: document.getElementById('default-difficulty').value,
                defaultQuestionCount: parseInt(document.getElementById('default-question-count').value),
                interfaceLanguage: document.getElementById('interface-language').value,
                termsLanguage: document.getElementById('terms-language').value,
                autoSave: document.getElementById('auto-save').checked
            };
            localStorage.setItem('chemistryAppSettings', JSON.stringify(settings));
            alert('تم حفظ الإعدادات بنجاح!');
            updateUserInterface();
        }

        function updateUserInterface() {
            const settings = JSON.parse(localStorage.getItem('chemistryAppSettings') || '{}');
            document.getElementById('username-display').textContent = settings.username || studentName;
            document.getElementById('result-username').textContent = settings.username || studentName;
            const userLevel = settings.userLevel || 'beginner';
            document.getElementById('user-level').textContent = 
                userLevel === 'beginner' ? 'المستوى: مبتدئ' : 
                userLevel === 'intermediate' ? 'المستوى: متوسط' : 'المستوى: متقدم';
            if (settings.darkMode) {
                document.documentElement.style.setProperty('--card-bg', 'rgba(30, 41, 59, 0.95)');
                document.documentElement.style.setProperty('--dark', '#f8fafc');
                document.documentElement.style.setProperty('--light', '#1e293b');
            } else {
                document.documentElement.style.setProperty('--card-bg', 'rgba(255, 255, 255, 0.95)');
                document.documentElement.style.setProperty('--dark', '#1e293b');
                document.documentElement.style.setProperty('--light', '#f8fafc');
            }
            soundEnabled = settings.soundEnabled !== false;
        }

        function updateUserLevel(averageScore) {
            let userLevel;
            if (averageScore < 50) userLevel = 'beginner';
            else if (averageScore < 80) userLevel = 'intermediate';
            else userLevel = 'advanced';
            document.getElementById('user-level').textContent = 
                userLevel === 'beginner' ? 'المستوى: مبتدئ' : 
                userLevel === 'intermediate' ? 'المستوى: متوسط' : 'المستوى: متقدم';
            const settings = JSON.parse(localStorage.getItem('chemistryAppSettings') || '{}');
            settings.userLevel = userLevel;
            localStorage.setItem('chemistryAppSettings', JSON.stringify(settings));
            document.getElementById('user-level-select').value = userLevel;
        }

        function startQuiz() {
            const questionCount = parseInt(document.getElementById('question-count').value);
            const difficulty = document.getElementById('difficulty').value;
            let filteredQuestions = allQuestions;
            if (difficulty !== "all") {
                filteredQuestions = allQuestions.filter(q => q.difficulty === difficulty);
            }
            currentQuestions = getRandomQuestions(filteredQuestions, questionCount);
            currentQuestion = 0;
            score = 0;
            userAnswers = [];
            weakLessons = {};
            if (quizMode === 'exam') {
                quizTime = 1800;
                startTimer();
            }
            navigateTo('quiz');
            showQuestion();
        }

        function getRandomQuestions(questions, count) {
            if (count >= questions.length) return shuffleArray([...questions]);
            const shuffled = shuffleArray([...questions]);
            return shuffled.slice(0, count);
        }

        function shuffleArray(array) {
            const newArray = [...array];
            for (let i = newArray.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [newArray[i], newArray[j]] = [newArray[j], newArray[i]];
            }
            return newArray;
        }

        function showQuestion() {
            const question = currentQuestions[currentQuestion];
            document.getElementById('question').textContent = question.question;
            document.getElementById('question-counter').textContent = `السؤال ${currentQuestion + 1} من ${currentQuestions.length}`;
            document.getElementById('progress').style.width = `${((currentQuestion + 1) / currentQuestions.length) * 100}%`;
            const optionsElement = document.getElementById('options');
            optionsElement.innerHTML = '';
            question.options.forEach((option, index) => {
                const optionElement = document.createElement('div');
                optionElement.classList.add('option');
                optionElement.innerHTML = `${option}<span class="option-number">${String.fromCharCode(65 + index)}</span>`;
                optionElement.addEventListener('click', () => selectOption(index));
                optionsElement.appendChild(optionElement);
            });
            document.getElementById('explanation').style.display = 'none';
            document.getElementById('next-btn').disabled = true;
            document.getElementById('next-btn').innerHTML = currentQuestion === currentQuestions.length - 1 
                ? '<i class="fas fa-flag-checkered"></i> إنهاء الاختبار' 
                : '<i class="fas fa-arrow-left"></i> التالي';
            document.getElementById('score-display').textContent = `النقاط: ${score}`;
        }

        function selectOption(selectedIndex) {
            const options = document.querySelectorAll('.option');
            const correctIndex = currentQuestions[currentQuestion].correct;
            const question = currentQuestions[currentQuestion];
            options.forEach(option => {
                option.classList.add('disabled');
                option.style.pointerEvents = 'none';
            });
            options[selectedIndex].classList.add('selected');
            const isCorrect = selectedIndex === correctIndex;
            if (isCorrect) {
                options[selectedIndex].classList.add('correct');
                score++;
                if (soundEnabled) {
                    correctSound.currentTime = 0;
                    correctSound.play().catch(e => console.log(e));
                }
            } else {
                options[selectedIndex].classList.add('wrong');
                options[correctIndex].classList.add('correct');
                if (soundEnabled) {
                    failSound.currentTime = 0;
                    failSound.play().catch(e => console.log(e));
                }
                weakLessons[question.lesson] = (weakLessons[question.lesson] || 0) + 1;
            }
            userAnswers.push({
                question: question.question,
                selected: selectedIndex,
                correct: correctIndex,
                isCorrect: isCorrect,
                explanation: question.explanation,
                lesson: question.lesson
            });
            if (quizMode === 'practice') showExplanation(isCorrect, selectedIndex);
            document.getElementById('next-btn').disabled = false;
            document.getElementById('score-display').textContent = `النقاط: ${score}`;
        }

        function showExplanation(isCorrect, selectedIndex) {
            const question = currentQuestions[currentQuestion];
            const correctAnswer = question.options[question.correct];
            const explanationElement = document.getElementById('explanation');
            explanationElement.innerHTML = `
                <h3><i class="fas ${isCorrect ? 'fa-check-circle' : 'fa-times-circle'}"></i> ${isCorrect ? 'إجابة صحيحة!' : 'إجابة خاطئة!'}</h3>
                <p><strong>التعليل:</strong> ${question.explanation}</p>
                ${!isCorrect ? `
                    <div style="background: #fff3e0; padding: 15px; border-radius: 10px; margin-top: 15px; border-right: 4px solid #ff9800;">
                        <strong>الإجابة الصحيحة:</strong> ${correctAnswer}
                    </div>
                ` : ''}
                <div style="background: #e3f2fd; padding: 15px; border-radius: 10px; margin-top: 15px; border-right: 4px solid #2196f3;">
                    <strong>الدرس:</strong> ${question.lesson}
                </div>
            `;
            explanationElement.style.display = 'block';
        }

        function nextQuestion() {
            if (currentQuestion < currentQuestions.length - 1) {
                currentQuestion++;
                showQuestion();
            } else {
                endQuiz();
            }
        }

        function startTimer() {
            updateTimerDisplay();
            timerInterval = setInterval(() => {
                quizTime--;
                updateTimerDisplay();
                if (quizTime <= 0) endQuiz();
            }, 1000);
        }

        function updateTimerDisplay() {
            const minutes = Math.floor(quizTime / 60);
            const seconds = quizTime % 60;
            document.getElementById('quiz-timer').textContent = 
                `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
        }

        function endQuiz() {
            if (timerInterval) clearInterval(timerInterval);
            if (soundEnabled) {
                completeSound.currentTime = 0;
                completeSound.play().catch(e => console.log(e));
            }
            navigateTo('results');
            showResults();
            saveQuizResults();
            const percentage = Math.round((score / currentQuestions.length) * 100);
            addNotification('تم إنهاء الاختبار!', `لقد أنهيت الاختبار بنتيجة ${percentage}%. اضغط لعرض التفاصيل.`, 'success');
        }

        function showResults() {
            const percentage = Math.round((score / currentQuestions.length) * 100);
            document.getElementById('final-score').textContent = `${percentage}%`;
            document.getElementById('result-score').textContent = `${score} من ${currentQuestions.length}`;
            document.getElementById('total-questions').textContent = currentQuestions.length;
            const userRank = getUserRank(percentage);
            document.getElementById('user-rank').textContent = userRank.text;
            document.getElementById('user-rank').className = `rank-badge ${userRank.class}`;
            const timeSpent = quizMode === 'exam' ? 
                `30:00 - ${document.getElementById('quiz-timer').textContent}` : '--:--';
            document.getElementById('time-taken').textContent = timeSpent;
            const canvas = document.getElementById('result-chart');
            const ctx = canvas.getContext('2d');
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.beginPath();
            ctx.arc(125, 125, 100, 0, 2 * Math.PI);
            ctx.strokeStyle = '#e0e0e0';
            ctx.lineWidth = 15;
            ctx.stroke();
            ctx.beginPath();
            ctx.arc(125, 125, 100, -0.5 * Math.PI, (2 * percentage / 100 - 0.5) * Math.PI);
            ctx.strokeStyle = percentage >= 70 ? '#10b981' : percentage >= 50 ? '#f59e0b' : '#ef4444';
            ctx.lineWidth = 15;
            ctx.stroke();
            ctx.font = 'bold 30px Arial';
            ctx.fillStyle = percentage >= 70 ? '#10b981' : percentage >= 50 ? '#f59e0b' : '#ef4444';
            ctx.textAlign = 'center';
            ctx.textBaseline = 'middle';
            ctx.fillText(`${percentage}%`, 125, 125);
            const randomPercentage = Math.floor(Math.random() * 30) + 60;
            document.getElementById('comparison').innerHTML = `
                <h3><i class="fas fa-chart-line"></i> مقارنة مع الآخرين</h3>
                <p>${randomPercentage}% من الطلاب حصلوا على نفس نتيجتك تقريبًا</p>
            `;
            const weakLessonsElement = document.getElementById('weak-lessons');
            if (Object.keys(weakLessons).length > 0) {
                let weakLessonsHTML = '<h3><i class="fas fa-book"></i> الدروس التي تحتاج إلى مراجعة:</h3>';
                for (const lesson in weakLessons) {
                    weakLessonsHTML += `
                        <div class="lesson-item">
                            <strong>${lesson}</strong>
                            <p>ذاكر هذا الدرس لتحسين أدائك في المستقبل</p>
                        </div>
                    `;
                }
                weakLessonsElement.innerHTML = weakLessonsHTML;
            } else {
                weakLessonsElement.innerHTML = '<h3><i class="fas fa-star"></i> ممتاز! لا توجد دروس تحتاج إلى مراجعة</h3>';
            }
            createPerformanceChart();
            showImprovementTips(percentage);
            if (quizMode === 'exam') showExamResults();
        }

        function getUserRank(percentage) {
            if (percentage < 35) return { text: 'غاز خامل', class: 'rank-inert' };
            else if (percentage >= 36 && percentage <= 50) return { text: 'متفاعل نشيط', class: 'rank-active' };
            else if (percentage >= 51 && percentage <= 89) return { text: 'كيميائي جيد', class: 'rank-good' };
            else return { text: 'العالم العبقري', class: 'rank-genius' };
        }

        function createPerformanceChart() {
            const canvas = document.getElementById('performance-chart');
            const ctx = canvas.getContext('2d');
            const labels = ['الاختبار 1', 'الاختبار 2', 'الاختبار 3', 'الاختبار 4', 'الاختبار 5'];
            const data = [
                Math.floor(Math.random() * 30) + 50,
                Math.floor(Math.random() * 30) + 50,
                Math.floor(Math.random() * 30) + 50,
                Math.floor(Math.random() * 30) + 50,
                Math.floor(Math.random() * 30) + 50
            ];
            const percentage = Math.round((score / currentQuestions.length) * 100);
            labels.push('هذا الاختبار');
            data.push(percentage);
            if (window.performanceChartInstance) {
                window.performanceChartInstance.destroy();
            }
            window.performanceChartInstance = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'نتائج الاختبارات',
                        data: data,
                        borderColor: '#4a6baf',
                        backgroundColor: 'rgba(74, 107, 175, 0.1)',
                        borderWidth: 2,
                        fill: true,
                        tension: 0.4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            max: 100,
                            ticks: { callback: function(value) { return value + '%'; } }
                        }
                    },
                    plugins: {
                        legend: { display: true, position: 'top', rtl: true }
                    }
                }
            });
        }

        function showImprovementTips(percentage) {
            const tipsElement = document.getElementById('improvement-tips');
            let tipsHTML = '';
            if (percentage < 50) {
                tipsHTML = `
                    <li>ركز على فهم الأساسيات قبل الانتقال إلى المواضيع المتقدمة</li>
                    <li>استخدم وضع الممارسة للتعلم من أخطائك</li>
                    <li>اذهب إلى قسم المحاكاة لفهم المفاهيم بشكل عملي</li>
                    <li>خصص وقتاً منتظماً للمراجعة</li>
                `;
            } else if (percentage >= 50 && percentage < 80) {
                tipsHTML = `
                    <li>ركز على تحسين نقاط ضعفك المحددة</li>
                    <li>جرب وضع الامتحان لتحسين إدارة الوقت</li>
                    <li>استخدم السبورة التفاعلية لحل المسائل المعقدة</li>
                    <li>شارك في المنافسة مع زملائك لتحفيز نفسك</li>
                `;
            } else {
                tipsHTML = `
                    <li>تهانينا! أنت على المسار الصحيح</li>
                    <li>جرب اختبارات المستوى المتقدم</li>
                    <li>ساعد زملائك في فهم المواضيع الصعبة</li>
                    <li>استمر في التعلم والاستكشاف للمواضيع المتقدمة</li>
                `;
            }
            tipsElement.innerHTML = tipsHTML;
        }

        function showExamResults() {
            const weakLessonsElement = document.getElementById('weak-lessons');
            let examResultsHTML = '<h3><i class="fas fa-clipboard-list"></i> تفاصيل الإجابات:</h3>';
            userAnswers.forEach((answer, index) => {
                if (!answer.isCorrect) {
                    examResultsHTML += `
                        <div class="lesson-item">
                            <strong>السؤال ${index + 1}:</strong> ${answer.question}
                            <p><strong>إجابتك:</strong> ${currentQuestions[index].options[answer.selected]}</p>
                            <p><strong>الإجابة الصحيحة:</strong> ${currentQuestions[index].options[answer.correct]}</p>
                            <p><strong>التعليل:</strong> ${answer.explanation}</p>
                        </div>
                    `;
                }
            });
            weakLessonsElement.innerHTML += examResultsHTML;
        }

        function saveQuizResults() {
            const percentage = Math.round((score / currentQuestions.length) * 100);
            const quizResults = JSON.parse(localStorage.getItem('quizResults') || '[]');
            const newResult = {
                date: new Date().toLocaleDateString('ar-SA'),
                time: new Date().toLocaleTimeString('ar-SA'),
                score: percentage,
                totalQuestions: currentQuestions.length,
                correctAnswers: score,
                mode: quizMode,
                weakLessons: weakLessons,
                studentName: studentName,
                studentSection: studentSection,
                timeSpent: quizMode === 'exam' ? 
                    `30:00 - ${document.getElementById('quiz-timer').textContent}` : '--:--'
            };
            quizResults.unshift(newResult);
            localStorage.setItem('quizResults', JSON.stringify(quizResults));
            updateUserLevelFromResults();
        }

        function updateUserLevelFromResults() {
            const quizResults = JSON.parse(localStorage.getItem('quizResults') || '[]');
            if (quizResults.length > 0) {
                const totalScore = quizResults.reduce((sum, result) => sum + result.score, 0);
                const averageScore = Math.round(totalScore / quizResults.length);
                updateUserLevel(averageScore);
            }
        }

        function updateProgressScreen() {
            const quizResults = JSON.parse(localStorage.getItem('quizResults') || '[]');
            if (quizResults.length > 0) {
                const totalScore = quizResults.reduce((sum, result) => sum + result.score, 0);
                const averageScore = Math.round(totalScore / quizResults.length);
                const bestScore = Math.max(...quizResults.map(result => result.score));
                const totalTime = quizResults.length * 30;
                document.getElementById('average-score').textContent = `${averageScore}%`;
                document.getElementById('best-score').textContent = `${bestScore}%`;
                document.getElementById('total-quizzes').textContent = quizResults.length;
                document.getElementById('total-time').textContent = `${totalTime} د`;
                updateUserLevel(averageScore);
            } else {
                document.getElementById('average-score').textContent = '0%';
                document.getElementById('best-score').textContent = '0%';
                document.getElementById('total-quizzes').textContent = '0';
                document.getElementById('total-time').textContent = '0 د';
            }
            const historyTable = document.getElementById('quiz-history');
            historyTable.innerHTML = '';
            quizResults.forEach((result) => {
                const scoreClass = result.score >= 70 ? 'score-high' : 
                                 result.score >= 50 ? 'score-medium' : 'score-low';
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${result.date} - ${result.time}</td>
                    <td>${result.mode === 'practice' ? 'تدريب' : 'امتحان'}</td>
                    <td><span class="score-badge ${scoreClass}">${result.score}%</span></td>
                    <td>${result.timeSpent}</td>
                    <td>${result.totalQuestions}</td>
                `;
                historyTable.appendChild(row);
            });
        }

        function updateLeaderboard() {
            const leaderboardList = document.getElementById('leaderboard-list');
            leaderboardList.innerHTML = '';
            const quizResults = JSON.parse(localStorage.getItem('quizResults') || '[]');
            let userBestScore = 0;
            if (quizResults.length > 0) {
                userBestScore = Math.max(...quizResults.map(result => result.score));
            }
            const allScores = [...defaultLeaderboard.map(user => user.score)];
            if (userBestScore > 0) allScores.push(userBestScore);
            allScores.sort((a, b) => b - a);
            const leaderboardData = [];
            defaultLeaderboard.forEach(user => {
                leaderboardData.push({
                    name: user.name,
                    score: user.score,
                    section: user.section,
                    isCurrentUser: false
                });
            });
            if (userBestScore > 0 && allScores.indexOf(userBestScore) < 10) {
                leaderboardData.push({
                    name: studentName,
                    score: userBestScore,
                    section: studentSection,
                    isCurrentUser: true
                });
            }
            leaderboardData.sort((a, b) => b.score - a.score);
            const top10 = leaderboardData.slice(0, 10);
            top10.forEach((user, index) => {
                const item = document.createElement('div');
                item.className = `leaderboard-item ${user.isCurrentUser ? 'current-user' : ''}`;
                item.innerHTML = `
                    <div class="leaderboard-rank">${index + 1}</div>
                    <div class="leaderboard-user">
                        <h4>${user.name}</h4>
                        <p>${user.section}</p>
                    </div>
                    <div class="leaderboard-score">${user.score}%</div>
                `;
                leaderboardList.appendChild(item);
            });
            if (userBestScore > 0 && !top10.some(user => user.isCurrentUser)) {
                const userRank = allScores.indexOf(userBestScore) + 1;
                const item = document.createElement('div');
                item.className = 'leaderboard-item current-user';
                item.innerHTML = `
                    <div class="leaderboard-rank">${userRank}</div>
                    <div class="leaderboard-user">
                        <h4>${studentName} (أنت)</h4>
                        <p>${studentSection}</p>
                    </div>
                    <div class="leaderboard-score">${userBestScore}%</div>
                `;
                leaderboardList.appendChild(item);
            }
        }

        function addNotification(title, message, type = 'info') {
            const notification = {
                id: Date.now(),
                title,
                message,
                type,
                time: new Date().toLocaleTimeString('ar-SA'),
                date: new Date().toLocaleDateString('ar-SA'),
                read: false
            };
            notifications.unshift(notification);
            localStorage.setItem('chemistryAppNotifications', JSON.stringify(notifications));
            if (document.getElementById('notifications').classList.contains('active')) {
                updateNotifications();
            }
        }

        function updateNotifications() {
            const notificationsList = document.getElementById('notifications-list');
            notificationsList.innerHTML = '';
            if (notifications.length === 0) {
                notificationsList.innerHTML = '<p style="text-align: center; padding: 20px;">لا توجد إشعارات</p>';
                return;
            }
            notifications.forEach(notification => {
                const notificationItem = document.createElement('div');
                notificationItem.className = `notification-item ${notification.read ? '' : 'unread'}`;
                notificationItem.innerHTML = `
                    <div class="notification-icon">
                        <i class="fas fa-${getNotificationIcon(notification.type)}"></i>
                    </div>
                    <div class="notification-content">
                        <div class="notification-title">${notification.title}</div>
                        <div class="notification-message">${notification.message}</div>
                        <div class="notification-time">${notification.date} - ${notification.time}</div>
                    </div>
                `;
                notificationItem.addEventListener('click', () => {
                    notification.read = true;
                    localStorage.setItem('chemistryAppNotifications', JSON.stringify(notifications));
                    updateNotifications();
                });
                notificationsList.appendChild(notificationItem);
            });
        }

        function getNotificationIcon(type) {
            switch (type) {
                case 'success': return 'check-circle';
                case 'warning': return 'exclamation-triangle';
                case 'error': return 'times-circle';
                default: return 'info-circle';
            }
        }

        function updateProfile() {
            const quizResults = JSON.parse(localStorage.getItem('quizResults') || '[]');
            const settings = JSON.parse(localStorage.getItem('chemistryAppSettings') || '{}');
            if (quizResults.length > 0) {
                const totalScore = quizResults.reduce((sum, result) => sum + result.score, 0);
                const averageScore = Math.round(totalScore / quizResults.length);
                const bestScore = Math.max(...quizResults.map(result => result.score));
                const totalTime = quizResults.length * 30;
                document.getElementById('profile-total-quizzes').textContent = quizResults.length;
                document.getElementById('profile-average-score').textContent = `${averageScore}%`;
                document.getElementById('profile-best-score').textContent = `${bestScore}%`;
                document.getElementById('profile-total-time').textContent = `${totalTime} د`;
                const userRank = getUserRank(averageScore);
                document.getElementById('profile-rank').textContent = userRank.text;
                document.getElementById('profile-rank').className = `rank-badge ${userRank.class}`;
            } else {
                document.getElementById('profile-total-quizzes').textContent = '0';
                document.getElementById('profile-average-score').textContent = '0%';
                document.getElementById('profile-best-score').textContent = '0%';
                document.getElementById('profile-total-time').textContent = '0 د';
            }
            document.getElementById('profile-username').value = settings.username || studentName;
            document.getElementById('profile-section').textContent = `الشعبة: ${studentSection}`;
            document.getElementById('profile-level').textContent = `المستوى: ${settings.userLevel === 'beginner' ? 'مبتدئ' : settings.userLevel === 'intermediate' ? 'متوسط' : 'متقدم'}`;
            document.getElementById('profile-bio').value = settings.bio || '';
        }

        function saveProfile() {
            const settings = JSON.parse(localStorage.getItem('chemistryAppSettings') || '{}');
            settings.username = document.getElementById('profile-username').value;
            settings.bio = document.getElementById('profile-bio').value;
            localStorage.setItem('chemistryAppSettings', JSON.stringify(settings));
            const user = getLoggedInUser();
            if (user) {
                user.name = settings.username;
                localStorage.setItem('chemistryCurrentUser', JSON.stringify(user));
            }
            updateUserInterface();
            alert('تم حفظ الملف الشخصي بنجاح!');
        }

        function exportData() {
            const data = {
                settings: JSON.parse(localStorage.getItem('chemistryAppSettings') || '{}'),
                quizResults: JSON.parse(localStorage.getItem('quizResults') || '[]'),
                notifications: notifications
            };
            const dataStr = JSON.stringify(data, null, 2);
            const dataBlob = new Blob([dataStr], {type: 'application/json'});
            const link = document.createElement('a');
            link.href = URL.createObjectURL(dataBlob);
            link.download = 'chemistry_app_data.json';
            link.click();
        }

        function clearData() {
            if (confirm('هل أنت متأكد من رغبتك في مسح جميع البيانات؟ لا يمكن التراجع عن هذا الإجراء.')) {
                localStorage.removeItem('chemistryAppSettings');
                localStorage.removeItem('quizResults');
                localStorage.removeItem('chemistryAppNotifications');
                notifications = [];
                alert('تم مسح البيانات بنجاح!');
                initializeSettings();
                updateProgressScreen();
                updateNotifications();
            }
        }

        function clearNotifications() {
            if (confirm('هل أنت متأكد من رغبتك في مسح جميع الإشعارات؟')) {
                notifications = [];
                localStorage.setItem('chemistryAppNotifications', JSON.stringify(notifications));
                updateNotifications();
            }
        }

        document.addEventListener('DOMContentLoaded', function() {
            document.querySelectorAll('.nav-link').forEach(link => {
                link.addEventListener('click', function(e) {
                    e.preventDefault();
                    const screenId = this.getAttribute('data-screen');
                    navigateTo(screenId);
                });
            });
            document.getElementById('start-quiz').addEventListener('click', startQuiz);
            document.getElementById('next-btn').addEventListener('click', nextQuestion);
            document.getElementById('end-quiz').addEventListener('click', function() {
                if (confirm('هل أنت متأكد من إنهاء الاختبار؟')) endQuiz();
            });
            document.getElementById('save-settings').addEventListener('click', saveSettings);
            document.getElementById('save-profile').addEventListener('click', saveProfile);
            document.getElementById('export-data').addEventListener('click', exportData);
            document.getElementById('clear-data').addEventListener('click', clearData);
            document.getElementById('clear-notifications').addEventListener('click', clearNotifications);
            document.getElementById('sound-enabled').addEventListener('change', function() {
                soundEnabled = this.checked;
            });
            document.getElementById('login-form').addEventListener('submit', handleLogin);
            document.getElementById('logout-btn').addEventListener('click', logoutUser);
            document.getElementById('clear-whiteboard').addEventListener('click', function() {
                alert('استخدم أدوات Canva الموجودة في السبورة للمسح أو الرسم');
            });
            document.querySelectorAll('.quiz-option').forEach(option => {
                option.addEventListener('click', function() {
                    document.querySelectorAll('.quiz-option').forEach(opt => opt.classList.remove('selected'));
                    this.classList.add('selected');
                    quizMode = this.getAttribute('data-mode');
                });
            });
            document.querySelector('.quiz-option').classList.add('selected');
            quizMode = document.querySelector('.quiz-option').getAttribute('data-mode');
            window.addEventListener('hashchange', handleRoute);
            handleRoute();
        });
    </script>
</body>
</html>

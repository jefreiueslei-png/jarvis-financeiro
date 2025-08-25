<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jarvis Financeiro - Sistema Completo</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root {
            --primary: #2c3e50;
            --secondary: #3498db;
            --accent: #e74c3c;
            --light: #ecf0f1;
            --dark: #2c3e50;
            --success: #2ecc71;
            --warning: #f39c12;
            --info: #17a2b8;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a2a6c, #2a5298, #3498db);
            color: #333;
            line-height: 1.6;
            min-height: 100vh;
            padding: 0;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 10px;
            padding: 20px 30px;
            margin-bottom: 25px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .logo h1 {
            color: var(--primary);
            font-size: 2.2rem;
        }
        
        .logo-icon {
            font-size: 2.5rem;
            color: var(--secondary);
        }
        
        nav {
            display: flex;
            gap: 20px;
        }
        
        nav a {
            color: var(--dark);
            text-decoration: none;
            font-weight: 600;
            padding: 8px 15px;
            border-radius: 5px;
            transition: all 0.3s;
        }
        
        nav a:hover, nav a.active {
            background: var(--secondary);
            color: white;
        }
        
        .user-actions {
            display: flex;
            gap: 15px;
            align-items: center;
        }
        
        .btn {
            display: inline-block;
            background: var(--secondary);
            color: white;
            padding: 10px 20px;
            border-radius: 5px;
            text-decoration: none;
            font-weight: 600;
            transition: background 0.3s;
            border: none;
            cursor: pointer;
        }
        
        .btn:hover {
            background: #2980b9;
        }
        
        .btn-outline {
            background: transparent;
            border: 2px solid var(--secondary);
            color: var(--secondary);
        }
        
        .btn-outline:hover {
            background: var(--secondary);
            color: white;
        }
        
        .dashboard {
            display: grid;
            grid-template-columns: 1fr 3fr;
            gap: 25px;
        }
        
        .sidebar {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
        }
        
        .sidebar h2 {
            color: var(--primary);
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 2px solid var(--secondary);
        }
        
        .menu-item {
            display: flex;
            align-items: center;
            gap: 15px;
            padding: 15px;
            margin-bottom: 10px;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .menu-item:hover, .menu-item.active {
            background: var(--secondary);
            color: white;
        }
        
        .menu-item i {
            font-size: 1.2rem;
        }
        
        .main-content {
            display: flex;
            flex-direction: column;
            gap: 25px;
        }
        
        .card {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
        }
        
        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .card-header h2 {
            color: var(--primary);
        }
        
        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 25px;
        }
        
        .stat-card {
            background: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.08);
            display: flex;
            flex-direction: column;
        }
        
        .stat-card .value {
            font-size: 2.2rem;
            font-weight: 700;
            color: var(--primary);
            margin: 10px 0;
        }
        
        .stat-card .label {
            color: #7f8c8d;
            font-size: 0.9rem;
        }
        
        .stat-card .icon {
            align-self: flex-end;
            font-size: 2.5rem;
            color: var(--secondary);
            opacity: 0.7;
        }
        
        .chart-container {
            height: 300px;
            margin-top: 20px;
        }
        
        .transactions {
            margin-top: 20px;
        }
        
        .transaction-item {
            display: grid;
            grid-template-columns: 2fr 1fr 1fr 1fr;
            padding: 15px;
            border-bottom: 1px solid #eee;
        }
        
        .transaction-item:last-child {
            border-bottom: none;
        }
        
        .transaction-item .amount.income {
            color: var(--success);
            font-weight: 600;
        }
        
        .transaction-item .amount.expense {
            color: var(--accent);
            font-weight: 600;
        }
        
        .filters {
            display: flex;
            gap: 15px;
            margin-bottom: 20px;
        }
        
        .filter-item {
            background: white;
            padding: 8px 15px;
            border-radius: 20px;
            font-size: 0.9rem;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .filter-item.active {
            background: var(--secondary);
            color: white;
        }
        
        @media (max-width: 992px) {
            .dashboard {
                grid-template-columns: 1fr;
            }
            
            header {
                flex-direction: column;
                gap: 20px;
            }
            
            nav {
                flex-wrap: wrap;
                justify-content: center;
            }
            
            .stats {
                grid-template-columns: 1fr 1fr;
            }
        }
        
        @media (max-width: 576px) {
            .stats {
                grid-template-columns: 1fr;
            }
            
            .user-actions {
                flex-direction: column;
                width: 100%;
            }
            
            .btn {
                width: 100%;
                text-align: center;
            }
            
            .transaction-item {
                grid-template-columns: 1fr 1fr;
                gap: 10px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="logo">
                <i class="fas fa-robot logo-icon"></i>
                <h1>Jarvis Financeiro</h1>
            </div>
            
            <nav>
                <a href="#" class="active"><i class="fas fa-home"></i> Dashboard</a>
                <a href="#"><i class="fas fa-wallet"></i> Transações</a>
                <a href="#"><i class="fas fa-chart-pie"></i> Relatórios</a>
                <a href="#"><i class="fas fa-cog"></i> Configurações</a>
            </nav>
            
            <div class="user-actions">
                <button class="btn btn-outline"><i class="fas fa-bell"></i></button>
                <button class="btn"><i class="fas fa-plus"></i> Nova Transação</button>
            </div>
        </header>
        
        <div class="dashboard">
            <div class="sidebar">
                <h2>Menu</h2>
                
                <div class="menu-item active">
                    <i class="fas fa-home"></i>
                    <span>Visão Geral</span>
                </div>
                
                <div class="menu-item">
                    <i class="fas fa-money-bill-wave"></i>
                    <span>Despesas</span>
                </div>
                
                <div class="menu-item">
                    <i class="fas fa-dollar-sign"></i>
                    <span>Receitas</span>
                </div>
                
                <div class="menu-item">
                    <i class="fas fa-chart-line"></i>
                    <span>Investimentos</span>
                </div>
                
                <div class="menu-item">
                    <i class="fas fa-piggy-bank"></i>
                    <span>Economias</span>
                </div>
                
                <div class="menu-item">
                    <i class="fas fa-calendar"></i>
                    <span>Planejamento</span>
                </div>
                
                <div class="menu-item">
                    <i class="fas fa-file-invoice-dollar"></i>
                    <span>Orçamento</span>
                </div>
                
                <div class="menu-item">
                    <i class="fas fa-hand-holding-usd"></i>
                    <span>Empréstimos</span>
                </div>
                
                <div class="menu-item">
                    <i class="fas fa-taxi"></i>
                    <span>Impostos</span>
                </div>
            </div>
            
            <div class="main-content">
                <div class="card">
                    <div class="card-header">
                        <h2>Visão Geral Financeira</h2>
                        <div class="filters">
                            <div class="filter-item active">Hoje</div>
                            <div class="filter-item">Esta Semana</div>
                            <div class="filter-item">Este Mês</div>
                            <div class="filter-item">Personalizado</div>
                        </div>
                    </div>
                    
                    <div class="stats">
                        <div class="stat-card">
                            <span class="label">Saldo Disponível</span>
                            <span class="value">R$ 8.245,00</span>
                            <i class="fas fa-wallet icon"></i>
                        </div>
                        
                        <div class="stat-card">
                            <span class="label">Receitas</span>
                            <span class="value">R$ 12.540,00</span>
                            <i class="fas fa-arrow-up icon"></i>
                        </div>
                        
                        <div class="stat-card">
                            <span class="label">Despesas</span>
                            <span class="value">R$ 4.295,00</span>
                            <i class="fas fa-arrow-down icon"></i>
                        </div>
                        
                        <div class="stat-card">
                            <span class="label">Investimentos</span>
                            <span class="value">R$ 35.800,00</span>
                            <i class="fas fa-chart-line icon"></i>
                        </div>
                    </div>
                    
                    <div class="chart-container">
                        <canvas id="financialChart"></canvas>
                    </div>
                </div>
                
                <div class="card">
                    <div class="card-header">
                        <h2>Últimas Transações</h2>
                        <button class="btn btn-outline">Ver Todas</button>
                    </div>
                    
                    <div class="transactions">
                        <div class="transaction-item">
                            <div class="description">Salário</div>
                            <div class="category">Receita</div>
                            <div class="date">15/06/2023</div>
                            <div class="amount income">R$ 6.500,00</div>
                        </div>
                        
                        <div class="transaction-item">
                            <div class="description">Aluguel</div>
                            <div class="category">Moradia</div>
                            <div class="date">10/06/2023</div>
                            <div class="amount expense">- R$ 1.800,00</div>
                        </div>
                        
                        <div class="transaction-item">
                            <div class="description">Supermercado</div>
                            <div class="category">Alimentação</div>
                            <div class="date">08/06/2023</div>
                            <div class="amount expense">- R$ 450,00</div>
                        </div>
                        
                        <div class="transaction-item">
                            <div class="description">Internet</div>
                            <div class="category">Serviços</div>
                            <div class="date">05/06/2023</div>
                            <div class="amount expense">- R$ 120,00</div>
                        </div>
                        
                        <div class="transaction-item">
                            <div class="description">Freelance</div>
                            <div class="category">Receita</div>
                            <div class="date">02/06/2023</div>
                            <div class="amount income">R$ 2.300,00</div>
                        </div>
                    </div>
                </div>
                
                <div class="card">
                    <div class="card-header">
                        <h2>Metas Financeiras</h2>
                        <button class="btn">Nova Meta</button>
                    </div>
                    
                    <div class="stats">
                        <div class="stat-card">
                            <span class="label">Reserva de Emergência</span>
                            <div class="progress" style="height: 10px; background: #eee; border-radius: 5px; margin: 10px 0;">
                                <div class="progress-bar" style="height: 100%; width: 75%; background: var(--success); border-radius: 5px;"></div>
                            </div>
                            <span class="value">75% concluído</span>
                        </div>
                        
                        <div class="stat-card">
                            <span class="label">Viagem Internacional</span>
                            <div class="progress" style="height: 10px; background: #eee; border-radius: 5px; margin: 10px 0;">
                                <div class="progress-bar" style="height: 100%; width: 40%; background: var(--info); border-radius: 5px;"></div>
                            </div>
                            <span class="value">40% concluído</span>
                        </div>
                        
                        <div class="stat-card">
                            <span class="label">Trocar de Carro</span>
                            <div class="progress" style="height: 10px; background: #eee; border-radius: 5px; margin: 10px 0;">
                                <div class="progress-bar" style="height: 100%; width: 25%; background: var(--warning); border-radius: 5px;"></div>
                            </div>
                            <span class="value">25% concluído</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const ctx = document.getElementById('financialChart').getContext('2d');
            
            // Dados do gráfico
            const financialChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ['Jan', 'Fev', 'Mar', 'Abr', 'Mai', 'Jun', 'Jul', 'Ago', 'Set', 'Out', 'Nov', 'Dez'],
                    datasets: [{
                        label: 'Receitas',
                        data: [10500, 12000, 11500, 12500, 13000, 12500, 13500, 14000, 13800, 14200, 14500, 15000],
                        borderColor: '#2ecc71',
                        backgroundColor: 'rgba(46, 204, 113, 0.1)',
                        fill: true,
                        tension: 0.4
                    }, {
                        label: 'Despesas',
                        data: [8500, 9000, 9200, 8800, 9500, 9200, 10000, 10500, 10200, 9800, 10100, 10500],
                        borderColor: '#e74c3c',
                        backgroundColor: 'rgba(231, 76, 60, 0.1)',
                        fill: true,
                        tension: 0.4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        title: {
                            display: true,
                            text: 'Desempenho Financeiro Anual',
                            font: {
                                size: 16
                            }
                        },
                        tooltip: {
                            mode: 'index',
                            intersect: false,
                            callbacks: {
                                label: function(context) {
                                    return context.dataset.label + ': R$ ' + context.parsed.y.toLocaleString('pt-BR');
                                }
                            }
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: false,
                            ticks: {
                                callback: function(value) {
                                    return 'R$ ' + value.toLocaleString('pt-BR');
                                }
                            }
                        }
                    }
                }
            });
            
            // Simular notificação
            setTimeout(() => {
                alert('Sistema Jarvis: Sua análise financeira do mês está disponível!');
            }, 2000);
        });
    </script>
</body>
</html>

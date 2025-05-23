<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Gerenciamento de Gado</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        /* Estilos gerais */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            background-color: #f3f4f6;
            color: #1f2937;
        }
        .min-h-screen {
            min-height: 100vh;
        }
        
        /* Sidebar */
        .sidebar {
            width: 16rem;
            background-color: #166534;
            color: white;
            position: fixed;
            height: 100vh;
            overflow-y: auto;
            transition: all 0.3s ease;
        }
        .sidebar-header {
            padding: 1rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
            border-bottom: 1px solid #15803d;
        }
        .sidebar-brand {
            display: flex;
            align-items: center;
            gap: 0.75rem;
            font-size: 1.25rem;
            font-weight: bold;
        }
        .sidebar-nav {
            padding: 1rem;
        }
        .sidebar-section {
            margin-bottom: 2rem;
        }
        .sidebar-section-title {
            color: #86efac;
            text-transform: uppercase;
            font-size: 0.75rem;
            font-weight: 600;
            margin-bottom: 0.75rem;
        }
        .sidebar-menu {
            list-style: none;
        }
        .sidebar-menu-item {
            margin-bottom: 0.5rem;
        }
        .sidebar-menu-link {
            display: flex;
            align-items: center;
            padding: 0.5rem;
            border-radius: 0.375rem;
            color: white;
            text-decoration: none;
        }
        .sidebar-menu-link:hover {
            background-color: #15803d;
        }
        .sidebar-menu-link.active {
            background-color: #15803d;
        }
        .sidebar-menu-icon {
            margin-right: 0.75rem;
        }
        
        /* Main Content */
        .main-content {
            margin-left: 16rem;
            min-height: 100vh;
        }
        
        /* Header */
        .header {
            background-color: white;
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
        }
        .header-container {
            max-width: 80rem;
            margin: 0 auto;
            padding: 1rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .page-title {
            font-size: 1.5rem;
            font-weight: bold;
            color: #1f2937;
        }
        .header-actions {
            display: flex;
            align-items: center;
            gap: 1rem;
        }
        .notification-btn {
            position: relative;
            padding: 0.5rem;
            border-radius: 9999px;
            background: transparent;
            border: none;
            cursor: pointer;
        }
        .notification-btn:hover {
            background-color: #f3f4f6;
        }
        .notification-indicator {
            position: absolute;
            top: 0;
            right: 0;
            height: 0.5rem;
            width: 0.5rem;
            border-radius: 9999px;
            background-color: #ef4444;
        }
        .user-profile {
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }
        .user-avatar {
            height: 2rem;
            width: 2rem;
            border-radius: 9999px;
            object-fit: cover;
        }
        .user-name {
            font-size: 0.875rem;
            font-weight: 500;
        }
        
        /* Content */
        .content {
            max-width: 80rem;
            margin: 0 auto;
            padding: 1.5rem;
        }
        
        /* Cards */
        .card {
            background-color: white;
            border-radius: 0.5rem;
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }
        .card-hover {
            transition: all 0.3s ease;
        }
        .card-hover:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
        }
        
        /* Stats */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(1, 1fr);
            gap: 1rem;
            margin-bottom: 2rem;
        }
        @media (min-width: 768px) {
            .stats-grid {
                grid-template-columns: repeat(4, 1fr);
            }
        }
        .stat-card {
            background-color: white;
            border-radius: 0.5rem;
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
            padding: 1rem;
        }
        .stat-card-content {
            display: flex;
            align-items: center;
        }
        .stat-card-icon {
            padding: 0.75rem;
            border-radius: 9999px;
            margin-right: 1rem;
        }
        .stat-card-icon.green {
            background-color: #dcfce7;
            color: #16a34a;
        }
        .stat-card-icon.blue {
            background-color: #dbeafe;
            color: #2563eb;
        }
        .stat-card-icon.yellow {
            background-color: #fef9c3;
            color: #ca8a04;
        }
        .stat-card-icon.red {
            background-color: #fee2e2;
            color: #dc2626;
        }
        .stat-card-label {
            font-size: 0.875rem;
            color: #6b7280;
        }
        .stat-card-value {
            font-size: 1.5rem;
            font-weight: bold;
        }
        
        /* Modules Grid */
        .modules-title {
            font-size: 1.25rem;
            font-weight: 600;
            color: #1f2937;
            margin-bottom: 1.5rem;
        }
        .modules-grid {
            display: grid;
            grid-template-columns: repeat(1, 1fr);
            gap: 1.5rem;
        }
        @media (min-width: 640px) {
            .modules-grid {
                grid-template-columns: repeat(2, 1fr);
            }
        }
        @media (min-width: 1024px) {
            .modules-grid {
                grid-template-columns: repeat(3, 1fr);
            }
        }
        .module-card {
            background-color: white;
            border-radius: 0.75rem;
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
            overflow: hidden;
            padding: 1.5rem;
        }
        .module-card-header {
            display: flex;
            align-items: center;
            margin-bottom: 1rem;
        }
        .module-card-icon {
            padding: 0.75rem;
            border-radius: 9999px;
            margin-right: 1rem;
        }
        .module-card-icon.green {
            background-color: #dcfce7;
            color: #16a34a;
        }
        .module-card-icon.blue {
            background-color: #dbeafe;
            color: #2563eb;
        }
        .module-card-icon.yellow {
            background-color: #fef9c3;
            color: #ca8a04;
        }
        .module-card-icon.purple {
            background-color: #f3e8ff;
            color: #9333ea;
        }
        .module-card-icon.red {
            background-color: #fee2e2;
            color: #dc2626;
        }
        .module-card-icon.gray {
            background-color: #f3f4f6;
            color: #4b5563;
        }
        .module-card-title {
            font-size: 1.125rem;
            font-weight: 600;
            color: #1f2937;
        }
        .module-card-description {
            color: #6b7280;
            margin-bottom: 1rem;
        }
        .module-card-actions {
            display: flex;
            flex-wrap: wrap;
            gap: 0.5rem;
        }
        
        /* Buttons */
        .btn {
            display: inline-flex;
            align-items: center;
            padding: 0.5rem 1rem;
            border-radius: 0.375rem;
            font-weight: 500;
            cursor: pointer;
            text-decoration: none;
            border: none;
        }
        .btn-icon {
            margin-right: 0.5rem;
        }
        .btn-primary {
            background-color: #16a34a;
            color: white;
        }
        .btn-primary:hover {
            background-color: #15803d;
        }
        .btn-secondary {
            background-color: #e5e7eb;
            color: #4b5563;
        }
        .btn-secondary:hover {
            background-color: #d1d5db;
        }
        .btn-green {
            background-color: #16a34a;
            color: white;
        }
        .btn-green:hover {
            background-color: #15803d;
        }
        .btn-green-light {
            background-color: #dcfce7;
            color: #16a34a;
        }
        .btn-green-light:hover {
            background-color: #bbf7d0;
        }
        .btn-blue {
            background-color: #2563eb;
            color: white;
        }
        .btn-blue:hover {
            background-color: #1d4ed8;
        }
        .btn-blue-light {
            background-color: #dbeafe;
            color: #2563eb;
        }
        .btn-blue-light:hover {
            background-color: #bfdbfe;
        }
        .btn-yellow {
            background-color: #ca8a04;
            color: white;
        }
        .btn-yellow:hover {
            background-color: #a16207;
        }
        .btn-yellow-light {
            background-color: #fef9c3;
            color: #ca8a04;
        }
        .btn-yellow-light:hover {
            background-color: #fef08a;
        }
        .btn-purple {
            background-color: #9333ea;
            color: white;
        }
        .btn-purple:hover {
            background-color: #7e22ce;
        }
        .btn-purple-light {
            background-color: #f3e8ff;
            color: #9333ea;
        }
        .btn-purple-light:hover {
            background-color: #e9d5ff;
        }
        .btn-red {
            background-color: #dc2626;
            color: white;
        }
        .btn-red:hover {
            background-color: #b91c1c;
        }
        .btn-red-light {
            background-color: #fee2e2;
            color: #dc2626;
        }
        .btn-red-light:hover {
            background-color: #fecaca;
        }
        .btn-gray {
            background-color: #4b5563;
            color: white;
        }
        .btn-gray:hover {
            background-color: #374151;
        }
        .btn-gray-light {
            background-color: #f3f4f6;
            color: #4b5563;
        }
        .btn-gray-light:hover {
            background-color: #e5e7eb;
        }
        
        /* Page Sections */
        .page-section {
            margin-bottom: 1.5rem;
        }
        .page-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
            padding: 0 1rem;
        }
        .page-title {
            font-size: 1.5rem;
            font-weight: 600;
            color: #1f2937;
        }
        
        /* Filters */
        .filters-card {
            background-color: white;
            border-radius: 0.5rem;
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
            padding: 1rem;
            margin-bottom: 1.5rem;
        }
        .filters-grid {
            display: grid;
            grid-template-columns: repeat(1, 1fr);
            gap: 1rem;
        }
        @media (min-width: 768px) {
            .filters-grid {
                grid-template-columns: repeat(4, 1fr);
            }
        }
        .filter-group {
            margin-bottom: 1rem;
        }
        .filter-label {
            display: block;
            font-size: 0.875rem;
            font-weight: 500;
            color: #4b5563;
            margin-bottom: 0.25rem;
        }
        .filter-input {
            width: 100%;
            padding: 0.5rem 0.75rem;
            border: 1px solid #d1d5db;
            border-radius: 0.375rem;
        }
        .filter-actions {
            display: flex;
            justify-content: flex-end;
            margin-top: 1rem;
        }
        
        /* Tables */
        .table-card {
            background-color: white;
            border-radius: 0.5rem;
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }
        .table-responsive {
            overflow-x: auto;
        }
        table {
            min-width: 100%;
            border-collapse: collapse;
        }
        thead {
            background-color: #f9fafb;
        }
        th {
            padding: 0.75rem 1.5rem;
            text-align: left;
            font-size: 0.75rem;
            font-weight: 500;
            color: #6b7280;
            text-transform: uppercase;
            letter-spacing: 0.05em;
        }
        td {
            padding: 1rem 1.5rem;
            white-space: nowrap;
            font-size: 0.875rem;
            color: #6b7280;
            border-top: 1px solid #e5e7eb;
        }
        tr:hover td {
            background-color: #f9fafb;
        }
        .table-actions {
            text-align: right;
        }
        .table-action-btn {
            color: #4b5563;
            margin-left: 0.75rem;
            text-decoration: none;
        }
        .table-action-btn:hover {
            color: #1f2937;
        }
        .table-action-btn.edit {
            color: #2563eb;
        }
        .table-action-btn.edit:hover {
            color: #1d4ed8;
        }
        .table-action-btn.delete {
            color: #dc2626;
        }
        .table-action-btn.delete:hover {
            color: #b91c1c;
        }
        .table-footer {
            background-color: #f9fafb;
            padding: 0.75rem 1rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
            border-top: 1px solid #e5e7eb;
        }
        .table-info {
            font-size: 0.875rem;
            color: #6b7280;
        }
        .pagination {
            display: flex;
            align-items: center;
        }
        .pagination-item {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            min-width: 2rem;
            height: 2rem;
            padding: 0 0.5rem;
            margin: 0 0.25rem;
            border: 1px solid #d1d5db;
            border-radius: 0.375rem;
            font-size: 0.875rem;
            color: #4b5563;
            text-decoration: none;
        }
        .pagination-item:hover {
            background-color: #f3f4f6;
        }
        .pagination-item.active {
            background-color: #dcfce7;
            border-color: #16a34a;
            color: #16a34a;
        }
        
        /* Status Badges */
        .badge {
            display: inline-flex;
            align-items: center;
            padding: 0.125rem 0.5rem;
            border-radius: 9999px;
            font-size: 0.75rem;
            font-weight: 600;
        }
        .badge-green {
            background-color: #dcfce7;
            color: #16a34a;
        }
        .badge-yellow {
            background-color: #fef9c3;
            color: #ca8a04;
        }
        .badge-red {
            background-color: #fee2e2;
            color: #dc2626;
        }
        
        /* Modals */
        .modal {
            display: none;
            position: fixed;
            z-index: 100;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
        }
        .modal-content {
            background-color: white;
            margin: 10% auto;
            padding: 1.5rem;
            border-radius: 0.5rem;
            width: 90%;
            max-width: 600px;
        }
        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
        }
        .modal-title {
            font-size: 1.125rem;
            font-weight: 600;
            color: #1f2937;
        }
        .modal-close {
            font-size: 1.5rem;
            font-weight: bold;
            color: #6b7280;
            cursor: pointer;
        }
        .modal-body {
            margin-bottom: 1.5rem;
        }
        .modal-footer {
            display: flex;
            justify-content: flex-end;
        }
        
        /* Forms */
        .form-grid {
            display: grid;
            grid-template-columns: repeat(1, 1fr);
            gap: 1rem;
            margin-bottom: 1rem;
        }
        @media (min-width: 768px) {
            .form-grid {
                grid-template-columns: repeat(2, 1fr);
            }
        }
        .form-group {
            margin-bottom: 1rem;
        }
        .form-label {
            display: block;
            font-size: 0.875rem;
            font-weight: 500;
            color: #4b5563;
            margin-bottom: 0.25rem;
        }
        .form-control {
            width: 100%;
            padding: 0.5rem 0.75rem;
            border: 1px solid #d1d5db;
            border-radius: 0.375rem;
        }
        .form-control:focus {
            outline: none;
            border-color: #16a34a;
            box-shadow: 0 0 0 3px rgba(22, 163, 74, 0.1);
        }
        .form-group-full {
            grid-column: span 2;
        }
        
        /* Calendar */
        .calendar-grid {
            display: grid;
            grid-template-columns: repeat(1, 1fr);
            gap: 1rem;
        }
        @media (min-width: 768px) {
            .calendar-grid {
                grid-template-columns: repeat(4, 1fr);
            }
        }
        .calendar-card {
            padding: 1rem;
            border-radius: 0.5rem;
        }
        .calendar-card.green {
            background-color: #f0fdf4;
            border: 1px solid #dcfce7;
        }
        .calendar-card.blue {
            background-color: #eff6ff;
            border: 1px solid #dbeafe;
        }
        .calendar-card.yellow {
            background-color: #fefce8;
            border: 1px solid #fef9c3;
        }
        .calendar-card.red {
            background-color: #fef2f2;
            border: 1px solid #fee2e2;
        }
        .calendar-card-header {
            display: flex;
            align-items: center;
            margin-bottom: 0.5rem;
        }
        .calendar-card-icon {
            padding: 0.5rem;
            border-radius: 9999px;
            margin-right: 0.75rem;
        }
        .calendar-card-icon.green {
            background-color: #dcfce7;
            color: #16a34a;
        }
        .calendar-card-icon.blue {
            background-color: #dbeafe;
            color: #2563eb;
        }
        .calendar-card-icon.yellow {
            background-color: #fef9c3;
            color: #ca8a04;
        }
        .calendar-card-icon.red {
            background-color: #fee2e2;
            color: #dc2626;
        }
        .calendar-card-title {
            font-size: 1.125rem;
            font-weight: 500;
            color: #1f2937;
        }
        .calendar-card-list {
            list-style: none;
        }
        .calendar-card-item {
            display: flex;
            align-items: flex-start;
            margin-bottom: 0.5rem;
        }
        .calendar-card-marker {
            display: inline-block;
            width: 0.75rem;
            height: 0.75rem;
            border-radius: 9999px;
            margin-top: 0.375rem;
            margin-right: 0.5rem;
        }
        .calendar-card-marker.green {
            background-color: #16a34a;
        }
        .calendar-card-marker.blue {
            background-color: #2563eb;
        }
        .calendar-card-marker.yellow {
            background-color: #ca8a04;
        }
        .calendar-card-marker.red {
            background-color: #dc2626;
        }
        .calendar-card-text {
            font-size: 0.875rem;
        }
        
        /* Mobile Adjustments */
        .mobile-menu-btn {
            display: none;
            position: fixed;
            top: 1rem;
            left: 1rem;
            z-index: 50;
            padding: 0.5rem;
            background-color: #166534;
            color: white;
            border: none;
            border-radius: 0.375rem;
            cursor: pointer;
        }
        .sidebar-close-btn {
            display: none;
            padding: 0.25rem;
            border-radius: 9999px;
            background: transparent;
            border: none;
            color: white;
            cursor: pointer;
        }
        .sidebar-close-btn:hover {
            background-color: #15803d;
        }
        
        @media (max-width: 768px) {
            .mobile-menu-btn {
                display: block;
            }
            .sidebar-close-btn {
                display: block;
            }
            .sidebar {
                transform: translateX(-100%);
                position: fixed;
                z-index: 50;
                height: 100vh;
                top: 0;
                left: 0;
            }
            .sidebar.active {
                transform: translateX(0);
            }
            .main-content {
                margin-left: 0;
            }
        }
        
        /* Page Display */
        .page {
            display: none;
        }
        .page.active {
            display: block;
        }
    </style>
</head>
<body>
    <div id="app" class="min-h-screen">
        <!-- Mobile Menu Button -->
        <button id="menu-button" class="mobile-menu-btn">
            <i class="fas fa-bars"></i>
        </button>

        <!-- Sidebar -->
        <div id="sidebar" class="sidebar">
            <div class="sidebar-header">
                <div class="sidebar-brand">
                    <i class="fas fa-cow"></i>
                    <span>AgroTech</span>
                </div>
                <button id="closeMenu" class="sidebar-close-btn">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            <nav class="sidebar-nav">
                <div class="sidebar-section">
                    <h3 class="sidebar-section-title">Menu Principal</h3>
                    <ul class="sidebar-menu">
                        <li class="sidebar-menu-item">
                            <a href="#dashboard" class="sidebar-menu-link active" data-page="dashboard">
                                <i class="fas fa-home sidebar-menu-icon"></i>
                                <span>Home</span>
                            </a>
                        </li>
                        <li class="sidebar-menu-item">
                            <a href="#rebanho" class="sidebar-menu-link" data-page="rebanho">
                                <i class="fas fa-cow sidebar-menu-icon"></i>
                                <span>Rebanho</span>
                            </a>
                        </li>
                        <li class="sidebar-menu-item">
                            <a href="#pesagem" class="sidebar-menu-link" data-page="pesagem">
                                <i class="fas fa-weight-scale sidebar-menu-icon"></i>
                                <span>Pesagem</span>
                            </a>
                        </li>
                        <li class="sidebar-menu-item">
                            <a href="#vacinacao" class="sidebar-menu-link" data-page="vacinacao">
                                <i class="fas fa-syringe sidebar-menu-icon"></i>
                                <span>Vacinação</span>
                            </a>
                        </li>
                        <li class="sidebar-menu-item">
                            <a href="#reproducao" class="sidebar-menu-link" data-page="reproducao">
                                <i class="fas fa-dna sidebar-menu-icon"></i>
                                <span>Reprodução</span>
                            </a>
                        </li>
                        <li class="sidebar-menu-item">
                            <a href="#financeiro" class="sidebar-menu-link" data-page="financeiro">
                                <i class="fas fa-money-bill-wave sidebar-menu-icon"></i>
                                <span>Financeiro</span>
                            </a>
                        </li>
                    </ul>
                </div>
                <div class="sidebar-section">
                    <h3 class="sidebar-section-title">Configurações</h3>
                    <ul class="sidebar-menu">
                        <li class="sidebar-menu-item">
                            <a href="#" class="sidebar-menu-link">
                                <i class="fas fa-user sidebar-menu-icon"></i>
                                <span>Perfil</span>
                            </a>
                        </li>
                        <li class="sidebar-menu-item">
                            <a href="#" class="sidebar-menu-link">
                                <i class="fas fa-cog sidebar-menu-icon"></i>
                                <span>Configurações</span>
                            </a>
                        </li>
                        <li class="sidebar-menu-item">
                            <a href="#" id="logout-btn" class="sidebar-menu-link">
                                <i class="fas fa-sign-out-alt sidebar-menu-icon"></i>
                                <span>Sair</span>
                            </a>
                        </li>
                    </ul>
                </div>
            </nav>
        </div>

        <!-- Main Content -->
        <div class="main-content">
            <!-- Header -->
            <header class="header">
                <div class="header-container">
                    <h1 id="page-title" class="page-title">Dashboard</h1>
                    <div class="header-actions">
                        <button class="notification-btn">
                            <i class="fas fa-bell text-gray-600"></i>
                            <span class="notification-indicator"></span>
                        </button>
                        <div class="user-profile">
                            <img class="user-avatar" src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80" alt="">
                            <span class="user-name">Fazendeiro</span>
                        </div>
                    </div>
                </div>
            </header>

            <!-- Pages Content -->
            <main class="content">
                <!-- Dashboard Page -->
                <div id="dashboard-page" class="page active">
                    <!-- Stats -->
                    <div class="stats-grid">
                        <div class="stat-card">
                            <div class="stat-card-content">
                                <div class="stat-card-icon green">
                                    <i class="fas fa-cow"></i>
                                </div>
                                <div>
                                    <p class="stat-card-label">Total de Cabeças</p>
                                    <p class="stat-card-value">1,234</p>
                                </div>
                            </div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-card-content">
                                <div class="stat-card-icon blue">
                                    <i class="fas fa-weight-scale"></i>
                                </div>
                                <div>
                                    <p class="stat-card-label">Peso Médio</p>
                                    <p class="stat-card-value">450 kg</p>
                                </div>
                            </div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-card-content">
                                <div class="stat-card-icon yellow">
                                    <i class="fas fa-syringe"></i>
                                </div>
                                <div>
                                    <p class="stat-card-label">Vacinas Pendentes</p>
                                    <p class="stat-card-value">56</p>
                                </div>
                            </div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-card-content">
                                <div class="stat-card-icon red">
                                    <i class="fas fa-money-bill-wave"></i>
                                </div>
                                <div>
                                    <p class="stat-card-label">Lucro Mensal</p>
                                    <p class="stat-card-value">R$ 25,670</p>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Modules -->
                    <h2 class="modules-title">Módulos do Sistema</h2>
                    <div class="modules-grid">
                        <!-- Rebanho Card -->
                        <div class="module-card card-hover">
                            <div class="module-card-header">
                                <div class="module-card-icon green">
                                    <i class="fas fa-cow"></i>
                                </div>
                                <h3 class="module-card-title">Gerenciar Rebanho</h3>
                            </div>
                            <p class="module-card-description">Cadastre, visualize e gerencie todo o seu rebanho bovino com facilidade.</p>
                            <div class="module-card-actions">
                                <a href="#rebanho" class="btn btn-green" data-page="rebanho">
                                    <i class="fas fa-plus btn-icon"></i> Adicionar
                                </a>
                                <a href="#rebanho" class="btn btn-green-light" data-page="rebanho">
                                    <i class="fas fa-list btn-icon"></i> Listar
                                </a>
                                <a href="#rebanho" class="btn btn-green-light" data-page="rebanho">
                                    <i class="fas fa-chart-bar btn-icon"></i> Relatórios
                                </a>
                            </div>
                        </div>

                        <!-- Pesagem Card -->
                        <div class="module-card card-hover">
                            <div class="module-card-header">
                                <div class="module-card-icon blue">
                                    <i class="fas fa-weight-scale"></i>
                                </div>
                                <h3 class="module-card-title">Controle de Pesagem</h3>
                            </div>
                            <p class="module-card-description">Registre e acompanhe o desenvolvimento do peso do seu gado ao longo do tempo.</p>
                            <div class="module-card-actions">
                                <a href="#pesagem" class="btn btn-blue" data-page="pesagem">
                                    <i class="fas fa-plus btn-icon"></i> Nova Pesagem
                                </a>
                                <a href="#pesagem" class="btn btn-blue-light" data-page="pesagem">
                                    <i class="fas fa-list btn-icon"></i> Histórico
                                </a>
                                <a href="#pesagem" class="btn btn-blue-light" data-page="pesagem">
                                    <i class="fas fa-chart-line btn-icon"></i> Evolução
                                </a>
                            </div>
                        </div>

                        <!-- Vacinação Card -->
                        <div class="module-card card-hover">
                            <div class="module-card-header">
                                <div class="module-card-icon yellow">
                                    <i class="fas fa-syringe"></i>
                                </div>
                                <h3 class="module-card-title">Controle de Vacinação</h3>
                            </div>
                            <p class="module-card-description">Gerencie o calendário de vacinação do seu rebanho e mantenha os registros em dia.</p>
                            <div class="module-card-actions">
                                <a href="#vacinacao" class="btn btn-yellow" data-page="vacinacao">
                                    <i class="fas fa-plus btn-icon"></i> Nova Vacina
                                </a>
                                <a href="#vacinacao" class="btn btn-yellow-light" data-page="vacinacao">
                                    <i class="fas fa-calendar btn-icon"></i> Calendário
                                </a>
                                <a href="#vacinacao" class="btn btn-yellow-light" data-page="vacinacao">
                                    <i class="fas fa-list-check btn-icon"></i> Pendentes
                                </a>
                            </div>
                        </div>

                        <!-- Reprodução Card -->
                        <div class="module-card card-hover">
                            <div class="module-card-header">
                                <div class="module-card-icon purple">
                                    <i class="fas fa-dna"></i>
                                </div>
                                <h3 class="module-card-title">Controle Reprodutivo</h3>
                            </div>
                            <p class="module-card-description">Acompanhe o ciclo reprodutivo do seu rebanho e gerencie coberturas e nascimentos.</p>
                            <div class="module-card-actions">
                                <a href="#reproducao" class="btn btn-purple" data-page="reproducao">
                                    <i class="fas fa-plus btn-icon"></i> Nova Cobertura
                                </a>
                                <a href="#reproducao" class="btn btn-purple-light" data-page="reproducao">
                                    <i class="fas fa-list btn-icon"></i> Histórico
                                </a>
                                <a href="#reproducao" class="btn btn-purple-light" data-page="reproducao">
                                    <i class="fas fa-chart-line btn-icon"></i> Estatísticas
                                </a>
                            </div>
                        </div>

                        <!-- Financeiro Card -->
                        <div class="module-card card-hover">
                            <div class="module-card-header">
                                <div class="module-card-icon red">
                                    <i class="fas fa-money-bill-wave"></i>
                                </div>
                                <h3 class="module-card-title">Gestão Financeira</h3>
                            </div>
                            <p class="module-card-description">Controle receitas, despesas e acompanhe a rentabilidade da sua fazenda.</p>
                            <div class="module-card-actions">
                                <a href="#financeiro" class="btn btn-red" data-page="financeiro">
                                    <i class="fas fa-plus btn-icon"></i> Nova Transação
                                </a>
                                <a href="#financeiro" class="btn btn-red-light" data-page="financeiro">
                                    <i class="fas fa-chart-pie btn-icon"></i> Relatórios
                                </a>
                                <a href="#financeiro" class="btn btn-red-light" data-page="financeiro">
                                    <i class="fas fa-file-invoice-dollar btn-icon"></i> Fluxo de Caixa
                                </a>
                            </div>
                        </div>

                        <!-- Relatórios Card -->
                        <div class="module-card card-hover">
                            <div class="module-card-header">
                                <div class="module-card-icon gray">
                                    <i class="fas fa-chart-bar"></i>
                                </div>
                                <h3 class="module-card-title">Relatórios Gerais</h3>
                            </div>
                            <p class="module-card-description">Visualize relatórios consolidados e obtenha insights sobre sua operação.</p>
                            <div class="module-card-actions">
                                <a href="#" class="btn btn-gray">
                                    <i class="fas fa-file-pdf btn-icon"></i> Exportar PDF
                                </a>
                                <a href="#" class="btn btn-gray-light">
                                    <i class="fas fa-file-excel btn-icon"></i> Exportar Excel
                                </a>
                                <a href="#" class="btn btn-gray-light">
                                    <i class="fas fa-print btn-icon"></i> Imprimir
                                </a>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Rebanho Page -->
                <div id="rebanho-page" class="page">
                    <div class="page-section">
                        <div class="page-header">
                            <h2 class="page-title">Gestão de Rebanho</h2>
                            <button id="add-animal-btn" class="btn btn-green">
                                <i class="fas fa-plus btn-icon"></i> Cadastrar Animal
                            </button>
                        </div>
                    </div>

                    <!-- Filters -->
                    <div class="page-section">
                        <div class="filters-card">
                            <div class="filters-grid">
                                <div class="filter-group">
                                    <label class="filter-label">Identificação</label>
                                    <input type="text" class="filter-input" placeholder="Nome ou número">
                                </div>
                                <div class="filter-group">
                                    <label class="filter-label">Raça</label>
                                    <select class="filter-input">
                                        <option>Todas</option>
                                        <option>Nelore</option>
                                        <option>Angus</option>
                                        <option>Brahman</option>
                                        <option>Girolando</option>
                                        <option>Holandês</option>
                                    </select>
                                </div>
                                <div class="filter-group">
                                    <label class="filter-label">Sexo</label>
                                    <select class="filter-input">
                                        <option>Todos</option>
                                        <option>Macho</option>
                                        <option>Fêmea</option>
                                    </select>
                                </div>
                                <div class="filter-group">
                                    <label class="filter-label">Situação</label>
                                    <select class="filter-input">
                                        <option>Todas</option>
                                        <option>Ativo</option>
                                        <option>Inativo</option>
                                    </select>
                                </div>
                            </div>
                            <div class="filter-actions">
                                <button class="btn btn-secondary" style="margin-right: 0.5rem;">
                                    Limpar
                                </button>
                                <button class="btn btn-green">
                                    Aplicar Filtros
                                </button>
                            </div>
                        </div>
                    </div>

                    <!-- Animals Table -->
                    <div class="page-section">
                        <div class="table-card">
                            <div class="table-responsive">
                                <table>
                                    <thead>
                                        <tr>
                                            <th>Nome</th>
                                            <th>Número (Brinco)</th>
                                            <th>Raça</th>
                                            <th>Sexo</th>
                                            <th>Data de Nascimento</th>
                                            <th>Situação</th>
                                            <th class="table-actions">Ações</th>
                                        </tr>
                                    </thead>
                                    <tbody>
                                        <tr>
                                            <td>Boi Nelore</td>
                                            <td>#1001</td>
                                            <td>Nelore</td>
                                            <td>Macho</td>
                                            <td>15/03/2023</td>
                                            <td><span class="badge badge-green">Ativo</span></td>
                                            <td class="table-actions">
                                                <a href="#" class="table-action-btn edit"><i class="fas fa-edit"></i></a>
                                                <a href="#" class="table-action-btn delete"><i class="fas fa-trash"></i></a>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td>Vaca Angus</td>
                                            <td>#1002</td>
                                            <td>Angus</td>
                                            <td>Fêmea</td>
                                            <td>22/05/2022</td>
                                            <td><span class="badge badge-green">Ativo</span></td>
                                            <td class="table-actions">
                                                <a href="#" class="table-action-btn edit"><i class="fas fa-edit"></i></a>
                                                <a href="#" class="table-action-btn delete"><i class="fas fa-trash"></i></a>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td>Bezerro Brahman</td>
                                            <td>#1003</td>
                                            <td>Brahman</td>
                                            <td>Macho</td>
                                            <td>10/11/2024</td>
                                            <td><span class="badge badge-green">Ativo</span></td>
                                            <td class="table-actions">
                                                <a href="#" class="table-action-btn edit"><i class="fas fa-edit"></i></a>
                                                <a href="#" class="table-action-btn delete"><i class="fas fa-trash"></i></a>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td>Vaca Girolando</td>
                                            <td>#1004</td>
                                            <td>Girolando</td>
                                            <td>Fêmea</td>
                                            <td>05/07/2021</td>
                                            <td><span class="badge badge-yellow">Inativo</span></td>
                                            <td class="table-actions">
                                                <a href="#" class="table-action-btn edit"><i class="fas fa-edit"></i></a>
                                                <a href="#" class="table-action-btn delete"><i class="fas fa-trash"></i></a>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td>Touro Nelore</td>
                                            <td>#1005</td>
                                            <td>Nelore</td>
                                            <td>Macho</td>
                                            <td>18/02/2020</td>
                                            <td><span class="badge badge-green">Ativo</span></td>
                                            <td class="table-actions">
                                                <a href="#" class="table-action-btn edit"><i class="fas fa-edit"></i></a>
                                                <a href="#" class="table-action-btn delete"><i class="fas fa-trash"></i></a>
                                            </td>
                                        </tr>
                                    </tbody>
                                </table>
                            </div>
                            <div class="table-footer">
                                <div class="table-info">
                                    Mostrando <span>1</span> a <span>5</span> de <span>24</span> resultados
                                </div>
                                <div class="pagination">
                                    <a href="#" class="pagination-item">
                                        <i class="fas fa-chevron-left"></i>
                                    </a>
                                    <a href="#" class="pagination-item active">1</a>
                                    <a href="#" class="pagination-item">2</a>
                                    <a href="#" class="pagination-item">3</a>
                                    <a href="#" class="pagination-item">
                                        <i class="fas fa-chevron-right"></i>
                                    </a>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Pesagem Page -->
                <div id="pesagem-page" class="page">
                    <div class="page-section">
                        <div class="page-header">
                            <h2 class="page-title">Controle de Pesagem</h2>
                            <button id="add-weighing-btn" class="btn btn-blue">
                                <i class="fas fa-plus btn-icon"></i> Nova Pesagem
                            </button>
                        </div>
                    </div>

                    <!-- Filters -->
                    <div class="page-section">
                        <div class="filters-card">
                            <div class="filters-grid">
                                <div class="filter-group">
                                    <label class="filter-label">Animal</label>
                                    <select class="filter-input">
                                        <option>Todos</option>
                                        <option>Boi Nelore (#1001)</option>
                                        <option>Vaca Angus (#1002)</option>
                                        <option>Bezerro Brahman (#1003)</option>
                                        <option>Vaca Girolando (#1004)</option>
                                        <option>Touro Nelore (#1005)</option>
                                    </select>
                                </div>
                                <div class="filter-group">
                                    <label class="filter-label">Período</label>
                                    <div style="display: flex; gap: 0.5rem;">
                                        <input type="date" class="filter-input" placeholder="De">
                                        <input type="date" class="filter-input" placeholder="Até">
                                    </div>
                                </div>
                                <div class="filter-group">
                                    <label class="filter-label">Ordenar por</label>
                                    <select class="filter-input">
                                        <option>Data (mais recente)</option>
                                        <option>Data (mais antiga)</option>
                                        <option>Animal (A-Z)</option>
                                        <option>Peso (maior)</option>
                                        <option>Peso (menor)</option>
                                        <option>Variação (maior)</option>
                                        <option>Variação (menor)</option>
                                    </select>
                                </div>
                                <div class="filter-group">
                                    <label class="filter-label">Responsável</label>
                                    <select class="filter-input">
                                        <option>Todos</option>
                                        <option>João Silva</option>
                                        <option>Maria Oliveira</option>
                                        <option>Carlos Santos</option>
                                    </select>
                                </div>
                            </div>
                            <div class="filter-actions">
                                <button class="btn btn-secondary" style="margin-right: 0.5rem;">
                                    Limpar
                                </button>
                                <button class="btn btn-blue">
                                    Aplicar Filtros
                                </button>
                            </div>
                        </div>
                    </div>

                    <!-- Weighing Table -->
                    <div class="page-section">
                        <div class="table-card">
                            <div class="table-responsive">
                                <table>
                                    <thead>
                                        <tr>
                                            <th>Data da Pesagem</th>
                                            <th>Animal</th>
                                            <th>Peso (kg)</th>
                                            <th>Variação</th>
                                            <th>Responsável</th>
                                            <th>Observações</th>
                                            <th class="table-actions">Ações</th>
                                        </tr>
                                    </thead>
                                    <tbody>
                                        <tr>
                                            <td>15/05/2025</td>
                                            <td>Boi Nelore (#1001)</td>
                                            <td>480 kg</td>
                                            <td style="color: #16a34a;">+15 kg</td>
                                            <td>João Silva</td>
                                            <td>Ganho de peso conforme esperado</td>
                                            <td class="table-actions">
                                                <a href="#" class="table-action-btn edit"><i class="fas fa-edit"></i></a>
                                                <a href="#" class="table-action-btn delete"><i class="fas fa-trash"></i></a>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td>10/05/2025</td>
                                            <td>Vaca Angus (#1002)</td>
                                            <td>520 kg</td>
                                            <td style="color: #16a34a;">+8 kg</td>
                                            <td>Maria Oliveira</td>
                                            <td>Ganho de peso estável</td>
                                            <td class="table-actions">
                                                <a href="#" class="table-action-btn edit"><i class="fas fa-edit"></i></a>
                                                <a href="#" class="table-action-btn delete"><i class="fas fa-trash"></i></a>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td>05/05/2025</td>
                                            <td>Bezerro Brahman (#1003)</td>
                                            <td>180 kg</td>
                                            <td style="color: #16a34a;">+12 kg</td>
                                            <td>Carlos Santos</td>
                                            <td>Desenvolvimento acima do esperado</td>
                                            <td class="table-actions">
                                                <a href="#" class="table-action-btn edit"><i class="fas fa-edit"></i></a>
                                                <a href="#" class="table-action-btn delete"><i class="fas fa-trash"></i></a>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td>01/05/2025</td>
                                            <td>Touro Nelore (#1005)</td>
                                            <td>680 kg</td>
                                            <td style="color: #dc2626;">-5 kg</td>
                                            <td>João Silva</td>
                                            <td>Perda de peso, verificar alimentação</td>
                                            <td class="table-actions">
                                                <a href="#" class="table-action-btn edit"><i class="fas fa-edit"></i></a>
                                                <a href="#" class="table-action-btn delete"><i class="fas fa-trash"></i></a>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td>25/04/2025</td>
                                            <td>Vaca Girolando (#1004)</td>
                                            <td>550 kg</td>
                                            <td style="color: #16a34a;">+10 kg</td>
                                            <td>Maria Oliveira</td>
                                            <td>Ganho de peso satisfatório</td>
                                            <td class="table-actions">
                                                <a href="#" class="table-action-btn edit"><i class="fas fa-edit"></i></a>
                                                <a href="#" class="table-action-btn delete"><i class="fas fa-trash"></i></a>
                                            </td>
                                        </tr>
                                    </tbody>
                                </table>
                            </div>
                            <div class="table-footer">
                                <div class="table-info">
                                    Mostrando <span>1</span> a <span>5</span> de <span>18</span> resultados
                                </div>
                                <div class="pagination">
                                    <a href="#" class="pagination-item">
                                        <i class="fas fa-chevron-left"></i>
                                    </a>
                                    <a href="#" class="pagination-item active">1</a>
                                    <a href="#" class="pagination-item">2</a>
                                    <a href="#" class="pagination-item">3</a>
                                    <a href="#" class="pagination-item">
                                        <i class="fas fa-chevron-right"></i>
                                    </a>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Vacinação Page -->
                <div id="vacinacao-page" class="page">
                    <div class="page-section">
                        <div class="page-header">
                            <h2 class="page-title">Controle de Vacinação</h2>
                            <button id="add-vaccine-btn" class="btn btn-yellow">
                                <i class="fas fa-plus btn-icon"></i> Nova Vacinação
                            </button>
                        </div>
                    </div>

                    <!-- Filters -->
                    <div class="page-section">
                        <div class="filters-card">
                            <div class="filters-grid">
                                <div class="filter-group">
                                    <label class="filter-label">Tipo de Vacina</label>
                                    <select class="filter-input">
                                        <option>Todos</option>
                                        <option>Febre Aftosa</option>
                                        <option>Brucelose</option>
                                        <option>Raiva</option>
                                        <option>Carbúnculo</option>
                                        <option>Clostridioses</option>
                                    </select>
                                </div>
                                <div class="filter-group">
                                    <label class="filter-label">Status</label>
                                    <select class="filter-input">
                                        <option>Todos</option>
                                        <option>Pendente</option>
                                        <option>Realizada</option>
                                        <option>Atrasada</option>
                                    </select>
                                </div>
                                <div class="filter-group">
                                    <label class="filter-label">Período</label>
                                    <div style="display: flex; gap: 0.5rem;">
                                        <input type="date" class="filter-input" placeholder="De">
                                        <input type="date" class="filter-input" placeholder="Até">
                                    </div>
                                </div>
                            </div>
                            <div class="filter-actions">
                                <button class="btn btn-secondary" style="margin-right: 0.5rem;">
                                    Limpar
                                </button>
                                <button class="btn btn-yellow">
                                    Aplicar Filtros
                                </button>
                            </div>
                        </div>
                    </div>

                    <!-- Vaccination Table -->
                    <div class="page-section">
                        <div class="table-card">
                            <div class="table-responsive">
                                <table>
                                    <thead>
                                        <tr>
                                            <th>Data</th>
                                            <th>Nome da Vacina</th>
                                            <th>Animais Vacinados</th>
                                            <th>Dose</th>
                                            <th>Status</th>
                                            <th>Responsável</th>
                                            <th class="table-actions">Ações</th>
                                        </tr>
                                    </thead>
                                    <tbody>
                                        <tr>
                                            <td>15/05/2025</td>
                                            <td>Febre Aftosa</td>
                                            <td>24 animais</td>
                                            <td>5ml</td>
                                            <td><span class="badge badge-green">Realizada</span></td>
                                            <td>João Silva</td>
                                            <td class="table-actions">
                                                <a href="#" class="table-action-btn edit"><i class="fas fa-edit"></i></a>
                                                <a href="#" class="table-action-btn delete"><i class="fas fa-trash"></i></a>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td>01/06/2025</td>
                                            <td>Brucelose</td>
                                            <td>12 animais</td>
                                            <td>3ml</td>
                                            <td><span class="badge badge-yellow">Pendente</span></td>
                                            <td>Maria Oliveira</td>
                                            <td class="table-actions">
                                                <a href="#" class="table-action-btn edit"><i class="fas fa-edit"></i></a>
                                                <a href="#" class="table-action-btn delete"><i class="fas fa-trash"></i></a>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td>10/04/2025</td>
                                            <td>Raiva</td>
                                            <td>18 animais</td>
                                            <td>2ml</td>
                                            <td><span class="badge badge-green">Realizada</span></td>
                                            <td>Carlos Santos</td>
                                            <td class="table-actions">
                                                <a href="#" class="table-action-btn edit"><i class="fas fa-edit"></i></a>
                                                <a href="#" class="table-action-btn delete"><i class="fas fa-trash"></i></a>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td>05/03/2025</td>
                                            <td>Carbúnculo</td>
                                            <td>15 animais</td>
                                            <td>4ml</td>
                                            <td><span class="badge badge-red">Atrasada</span></td>
                                            <td>João Silva</td>
                                            <td class="table-actions">
                                                <a href="#" class="table-action-btn edit"><i class="fas fa-edit"></i></a>
                                                <a href="#" class="table-action-btn delete"><i class="fas fa-trash"></i></a>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td>20/07/2025</td>
                                            <td>Clostridioses</td>
                                            <td>22 animais</td>
                                            <td>3ml</td>
                                            <td><span class="badge badge-yellow">Pendente</span></td>
                                            <td>Maria Oliveira</td>
                                            <td class="table-actions">
                                                <a href="#" class="table-action-btn edit"><i class="fas fa-edit"></i></a>
                                                <a href="#" class="table-action-btn delete"><i class="fas fa-trash"></i></a>
                                            </td>
                                        </tr>
                                    </tbody>
                                </table>
                            </div>
                            <div class="table-footer">
                                <div class="table-info">
                                    Mostrando <span>1</span> a <span>5</span> de <span>12</span> resultados
                                </div>
                                <div class="pagination">
                                    <a href="#" class="pagination-item">
                                        <i class="fas fa-chevron-left"></i>
                                    </a>
                                    <a href="#" class="pagination-item active">1</a>
                                    <a href="#" class="pagination-item">2</a>
                                    <a href="#" class="pagination-item">3</a>
                                    <a href="#" class="pagination-item">
                                        <i class="fas fa-chevron-right"></i>
                                    </a>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Vaccination Calendar -->
                    <div class="page-section">
                        <h3 class="modules-title">Calendário de Vacinação</h3>
                        <div class="calendar-grid">
                            <div class="calendar-card green">
                                <div class="calendar-card-header">
                                    <div class="calendar-card-icon green">
                                        <i class="fas fa-syringe"></i>
                                    </div>
                                    <h4 class="calendar-card-title">1º Trimestre</h4>
                                </div>
                                <ul class="calendar-card-list">
                                    <li class="calendar-card-item">
                                        <span class="calendar-card-marker green"></span>
                                        <span class="calendar-card-text">Febre Aftosa (Fevereiro)</span>
                                    </li>
                                    <li class="calendar-card-item">
                                        <span class="calendar-card-marker green"></span>
                                        <span class="calendar-card-text">Carbúnculo (Março)</span>
                                    </li>
                                </ul>
                            </div>
                            <div class="calendar-card blue">
                                <div class="calendar-card-header">
                                    <div class="calendar-card-icon blue">
                                        <i class="fas fa-syringe"></i>
                                    </div>
                                    <h4 class="calendar-card-title">2º Trimestre</h4>
                                </div>
                                <ul class="calendar-card-list">
                                    <li class="calendar-card-item">
                                        <span class="calendar-card-marker blue"></span>
                                        <span class="calendar-card-text">Brucelose (Abril)</span>
                                    </li>
                                    <li class="calendar-card-item">
                                        <span class="calendar-card-marker blue"></span>
                                        <span class="calendar-card-text">Raiva (Maio)</span>
                                    </li>
                                </ul>
                            </div>
                            <div class="calendar-card yellow">
                                <div class="calendar-card-header">
                                    <div class="calendar-card-icon yellow">
                                        <i class="fas fa-syringe"></i>
                                    </div>
                                    <h4 class="calendar-card-title">3º Trimestre</h4>
                                </div>
                                <ul class="calendar-card-list">
                                    <li class="calendar-card-item">
                                        <span class="calendar-card-marker yellow"></span>
                                        <span class="calendar-card-text">Clostridioses (Julho)</span>
                                    </li>
                                    <li class="calendar-card-item">
                                        <span class="calendar-card-marker yellow"></span>
                                        <span class="calendar-card-text">IBR/BVD (Agosto)</span>
                                    </li>
                                </ul>
                            </div>
                            <div class="calendar-card red">
                                <div class="calendar-card-header">
                                    <div class="calendar-card-icon red">
                                        <i class="fas fa-syringe"></i>
                                    </div>
                                    <h4 class="calendar-card-title">4º Trimestre</h4>
                                </div>
                                <ul class="calendar-card-list">
                                    <li class="calendar-card-item">
                                        <span class="calendar-card-marker red"></span>
                                        <span class="calendar-card-text">Febre Aftosa (Novembro)</span>
                                    </li>
                                    <li class="calendar-card-item">
                                        <span class="calendar-card-marker red"></span>
                                        <span class="calendar-card-text">Vermifugação (Dezembro)</span>
                                    </li>
                                </ul>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Reprodução Page -->
                <div id="reproducao-page" class="page">
                    <div class="page-section">
                        <div class="page-header">
                            <h2 class="page-title">Controle Reprodutivo</h2>
                            <button id="add-breeding-btn" class="btn btn-purple">
                                <i class="fas fa-plus btn-icon"></i> Nova Cobertura
                            </button>
                        </div>
                    </div>

                    <!-- Filters -->
                    <div class="page-section">
                        <div class="filters-card">
                            <div class="filters-grid">
                                <div class="filter-group">
                                    <label class="filter-label">Animal</label>
                                    <select class="filter-input">
                                        <option>Todos</option>
                                        <option>Vaca Angus (#1002)</option>
                                        <option>Vaca Girolando (#1004)</option>
                                        <option>Vaca Holandesa (#1006)</option>
                                    </select>
                                </div>
                                <div class="filter-group">
                                    <label class="filter-label">Status</label>
                                    <select class="filter-input">
                                        <option>Todos</option>
                                        <option>Prenhe</option>
                                        <option>Não Prenhe</option>
                                        <option>Em Observação</option>
                                    </select>
                                </div>
                                <div class="filter-group">
                                    <label class="filter-label">Período</label>
                                    <div style="display: flex; gap: 0.5rem;">
                                        <input type="date" class="filter-input" placeholder="De">
                                        <input type="date" class="filter-input" placeholder="Até">
                                    </div>
                                </div>
                            </div>
                            <div class="filter-actions">
                                <button class="btn btn-secondary" style="margin-right: 0.5rem;">
                                    Limpar
                                </button>
                                <button class="btn btn-purple">
                                    Aplicar Filtros
                                </button>
                            </div>
                        </div>
                    </div>

                    <!-- Breeding Table -->
                    <div class="page-section">
                        <div class="table-card">
                            <div class="table-responsive">
                                <table>
                                    <thead>
                                        <tr>
                                            <th>Data da Cobertura</th>
                                            <th>Fêmea</th>
                                            <th>Macho</th>
                                            <th>Resultado</th>
                                            <th>Data de Nascimento</th>
                                            <th>Observações</th>
                                            <th class="table-actions">Ações</th>
                                        </tr>
                                    </thead>
                                    <tbody>
                                        <tr>
                                            <td>15/01/2025</td>
                                            <td>Vaca Angus (#1002)</td>
                                            <td>Touro Nelore (#1005)</td>
                                            <td><span class="badge badge-green">Prenhe</span></td>
                                            <td>Previsto: 25/10/2025</td>
                                            <td>Gestação saudável</td>
                                            <td class="table-actions">
                                                <a href="#" class="table-action-btn edit"><i class="fas fa-edit"></i></a>
                                                <a href="#" class="table-action-btn delete"><i class="fas fa-trash"></i></a>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td>05/02/2025</td>
                                            <td>Vaca Girolando (#1004)</td>
                                            <td>Touro Brahman (#1008)</td>
                                            <td><span class="badge badge-red">Não Prenhe</span></td>
                                            <td>-</td>
                                            <td>Tentar nova cobertura em 30 dias</td>
                                            <td class="table-actions">
                                                <a href="#" class="table-action-btn edit"><i class="fas fa-edit"></i></a>
                                                <a href="#" class="table-action-btn delete"><i class="fas fa-trash"></i></a>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td>20/03/2025</td>
                                            <td>Vaca Holandesa (#1006)</td>
                                            <td>Touro Angus (#1010)</td>
                                            <td><span class="badge badge-yellow">Em Observação</span></td>
                                            <td>-</td>
                                            <td>Aguardando confirmação</td>
                                            <td class="table-actions">
                                                <a href="#" class="table-action-btn edit"><i class="fas fa-edit"></i></a>
                                                <a href="#" class="table-action-btn delete"><i class="fas fa-trash"></i></a>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td>10/12/2024</td>
                                            <td>Vaca Angus (#1002)</td>
                                            <td>Touro Nelore (#1005)</td>
                                            <td><span class="badge badge-green">Prenhe</span></td>
                                            <td>15/09/2025</td>
                                            <td>Bezerro saudável</td>
                                            <td class="table-actions">
                                                <a href="#" class="table-action-btn edit"><i class="fas fa-edit"></i></a>
                                                <a href="#" class="table-action-btn delete"><i class="fas fa-trash"></i></a>
                                            </td>
                                        </tr>
                                        <tr>
                                            <td>05/04/2025</td>
                                            <td>Vaca Girolando (#1004)</td>
                                            <td>Touro Brahman (#1008)</td>
                                            <td><span class="badge badge-green">Prenhe</span></td>
                                            <td>Previsto: 15/01/2026</td>
                                            <td>Gestação recente</td>
                                            <td class="table-actions">
                                                <a href="#" class="table-action-btn edit"><i class="fas fa-edit"></i></a>
                                                <a href="#" class="table-action-btn delete"><i class="fas fa-trash"></i></a>
                                            </td>
                                        </tr>
                                    </tbody>
                                </table>
                            </div>
                            <div class="table-footer">
                                <div class="table-info">
                                    Mostrando <span>1</span> a <span>5</span> de <span>10</span> resultados
                                </div>
                                <div class="pagination">
                                    <a href="#" class="pagination-item">
                                        <i class="fas fa-chevron-left"></i>
                                    </a>
                                    <a href="#" class="pagination-item active">1</a>
                                    <a href="#" class="pagination-item">2</a>
                                    <a href="#" class="pagination-item">3</a>
                                    <a href="#" class="pagination-item">
                                        <i class="fas fa-chevron-right"></i>
                                    </a>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Financeiro Page -->
                <div id="financeiro-page" class="page">
                    <div class="page-section">
                        <div class="page-header">
                            <h2 class="page-title">Gestão Financeira</h2>
                            <button class="btn btn-red">
                                <i class="fas fa-plus btn-icon"></i> Nova Transação
                            </button>
                        </div>
                    </div>
                    <div class="page-section">
                        <div style="background-color: white; padding: 1.5rem; border-radius: 0.5rem; box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1); text-align: center;">
                            <p style="font-size: 1.25rem; color: #6b7280;">Módulo em desenvolvimento</p>
                            <p style="color: #6b7280; margin-top: 0.5rem;">Esta funcionalidade estará disponível em breve.</p>
                        </div>
                    </div>
                </div>
            </main>
        </div>
    </div>

    <!-- Modals -->
    <!-- Modal Cadastro/Edição de Animal -->
    <div id="animal-modal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 class="modal-title">Cadastrar Novo Animal</h3>
                <span class="modal-close">&times;</span>
            </div>
            <form id="animal-form">
                <div class="form-grid">
                    <div class="form-group">
                        <label class="form-label">Nome</label>
                        <input type="text" class="form-control" placeholder="Nome do animal">
                    </div>
                    <div class="form-group">
                        <label class="form-label">Número (Brinco)</label>
                        <input type="text" class="form-control" placeholder="Número de identificação">
                    </div>
                    <div class="form-group">
                        <label class="form-label">Raça</label>
                        <select class="form-control">
                            <option>Selecione</option>
                            <option>Nelore</option>
                            <option>Angus</option>
                            <option>Brahman</option>
                            <option>Girolando</option>
                            <option>Holandês</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label class="form-label">Sexo</label>
                        <select class="form-control">
                            <option>Selecione</option>
                            <option>Macho</option>
                            <option>Fêmea</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label class="form-label">Data de Nascimento</label>
                        <input type="date" class="form-control">
                    </div>
                    <div class="form-group">
                        <label class="form-label">Situação</label>
                        <select class="form-control">
                            <option>Ativo</option>
                            <option>Inativo</option>
                        </select>
                    </div>
                    <div class="form-group form-group-full">
                        <label class="form-label">Observações</label>
                        <textarea class="form-control" rows="3" placeholder="Observações sobre o animal"></textarea>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" id="cancel-animal" style="margin-right: 0.5rem;">Cancelar</button>
                    <button type="submit" class="btn btn-green">Salvar</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Modal Nova Pesagem -->
    <div id="weighing-modal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 class="modal-title">Nova Pesagem</h3>
                <span class="modal-close">&times;</span>
            </div>
            <form id="weighing-form">
                <div class="form-grid">
                    <div class="form-group">
                        <label class="form-label">Data da Pesagem</label>
                        <input type="date" class="form-control" value="2025-05-20">
                    </div>
                    <div class="form-group">
                        <label class="form-label">Animal</label>
                        <select class="form-control">
                            <option>Selecione</option>
                            <option>Boi Nelore (#1001)</option>
                            <option>Vaca Angus (#1002)</option>
                            <option>Bezerro Brahman (#1003)</option>
                            <option>Vaca Girolando (#1004)</option>
                            <option>Touro Nelore (#1005)</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label class="form-label">Peso (kg)</label>
                        <input type="number" class="form-control" placeholder="Peso em kg">
                    </div>
                    <div class="form-group">
                        <label class="form-label">Responsável</label>
                        <select class="form-control">
                            <option>Selecione</option>
                            <option>João Silva</option>
                            <option>Maria Oliveira</option>
                            <option>Carlos Santos</option>
                        </select>
                    </div>
                    <div class="form-group form-group-full">
                        <label class="form-label">Observações</label>
                        <textarea class="form-control" rows="3" placeholder="Observações sobre a pesagem"></textarea>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" id="cancel-weighing" style="margin-right: 0.5rem;">Cancelar</button>
                    <button type="submit" class="btn btn-blue">Salvar</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Modal Nova Vacinação -->
    <div id="vaccine-modal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 class="modal-title">Nova Vacinação</h3>
                <span class="modal-close">&times;</span>
            </div>
            <form id="vaccine-form">
                <div class="form-grid">
                    <div class="form-group">
                        <label class="form-label">Data da Vacinação</label>
                        <input type="date" class="form-control" value="2025-05-20">
                    </div>
                    <div class="form-group">
                        <label class="form-label">Nome da Vacina</label>
                        <select class="form-control">
                            <option>Selecione</option>
                            <option>Febre Aftosa</option>
                            <option>Brucelose</option>
                            <option>Raiva</option>
                            <option>Carbúnculo</option>
                            <option>Clostridioses</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label class="form-label">Dose (ml)</label>
                        <input type="number" class="form-control" placeholder="Dose em ml">
                    </div>
                    <div class="form-group">
                        <label class="form-label">Responsável</label>
                        <select class="form-control">
                            <option>Selecione</option>
                            <option>João Silva</option>
                            <option>Maria Oliveira</option>
                            <option>Carlos Santos</option>
                        </select>
                    </div>
                    <div class="form-group form-group-full">
                        <label class="form-label">Animais Vacinados</label>
                        <div style="border: 1px solid #d1d5db; border-radius: 0.375rem; padding: 0.75rem; max-height: 10rem; overflow-y: auto;">
                            <div style="display: flex; flex-direction: column; gap: 0.5rem;">
                                <div style="display: flex; align-items: center;">
                                    <input type="checkbox" style="margin-right: 0.5rem;">
                                    <label>Boi Nelore (#1001)</label>
                                </div>
                                <div style="display: flex; align-items: center;">
                                    <input type="checkbox" style="margin-right: 0.5rem;">
                                    <label>Vaca Angus (#1002)</label>
                                </div>
                                <div style="display: flex; align-items: center;">
                                    <input type="checkbox" style="margin-right: 0.5rem;">
                                    <label>Bezerro Brahman (#1003)</label>
                                </div>
                                <div style="display: flex; align-items: center;">
                                    <input type="checkbox" style="margin-right: 0.5rem;">
                                    <label>Vaca Girolando (#1004)</label>
                                </div>
                                <div style="display: flex; align-items: center;">
                                    <input type="checkbox" style="margin-right: 0.5rem;">
                                    <label>Touro Nelore (#1005)</label>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="form-group form-group-full">
                        <label class="form-label">Observações</label>
                        <textarea class="form-control" rows="3" placeholder="Observações sobre a vacinação"></textarea>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" id="cancel-vaccine" style="margin-right: 0.5rem;">Cancelar</button>
                    <button type="submit" class="btn btn-yellow">Salvar</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Modal Nova Cobertura -->
    <div id="breeding-modal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 class="modal-title">Nova Cobertura</h3>
                <span class="modal-close">&times;</span>
            </div>
            <form id="breeding-form">
                <div class="form-grid">
                    <div class="form-group">
                        <label class="form-label">Data da Cobertura</label>
                        <input type="date" class="form-control" value="2025-05-20">
                    </div>
                    <div class="form-group">
                        <label class="form-label">Fêmea</label>
                        <select class="form-control">
                            <option>Selecione</option>
                            <option>Vaca Angus (#1002)</option>
                            <option>Vaca Girolando (#1004)</option>
                            <option>Vaca Holandesa (#1006)</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label class="form-label">Macho</label>
                        <select class="form-control">
                            <option>Selecione</option>
                            <option>Touro Nelore (#1005)</option>
                            <option>Touro Brahman (#1008)</option>
                            <option>Touro Angus (#1010)</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label class="form-label">Método</label>
                        <select class="form-control">
                            <option>Selecione</option>
                            <option>Monta Natural</option>
                            <option>Inseminação Artificial</option>
                            <option>Transferência de Embrião</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label class="form-label">Resultado</label>
                        <select class="form-control">
                            <option>Em Observação</option>
                            <option>Prenhe</option>
                            <option>Não Prenhe</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label class="form-label">Data de Nascimento Prevista</label>
                        <input type="date" class="form-control">
                    </div>
                    <div class="form-group form-group-full">
                        <label class="form-label">Observações</label>
                        <textarea class="form-control" rows="3" placeholder="Observações sobre a cobertura"></textarea>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" id="cancel-breeding" style="margin-right: 0.5rem;">Cancelar</button>
                    <button type="submit" class="btn btn-purple">Salvar</button>
                </div>
            </form>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Referências às páginas
            const pages = {
                'dashboard': document.getElementById('dashboard-page'),
                'rebanho': document.getElementById('rebanho-page'),
                'pesagem': document.getElementById('pesagem-page'),
                'vacinacao': document.getElementById('vacinacao-page'),
                'reproducao': document.getElementById('reproducao-page'),
                'financeiro': document.getElementById('financeiro-page')
            };
            
            // Referência ao título da página
            const pageTitle = document.getElementById('page-title');
            
            // Mapeamento de títulos
            const titles = {
                'dashboard': 'Dashboard',
                'rebanho': 'Gestão de Rebanho',
                'pesagem': 'Controle de Pesagem',
                'vacinacao': 'Controle de Vacinação',
                'reproducao': 'Controle Reprodutivo',
                'financeiro': 'Gestão Financeira'
            };
            
            // Função para alternar entre páginas
            function navigateTo(pageId) {
                // Esconde todas as páginas
                Object.values(pages).forEach(page => {
                    if (page) page.classList.remove('active');
                });
                
                // Mostra a página selecionada
                if (pages[pageId]) {
                    pages[pageId].classList.add('active');
                    // Atualiza o título
                    if (pageTitle) pageTitle.textContent = titles[pageId] || pageId;
                    
                    // Destaca o item de menu ativo
                    document.querySelectorAll('.sidebar-menu-link').forEach(link => {
                        link.classList.remove('active');
                        if (link.getAttribute('data-page') === pageId) {
                            link.classList.add('active');
                        }
                    });
                    
                    // Atualiza a URL com o hash
                    window.location.hash = pageId;
                }
            }
            
            // Adiciona eventos de clique aos links de navegação
            document.querySelectorAll('[data-page]').forEach(link => {
                link.addEventListener('click', function(e) {
                    e.preventDefault();
                    const pageId = this.getAttribute('data-page');
                    if (pageId) navigateTo(pageId);
                });
            });
            
            // Controle do menu mobile
            const menuButton = document.getElementById('menu-button');
            const closeMenu = document.getElementById('closeMenu');
            const sidebar = document.getElementById('sidebar');
            
            if (menuButton) {
                menuButton.addEventListener('click', function() {
                    sidebar.classList.add('active');
                });
            }
            
            if (closeMenu) {
                closeMenu.addEventListener('click', function() {
                    sidebar.classList.remove('active');
                });
            }
            
            // Navegação baseada em hash na URL
            function handleHashChange() {
                const hash = window.location.hash.substring(1);
                if (hash && pages[hash]) {
                    navigateTo(hash);
                } else if (!hash) {
                    navigateTo('dashboard');
                }
            }
            
            // Inicializa com base no hash atual
            handleHashChange();
            
            // Adiciona listener para mudanças no hash
            window.addEventListener('hashchange', handleHashChange);
            
            // Modal de Cadastro/Edição de Animal
            setupModal('animal-modal', 'add-animal-btn', 'animal-form', 'cancel-animal', 'Animal cadastrado com sucesso!');
            
            // Modal de Nova Pesagem
            setupModal('weighing-modal', 'add-weighing-btn', 'weighing-form', 'cancel-weighing', 'Pesagem registrada com sucesso!');
            
            // Modal de Nova Vacinação
            setupModal('vaccine-modal', 'add-vaccine-btn', 'vaccine-form', 'cancel-vaccine', 'Vacinação registrada com sucesso!');
            
            // Modal de Nova Cobertura
            setupModal('breeding-modal', 'add-breeding-btn', 'breeding-form', 'cancel-breeding', 'Cobertura registrada com sucesso!');
            
            // Função para configurar modais
            function setupModal(modalId, openBtnId, formId, cancelBtnId, successMessage) {
                const modal = document.getElementById(modalId);
                if (!modal) return;
                
                const openBtn = document.getElementById(openBtnId);
                const closeBtn = modal.querySelector('.modal-close');
                const cancelBtn = document.getElementById(cancelBtnId);
                const form = document.getElementById(formId);
                
                // Abrir modal
                if (openBtn) {
                    openBtn.addEventListener('click', function() {
                        modal.style.display = 'block';
                    });
                }
                
                // Fechar modal
                if (closeBtn) {
                    closeBtn.addEventListener('click', function() {
                        modal.style.display = 'none';
                    });
                }
                
                if (cancelBtn) {
                    cancelBtn.addEventListener('click', function() {
                        modal.style.display = 'none';
                    });
                }
                
                // Fechar modal ao clicar fora
                window.addEventListener('click', function(event) {
                    if (event.target == modal) {
                        modal.style.display = 'none';
                    }
                });
                
                // Formulário
                if (form) {
                    form.addEventListener('submit', function(e) {
                        e.preventDefault();
                        // Aqui seria a lógica para salvar os dados
                        alert(successMessage);
                        modal.style.display = 'none';
                    });
                }
            }
        });
    </script>
</body>
</html>

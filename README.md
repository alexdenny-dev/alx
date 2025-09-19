<!DOCTYPE html>
<html lang="ro">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FacturiPay - Toate facturile într-un singur loc</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            text-align: center;
            color: white;
            margin-bottom: 40px;
            animation: slideDown 0.6s ease-out;
        }

        @keyframes slideDown {
            from {
                opacity: 0;
                transform: translateY(-30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .header p {
            font-size: 1.1rem;
            opacity: 0.9;
        }

        .wallet-section {
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 30px;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.2);
            animation: fadeIn 0.8s ease-out 0.2s both;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .wallet-balance {
            font-size: 2rem;
            color: white;
            font-weight: bold;
            margin-bottom: 10px;
        }

        .wallet-text {
            color: rgba(255, 255, 255, 0.9);
            margin-bottom: 20px;
        }

        .add-funds-btn {
            background: linear-gradient(45deg, #4CAF50, #45a049);
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 25px;
            font-size: 1rem;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(76, 175, 80, 0.3);
        }

        .add-funds-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(76, 175, 80, 0.4);
        }

        .categories-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 25px;
            margin-bottom: 30px;
        }

        .category {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            transition: all 0.3s ease;
            animation: fadeInUp 0.6s ease-out;
            animation-fill-mode: both;
            position: relative;
        }

        .category:nth-child(1) { animation-delay: 0.1s; }
        .category:nth-child(2) { animation-delay: 0.2s; }
        .category:nth-child(3) { animation-delay: 0.3s; }
        .category:nth-child(4) { animation-delay: 0.4s; }
        .category:nth-child(5) { animation-delay: 0.5s; }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .category:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.15);
        }

        .category-header {
            display: flex;
            align-items: center;
            margin-bottom: 20px;
        }

        .category-icon {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            margin-right: 15px;
        }

        .energy .category-icon { background: linear-gradient(135deg, #FFB347, #FF6B35); }
        .communication .category-icon { background: linear-gradient(135deg, #4A90E2, #357ABD); }
        .utilities .category-icon { background: linear-gradient(135deg, #5CB3CC, #4A90CC); }
        .financial .category-icon { background: linear-gradient(135deg, #9B59B6, #8E44AD); }
        .maintenance .category-icon { background: linear-gradient(135deg, #FF9500, #FF6B00); }

        .category h3 {
            color: #2c3e50;
            font-size: 1.2rem;
            margin: 0;
        }

        .providers {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(110px, 1fr));
            gap: 12px;
            margin-bottom: 15px;
        }

        .providers.expanded {
            max-height: none !important;
        }

        .provider {
            background: #f8f9fa;
            border: 2px solid transparent;
            border-radius: 12px;
            padding: 12px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .provider:before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transition: left 0.5s;
        }

        .provider:hover {
            border-color: #667eea;
            transform: scale(1.05);
            background: #e8f2ff;
        }

        .provider:hover:before {
            left: 100%;
        }

        .provider-logo {
            width: 45px;
            height: 45px;
            margin: 0 auto 8px;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 11px;
            color: white;
            background-size: contain;
            background-position: center;
            background-repeat: no-repeat;
            position: relative;
            overflow: hidden;
            background-color: white;
            border: 1px solid #e0e0e0;
        }

        .provider-name {
            font-size: 0.8rem;
            color: #333;
            font-weight: 500;
            line-height: 1.2;
        }

        .see-more-btn {
            position: absolute;
            bottom: 15px;
            right: 15px;
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 20px;
            font-size: 0.8rem;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 2px 8px rgba(102, 126, 234, 0.3);
        }

        .see-more-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(102, 126, 234, 0.4);
        }

        .hidden-providers {
            display: none;
        }

        .hidden-providers.show {
            display: contents;
        }

        /* Logo-uri reale folosind favicon-uri și imagini CDN */
        .hidroelectrica { background-image: url('https://www.hidroelectrica.ro/favicon.ico'); background-size: 70%; background-color: #1e40af; }
        .eon { background-image: url('https://www.eon.ro/favicon.ico'); background-size: 80%; background-color: #ef4444; }
        .engie { background-image: url('https://www.engie.ro/favicon.ico'); background-size: 80%; background-color: #0ea5e9; }
        .premier { background-color: #059669; color: white; font-size: 8px; }
        .nova { background-color: #7c3aed; color: white; font-size: 9px; }
        .digi-energy { background-color: #000; color: white; font-size: 8px; }
        
        .orange { background-image: url('https://www.orange.ro/favicon.ico'); background-size: 80%; background-color: #ff6600; }
        .vodafone { background-image: url('https://www.vodafone.ro/favicon.ico'); background-size: 80%; background-color: #e60000; }
        .digi { background-image: url('https://www.digi.ro/favicon.ico'); background-size: 80%; background-color: #000; }
        .telekom { background-image: url('https://www.telekom.ro/favicon.ico'); background-size: 80%; background-color: #e20074; }
        .upc { background-color: #005baa; color: white; font-size: 10px; }
        .yoxo { background-color: #ff6b35; color: white; font-size: 9px; }
        .nextgen { background-color: #6366f1; color: white; font-size: 8px; }
        .rcs-rds { background-color: #dc2626; color: white; font-size: 8px; }
        
        .apa-nova { background-color: #0066cc; color: white; font-size: 8px; }
        .aquatim { background-color: #2563eb; color: white; font-size: 8px; }
        .somes { background-color: #059669; color: white; font-size: 8px; }
        .apa-serv { background-color: #0891b2; color: white; font-size: 7px; }
        .ecoaqua { background-color: #16a34a; color: white; font-size: 9px; }
        .rosal { background-color: #dc2626; color: white; font-size: 9px; }
        .salubris { background-color: #65a30d; color: white; font-size: 8px; }
        .comprest { background-color: #7c2d12; color: white; font-size: 8px; }
        
        .bcr { background-image: url('https://www.bcr.ro/favicon.ico'); background-size: 80%; background-color: #fbbf24; }
        .brd { background-image: url('https://www.brd.ro/favicon.ico'); background-size: 80%; background-color: #ef4444; }
        .ing { background-image: url('https://www.ing.ro/favicon.ico'); background-size: 80%; background-color: #ff6600; }
        .raiffeisen { background-image: url('https://www.raiffeisen.ro/favicon.ico'); background-size: 80%; background-color: #fbbf24; }
        .unicredit { background-color: #dc2626; color: white; font-size: 7px; }
        .bt { background-color: #f59e0b; color: white; font-size: 12px; }
        .cec { background-color: #10b981; color: white; font-size: 11px; }
        .alpha { background-color: #3b82f6; color: white; font-size: 9px; }

        .smart-bill { background-color: #22c55e; color: white; font-size: 8px; }
        .mea-casa { background-color: #3b82f6; color: white; font-size: 8px; }
        .admin-plus { background-color: #8b5cf6; color: white; font-size: 8px; }
        .casa-verde { background-color: #059669; color: white; font-size: 8px; }
        .domino { background-color: #f59e0b; color: white; font-size: 8px; }
        .urbis { background-color: #6b7280; color: white; font-size: 8px; }
        .confort { background-color: #84cc16; color: white; font-size: 8px; }
        .total-admin { background-color: #06b6d4; color: white; font-size: 7px; }

        .payment-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            animation: modalFadeIn 0.3s ease;
        }

        @keyframes modalFadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .modal-content {
            background: white;
            border-radius: 20px;
            padding: 40px;
            max-width: 500px;
            width: 90%;
            animation: modalSlideIn 0.4s ease;
        }

        @keyframes modalSlideIn {
            from {
                opacity: 0;
                transform: translateY(-50px) scale(0.9);
            }
            to {
                opacity: 1;
                transform: translateY(0) scale(1);
            }
        }

        .modal-header {
            text-align: center;
            margin-bottom: 30px;
        }

        .modal-header h2 {
            color: #2c3e50;
            margin-bottom: 10px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            color: #555;
            font-weight: 500;
        }

        .form-group input {
            width: 100%;
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            font-size: 16px;
            transition: border-color 0.3s ease;
        }

        .form-group input:focus {
            outline: none;
            border-color: #667eea;
        }

        .modal-actions {
            display: flex;
            gap: 15px;
            justify-content: center;
            margin-top: 30px;
        }

        .btn {
            padding: 12px 25px;
            border: none;
            border-radius: 25px;
            font-size: 16px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .btn-primary {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
        }

        .btn-secondary {
            background: #f8f9fa;
            color: #666;
            border: 2px solid #e0e0e0;
        }

        .btn-secondary:hover {
            background: #e9ecef;
        }

        .recent-payments {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 15px;
            padding: 25px;
            margin-top: 30px;
            animation: fadeIn 1s ease-out 0.5s both;
        }

        .recent-payments h3 {
            color: #2c3e50;
            margin-bottom: 20px;
            text-align: center;
        }

        .payment-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px;
            border-bottom: 1px solid #eee;
            transition: background 0.3s ease;
        }

        .payment-item:hover {
            background: #f8f9fa;
        }

        .payment-item:last-child {
            border-bottom: none;
        }

        .payment-info {
            display: flex;
            align-items: center;
        }

        .payment-status {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            margin-right: 15px;
        }

        .status-success { background: #28a745; }
        .status-pending { background: #ffc107; }

        @media (max-width: 1024px) {
            .categories-grid {
                grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            }
        }

        @media (max-width: 768px) {
            .container {
                padding: 15px;
            }

            .header h1 {
                font-size: 2rem;
            }

            .categories-grid {
                grid-template-columns: 1fr;
            }

            .providers {
                grid-template-columns: repeat(auto-fill, minmax(90px, 1fr));
                gap: 10px;
            }

            .modal-content {
                padding: 30px 20px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🏦 FacturiPay</h1>
            <p>Plătește toate facturile dintr-un singur loc - Simplu, Rapid, Sigur</p>
        </div>

        <div class="wallet-section">
            <div class="wallet-balance">2,450.75 LEI</div>
            <div class="wallet-text">Soldul tău disponibil</div>
            <button class="add-funds-btn" onclick="showAddFunds()">+ Adaugă Fonduri</button>
        </div>

        <div class="categories-grid">
            <div class="category energy">
                <div class="category-header">
                    <div class="category-icon">⚡</div>
                    <h3>Energie & Gaze</h3>
                </div>
                <div class="providers">
                    <!-- TOP 6 cei mai populari furnizori de energie -->
                    <div class="provider" onclick="openPayment('E.ON', 'Energie & Gaze')">
                        <div class="provider-logo eon">EON</div>
                        <div class="provider-name">E.ON</div>
                    </div>
                    <div class="provider" onclick="openPayment('ENGIE', 'Gaze Naturale')">
                        <div class="provider-logo engie">ENG</div>
                        <div class="provider-name">ENGIE</div>
                    </div>
                    <div class="provider" onclick="openPayment('Hidroelectrica', 'Energie Electrică')">
                        <div class="provider-logo hidroelectrica">HE</div>
                        <div class="provider-name">Hidroelectrica</div>
                    </div>
                    <div class="provider" onclick="openPayment('Digi Energy', 'Electricitate')">
                        <div class="provider-logo digi-energy">DE</div>
                        <div class="provider-name">Digi Energy</div>
                    </div>
                    <div class="provider" onclick="openPayment('Premier Energy', 'Energie')">
                        <div class="provider-logo premier">PE</div>
                        <div class="provider-name">Premier Energy</div>
                    </div>
                    <div class="provider" onclick="openPayment('Nova Power', 'Energie')">
                        <div class="provider-logo nova">NP</div>
                        <div class="provider-name">Nova Power</div>
                    </div>
                </div>
                <button class="see-more-btn" onclick="toggleProviders(this, 'energy')">Vezi mai multe</button>
            </div>

            <div class="category communication">
                <div class="category-header">
                    <div class="category-icon">📱</div>
                    <h3>Comunicații & Internet</h3>
                </div>
                <div class="providers">
                    <!-- TOP 6 cei mai populari furnizori de comunicații -->
                    <div class="provider" onclick="openPayment('Orange', 'Mobil & Internet')">
                        <div class="provider-logo orange">OR</div>
                        <div class="provider-name">Orange</div>
                    </div>
                    <div class="provider" onclick="openPayment('Vodafone', 'Mobil & Internet')">
                        <div class="provider-logo vodafone">VF</div>
                        <div class="provider-name">Vodafone</div>
                    </div>
                    <div class="provider" onclick="openPayment('Digi', 'TV & Internet')">
                        <div class="provider-logo digi">DG</div>
                        <div class="provider-name">Digi</div>
                    </div>
                    <div class="provider" onclick="openPayment('Telekom', 'Fix & Mobil')">
                        <div class="provider-logo telekom">TK</div>
                        <div class="provider-name">Telekom</div>
                    </div>
                    <div class="provider" onclick="openPayment('UPC', 'TV & Internet')">
                        <div class="provider-logo upc">UPC</div>
                        <div class="provider-name">UPC</div>
                    </div>
                    <div class="provider" onclick="openPayment('RCS-RDS', 'TV & Internet')">
                        <div class="provider-logo rcs-rds">RCS</div>
                        <div class="provider-name">RCS-RDS</div>
                    </div>
                    
                    <!-- Provideri mai puțin populari -->
                    <div class="provider hidden-providers" onclick="openPayment('YOXO', 'Mobil')">
                        <div class="provider-logo yoxo">YOXO</div>
                        <div class="provider-name">YOXO</div>
                    </div>
                    <div class="provider hidden-providers" onclick="openPayment('NextGen', 'Internet Fibră')">
                        <div class="provider-logo nextgen">NG</div>
                        <div class="provider-name">NextGen</div>
                    </div>
                </div>
                <button class="see-more-btn" onclick="toggleProviders(this, 'communication')">Vezi mai multe</button>
            </div>

            <div class="category utilities">
                <div class="category-header">
                    <div class="category-icon">💧</div>
                    <h3>Apă & Salubritate</h3>
                </div>
                <div class="providers">
                    <!-- TOP 6 cei mai populari furnizori de apă -->
                    <div class="provider" onclick="openPayment('Apa Nova București', 'Apă și Canal')">
                        <div class="provider-logo apa-nova">AN</div>
                        <div class="provider-name">Apa Nova</div>
                    </div>
                    <div class="provider" onclick="openPayment('Aquatim Timișoara', 'Apă și Canal')">
                        <div class="provider-logo aquatim">AQ</div>
                        <div class="provider-name">Aquatim</div>
                    </div>
                    <div class="provider" onclick="openPayment('Someș Cluj', 'Apă și Canal')">
                        <div class="provider-logo somes">SM</div>
                        <div class="provider-name">Someș</div>
                    </div>
                    <div class="provider" onclick="openPayment('RoSal', 'Salubritate')">
                        <div class="provider-logo rosal">RS</div>
                        <div class="provider-name">RoSal</div>
                    </div>
                    <div class="provider" onclick="openPayment('Apa Serv', 'Apă și Canal')">
                        <div class="provider-logo apa-serv">AS</div>
                        <div class="provider-name">Apa Serv</div>
                    </div>
                    <div class="provider" onclick="openPayment('Ecoaqua', 'Salubritate')">
                        <div class="provider-logo ecoaqua">EA</div>
                        <div class="provider-name">Ecoaqua</div>
                    </div>
                    
                    <!-- Furnizori mai mici -->
                    <div class="provider hidden-providers" onclick="openPayment('Salubris', 'Salubritate')">
                        <div class="provider-logo salubris">SAL</div>
                        <div class="provider-name">Salubris</div>
                    </div>
                    <div class="provider hidden-providers" onclick="openPayment('Comprest', 'Salubritate')">
                        <div class="provider-logo comprest">CPR</div>
                        <div class="provider-name">Comprest</div>
                    </div>
                </div>
                <button class="see-more-btn" onclick="toggleProviders(this, 'utilities')">Vezi mai multe</button>
            </div>

            <div class="category financial">
                <div class="category-header">
                    <div class="category-icon">🏛️</div>
                    <h3>Servicii Financiare</h3>
                </div>
                <div class="providers">
                    <!-- TOP 6 cele mai mari bănci din România -->
                    <div class="provider" onclick="openPayment('Banca Transilvania', 'Rate & Credite')">
                        <div class="provider-logo bt">BT</div>
                        <div class="provider-name">BT</div>
                    </div>
                    <div class="provider" onclick="openPayment('BCR', 'Rate & Credite')">
                        <div class="provider-logo bcr">BCR</div>
                        <div class="provider-name">BCR</div>
                    </div>
                    <div class="provider" onclick="openPayment('BRD', 'Rate & Credite')">
                        <div class="provider-logo brd">BRD</div>
                        <div class="provider-name">BRD</div>
                    </div>
                    <div class="provider" onclick="openPayment('ING Bank', 'Rate & Credite')">
                        <div class="provider-logo ing">ING</div>
                        <div class="provider-name">ING Bank</div>
                    </div>
                    <div class="provider" onclick="openPayment('Raiffeisen', 'Rate & Credite')">
                        <div class="provider-logo raiffeisen">RF</div>
                        <div class="provider-name">Raiffeisen</div>
                    </div>
                    <div class="provider" onclick="openPayment('UniCredit', 'Rate & Credite')">
                        <div class="provider-logo unicredit">UC</div>
                        <div class="provider-name">UniCredit</div>
                    </div>
                    
                    <!-- Bănci mai mici -->
                    <div class="provider hidden-providers" onclick="openPayment('CEC Bank', 'Rate & Credite')">
                        <div class="provider-logo cec">CEC</div>
                        <div class="provider-name">CEC Bank</div>
                    </div>
                    <div class="provider hidden-providers" onclick="openPayment('Alpha Bank', 'Rate & Credite')">
                        <div class="provider-logo alpha">ALPHA</div>
                        <div class="provider-name">Alpha Bank</div>
                    </div>
                </div>
                <button class="see-more-btn" onclick="toggleProviders(this, 'financial')">Vezi mai multe</button>
            </div>

            <!-- NOUA CATEGORIE: Întreținere & Administrare -->
            <div class="category maintenance">
                <div class="category-header">
                    <div class="category-icon">🏠</div>
                    <h3>Întreținere & Administrare</h3>
                </div>
                <div class="providers">
                    <div class="provider" onclick="openPayment('SmartBill', 'Întreținere Apartament')">
                        <div class="provider-logo smart-bill">SB</div>
                        <div class="provider-name">SmartBill</div>
                    </div>
                    <div class="provider" onclick="openPayment('Mea Casa', 'Administrare Bloc')">
                        <div class="provider-logo mea-casa">MC</div>
                        <div class="provider-name">Mea Casa</div>
                    </div>
                    <div class="provider" onclick="openPayment('AdminPlus', 'Gestiune Imobiliară')">
                        <div class="provider-logo admin-plus">AP</div>
                        <div class="provider-name">AdminPlus</div>
                    </div>
                    <div class="provider" onclick="openPayment('Casa Verde', 'Administrare Condominii')">
                        <div class="provider-logo casa-verde">CV</div>
                        <div class="provider-name">Casa Verde</div>
                    </div>
                    <div class="provider" onclick="openPayment('Domino Admin', 'Întreținere & Fond Reparații')">
                        <div class="provider-logo domino">DA</div>
                        <div class="provider-name">Domino Admin</div>
                    </div>
                    <div class="provider" onclick="openPayment('Urbis Management', 'Administrare Proprietăți')">
                        <div class="provider-logo urbis">UM</div>
                        <div class="provider-name">Urbis Mgmt</div>
                    </div>
                    
                    <!-- Companii ascunse -->
                    <div class="provider hidden-providers" onclick="openPayment('Confort Residence', 'Administrare Condominii')">
                        <div class="provider-logo confort">CR</div>
                        <div class="provider-name">Confort</div>
                    </div>
                    <div class="provider hidden-providers" onclick="openPayment('Total Admin', 'Gestiune Completă')">
                        <div class="provider-logo total-admin">TA</div>
                        <div class="provider-name">Total Admin</div>
                    </div>
                </div>
                <button class="see-more-btn" onclick="toggleProviders(this, 'maintenance')">Vezi mai multe</button>
            </div>
        </div>

        <div class="recent-payments">
            <h3>📋 Plăți Recente</h3>
            <div class="payment-item">
                <div class="payment-info">
                    <div class="payment-status status-success"></div>
                    <div>
                        <strong>E.ON - Energie Electrică</strong><br>
                        <small>Ieri, 14:30</small>
                    </div>
                </div>
                <div style="font-weight: bold; color: #28a745;">-187.50 LEI</div>
            </div>
            <div class="payment-item">
                <div class="payment-info">
                    <div class="payment-status status-success"></div>
                    <div>
                        <strong>Orange - Abonament Mobil</strong><br>
                        <small>2 zile în urmă, 10:15</small>
                    </div>
                </div>
                <div style="font-weight: bold; color: #28a745;">-65.00 LEI</div>
            </div>
            <div class="payment-item">
                <div class="payment-info">
                    <div class="payment-status status-success"></div>
                    <div>
                        <strong>SmartBill - Întreținere Apt 23</strong><br>
                        <small>3 zile în urmă, 09:45</small>
                    </div>
                </div>
                <div style="font-weight: bold; color: #28a745;">-320.00 LEI</div>
            </div>
            <div class="payment-item">
                <div class="payment-info">
                    <div class="payment-status status-pending"></div>
                    <div>
                        <strong>Apa Nova - Apă și Canal</strong><br>
                        <small>În procesare...</small>
                    </div>
                </div>
                <div style="font-weight: bold; color: #ffc107;">-92.30 LEI</div>
            </div>
        </div>
    </div>

    <!-- Modal pentru plată -->
    <div class="payment-modal" id="paymentModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 id="modalTitle">Plată Factură</h2>
                <p id="modalProvider"></p>
            </div>
            
            <div class="form-group">
                <label for="contractNumber">Numărul Contractului/Contorului:</label>
                <input type="text" id="contractNumber" placeholder="Ex: 123456789">
            </div>
            
            <div class="form-group">
                <label for="amount">Suma de plătit (LEI):</label>
                <input type="number" id="amount" placeholder="0.00" step="0.01">
            </div>
            
            <div class="form-group">
                <label for="description">Descriere (opțional):</label>
                <input type="text" id="description" placeholder="Ex: Factură luna decembrie">
            </div>
            
            <div class="modal-actions">
                <button class="btn btn-secondary" onclick="closeModal()">Anulează</button>
                <button class="btn btn-primary" onclick="processPayment()">Plătește Acum</button>
            </div>
        </div>
    </div>

    <script>
        let currentProvider = '';
        let currentService = '';

        // URL-uri oficiale pentru toate companiile
        const companyURLs = {
            'Hidroelectrica': 'https://www.hidroelectrica.ro',
            'E.ON': 'https://www.eon.ro',
            'ENGIE': 'https://www.engie.ro',
            'Premier Energy': 'https://premierenergy.ro',
            'Nova Power': 'https://www.novapower.ro',
            'Digi Energy': 'https://www.digi.ro/energie',
            
            'Orange': 'https://www.orange.ro',
            'Vodafone': 'https://www.vodafone.ro',
            'Digi': 'https://www.digi.ro',
            'Telekom': 'https://www.telekom.ro',
            'UPC': 'https://www.upc.ro',
            'YOXO': 'https://www.yoxo.ro',
            'NextGen': 'https://www.nextgen.ro',
            'RCS-RDS': 'https://www.rcs-rds.ro',
            
            'Apa Nova București': 'https://www.apanova.ro',
            'Aquatim Timișoara': 'https://www.aquatim.ro',
            'Someș Cluj': 'https://www.somesaqua.ro',
            'Apa Serv': 'https://www.apaserv.ro',
            'Ecoaqua': 'https://www.ecoaqua.ro',
            'RoSal': 'https://www.rosal.ro',
            'Salubris': 'https://www.salubris.ro',
            'Comprest': 'https://www.comprest.ro',
            
            'BCR': 'https://www.bcr.ro',
            'BRD': 'https://www.brd.ro',
            'ING Bank': 'https://www.ing.ro',
            'Raiffeisen': 'https://www.raiffeisen.ro',
            'UniCredit': 'https://www.unicredit.ro',
            'Banca Transilvania': 'https://www.btrl.ro',
            'CEC Bank': 'https://www.cec.ro',
            'Alpha Bank': 'https://www.alphabank.ro',
            
            'SmartBill': 'https://www.smartbill.ro',
            'Mea Casa': 'https://www.meacasa.ro',
            'AdminPlus': 'https://www.adminplus.ro',
            'Casa Verde': 'https://www.casaverde.ro',
            'Domino Admin': 'https://www.dominoadmin.ro',
            'Urbis Management': 'https://www.urbismanagement.ro',
            'Confort Residence': 'https://www.confortresidence.ro',
            'Total Admin': 'https://www.totaladmin.ro'
        };

        function openPayment(provider, service) {
            // URL-uri reale și funcționale
            const companyURLs = {
                // Energie & Gaze
                'Hidroelectrica': 'https://www.hidroelectrica.ro',
                'E.ON': 'https://www.eon.ro',
                'ENGIE': 'https://www.engie.ro',
                'Premier Energy': 'https://premierenergy.ro',
                'Nova Power': 'https://www.enel.ro',
                'Digi Energy': 'https://www.digi.ro/energie',
                
                // Comunicații
                'Orange': 'https://www.orange.ro',
                'Vodafone': 'https://www.vodafone.ro',
                'Digi': 'https://www.digi.ro',
                'Telekom': 'https://www.telekom.ro',
                'UPC': 'https://www.upc.ro',
                'RCS-RDS': 'https://www.digi.ro',
                'YOXO': 'https://www.yoxo.ro',
                'NextGen': 'https://www.nextgencomm.eu',
                
                // Apă & Salubritate
                'Apa Nova București': 'https://www.apanova.ro',
                'Aquatim Timișoara': 'https://www.aquatim.ro',
                'Someș Cluj': 'https://www.somesaqua.ro',
                'Apa Serv': 'https://www.apaserv.ro',
                'Ecoaqua': 'https://www.ecoaqua.ro',
                'RoSal': 'https://www.rosal.ro',
                'Salubris': 'https://www.salubris.ro',
                'Comprest': 'https://www.comprest.ro',
                
                // Bănci
                'BCR': 'https://www.bcr.ro',
                'BRD': 'https://www.brd.ro',
                'ING Bank': 'https://www.ing.ro',
                'Raiffeisen': 'https://www.raiffeisen.ro',
                'UniCredit': 'https://www.unicredit.ro',
                'Banca Transilvania': 'https://www.btrl.ro',
                'CEC Bank': 'https://www.cec.ro',
                'Alpha Bank': 'https://www.alphabank.ro',
                
                // Întreținere
                'SmartBill': 'https://www.smartbill.ro',
                'Mea Casa': 'https://www.online.meacasa.ro',
                'AdminPlus': 'https://www.adminplus.ro',
                'Casa Verde': 'https://www.casaverde.ro',
                'Domino Admin': 'https://www.dominoadmin.ro',
                'Urbis Management': 'https://www.urbismanagement.ro',
                'Confort Residence': 'https://www.confortresidence.ro',
                'Total Admin': 'https://www.totaladmin.ro'
            };

            const url = companyURLs[provider];
            
            if (url) {
                // Deschide direct site-ul oficial
                window.open(url, '_blank');
            } else {
                // Fallback - modal intern pentru plată
                currentProvider = provider;
                currentService = service;
                document.getElementById('modalTitle').textContent = `Plată ${provider}`;
                document.getElementById('modalProvider').textContent = service;
                document.getElementById('paymentModal').style.display = 'flex';
                
                setTimeout(() => {
                    document.getElementById('contractNumber').focus();
                }, 100);
            }
        }

        function toggleProviders(button, category) {
            const categoryElement = button.parentElement;
            const hiddenProviders = categoryElement.querySelectorAll('.hidden-providers');
            const isExpanded = button.textContent === 'Vezi mai puține';

            if (isExpanded) {
                // Ascunde providerii suplimentari
                hiddenProviders.forEach(provider => {
                    provider.classList.remove('show');
                });
                button.textContent = 'Vezi mai multe';
            } else {
                // Arată providerii suplimentari
                hiddenProviders.forEach(provider => {
                    provider.classList.add('show');
                });
                button.textContent = 'Vezi mai puține';
            }
        }

        function closeModal() {
            document.getElementById('paymentModal').style.display = 'none';
            // Resetează formul
            document.getElementById('contractNumber').value = '';
            document.getElementById('amount').value = '';
            document.getElementById('description').value = '';
        }

        function processPayment() {
            const contractNumber = document.getElementById('contractNumber').value;
            const amount = document.getElementById('amount').value;
            
            if (!contractNumber || !amount) {
                alert('Te rog completează numărul contractului și suma!');
                return;
            }

            if (parseFloat(amount) > 2450.75) {
                alert('Fonduri insuficiente! Te rog adaugă fonduri în cont.');
                return;
            }

            // Simulează procesarea plății
            alert(`✅ Plata de ${amount} LEI către ${currentProvider} a fost procesată cu succes!\n\n📧 Vei primi confirmarea pe email în câteva minute.`);
            
            // Actualizează soldul (simulat)
            const currentBalance = 2450.75;
            const newBalance = (currentBalance - parseFloat(amount)).toFixed(2);
            document.querySelector('.wallet-balance').textContent = newBalance + ' LEI';
            
            closeModal();
        }

        function showAddFunds() {
            alert('🏦 Opțiuni de adăugare fonduri:\n\n• Card bancar\n• Transfer bancar\n• PayPal\n• Crypto\n\nVei fi redirecționat către pagina de plăți...');
        }

        // Închide modalul la click pe background
        document.getElementById('paymentModal').addEventListener('click', function(e) {
            if (e.target === this) {
                closeModal();
            }
        });

        // Suport pentru tasta ESC
        document.addEventListener('keydown', function(e) {
            if (e.key === 'Escape' && document.getElementById('paymentModal').style.display === 'flex') {
                closeModal();
            }
        });

        // Animații la scroll (opțional)
        window.addEventListener('scroll', function() {
            const categories = document.querySelectorAll('.category');
            categories.forEach(category => {
                const rect = category.getBoundingClientRect();
                if (rect.top < window.innerHeight - 100) {
                    category.style.opacity = '1';
                    category.style.transform = 'translateY(0)';
                }
            });
        });
    </script>

</body>
</html>

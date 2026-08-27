<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema Contable</title>
    <!-- Bootstrap 5 CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body { background-color: #f8f9fa; }
        .section-page { display: none; }
        .section-page.active { display: block; }
    </style>
</head>
<body>

    <!-- Navegación -->
    <nav class="navbar navbar-expand-lg navbar-dark bg-primary mb-4">
        <div class="container">
            <a class="navbar-brand fw-bold" href="#">Sistema Contable</a>
            <div class="collapse navbar-collapse">
                <ul class="navbar-nav me-auto">
                    <li class="nav-item"><a class="nav-link active" href="#" onclick="showSection('dashboard')">Dashboard</a></li>
                    <li class="nav-item"><a class="nav-link" href="#" onclick="showSection('clientes')">Clientes</a></li>
                    <li class="nav-item"><a class="nav-link" href="#" onclick="showSection('proveedores')">Proveedores</a></li>
                    <li class="nav-item"><a class="nav-link" href="#" onclick="showSection('ventas')">Ventas</a></li>
                    <li class="nav-item"><a class="nav-link" href="#" onclick="showSection('compras')">Compras</a></li>
                </ul>
            </div>
        </div>
    </nav>

    <div class="container">

        <!-- DASHBOARD -->
        <div id="dashboard" class="section-page active">
            <h2 class="mb-4">Resumen Contable</h2>
            <div class="row mb-4">
                <div class="col-md-4">
                    <div class="card text-white bg-success">
                        <div class="card-body">
                            <h5 class="card-title">Ventas Totales (Ingresos)</h5>
                            <h3 id="dash-ingresos">$0.00</h3>
                        </div>
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="card text-white bg-danger">
                        <div class="card-body">
                            <h5 class="card-title">Compras Totales (Egresos)</h5>
                            <h3 id="dash-egresos">$0.00</h3>
                        </div>
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="card text-white bg-primary" id="card-balance">
                        <div class="card-body">
                            <h5 class="card-title">Balance Neto</h5>
                            <h3 id="dash-balance">$0.00</h3>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- MÓDULO CLIENTES -->
        <div id="clientes" class="section-page">
            <h2>Gestión de Clientes</h2>
            <div class="card my-3 p-3">
                <form id="form-cliente">
                    <div class="row g-2">
                        <div class="col-md-3"><input type="text" id="cli-nombre" class="form-control" placeholder="Nombre completo" required></div>
                        <div class="col-md-3"><input type="text" id="cli-id" class="form-control" placeholder="RFC/NIF/DNI" required></div>
                        <div class="col-md-3"><input type="text" id="cli-tel" class="form-control" placeholder="Teléfono"></div>
                        <div class="col-md-3"><input type="email" id="cli-email" class="form-control" placeholder="Correo"></div>
                    </div>
                    <button class="btn btn-success mt-3" type="submit">Agregar Cliente</button>
                </form>
            </div>
            <table class="table table-bordered bg-white">
                <thead><tr><th>Nombre</th><th>Identificación</th><th>Teléfono</th><th>Email</th></tr></thead>
                <tbody id="tabla-clientes"></tbody>
            </table>
        </div>

        <!-- MÓDULO PROVEEDORES -->
        <div id="proveedores" class="section-page">
            <h2>Gestión de Proveedores</h2>
            <div class="card my-3 p-3">
                <form id="form-proveedor">
                    <div class="row g-2">
                        <div class="col-md-3"><input type="text" id="prov-nombre" class="form-control" placeholder="Razón Social" required></div>
                        <div class="col-md-3"><input type="text" id="prov-id" class="form-control" placeholder="RFC/NIF" required></div>
                        <div class="col-md-3"><input type="text" id="prov-tel" class="form-control" placeholder="Teléfono"></div>
                        <div class="col-md-3"><input type="email" id="prov-email" class="form-control" placeholder="Correo"></div>
                    </div>
                    <button class="btn btn-primary mt-3" type="submit">Agregar Proveedor</button>
                </form>
            </div>
            <table class="table table-bordered bg-white">
                <thead><tr><th>Empresa</th><th>Identificación</th><th>Teléfono</th><th>Email</th></tr></thead>
                <tbody id="tabla-proveedores"></tbody>
            </table>
        </div>

        <!-- MÓDULO VENTAS -->
        <div id="ventas" class="section-page">
            <h2>Registro de Ventas (Ingresos)</h2>
            <div class="card my-3 p-3">
                <form id="form-venta">
                    <div class="row g-2">
                        <div class="col-md-4">
                            <select id="venta-cliente" class="form-control" required>
                                <option value="">Seleccione Cliente</option>
                            </select>
                        </div>
                        <div class="col-md-5"><input type="text" id="venta-concepto" class="form-control" placeholder="Concepto/Descripción" required></div>
                        <div class="col-md-3"><input type="number" step="0.01" id="venta-monto" class="form-control" placeholder="Monto Total" required></div>
                    </div>
                    <button class="btn btn-success mt-3" type="submit">Registrar Venta</button>
                </form>
            </div>
            <table class="table table-striped bg-white">
                <thead><tr><th>Cliente</th><th>Concepto</th><th>Monto</th></tr></thead>
                <tbody id="tabla-ventas"></tbody>
            </table>
        </div>

        <!-- MÓDULO COMPRAS -->
        <div id="compras" class="section-page">
            <h2>Registro de Compras (Egresos)</h2>
            <div class="card my-3 p-3">
                <form id="form-compra">
                    <div class="row g-2">
                        <div class="col-md-4">
                            <select id="compra-proveedor" class="form-control" required>
                                <option value="">Seleccione Proveedor</option>
                            </select>
                        </div>
                        <div class="col-md-5"><input type="text" id="compra-concepto" class="form-control" placeholder="Concepto/Descripción" required></div>
                        <div class="col-md-3"><input type="number" step="0.01" id="compra-monto" class="form-control" placeholder="Monto Total" required></div>
                    </div>
                    <button class="btn btn-danger mt-3" type="submit">Registrar Compra</button>
                </form>
            </div>
            <table class="table table-striped bg-white">
                <thead><tr><th>Proveedor</th><th>Concepto</th><th>Monto</th></tr></thead>
                <tbody id="tabla-compras"></tbody>
            </table>
        </div>

    </div>

    <!-- JavaScript del Sistema -->
    <script>
        const db = { clientes: [], proveedores: [], ventas: [], compras: [] };

        function showSection(sectionId) {
            document.querySelectorAll('.section-page').forEach(sec => sec.classList.remove('active'));
            document.getElementById(sectionId).classList.add('active');
        }

        // Agregar Cliente
        document.getElementById('form-cliente').addEventListener('submit', (e) => {
            e.preventDefault();
            const cliente = {
                nombre: document.getElementById('cli-nombre').value,
                id: document.getElementById('cli-id').value,
                tel: document.getElementById('cli-tel').value,
                email: document.getElementById('cli-email').value
            };
            db.clientes.push(cliente);
            renderClientes();
            e.target.reset();
        });

        // Agregar Proveedor
        document.getElementById('form-proveedor').addEventListener('submit', (e) => {
            e.preventDefault();
            const proveedor = {
                nombre: document.getElementById('prov-nombre').value,
                id: document.getElementById('prov-id').value,
                tel: document.getElementById('prov-tel').value,
                email: document.getElementById('prov-email').value
            };
            db.proveedores.push(proveedor);
            renderProveedores();
            e.target.reset();
        });

        // Registrar Venta
        document.getElementById('form-venta').addEventListener('submit', (e) => {
            e.preventDefault();
            const venta = {
                cliente: document.getElementById('venta-cliente').value,
                concepto: document.getElementById('venta-concepto').value,
                monto: parseFloat(document.getElementById('venta-monto').value)
            };
            db.ventas.push(venta);
            renderVentas();
            updateDashboard();
            e.target.reset();
        });

        // Registrar Compra
        document.getElementById('form-compra').addEventListener('submit', (e) => {
            e.preventDefault();
            const compra = {
                proveedor: document.getElementById('compra-proveedor').value,
                concepto: document.getElementById('compra-concepto').value,
                monto: parseFloat(document.getElementById('compra-monto').value)
            };
            db.compras.push(compra);
            renderCompras();
            updateDashboard();
            e.target.reset();
        });

        function renderClientes() {
            const tbody = document.getElementById('tabla-clientes');
            const selectVenta = document.getElementById('venta-cliente');
            tbody.innerHTML = '';
            selectVenta.innerHTML = '<option value="">Seleccione Cliente</option>';
            db.clientes.forEach(c => {
                tbody.innerHTML += `<tr><td>${c.nombre}</td><td>${c.id}</td><td>${c.tel}</td><td>${c.email}</td></tr>`;
                selectVenta.innerHTML += `<option value="${c.nombre}">${c.nombre}</option>`;
            });
        }

        function renderProveedores() {
            const tbody = document.getElementById('tabla-proveedores');
            const selectCompra = document.getElementById('compra-proveedor');
            tbody.innerHTML = '';
            selectCompra.innerHTML = '<option value="">Seleccione Proveedor</option>';
            db.proveedores.forEach(p => {
                tbody.innerHTML += `<tr><td>${p.nombre}</td><td>${p.id}</td><td>${p.tel}</td><td>${p.email}</td></tr>`;
                selectCompra.innerHTML += `<option value="${p.nombre}">${p.nombre}</option>`;
            });
        }

        function renderVentas() {
            const tbody = document.getElementById('tabla-ventas');
            tbody.innerHTML = '';
            db.ventas.forEach(v => {
                tbody.innerHTML += `<tr><td>${v.cliente}</td><td>${v.concepto}</td><td>$${v.monto.toFixed(2)}</td></tr>`;
            });
        }

        function renderCompras() {
            const tbody = document.getElementById('tabla-compras');
            tbody.innerHTML = '';
            db.compras.forEach(c => {
                tbody.innerHTML += `<tr><td>${c.proveedor}</td><td>${c.concepto}</td><td>$${c.monto.toFixed(2)}</td></tr>`;
            });
        }

        function updateDashboard() {
            const totalVentas = db.ventas.reduce((sum, v) => sum + v.monto, 0);
            const totalCompras = db.compras.reduce((sum, c) => sum + c.monto, 0);
            const balance = totalVentas - totalCompras;

            document.getElementById('dash-ingresos').innerText = `$${totalVentas.toFixed(2)}`;
            document.getElementById('dash-egresos').innerText = `$${totalCompras.toFixed(2)}`;
            document.getElementById('dash-balance').innerText = `$${balance.toFixed(2)}`;
        }
    </script>
</body>
</html>

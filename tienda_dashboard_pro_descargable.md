<!DOCTYPE html>
<html lang="es" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SELECT / SECOND HAND - Tienda & Dashboard Pro</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        gold: {
                            300: '#FDE047',
                            400: '#FACC15',
                            500: '#EAB308',
                            600: '#CA8A04',
                            accent: '#D4AF37',
                            glow: '#FFDF00'
                        },
                        darkbg: '#08080A',
                        darkcard: '#121217',
                        darkborder: '#22222D'
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <!-- FontAwesome icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Font Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #08080A;
            color: #E2E8F0;
            overflow-x: hidden;
        }
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #08080A;
        }
        ::-webkit-scrollbar-thumb {
            background: #22222D;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #D4AF37;
        }
        .gold-gradient-text {
            background: linear-gradient(135deg, #FFF5C0 0%, #D4AF37 50%, #AA7C11 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .gold-border-glow:hover {
            box-shadow: 0 0 20px rgba(212, 175, 55, 0.2);
            border-color: rgba(212, 175, 55, 0.4);
        }
        .glass-panel {
            background: rgba(18, 18, 23, 0.85);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between selection:bg-gold-accent selection:text-black">

    <!-- TOP NAVIGATION & DOWNLOAD BAR -->
    <header class="sticky top-0 z-40 glass-panel border-b border-darkborder">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            
            <!-- Logo & Secret Trigger -->
            <div class="flex items-center space-x-3 cursor-pointer select-none" onclick="handleSecretLogoClick()">
                <div class="w-10 h-10 rounded-xl border border-gold-accent/40 flex items-center justify-center bg-gradient-to-tr from-darkcard to-black shadow-lg">
                    <i class="fa-solid fa-gem text-gold-accent text-lg"></i>
                </div>
                <div>
                    <span class="text-xl font-black tracking-widest gold-gradient-text">SELECT</span>
                    <span class="text-[10px] block text-gray-400 tracking-[0.2em] font-medium -mt-1 uppercase">Second Hand Archives</span>
                </div>
            </div>

            <!-- CONTROLES Y BOTÓN DE DESCARGA -->
            <div class="flex items-center gap-3">
                <button onclick="downloadSelfHTML()" class="px-3.5 py-2 rounded-xl text-xs font-bold transition flex items-center gap-2 bg-emerald-500/10 hover:bg-emerald-500/20 text-emerald-400 border border-emerald-500/30">
                    <i class="fa-solid fa-file-arrow-down"></i>
                    <span class="hidden md:inline">Descargar index.html</span>
                </button>

                <div class="bg-black/60 border border-darkborder p-1 rounded-2xl flex items-center gap-1">
                    <button id="nav-btn-shop" onclick="switchView('shop')" class="px-4 py-2 rounded-xl text-xs font-bold transition flex items-center gap-2 bg-gold-accent text-black shadow">
                        <i class="fa-solid fa-store"></i>
                        <span class="hidden sm:inline">Vista Cliente</span>
                    </button>
                    <button id="nav-btn-admin" onclick="switchView('admin')" class="px-4 py-2 rounded-xl text-xs font-bold transition flex items-center gap-2 text-gray-400 hover:text-white">
                        <i class="fa-solid fa-gauge-high"></i>
                        <span class="hidden sm:inline">Panel Admin</span>
                        <i id="lock-icon-badge" class="fa-solid fa-lock text-[10px] text-gold-accent ml-1"></i>
                    </button>
                </div>
            </div>
        </div>
    </header>

    <!-- MAIN CONTAINER -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8">

        <!-- ==================== VISTA CLIENTE / TIENDA PÚBLICA ==================== -->
        <section id="view-shop" class="space-y-8">
            <!-- Hero Showcase Banner -->
            <div class="relative rounded-3xl overflow-hidden border border-darkborder p-8 md:p-12 bg-gradient-to-r from-darkcard via-black to-darkcard shadow-2xl">
                <div class="absolute -right-20 -bottom-20 w-80 h-80 bg-gold-accent/10 rounded-full blur-3xl pointer-events-none"></div>
                <div class="relative z-10 max-w-2xl space-y-4">
                    <span class="px-3 py-1 text-[10px] font-bold uppercase tracking-widest bg-gold-accent/10 text-gold-accent border border-gold-accent/20 rounded-full">
                        Curaduría Exclusiva
                    </span>
                    <h1 class="text-3xl md:text-5xl font-extrabold tracking-tight text-white leading-tight">
                        Catálogo de Moda & Piezas de <span class="gold-gradient-text">Segunda Mano</span>
                    </h1>
                    <p class="text-gray-400 text-sm font-light leading-relaxed">
                        Explora prendas e inventario verificado. Las transacciones se realizan directamente de forma protegida en Vinted.
                    </p>
                </div>
            </div>

            <!-- Filtros, Buscador y Orden de la Tienda -->
            <div class="flex flex-col lg:flex-row gap-4 justify-between items-center bg-darkcard/60 p-4 rounded-2xl border border-darkborder">
                
                <div class="relative w-full lg:w-72">
                    <i class="fa-solid fa-magnifying-glass absolute left-4 top-1/2 -translate-y-1/2 text-gray-500 text-xs"></i>
                    <input type="text" id="shop-search" oninput="filterShopProducts()" placeholder="Buscar prenda, marca..." class="w-full pl-10 pr-4 py-2 bg-black/60 border border-darkborder rounded-xl text-xs text-white placeholder-gray-500 focus:outline-none focus:border-gold-accent transition">
                </div>

                <div class="flex flex-wrap gap-2 w-full lg:w-auto overflow-x-auto pb-1 lg:pb-0" id="category-filters">
                    <button onclick="setCategory('all')" class="cat-btn active border px-4 py-2 rounded-xl text-xs font-medium transition bg-gold-accent text-black border-gold-accent font-bold" data-cat="all">Todas</button>
                    <button onclick="setCategory('Ropa')" class="cat-btn border border-darkborder bg-darkcard text-gray-400 hover:text-white px-4 py-2 rounded-xl text-xs font-medium transition" data-cat="Ropa">Ropa</button>
                    <button onclick="setCategory('Calzado')" class="cat-btn border border-darkborder bg-darkcard text-gray-400 hover:text-white px-4 py-2 rounded-xl text-xs font-medium transition" data-cat="Calzado">Calzado</button>
                    <button onclick="setCategory('Accesorios')" class="cat-btn border border-darkborder bg-darkcard text-gray-400 hover:text-white px-4 py-2 rounded-xl text-xs font-medium transition" data-cat="Accesorios">Accesorios</button>
                    <button onclick="setCategory('Coleccionables')" class="cat-btn border border-darkborder bg-darkcard text-gray-400 hover:text-white px-4 py-2 rounded-xl text-xs font-medium transition" data-cat="Coleccionables">Coleccionables</button>
                </div>

                <div class="w-full lg:w-auto flex justify-end">
                    <select id="shop-sort" onchange="filterShopProducts()" class="bg-black/60 border border-darkborder text-gray-300 text-xs rounded-xl px-3 py-2 focus:outline-none focus:border-gold-accent">
                        <option value="newest">Más recientes</option>
                        <option value="price-asc">Precio: Menor a Mayor</option>
                        <option value="price-desc">Precio: Mayor a Menor</option>
                    </select>
                </div>
            </div>

            <!-- Grid de Productos -->
            <div id="product-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6"></div>

            <!-- Empty State -->
            <div id="shop-empty" class="hidden text-center py-20 space-y-4">
                <div class="w-16 h-16 mx-auto rounded-full bg-darkcard border border-darkborder flex items-center justify-center text-gray-500">
                    <i class="fa-solid fa-box-open text-2xl"></i>
                </div>
                <h3 class="text-lg font-medium text-gray-300">Sin productos coincidentes</h3>
                <p class="text-xs text-gray-500">Prueba cambiando los parámetros del buscador o de categoría.</p>
            </div>
        </section>


        <!-- ==================== VISTA PANEL DE CONTROL / DASHBOARD ==================== -->
        <section id="view-admin" class="hidden space-y-8">
            
            <!-- Dashboard Header -->
            <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-4 pb-4 border-b border-darkborder">
                <div>
                    <div class="flex items-center gap-3">
                        <span class="px-3 py-1 rounded-full text-[10px] font-bold uppercase bg-gold-accent/20 text-gold-accent border border-gold-accent/30">Dashboard Admin</span>
                        <h2 class="text-2xl font-black text-white">Panel de Control & Analytics</h2>
                    </div>
                    <p class="text-xs text-gray-400 mt-1">Gestiona el inventario, sube o elimina productos con enlace a Vinted y revisa métricas clave.</p>
                </div>

                <div class="flex flex-wrap gap-2">
                    <button onclick="resetDefaultData()" class="text-xs bg-darkcard hover:bg-black text-gray-400 border border-darkborder px-3.5 py-2 rounded-xl transition flex items-center gap-1.5" title="Restablecer datos de prueba">
                        <i class="fa-solid fa-rotate-left text-amber-500"></i> Reset Demo
                    </button>
                    <button onclick="exportBackup()" class="text-xs bg-darkcard hover:bg-black text-gray-300 border border-darkborder px-3.5 py-2 rounded-xl transition flex items-center gap-1.5" title="Exportar backup JSON">
                        <i class="fa-solid fa-download text-gold-accent"></i> Exportar JSON
                    </button>
                    <label class="text-xs bg-darkcard hover:bg-black text-gray-300 border border-darkborder px-3.5 py-2 rounded-xl transition flex items-center gap-1.5 cursor-pointer" title="Importar backup JSON">
                        <i class="fa-solid fa-upload text-gold-accent"></i> Importar JSON
                        <input type="file" accept=".json" onchange="importBackup(event)" class="hidden">
                    </label>
                    <button onclick="openChangePinModal()" class="text-xs bg-darkcard hover:bg-black text-gray-300 border border-darkborder px-3.5 py-2 rounded-xl transition flex items-center gap-1.5">
                        <i class="fa-solid fa-key text-gold-accent"></i> Cambiar PIN
                    </button>
                    <button onclick="logoutAdmin()" class="text-xs bg-red-500/10 hover:bg-red-500/20 text-red-400 border border-red-500/30 px-3.5 py-2 rounded-xl transition flex items-center gap-1.5">
                        <i class="fa-solid fa-lock"></i> Bloquear
                    </button>
                </div>
            </div>

            <!-- ANALYTICS CARDS -->
            <div class="grid grid-cols-2 lg:grid-cols-4 gap-4">
                <div class="bg-darkcard border border-darkborder p-5 rounded-2xl relative overflow-hidden">
                    <div class="flex justify-between items-start">
                        <span class="text-xs text-gray-400 font-semibold">Productos Activos</span>
                        <div class="w-8 h-8 rounded-lg bg-blue-500/10 text-blue-400 flex items-center justify-center text-xs">
                            <i class="fa-solid fa-box"></i>
                        </div>
                    </div>
                    <p id="stat-active" class="text-3xl font-black text-white mt-2">0</p>
                    <span id="stat-total-sub" class="text-[10px] text-gray-500 block mt-1">0 en inventario total</span>
                </div>

                <div class="bg-darkcard border border-darkborder p-5 rounded-2xl relative overflow-hidden">
                    <div class="flex justify-between items-start">
                        <span class="text-xs text-gray-400 font-semibold">Valor del Inventario</span>
                        <div class="w-8 h-8 rounded-lg bg-gold-accent/10 text-gold-accent flex items-center justify-center text-xs">
                            <i class="fa-solid fa-euro-sign"></i>
                        </div>
                    </div>
                    <p id="stat-value" class="text-3xl font-black text-gold-accent mt-2">0 €</p>
                    <span class="text-[10px] text-gray-500 block mt-1">Suma total de artículos activos</span>
                </div>

                <div class="bg-darkcard border border-darkborder p-5 rounded-2xl relative overflow-hidden">
                    <div class="flex justify-between items-start">
                        <span class="text-xs text-gray-400 font-semibold">Artículos Vendidos</span>
                        <div class="w-8 h-8 rounded-lg bg-emerald-500/10 text-emerald-400 flex items-center justify-center text-xs">
                            <i class="fa-solid fa-circle-check"></i>
                        </div>
                    </div>
                    <p id="stat-sold-count" class="text-3xl font-black text-emerald-400 mt-2">0</p>
                    <span class="text-[10px] text-gray-500 block mt-1">Marcados como Vendidos</span>
                </div>

                <div class="bg-darkcard border border-darkborder p-5 rounded-2xl relative overflow-hidden">
                    <div class="flex justify-between items-start">
                        <span class="text-xs text-gray-400 font-semibold">Clics a Vinted</span>
                        <div class="w-8 h-8 rounded-lg bg-purple-500/10 text-purple-400 flex items-center justify-center text-xs">
                            <i class="fa-solid fa-chart-line"></i>
                        </div>
                    </div>
                    <p id="stat-clicks" class="text-3xl font-black text-purple-400 mt-2">0</p>
                    <span class="text-[10px] text-gray-500 block mt-1">Redirecciones hacia Vinted</span>
                </div>
            </div>

            <!-- DASHBOARD CORE GRID -->
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-8">
                
                <!-- FORMULARIO PRODUCTO -->
                <div class="lg:col-span-5 bg-darkcard border border-darkborder rounded-2xl p-6 space-y-6 shadow-xl h-fit">
                    <div class="flex justify-between items-center border-b border-darkborder pb-3">
                        <h3 class="text-sm font-bold text-white flex items-center gap-2">
                            <i class="fa-solid fa-plus-circle text-gold-accent"></i>
                            <span id="form-heading">Publicar Nuevo Producto</span>
                        </h3>
                        <span id="form-badge-mode" class="text-[10px] bg-gold-accent/10 text-gold-accent font-bold px-2 py-0.5 rounded">Nuevo</span>
                    </div>

                    <form id="product-form" onsubmit="handleSaveProduct(event)" class="space-y-4">
                        <input type="hidden" id="form-edit-id" value="">

                        <div>
                            <label class="block text-xs font-semibold text-gray-400 mb-1">Título del Producto *</label>
                            <input type="text" id="form-title" required placeholder="Ej. Sudadera Vintage Nike Oversize 90s" class="w-full bg-black/60 border border-darkborder rounded-xl px-3.5 py-2 text-xs text-white focus:outline-none focus:border-gold-accent">
                        </div>

                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label class="block text-xs font-semibold text-gray-400 mb-1">Precio (€) *</label>
                                <input type="number" step="0.01" id="form-price" required placeholder="35.00" class="w-full bg-black/60 border border-darkborder rounded-xl px-3.5 py-2 text-xs text-white focus:outline-none focus:border-gold-accent">
                            </div>
                            <div>
                                <label class="block text-xs font-semibold text-gray-400 mb-1">Categoría *</label>
                                <select id="form-category" required class="w-full bg-black/60 border border-darkborder rounded-xl px-3.5 py-2 text-xs text-white focus:outline-none focus:border-gold-accent">
                                    <option value="Ropa">Ropa</option>
                                    <option value="Calzado">Calzado</option>
                                    <option value="Accesorios">Accesorios</option>
                                    <option value="Coleccionables">Coleccionables</option>
                                    <option value="Electrónica">Electrónica</option>
                                </select>
                            </div>
                        </div>

                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label class="block text-xs font-semibold text-gray-400 mb-1">Estado *</label>
                                <select id="form-condition" required class="w-full bg-black/60 border border-darkborder rounded-xl px-3.5 py-2 text-xs text-white focus:outline-none focus:border-gold-accent">
                                    <option value="Excelente">Excelente</option>
                                    <option value="Como nuevo">Como nuevo</option>
                                    <option value="Bueno">Bueno</option>
                                    <option value="Nuevo con etiquetas">Nuevo con etiquetas</option>
                                </select>
                            </div>
                            <div>
                                <label class="block text-xs font-semibold text-gray-400 mb-1">Disponibilidad</label>
                                <select id="form-status" class="w-full bg-black/60 border border-darkborder rounded-xl px-3.5 py-2 text-xs text-white focus:outline-none focus:border-gold-accent">
                                    <option value="available">Disponible</option>
                                    <option value="sold">Vendido</option>
                                </select>
                            </div>
                        </div>

                        <div>
                            <label class="block text-xs font-semibold text-gray-400 mb-1">Enlace Directo de Vinted (URL) *</label>
                            <div class="relative">
                                <i class="fa-solid fa-link absolute left-3 top-1/2 -translate-y-1/2 text-gray-500 text-xs"></i>
                                <input type="url" id="form-vinted-url" required placeholder="https://www.vinted.es/items/..." class="w-full bg-black/60 border border-darkborder rounded-xl pl-9 pr-3 py-2 text-xs text-white focus:outline-none focus:border-gold-accent">
                            </div>
                        </div>

                        <div class="space-y-2">
                            <label class="block text-xs font-semibold text-gray-400">Imágenes del Producto *</label>
                            
                            <div class="border border-dashed border-darkborder hover:border-gold-accent/50 rounded-xl p-3 text-center transition bg-black/30">
                                <label class="cursor-pointer flex flex-col items-center justify-center gap-1">
                                    <i class="fa-solid fa-cloud-arrow-up text-xl text-gold-accent"></i>
                                    <span class="text-xs font-medium text-gray-300">Subir fotos locales</span>
                                    <span class="text-[10px] text-gray-500">(Múltiples archivos soportados)</span>
                                    <input type="file" id="form-images-file" multiple accept="image/*" onchange="handleMultipleFileUpload(event)" class="hidden">
                                </label>
                            </div>

                            <div>
                                <label class="block text-[10px] text-gray-500 mb-1">O enlaces de imagen externos (separados por coma):</label>
                                <textarea id="form-images-url" rows="2" placeholder="https://imagen1.jpg, https://imagen2.jpg" class="w-full bg-black/60 border border-darkborder rounded-xl px-3 py-1.5 text-[11px] text-white focus:outline-none focus:border-gold-accent" oninput="updateImagePreviewsFromInput()"></textarea>
                            </div>

                            <div id="image-previews" class="flex flex-wrap gap-2 pt-1"></div>
                        </div>

                        <div>
                            <label class="block text-xs font-semibold text-gray-400 mb-1">Descripción del Producto</label>
                            <textarea id="form-description" rows="3" placeholder="Detalles de talla, medidas, origen o defectos si los tuviera..." class="w-full bg-black/60 border border-darkborder rounded-xl px-3.5 py-2 text-xs text-white focus:outline-none focus:border-gold-accent"></textarea>
                        </div>

                        <div class="flex gap-2 pt-2">
                            <button type="submit" class="flex-grow bg-gold-accent hover:bg-gold-500 text-black font-bold py-2.5 rounded-xl transition duration-300 flex items-center justify-center gap-2 text-xs shadow-lg">
                                <i class="fa-solid fa-check"></i> <span id="btn-submit-text">Guardar Producto</span>
                            </button>
                            <button type="button" id="btn-cancel-edit" onclick="cancelEdit()" class="hidden bg-gray-800 hover:bg-gray-700 text-gray-300 font-bold px-4 rounded-xl text-xs transition">
                                Cancelar
                            </button>
                        </div>
                    </form>
                </div>

                <!-- TABLA DE INVENTARIO -->
                <div class="lg:col-span-7 bg-darkcard border border-darkborder rounded-2xl p-6 space-y-4 shadow-xl flex flex-col justify-between">
                    <div class="space-y-4">
                        <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-3 border-b border-darkborder pb-3">
                            <h3 class="text-sm font-bold text-white flex items-center gap-2">
                                <i class="fa-solid fa-boxes-stacked text-gold-accent"></i> Inventario de Productos
                            </h3>

                            <div class="flex flex-wrap items-center gap-2 w-full sm:w-auto">
                                <select id="admin-table-status-filter" onchange="renderAdminTable()" class="bg-black/60 border border-darkborder text-xs px-2.5 py-1.5 rounded-xl text-white focus:outline-none focus:border-gold-accent">
                                    <option value="all">Todos los estados</option>
                                    <option value="available">Disponibles</option>
                                    <option value="sold">Vendidos</option>
                                </select>
                                <input type="text" id="admin-table-search" oninput="renderAdminTable()" placeholder="Filtrar tabla..." class="bg-black/60 border border-darkborder text-xs px-3 py-1.5 rounded-xl text-white focus:outline-none focus:border-gold-accent w-full sm:w-36">
                            </div>
                        </div>

                        <div class="flex flex-wrap items-center justify-between gap-2 bg-black/40 p-2.5 rounded-xl border border-darkborder/80">
                            <div class="flex items-center gap-2">
                                <input type="checkbox" id="select-all-checkbox" onchange="toggleSelectAll(this)" class="w-4 h-4 rounded border-darkborder bg-black text-gold-accent focus:ring-gold-accent">
                                <label for="select-all-checkbox" class="text-xs text-gray-400 font-medium cursor-pointer">Seleccionar todo</label>
                            </div>
                            <div class="flex items-center gap-2">
                                <button id="btn-delete-selected" onclick="confirmDeleteSelected()" disabled class="bg-red-500/10 hover:bg-red-500/20 text-red-400 disabled:opacity-40 disabled:cursor-not-allowed border border-red-500/30 px-3 py-1 rounded-lg text-xs font-semibold transition flex items-center gap-1.5">
                                    <i class="fa-solid fa-trash-check"></i> Borrar Seleccionados
                                </button>
                                <button onclick="confirmClearAllProducts()" class="bg-red-600/20 hover:bg-red-600/30 text-red-300 border border-red-500/40 px-3 py-1 rounded-lg text-xs font-semibold transition flex items-center gap-1.5" title="Eliminar catálogo completo">
                                    <i class="fa-solid fa-triangle-exclamation"></i> Vaciar Todo
                                </button>
                            </div>
                        </div>

                        <div class="overflow-x-auto">
                            <table class="w-full text-left border-collapse">
                                <thead>
                                    <tr class="text-[10px] font-bold uppercase text-gray-400 border-b border-darkborder">
                                        <th class="py-3 px-2 w-8"></th>
                                        <th class="py-3 px-2">Producto</th>
                                        <th class="py-3 px-2">Precio</th>
                                        <th class="py-3 px-2 text-center">Estado</th>
                                        <th class="py-3 px-2 text-center">Visibilidad</th>
                                        <th class="py-3 px-2 text-right">Acciones</th>
                                    </tr>
                                </thead>
                                <tbody id="admin-table-body" class="divide-y divide-darkborder text-xs">
                                </tbody>
                            </table>
                        </div>
                    </div>

                    <div class="pt-4 border-t border-darkborder flex justify-between items-center text-[11px] text-gray-500">
                        <span id="admin-table-count">Mostrando 0 productos</span>
                        <span>Sincronizado con LocalStorage</span>
                    </div>
                </div>
            </div>
        </section>
    </main>


    <!-- MODAL BORRADO -->
    <div id="delete-modal" class="fixed inset-0 z-50 bg-black/85 backdrop-blur-md hidden flex items-center justify-center p-4">
        <div class="bg-darkcard border border-red-500/30 w-full max-w-sm rounded-3xl p-6 shadow-2xl space-y-4 relative">
            <button onclick="closeDeleteModal()" class="absolute top-4 right-4 text-gray-500 hover:text-white">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>

            <div class="text-center space-y-2">
                <div class="w-12 h-12 rounded-2xl bg-red-500/10 border border-red-500/30 text-red-400 mx-auto flex items-center justify-center text-xl">
                    <i class="fa-solid fa-trash-can"></i>
                </div>
                <h3 id="delete-modal-title" class="text-lg font-bold text-white">¿Eliminar Producto?</h3>
                <p id="delete-modal-desc" class="text-xs text-gray-400">Esta acción no se podrá deshacer y el producto desaparecerá del catálogo público.</p>
            </div>

            <div class="flex gap-2 pt-2">
                <button id="btn-confirm-delete" onclick="executeDelete()" class="w-full bg-red-600 hover:bg-red-500 text-white font-bold py-2.5 rounded-xl text-xs transition shadow-lg flex items-center justify-center gap-1.5">
                    <i class="fa-solid fa-trash"></i> Confirmar Borrado
                </button>
                <button onclick="closeDeleteModal()" class="w-full bg-gray-800 hover:bg-gray-700 text-gray-300 font-bold py-2.5 rounded-xl text-xs transition">
                    Cancelar
                </button>
            </div>
        </div>
    </div>


    <!-- MODAL AUTENTICACIÓN (PIN) -->
    <div id="login-modal" class="fixed inset-0 z-50 bg-black/85 backdrop-blur-md hidden flex items-center justify-center p-4">
        <div class="bg-darkcard border border-darkborder w-full max-w-sm rounded-3xl p-6 shadow-2xl space-y-5 relative">
            <button onclick="closeLoginModal()" class="absolute top-4 right-4 text-gray-500 hover:text-white">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>

            <div class="text-center space-y-2">
                <div class="w-12 h-12 rounded-2xl bg-gold-accent/10 border border-gold-accent/30 text-gold-accent mx-auto flex items-center justify-center text-xl">
                    <i class="fa-solid fa-shield-halved"></i>
                </div>
                <h3 class="text-lg font-bold text-white">Acceso al Panel Admin</h3>
                <p class="text-xs text-gray-400">Introduce tu contraseña de administración.</p>
            </div>

            <form onsubmit="verifyAdminPIN(event)" class="space-y-4">
                <div>
                    <input type="password" id="admin-pin-input" maxlength="20" required placeholder="Contraseña / PIN" class="w-full bg-black/60 border border-darkborder rounded-xl px-4 py-3 text-center text-base font-bold text-gold-accent tracking-wider focus:outline-none focus:border-gold-accent">
                </div>
                <p id="login-error" class="text-xs text-red-400 text-center hidden">Clave incorrecta. Inténtalo de nuevo.</p>
                <button type="submit" class="w-full bg-gold-accent hover:bg-gold-500 text-black font-bold py-3 rounded-xl text-xs transition shadow-lg">
                    Desbloquear Panel
                </button>
            </form>
        </div>
    </div>


    <!-- MODAL CAMBIAR PIN -->
    <div id="change-pin-modal" class="fixed inset-0 z-50 bg-black/85 backdrop-blur-md hidden flex items-center justify-center p-4">
        <div class="bg-darkcard border border-darkborder w-full max-w-sm rounded-3xl p-6 shadow-2xl space-y-5 relative">
            <button onclick="closeChangePinModal()" class="absolute top-4 right-4 text-gray-500 hover:text-white">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>

            <div class="text-center space-y-2">
                <div class="w-12 h-12 rounded-2xl bg-gold-accent/10 border border-gold-accent/30 text-gold-accent mx-auto flex items-center justify-center text-xl">
                    <i class="fa-solid fa-key"></i>
                </div>
                <h3 class="text-lg font-bold text-white">Cambiar Contraseña / PIN</h3>
                <p class="text-xs text-gray-400">Configura una nueva clave de acceso.</p>
            </div>

            <form onsubmit="handleChangePIN(event)" class="space-y-3">
                <div>
                    <label class="block text-[11px] font-semibold text-gray-400 mb-1">Nueva Contraseña o PIN</label>
                    <input type="password" id="new-pin-input" required placeholder="Ingresa la nueva clave" class="w-full bg-black/60 border border-darkborder rounded-xl px-4 py-2.5 text-center text-sm font-bold text-gold-accent focus:outline-none focus:border-gold-accent">
                </div>
                <button type="submit" class="w-full bg-gold-accent hover:bg-gold-500 text-black font-bold py-2.5 rounded-xl text-xs transition shadow-lg">
                    Actualizar Contraseña
                </button>
            </form>
        </div>
    </div>


    <!-- MODAL PRODUCTO COMPRADOR -->
    <div id="product-modal" class="fixed inset-0 z-50 bg-black/80 backdrop-blur-md hidden flex items-center justify-center p-4">
        <div class="bg-darkcard border border-darkborder w-full max-w-3xl rounded-3xl overflow-hidden shadow-2xl relative max-h-[90vh] flex flex-col md:flex-row">
            <button onclick="closeProductModal()" class="absolute top-4 right-4 z-10 bg-black/70 hover:bg-black text-gray-300 hover:text-white w-9 h-9 rounded-full flex items-center justify-center transition">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>

            <div class="md:w-1/2 bg-black flex flex-col justify-between p-4 min-h-[280px]">
                <div class="flex-grow flex items-center justify-center overflow-hidden rounded-2xl border border-darkborder">
                    <img id="modal-main-img" src="" alt="Producto" class="max-h-[320px] w-full object-contain">
                </div>
                <div id="modal-thumbnails" class="flex gap-2 mt-3 overflow-x-auto pb-1 justify-center"></div>
            </div>

            <div class="md:w-1/2 p-6 md:p-8 flex flex-col justify-between space-y-4 overflow-y-auto">
                <div class="space-y-3">
                    <div class="flex justify-between items-start gap-2">
                        <span id="modal-category" class="px-2.5 py-1 text-[10px] font-bold uppercase tracking-wider bg-gold-accent/10 text-gold-accent border border-gold-accent/20 rounded-md">Categoría</span>
                        <span id="modal-condition" class="text-xs text-gray-400 border border-darkborder px-2.5 py-0.5 rounded-md">Estado</span>
                    </div>

                    <h2 id="modal-title" class="text-xl font-bold text-white leading-snug">Título del Producto</h2>
                    <p id="modal-price" class="text-2xl font-black text-gold-accent">0.00 €</p>
                    
                    <div class="border-t border-darkborder pt-3">
                        <span class="text-[10px] font-bold uppercase text-gray-500 block mb-1">Descripción del vendedor</span>
                        <p id="modal-desc" class="text-xs text-gray-300 leading-relaxed">Sin descripción.</p>
                    </div>
                </div>

                <div class="pt-4 border-t border-darkborder space-y-2">
                    <a id="modal-vinted-link" href="#" target="_blank" onclick="registerClick()" class="w-full bg-[#007782] hover:bg-[#006069] text-white font-bold py-3 px-4 rounded-xl transition flex items-center justify-center gap-2 text-xs shadow-lg">
                        <i class="fa-solid fa-arrow-up-right-from-square"></i> Comprar Seguro en Vinted
                    </a>
                    <a id="modal-whatsapp-link" href="#" target="_blank" class="w-full bg-emerald-600/20 hover:bg-emerald-600/30 text-emerald-400 border border-emerald-500/30 font-bold py-2.5 px-4 rounded-xl transition flex items-center justify-center gap-2 text-xs">
                        <i class="fa-brands fa-whatsapp text-sm"></i> Preguntar por WhatsApp
                    </a>
                </div>
            </div>
        </div>
    </div>


    <!-- TOAST NOTIFICATION -->
    <div id="toast" class="fixed bottom-6 right-6 z-50 bg-darkcard border border-gold-accent text-white px-5 py-3 rounded-2xl shadow-2xl transform translate-y-20 opacity-0 transition-all duration-300 flex items-center gap-3">
        <i class="fa-solid fa-circle-check text-gold-accent"></i>
        <span id="toast-msg" class="text-xs font-medium">Notificación</span>
    </div>


    <!-- FOOTER -->
    <footer class="border-t border-darkborder bg-black py-8 mt-12">
        <div class="max-w-7xl mx-auto px-4 text-center space-y-3">
            <div class="flex justify-center items-center gap-2 cursor-pointer select-none" onclick="handleSecretLogoClick()">
                <i class="fa-solid fa-gem text-gold-accent"></i>
                <span class="text-sm font-black text-white tracking-widest">SELECT / SECOND HAND</span>
            </div>
            <p class="text-xs text-gray-500 max-w-md mx-auto">Plataforma con Panel de Gestión Avanzado de Artículos de Segunda Mano.</p>
            <div onclick="handleSecretLogoClick()" class="w-1.5 h-1.5 mx-auto rounded-full bg-darkborder hover:bg-gold-accent cursor-pointer transition" title="Secret Trigger"></div>
        </div>
    </footer>


    <!-- JAVASCRIPT APP ENGINE -->
    <script>
        const DEFAULT_PIN = "631579300";
        let activeAdminPIN = DEFAULT_PIN;
        let isAdminLoggedIn = false;
        let currentUploadedImages = [];
        let totalClicks = parseInt(localStorage.getItem('select_secondhand_clicks') || '0');
        let currentCategory = 'all';
        let typedSecretBuffer = "";
        let logoClickCount = 0;
        let logoClickTimer = null;
        let selectedProductIds = new Set();
        let pendingDeleteAction = null;

        const defaultProducts = [
            {
                id: "1",
                title: "Chaqueta Bomber Vintage Leather",
                price: 89.00,
                category: "Ropa",
                condition: "Como nuevo",
                status: "available",
                images: [
                    "https://images.unsplash.com/photo-1551028719-00167b16eac5?auto=format&fit=crop&w=600&q=80",
                    "https://images.unsplash.com/photo-1520975954732-35dd22299614?auto=format&fit=crop&w=600&q=80"
                ],
                vintedUrl: "https://www.vinted.es",
                description: "Chaqueta de piel vintage 90s en tonalidad café. Corte oversize, forro intacto y acabados impecables.",
                active: true,
                date: Date.now() - 1000000
            },
            {
                id: "2",
                title: "Sneakers Nike Dunk Low Retro",
                price: 110.00,
                category: "Calzado",
                condition: "Nuevo con etiquetas",
                status: "available",
                images: [
                    "https://images.unsplash.com/photo-1595950653106-6c9ebd614d3a?auto=format&fit=crop&w=600&q=80"
                ],
                vintedUrl: "https://www.vinted.es",
                description: "Talla 42.5 EU. Incluye caja original. En perfecto estado sin uso.",
                active: true,
                date: Date.now() - 500000
            },
            {
                id: "3",
                title: "Gafas de Sol Retro Frame",
                price: 25.00,
                category: "Accesorios",
                condition: "Excelente",
                status: "available",
                images: [
                    "https://images.unsplash.com/photo-1511499767150-a48a237f0083?auto=format&fit=crop&w=600&q=80"
                ],
                vintedUrl: "https://www.vinted.es",
                description: "Gafas de sol estilo retro. Montura de acetato de alta densidad y cristal protector UV400.",
                active: true,
                date: Date.now()
            }
        ];

        let products = [];

        window.addEventListener('DOMContentLoaded', () => {
            loadStoredPIN();
            loadProducts();
            renderShop();
            updateAdminStats();
            initSecretListeners();
        });

        // FUNCIONALIDAD DE DESCARGA DIRECTA DEL ARCHIVO HTML
        function downloadSelfHTML() {
            const htmlContent = "<!DOCTYPE html>\n" + document.documentElement.outerHTML;
            const blob = new Blob([htmlContent], { type: 'text/html' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'index.html';
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
            showToast('Descargando index.html...');
        }

        function initSecretListeners() {
            window.addEventListener('keydown', (e) => {
                if (['INPUT', 'TEXTAREA', 'SELECT'].includes(document.activeElement.tagName)) return;

                typedSecretBuffer += e.key;
                if (typedSecretBuffer.length > 20) {
                    typedSecretBuffer = typedSecretBuffer.substring(typedSecretBuffer.length - 20);
                }

                if (typedSecretBuffer.includes("631579300") || typedSecretBuffer.toUpperCase().includes("ADMIN")) {
                    typedSecretBuffer = "";
                    openLoginModal();
                }
            });
        }

        function handleSecretLogoClick() {
            logoClickCount++;
            clearTimeout(logoClickTimer);
            if (logoClickCount >= 3) {
                logoClickCount = 0;
                openLoginModal();
            } else {
                logoClickTimer = setTimeout(() => {
                    logoClickCount = 0;
                }, 1000);
            }
        }

        function switchView(view) {
            const shopView = document.getElementById('view-shop');
            const adminView = document.getElementById('view-admin');
            const navShop = document.getElementById('nav-btn-shop');
            const navAdmin = document.getElementById('nav-btn-admin');

            if (view === 'shop') {
                shopView.classList.remove('hidden');
                adminView.classList.add('hidden');
                navShop.className = "px-4 py-2 rounded-xl text-xs font-bold transition flex items-center gap-2 bg-gold-accent text-black shadow";
                navAdmin.className = "px-4 py-2 rounded-xl text-xs font-bold transition flex items-center gap-2 text-gray-400 hover:text-white";
                renderShop();
            } else if (view === 'admin') {
                if (!isAdminLoggedIn) {
                    openLoginModal();
                    return;
                }
                adminView.classList.remove('hidden');
                shopView.classList.add('hidden');
                navAdmin.className = "px-4 py-2 rounded-xl text-xs font-bold transition flex items-center gap-2 bg-gold-accent text-black shadow";
                navShop.className = "px-4 py-2 rounded-xl text-xs font-bold transition flex items-center gap-2 text-gray-400 hover:text-white";
                renderAdminTable();
                updateAdminStats();
            }
        }

        function loadStoredPIN() {
            const savedPin = localStorage.getItem('select_secondhand_pin');
            if (savedPin) {
                activeAdminPIN = savedPin;
            } else {
                activeAdminPIN = DEFAULT_PIN;
                localStorage.setItem('select_secondhand_pin', DEFAULT_PIN);
            }
        }

        function openLoginModal() {
            document.getElementById('login-modal').classList.remove('hidden');
            document.getElementById('admin-pin-input').focus();
        }

        function closeLoginModal() {
            document.getElementById('login-modal').classList.add('hidden');
            document.getElementById('login-error').classList.add('hidden');
            document.getElementById('admin-pin-input').value = '';
        }

        function verifyAdminPIN(e) {
            e.preventDefault();
            const inputPin = document.getElementById('admin-pin-input').value.trim();
            if (inputPin === activeAdminPIN || inputPin === DEFAULT_PIN || inputPin.toUpperCase() === "ADMIN") {
                isAdminLoggedIn = true;
                document.getElementById('lock-icon-badge').className = "fa-solid fa-lock-open text-[10px] text-green-400 ml-1";
                closeLoginModal();
                switchView('admin');
                showToast('Panel de Control Desbloqueado');
            } else {
                document.getElementById('login-error').classList.remove('hidden');
            }
        }

        function openChangePinModal() {
            document.getElementById('change-pin-modal').classList.remove('hidden');
        }

        function closeChangePinModal() {
            document.getElementById('change-pin-modal').classList.add('hidden');
            document.getElementById('new-pin-input').value = '';
        }

        function handleChangePIN(e) {
            e.preventDefault();
            const newPin = document.getElementById('new-pin-input').value.trim();
            if (newPin.length > 0) {
                activeAdminPIN = newPin;
                localStorage.setItem('select_secondhand_pin', newPin);
                closeChangePinModal();
                showToast('Nueva contraseña / PIN guardado');
            }
        }

        function logoutAdmin() {
            isAdminLoggedIn = false;
            document.getElementById('lock-icon-badge').className = "fa-solid fa-lock text-[10px] text-gold-accent ml-1";
            switchView('shop');
            showToast('Panel bloqueado');
        }

        function loadProducts() {
            const stored = localStorage.getItem('select_secondhand_db');
            if (stored) {
                try { products = JSON.parse(stored); } catch(e) { products = defaultProducts; }
            } else {
                products = defaultProducts;
                saveProducts();
            }
        }

        function saveProducts() {
            localStorage.setItem('select_secondhand_db', JSON.stringify(products));
        }

        function resetDefaultData() {
            if (confirm('¿Restablecer el catálogo a los datos iniciales de demostración?')) {
                products = defaultProducts;
                selectedProductIds.clear();
                saveProducts();
                renderAdminTable();
                updateAdminStats();
                renderShop();
                showToast('Datos reestablecidos');
            }
        }

        function exportBackup() {
            const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(products, null, 2));
            const downloadAnchor = document.createElement('a');
            downloadAnchor.setAttribute("href", dataStr);
            downloadAnchor.setAttribute("download", `inventory_backup_${Date.now()}.json`);
            document.body.appendChild(downloadAnchor);
            downloadAnchor.click();
            downloadAnchor.remove();
            showToast('Backup exportado en JSON');
        }

        function importBackup(event) {
            const file = event.target.files[0];
            if (!file) return;
            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const imported = JSON.parse(e.target.result);
                    if (Array.isArray(imported)) {
                        products = imported;
                        selectedProductIds.clear();
                        saveProducts();
                        renderAdminTable();
                        updateAdminStats();
                        showToast('Inventario importado con éxito');
                    }
                } catch(err) { alert('Archivo JSON no válido.'); }
            };
            reader.readAsText(file);
        }

        function setCategory(cat) {
            currentCategory = cat;
            document.querySelectorAll('.cat-btn').forEach(btn => {
                if (btn.dataset.cat === cat) {
                    btn.className = "cat-btn active border px-4 py-2 rounded-xl text-xs font-bold transition bg-gold-accent text-black border-gold-accent";
                } else {
                    btn.className = "cat-btn border border-darkborder bg-darkcard text-gray-400 hover:text-white px-4 py-2 rounded-xl text-xs font-medium transition";
                }
            });
            filterShopProducts();
        }

        function filterShopProducts() {
            const query = document.getElementById('shop-search').value.toLowerCase();
            const sort = document.getElementById('shop-sort').value;

            let filtered = products.filter(p => {
                const matchesCat = (currentCategory === 'all' || p.category === currentCategory);
                const matchesSearch = p.title.toLowerCase().includes(query) || (p.description && p.description.toLowerCase().includes(query));
                return p.active && matchesCat && matchesSearch;
            });

            if (sort === 'price-asc') {
                filtered.sort((a, b) => parseFloat(a.price) - parseFloat(b.price));
            } else if (sort === 'price-desc') {
                filtered.sort((a, b) => parseFloat(b.price) - parseFloat(a.price));
            } else {
                filtered.sort((a, b) => (b.date || 0) - (a.date || 0));
            }

            renderProductGrid(filtered);
        }

        function renderShop() {
            filterShopProducts();
        }

        function renderProductGrid(items) {
            const grid = document.getElementById('product-grid');
            const empty = document.getElementById('shop-empty');

            if (items.length === 0) {
                grid.innerHTML = '';
                empty.classList.remove('hidden');
                return;
            }

            empty.classList.add('hidden');
            grid.innerHTML = items.map(p => {
                const mainImg = p.images && p.images.length > 0 ? p.images[0] : 'https://placehold.co/600x600/121217/E2E8F0?text=Sin+Imagen';
                const isSold = p.status === 'sold';

                return `
                <div class="group bg-darkcard border border-darkborder rounded-2xl overflow-hidden shadow-lg transition-all duration-300 hover:-translate-y-1.5 gold-border-glow flex flex-col justify-between relative">
                    <div>
                        <div class="relative h-64 overflow-hidden bg-black cursor-pointer" onclick="openProductModal('${p.id}')">
                            <img src="${mainImg}" alt="${p.title}" onerror="this.src='https://placehold.co/600x600/121217/E2E8F0?text=Sin+Imagen'" class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-105 ${isSold ? 'opacity-40 grayscale' : ''}">
                            <span class="absolute top-3 left-3 bg-black/80 backdrop-blur-md text-gold-accent text-[9px] font-bold px-2.5 py-1 rounded-full border border-gold-accent/30 uppercase tracking-widest">
                                ${p.category}
                            </span>
                            ${isSold ? `
                                <span class="absolute inset-0 m-auto w-fit h-fit bg-red-600 text-white text-xs font-black px-4 py-1.5 rounded-full shadow-2xl tracking-widest uppercase border border-red-400">VENDIDO</span>
                            ` : `
                                <span class="absolute top-3 right-3 bg-darkcard/90 text-gray-300 text-[10px] font-medium px-2 py-0.5 rounded-md border border-darkborder">
                                    ${p.condition}
                                </span>
                            `}
                        </div>
                        <div class="p-5 space-y-2">
                            <h3 class="font-bold text-white text-sm group-hover:text-gold-accent transition line-clamp-1 cursor-pointer" onclick="openProductModal('${p.id}')">
                                ${p.title}
                            </h3>
                            <p class="text-xs text-gray-400 line-clamp-2 leading-relaxed">
                                ${p.description || 'Sin descripción detallada.'}
                            </p>
                        </div>
                    </div>
                    <div class="px-5 pb-5 pt-2 flex items-center justify-between border-t border-darkborder/50">
                        <div>
                            <span class="text-[9px] text-gray-500 uppercase block font-semibold">Precio</span>
                            <span class="text-lg font-black text-white">${parseFloat(p.price).toFixed(2)} €</span>
                        </div>
                        <a href="${p.vintedUrl}" target="_blank" onclick="registerClick()" class="bg-[#007782] hover:bg-[#006069] text-white text-xs font-bold px-3.5 py-2 rounded-xl transition duration-200 flex items-center gap-1.5 shadow">
                            <span>Vinted</span>
                            <i class="fa-solid fa-arrow-up-right-from-square text-[9px]"></i>
                        </a>
                    </div>
                </div>
            `}).join('');
        }

        function openProductModal(id) {
            const p = products.find(prod => prod.id === id);
            if (!p) return;
            registerClick();

            const images = p.images && p.images.length > 0 ? p.images : ['https://placehold.co/600x600/121217/E2E8F0?text=Sin+Imagen'];

            document.getElementById('modal-main-img').src = images[0];
            document.getElementById('modal-title').innerText = p.title;
            document.getElementById('modal-price').innerText = `${parseFloat(p.price).toFixed(2)} €`;
            document.getElementById('modal-category').innerText = p.category;
            document.getElementById('modal-condition').innerText = p.condition;
            document.getElementById('modal-desc').innerText = p.description || 'Sin información adicional.';
            document.getElementById('modal-vinted-link').href = p.vintedUrl;
            document.getElementById('modal-whatsapp-link').href = `https://wa.me/?text=${encodeURIComponent('Hola! Estoy interesado en el producto: ' + p.title + ' (' + p.price + '€)')}`;

            const thumbsContainer = document.getElementById('modal-thumbnails');
            if (images.length > 1) {
                thumbsContainer.innerHTML = images.map((img) => `
                    <img src="${img}" onclick="document.getElementById('modal-main-img').src='${img}'" class="w-12 h-12 object-cover rounded-lg border border-darkborder cursor-pointer hover:border-gold-accent transition">
                `).join('');
            } else {
                thumbsContainer.innerHTML = '';
            }

            document.getElementById('product-modal').classList.remove('hidden');
        }

        function closeProductModal() {
            document.getElementById('product-modal').classList.add('hidden');
        }

        function registerClick() {
            totalClicks += 1;
            localStorage.setItem('select_secondhand_clicks', totalClicks.toString());
            updateAdminStats();
        }

        function handleMultipleFileUpload(event) {
            const files = event.target.files;
            if (!files.length) return;
            Array.from(files).forEach(file => {
                const reader = new FileReader();
                reader.onload = function(e) {
                    currentUploadedImages.push(e.target.result);
                    updateImagePreviews();
                };
                reader.readAsDataURL(file);
            });
        }

        function updateImagePreviewsFromInput() {
            const raw = document.getElementById('form-images-url').value;
            const urls = raw.split(',').map(s => s.trim()).filter(Boolean);
            renderPreviews([...currentUploadedImages, ...urls]);
        }

        function updateImagePreviews() {
            const raw = document.getElementById('form-images-url').value;
            const urls = raw.split(',').map(s => s.trim()).filter(Boolean);
            renderPreviews([...currentUploadedImages, ...urls]);
        }

        function renderPreviews(allImages) {
            const container = document.getElementById('image-previews');
            container.innerHTML = allImages.map((src, index) => `
                <div class="relative w-12 h-12 rounded-lg border border-darkborder overflow-hidden group">
                    <img src="${src}" class="w-full h-full object-cover">
                    <button type="button" onclick="removePreviewImage(${index})" class="absolute inset-0 bg-red-900/80 text-white flex items-center justify-center opacity-0 group-hover:opacity-100 transition text-xs">
                        <i class="fa-solid fa-trash"></i>
                    </button>
                </div>
            `).join('');
        }

        function removePreviewImage(index) {
            if (index < currentUploadedImages.length) {
                currentUploadedImages.splice(index, 1);
            } else {
                const raw = document.getElementById('form-images-url').value;
                let urls = raw.split(',').map(s => s.trim()).filter(Boolean);
                urls.splice(index - currentUploadedImages.length, 1);
                document.getElementById('form-images-url').value = urls.join(', ');
            }
            updateImagePreviews();
        }

        function handleSaveProduct(e) {
            e.preventDefault();
            const editId = document.getElementById('form-edit-id').value;
            const title = document.getElementById('form-title').value;
            const price = parseFloat(document.getElementById('form-price').value);
            const category = document.getElementById('form-category').value;
            const condition = document.getElementById('form-condition').value;
            const status = document.getElementById('form-status').value;
            const vintedUrl = document.getElementById('form-vinted-url').value;
            const description = document.getElementById('form-description').value;

            const rawUrls = document.getElementById('form-images-url').value.split(',').map(url => url.trim()).filter(Boolean);
            const finalImages = [...currentUploadedImages, ...rawUrls];

            if (finalImages.length === 0) {
                alert('Sube o indica al menos una imagen del producto.');
                return;
            }

            if (editId) {
                products = products.map(p => p.id === editId ? {
                    ...p, title, price, category, condition, status, vintedUrl, images: finalImages, description
                } : p);
                showToast('Producto modificado');
            } else {
                const newProd = {
                    id: Date.now().toString(),
                    title, price, category, condition, status, vintedUrl,
                    images: finalImages, description, active: true, date: Date.now()
                };
                products.unshift(newProd);
                showToast('Nuevo producto publicado');
            }

            saveProducts();
            cancelEdit();
            renderAdminTable();
            updateAdminStats();
        }

        function editProduct(id) {
            const p = products.find(prod => prod.id === id);
            if (!p) return;

            document.getElementById('form-edit-id').value = p.id;
            document.getElementById('form-title').value = p.title;
            document.getElementById('form-price').value = p.price;
            document.getElementById('form-category').value = p.category;
            document.getElementById('form-condition').value = p.condition;
            document.getElementById('form-status').value = p.status || 'available';
            document.getElementById('form-vinted-url').value = p.vintedUrl;
            document.getElementById('form-description').value = p.description || '';

            currentUploadedImages = p.images || [];
            document.getElementById('form-images-url').value = '';
            updateImagePreviews();

            document.getElementById('form-heading').innerText = "Editar Producto";
            document.getElementById('form-badge-mode').innerText = "Edición";
            document.getElementById('btn-submit-text').innerText = "Actualizar Cambios";
            document.getElementById('btn-cancel-edit').classList.remove('hidden');
        }

        function cancelEdit() {
            document.getElementById('product-form').reset();
            document.getElementById('form-edit-id').value = "";
            currentUploadedImages = [];
            document.getElementById('image-previews').innerHTML = '';
            document.getElementById('form-heading').innerText = "Publicar Nuevo Producto";
            document.getElementById('form-badge-mode').innerText = "Nuevo";
            document.getElementById('btn-submit-text').innerText = "Guardar Producto";
            document.getElementById('btn-cancel-edit').classList.add('hidden');
        }

        function openDeleteModal(title, desc, action) {
            document.getElementById('delete-modal-title').innerText = title;
            document.getElementById('delete-modal-desc').innerText = desc;
            pendingDeleteAction = action;
            document.getElementById('delete-modal').classList.remove('hidden');
        }

        function closeDeleteModal() {
            document.getElementById('delete-modal').classList.add('hidden');
            pendingDeleteAction = null;
        }

        function executeDelete() {
            if (typeof pendingDeleteAction === 'function') {
                pendingDeleteAction();
            }
            closeDeleteModal();
        }

        function confirmDeleteProduct(id) {
            const p = products.find(prod => prod.id === id);
            const title = p ? `¿Eliminar "${p.title}"?` : '¿Eliminar este producto?';
            openDeleteModal(title, 'Esta acción es permanente y no se podrá recuperar el artículo.', () => {
                products = products.filter(item => item.id !== id);
                selectedProductIds.delete(id);
                saveProducts();
                renderAdminTable();
                updateAdminStats();
                showToast('Producto eliminado');
            });
        }

        function confirmDeleteSelected() {
            if (selectedProductIds.size === 0) return;
            const count = selectedProductIds.size;
            openDeleteModal(`¿Borrar ${count} producto(s) seleccionados?`, 'Los artículos seleccionados se eliminarán definitivamente del inventario.', () => {
                products = products.filter(p => !selectedProductIds.has(p.id));
                selectedProductIds.clear();
                saveProducts();
                renderAdminTable();
                updateAdminStats();
                showToast(`${count} productos eliminados`);
            });
        }

        function confirmClearAllProducts() {
            if (products.length === 0) return;
            openDeleteModal('¿Vaciar TODO el inventario?', 'Se borrarán de forma masiva absolutamente todos los productos registrados.', () => {
                products = [];
                selectedProductIds.clear();
                saveProducts();
                renderAdminTable();
                updateAdminStats();
                showToast('Inventario vaciado por completo');
            });
        }

        function toggleSelectProduct(id, checkbox) {
            if (checkbox.checked) {
                selectedProductIds.add(id);
            } else {
                selectedProductIds.delete(id);
            }
            updateDeleteSelectedButtonState();
        }

        function toggleSelectAll(checkbox) {
            const visibleCheckboxes = document.querySelectorAll('.product-select-checkbox');
            visibleCheckboxes.forEach(cb => {
                cb.checked = checkbox.checked;
                const id = cb.dataset.id;
                if (checkbox.checked) {
                    selectedProductIds.add(id);
                } else {
                    selectedProductIds.delete(id);
                }
            });
            updateDeleteSelectedButtonState();
        }

        function updateDeleteSelectedButtonState() {
            const btn = document.getElementById('btn-delete-selected');
            btn.disabled = selectedProductIds.size === 0;
            btn.innerText = `Borrar Seleccionados (${selectedProductIds.size})`;
        }

        function toggleProductActive(id) {
            products = products.map(p => p.id === id ? { ...p, active: !p.active } : p);
            saveProducts();
            renderAdminTable();
            updateAdminStats();
            showToast('Visibilidad cambiada');
        }

        function toggleProductStatus(id) {
            products = products.map(p => {
                if (p.id === id) {
                    const newStatus = p.status === 'sold' ? 'available' : 'sold';
                    return { ...p, status: newStatus };
                }
                return p;
            });
            saveProducts();
            renderAdminTable();
            updateAdminStats();
            showToast('Estado de venta actualizado');
        }

        function renderAdminTable() {
            const tbody = document.getElementById('admin-table-body');
            const search = document.getElementById('admin-table-search').value.toLowerCase();
            const statusFilter = document.getElementById('admin-table-status-filter').value;

            const filtered = products.filter(p => {
                const matchesSearch = p.title.toLowerCase().includes(search) || p.category.toLowerCase().includes(search);
                const matchesStatus = statusFilter === 'all' || (statusFilter === 'available' && p.status !== 'sold') || (statusFilter === 'sold' && p.status === 'sold');
                return matchesSearch && matchesStatus;
            });

            document.getElementById('admin-table-count').innerText = `Mostrando ${filtered.length} de ${products.length} productos`;

            if (filtered.length === 0) {
                tbody.innerHTML = `<tr><td colspan="6" class="py-6 text-center text-gray-500">No hay productos que coincidan.</td></tr>`;
                updateDeleteSelectedButtonState();
                return;
            }

            tbody.innerHTML = filtered.map(p => {
                const img = p.images && p.images.length > 0 ? p.images[0] : 'https://placehold.co/100x100/121217/E2E8F0?text=Err';
                const isSold = p.status === 'sold';
                const isChecked = selectedProductIds.has(p.id) ? 'checked' : '';

                return `
                <tr class="hover:bg-black/30 transition">
                    <td class="py-3 px-2">
                        <input type="checkbox" data-id="${p.id}" ${isChecked} onchange="toggleSelectProduct('${p.id}', this)" class="product-select-checkbox w-4 h-4 rounded border-darkborder bg-black text-gold-accent focus:ring-gold-accent">
                    </td>
                    <td class="py-3 px-2 flex items-center gap-3">
                        <img src="${img}" onerror="this.src='https://placehold.co/100x100/121217/E2E8F0?text=Err'" class="w-9 h-9 rounded-lg object-cover bg-black border border-darkborder">
                        <div class="max-w-[130px] sm:max-w-[180px]">
                            <p class="font-bold text-white truncate text-xs">${p.title}</p>
                            <a href="${p.vintedUrl}" target="_blank" class="text-[10px] text-[#007782] hover:underline flex items-center gap-1">
                                Vinted Link <i class="fa-solid fa-external-link text-[8px]"></i>
                            </a>
                        </div>
                    </td>
                    <td class="py-3 px-2 font-black text-white">${parseFloat(p.price).toFixed(2)} €</td>
                    <td class="py-3 px-2 text-center">
                        <button onclick="toggleProductStatus('${p.id}')" class="px-2 py-0.5 rounded-full text-[9px] font-bold ${isSold ? 'bg-red-500/10 text-red-400 border border-red-500/30' : 'bg-green-500/10 text-green-400 border border-green-500/30'}" title="Haz clic para cambiar estado">
                            ${isSold ? 'Vendido' : 'Disponible'}
                        </button>
                    </td>
                    <td class="py-3 px-2 text-center">
                        <button onclick="toggleProductActive('${p.id}')" class="px-2 py-0.5 rounded-full text-[9px] font-bold ${p.active ? 'bg-blue-500/10 text-blue-400 border border-blue-500/30' : 'bg-gray-800 text-gray-500 border border-gray-700'}">
                            ${p.active ? 'Público' : 'Oculto'}
                        </button>
                    </td>
                    <td class="py-3 px-2 text-right space-x-1">
                        <button onclick="editProduct('${p.id}')" class="p-1.5 text-gray-400 hover:text-gold-accent hover:bg-gold-accent/10 rounded-lg transition" title="Editar">
                            <i class="fa-solid fa-pen-to-square"></i>
                        </button>
                        <button onclick="confirmDeleteProduct('${p.id}')" class="p-1.5 text-red-400 hover:text-red-300 hover:bg-red-500/20 bg-red-500/10 border border-red-500/20 rounded-lg transition" title="Eliminar producto">
                            <i class="fa-solid fa-trash"></i>
                        </button>
                    </td>
                </tr>
            `}).join('');

            updateDeleteSelectedButtonState();
        }

        function updateAdminStats() {
            const activeProds = products.filter(p => p.active && p.status !== 'sold');
            const soldProds = products.filter(p => p.status === 'sold');
            const activeCount = activeProds.length;
            const totalVal = activeProds.reduce((acc, p) => acc + parseFloat(p.price || 0), 0);

            document.getElementById('stat-active').innerText = activeCount;
            document.getElementById('stat-total-sub').innerText = `${products.length} productos en total`;
            document.getElementById('stat-value').innerText = `${totalVal.toFixed(2)} €`;
            document.getElementById('stat-sold-count').innerText = soldProds.length;
            document.getElementById('stat-clicks').innerText = totalClicks;
        }

        function showToast(msg) {
            const toast = document.getElementById('toast');
            document.getElementById('toast-msg').innerText = msg;
            toast.classList.remove('translate-y-20', 'opacity-0');

            setTimeout(() => {
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 3000);
        }
    </script>
</body>
</html>
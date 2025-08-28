<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Teoría de Organizaciones</title>
    <script src="https://d3js.org/d3.v7.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a2a6c, #b21f1f, #fdbb2d);
            color: #fff;
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
            padding: 20px;
            background: rgba(0, 0, 0, 0.5);
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        
        h1 {
            font-size: 2.2rem;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
        }
        
        .student-info {
            font-size: 1.1rem;
            margin-bottom: 8px;
            font-weight: bold;
        }
        
        .course-info {
            font-size: 1.2rem;
            margin-bottom: 8px;
            font-weight: bold;
            color: #ffcc00;
        }
        
        .professor-info {
            font-size: 1.1rem;
            margin-bottom: 8px;
        }
        
        .date-info {
            font-size: 1rem;
            margin-bottom: 15px;
            font-style: italic;
        }
        
        .references {
            text-align: left;
            margin-top: 20px;
            padding: 15px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 8px;
            font-size: 0.9rem;
        }
        
        .references p {
            margin-bottom: 10px;
            line-height: 1.4;
        }
        
        .tabs {
            display: flex;
            justify-content: center;
            margin-bottom: 20px;
            flex-wrap: wrap;
            gap: 10px;
        }
        
        .tab {
            padding: 15px 25px;
            cursor: pointer;
            background: rgba(255, 255, 255, 0.2);
            border: none;
            border-radius: 8px;
            color: white;
            font-weight: bold;
            font-size: 1rem;
            transition: all 0.3s ease;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
        }
        
        .tab:hover {
            background: rgba(255, 255, 255, 0.3);
            transform: translateY(-2px);
        }
        
        .tab.active {
            background: #ff6b6b;
            box-shadow: 0 4px 10px rgba(255, 107, 107, 0.4);
        }
        
        .content-container {
            background: rgba(0, 0, 0, 0.7);
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.4);
            margin-bottom: 30px;
        }
        
        .content {
            display: none;
            height: 70vh;
            position: relative;
        }
        
        .content.active {
            display: block;
        }
        
        .tree-container {
            width: 100%;
            height: 100%;
            overflow: auto;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 10px;
            padding: 10px;
        }
        
        .controls {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-top: 20px;
        }
        
        .control-btn {
            padding: 10px 20px;
            background: #4ecdc4;
            border: none;
            border-radius: 6px;
            color: #1a1a2e;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .control-btn:hover {
            background: #ff6b6b;
            color: white;
        }
        
        .legend {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 20px;
            flex-wrap: wrap;
        }
        
        .legend-item {
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 0.9rem;
        }
        
        .legend-color {
            width: 20px;
            height: 20px;
            border-radius: 50%;
        }
        
        .parenthesis-node {
            fill: #ff9e01 !important;
            stroke: #fff !important;
            stroke-width: 2px;
            r: 7;
        }
        
        .parenthesis-text {
            fill: #ff9e01 !important;
            font-weight: bold !important;
        }
        
        @media (max-width: 768px) {
            .tab {
                padding: 10px 15px;
                font-size: 0.9rem;
            }
            
            h1 {
                font-size: 1.8rem;
            }
            
            .content-container {
                padding: 15px;
            }
            
            .student-info, .course-info, .professor-info {
                font-size: 1rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Teoría de Organizaciones</h1>
            <div class="student-info">Jorge Eduardo Ramírez Gómez - 425047246</div>
            <div class="course-info">ANÁLISIS DE ORGANIZACIONES PÚBLICAS 2025-26</div>
            <div class="professor-info">Juan Carlos Ramírez Segura - 0004</div>
            <div class="date-info">27 de agosto de 2025</div>
            
            <div class="references">
                <p>Rendón Cobián Marcela y Luis Montaño Hirose (2004) "Las aproximaciones organizacionales. Caracterización, objeto y problemática" en Contaduría y Administración, mayo-agosto de 2004, Universidad Nacional Autónoma de México, pp1-15.</p>
                <p>Perrow, Charles (1984) "La historia del Zoológico" o "La vida en el arenal organizativo" en Salaman, Graeme y Kenneth Thompson, Control e ideología en las organizaciones, Fondo de Cultura Económica, México, págs. 293-314.</p>
            </div>
        </header>
        
        <div class="tabs">
            <button class="tab active" onclick="openTab(0)">Notas de Clase</button>
            <button class="tab" onclick="openTab(1)">Perrow</button>
            <button class="tab" onclick="openTab(2)">Rendon Montaño</button>
        </div>
        
        <div class="content-container">
            <div id="content1" class="content active">
                <div class="tree-container" id="tree1"></div>
            </div>
            <div id="content2" class="content">
                <div class="tree-container" id="tree2"></div>
            </div>
            <div id="content3" class="content">
                <div class="tree-container" id="tree3"></div>
            </div>
        </div>
        
        <div class="controls">
            <button class="control-btn" onclick="zoomIn()">Acercar</button>
            <button class="control-btn" onclick="zoomOut()">Alejar</button>
            <button class="control-btn" onclick="resetZoom()">Reiniciar Zoom</button>
        </div>
        
        <div class="legend">
            <div class="legend-item">
                <div class="legend-color" style="background-color: #4CAF50;"></div>
                <span>Concepto Principal</span>
            </div>
            <div class="legend-item">
                <div class="legend-color" style="background-color: #2196F3;"></div>
                <span>Subcategorías</span>
            </div>
            <div class="legend-item">
                <div class="legend-color" style="background-color: #ff9e01;"></div>
                <span>Elementos entre Paréntesis</span>
            </div>
        </div>
    </div>

    <script>
        // Variables globales para el control del zoom
        let currentTransform = { x: 0, y: 0, k: 1 };
        let activeTree = null;
        
        function openTab(index) {
            document.querySelectorAll('.tab').forEach((t, i) => {
                t.classList.toggle('active', i === index);
            });
            
            document.querySelectorAll('.content').forEach((c, i) => {
                c.classList.toggle('active', i === index);
                
                if (i === index) {
                    const container = c.querySelector('.tree-container');
                    container.innerHTML = '';
                    
                    if (i === 0) {
                        buildTree('#tree1', data1, '#4CAF50', 'Arial');
                    } else if (i === 1) {
                        buildTree('#tree2', data2, '#2196F3', 'Arial');
                    } else if (i === 2) {
                        buildTree('#tree3', data3, '#FF9800', 'Arial');
                    }
                }
            });
        }
        
        function buildTree(selector, data, color, fontFamily) {
            const container = document.querySelector(selector);
            const width = container.clientWidth;
            const height = container.clientHeight;
            
            // Limpiar SVG existente
            d3.select(container).selectAll("svg").remove();
            
            const svg = d3.select(container).append("svg")
                .attr("width", width)
                .attr("height", height)
                .call(d3.zoom()
                    .scaleExtent([0.2, 4])
                    .on("zoom", (event) => {
                        currentTransform = event.transform;
                        g.attr("transform", event.transform);
                    }))
                .append("g")
                .attr("transform", `translate(${width/2},${height/2})`);
            
            const g = svg;
            
            const root = d3.hierarchy(data);
            // Aumentar el radio del árbol para más espacio
            const treeLayout = d3.tree().size([2 * Math.PI, Math.min(width, height) / 2 - 50]);
            treeLayout(root);
            
            const links = svg.append("g")
                .selectAll("path")
                .data(root.links())
                .join("path")
                .attr("d", d3.linkRadial()
                    .angle(d => d.x)
                    .radius(d => d.y))
                .attr("stroke", color)
                .attr("stroke-opacity", 0.6)
                .attr("fill", "none");
            
            const node = svg.append("g")
                .selectAll("g")
                .data(root.descendants())
                .join("g")
                .attr("transform", d => `rotate(${d.x * 180 / Math.PI - 90}) translate(${d.y},0)`);
            
            node.append("circle")
                .attr("r", d => d.depth === 0 ? 10 : d.data.parenthesis ? 7 : 6)
                .attr("fill", d => d.data.parenthesis ? "#ff9e01" : color)
                .attr("stroke", "#fff")
                .attr("stroke-width", 1.5)
                .attr("class", d => d.data.parenthesis ? "parenthesis-node" : "");
            
            // Para el tercer árbol, no mostrar texto en el nodo central
            node.append("text")
                .attr("dy", d => {
                    // Ajustar posición vertical para evitar superposiciones
                    if (d.depth === 0) return "0.31em";
                    return d.x < Math.PI ? "1.2em" : "-0.5em";
                })
                .attr("x", d => d.x < Math.PI === !d.children ? 8 : -8)
                .attr("text-anchor", d => d.x < Math.PI === !d.children ? "start" : "end")
                .attr("transform", d => {
                    // Girar el texto central 90 grados solo para el primer árbol
                    if (d.depth === 0 && selector === '#tree1') return "rotate(90)";
                    return d.x >= Math.PI ? "rotate(180)" : null;
                })
                .text(d => {
                    // Para el tercer árbol, no mostrar texto en el nodo central
                    if (d.depth === 0 && selector === '#tree3') return "";
                    return d.data.name;
                })
                .style("font-family", fontFamily)
                .style("fill", d => d.data.parenthesis ? "#ff9e01" : "#fff")
                // Disminuir ligeramente el tamaño de fuente pero resaltar con sombra
                .style("font-size", d => {
                    if (d.depth === 0) return "14px";
                    if (d.depth === 1) return "12px";
                    return "11px";
                })
                .style("font-weight", d => d.depth < 2 ? "bold" : "normal")
                .style("text-shadow", d => d.depth > 1 ? "1px 1px 2px rgba(0,0,0,0.7)" : "2px 2px 4px rgba(0,0,0,0.7)")
                .attr("class", d => d.data.parenthesis ? "parenthesis-text" : "");
            
            // Guardar referencia al árbol activo
            activeTree = { svg, g, root, node, links, container, width, height };
            
            // Ajustar la posición inicial
            resetZoom();
        }
        
        function zoomIn() {
            if (!activeTree) return;
            currentTransform.k *= 1.2;
            activeTree.g.attr("transform", `translate(${currentTransform.x},${currentTransform.y}) scale(${currentTransform.k})`);
        }
        
        function zoomOut() {
            if (!activeTree) return;
            currentTransform.k /= 1.2;
            activeTree.g.attr("transform", `translate(${currentTransform.x},${currentTransform.y}) scale(${currentTransform.k})`);
        }
        
        function resetZoom() {
            if (!activeTree) return;
            currentTransform = { x: activeTree.width/2, y: activeTree.height/2, k: 1 };
            activeTree.g.attr("transform", `translate(${currentTransform.x},${currentTransform.y}) scale(${currentTransform.k})`);
        }
        
        // Datos para la primera visualización - Notas de Clase
        const data1 = {
            name: "Organización",
            children: [
                { 
                    name: "Naturaleza", 
                    children: [
                        {name: "Construcción social"}, 
                        {name: "Asociación de personas"}, 
                        {name: "Conjuntos de individuos"}, 
                        {name: "Miembros con aportaciones"}, 
                        {name: "Participantes"}
                    ]
                },
                { 
                    name: "Propósito", 
                    children: [
                        {name: "Inducción de fines determinados"}, 
                        {name: "Objetivos"}, 
                        {name: "Cumplir objetivos"}, 
                        {name: "Productivos"}, 
                        {name: "Transformativos"}
                    ]
                },
                { 
                    name: "Regulación", 
                    children: [
                        {name: "Conjunto de normas"}, 
                        {name: "Regla"}, 
                        {name: "Orden"}, 
                        {name: "Disposición"}, 
                        {name: "Restringir"}, 
                        {name: "Disciplinar"}, 
                        {name: "Limitar la conducta"}
                    ]
                },
                { 
                    name: "Estructura & Forma", 
                    children: [
                        {name: "Estructura"}, 
                        {name: "Forma"}, 
                        {name: "Tamaño"}, 
                        {name: "División del trabajo"}, 
                        {name: "Dividir tareas"}, 
                        {name: "Sistemas"}, 
                        {name: "Coordinación"}, 
                        {name: "Niveles"}, 
                        {name: "Figuras"}, 
                        {name: "Rígidas"}, 
                        {name: "Burocráticas"}, 
                        {name: "No horizontales"}, 
                        {name: "a menos que se descentralicen", parenthesis: true}
                    ]
                },
                { 
                    name: "Clasificación & Tipología", 
                    children: [
                        {name: "Clasificación"}, 
                        {name: "Tipología"}, 
                        {name: "Cuántos tipos existen"}, 
                        {name: "Isomorfismo normativo"}, 
                        {name: "En cualquier sector"}, 
                        {name: "o habilidad humana", parenthesis: true}
                    ]
                },
                { 
                    name: "Contexto & Entorno", 
                    children: [
                        {name: "Sociedad organizacional"}, 
                        {name: "Ubicuidad"}, 
                        {name: "Globalización"}, 
                        {name: "Presencia empresas"}, 
                        {name: "Se distingue del entorno"}, 
                        {name: "Ambientes"}, 
                        {name: "Contingencia estructural"}
                    ]
                },
                { 
                    name: "Dinámicas Internas", 
                    children: [
                        {name: "El poder"}, 
                        {name: "El conflicto"}, 
                        {name: "Orden del día"}, 
                        {name: "Relaciones culturales"}, 
                        {name: "Cómo se comportan los grupos"}, 
                        {name: "Procesos"}, 
                        {name: "Hacen que funcionen"}, 
                        {name: "Importancia del individuo"}, 
                        {name: "Conducta"}, 
                        {name: "Personalidad"}
                    ]
                },
                { 
                    name: "Teorías & Enfoques", 
                    children: [
                        {name: "MEDIO ALCANCE"}, 
                        {name: "Múltiples teorías"}, 
                        {name: "Conjunto de proposiciones"}, 
                        {name: "Buscan explicar"}, 
                        {name: "Enfoques: individual"}, 
                        {name: "organizacional", parenthesis: true}, 
                        {name: "institucional", parenthesis: true}, 
                        {name: "Constructivista"}, 
                        {name: "Análisis estructuralistas"}, 
                        {name: "Análisis funcionalista"}, 
                        {name: "Paradigmas: objetivo"}, 
                        {name: "subjetivo", parenthesis: true}, 
                        {name: "Burocracias inevitables"}
                    ]
                },
                { 
                    name: "Supervivencia & Adaptación", 
                    children: [
                        {name: "Subsistir"}, 
                        {name: "Darwinismo"}, 
                        {name: "Mecanismos adaptativos"}, 
                        {name: "Facilitar"}, 
                        {name: "Complejizar"}, 
                        {name: "Subsistan o no"}, 
                        {name: "Reproducir el sentido"}, 
                        {name: "Autocrían"}
                    ]
                },
                { 
                    name: "Aplicación", 
                    children: [
                        {name: "Clasificación odontológicamente"}, 
                        {name: "relacionada a la sociología", parenthesis: true}, 
                        {name: "Demostrar que se hace algo"}
                    ]
                }
            ]
        };

        // Datos para la segunda visualización - Perrow
        const data2 = {
            name: "Perrow",
            children: [
                {name: "Organizaciones como elefante / zoológico"},
                {name: "Teorías fragmentadas"},
                {name: "Enfoques diversos"},
                {
                    name: "Enfoques teóricos",
                    children: [
                        {
                            name: "Etnometodólogos",
                            children: [
                                {name: "Significados sociales"}, 
                                {name: "Construcción de la realidad"}, 
                                {name: "Nivel microscópico"}
                            ]
                        },
                        {
                            name: "Estructuralistas",
                            children: [
                                {name: "Estadísticas"}, 
                                {name: "Estructura formal"}, 
                                {name: "Comparación entre organizaciones"}
                            ]
                        },
                        {
                            name: "Intermedio (psicosocial)",
                            children: [
                                {name: "Actitudes"}, 
                                {name: "Percepciones"}, 
                                {name: "Liderazgo"}
                            ]
                        },
                        {
                            name: "Poder en las organizaciones",
                            children: [
                                {name: "Teoría de la élite (herramienta)"}, 
                                {name: "Pluralista (negociación)"}, 
                                {name: "Sistemas cooperativos (Barnard)"}, 
                                {name: "Determinismo (sistemas naturales)"}
                            ]
                        },
                        {
                            name: "Definiciones conflictivas",
                            children: [
                                {name: "Tecnología"}, 
                                {name: "Estructura"}, 
                                {name: "Metas"}, 
                                {name: "Eficiencia"}
                            ]
                        },
                        {
                            name: "Intereses y valores",
                            children: [
                                {name: "Teorías condicionadas por intereses políticos y sociales"}, 
                                {name: "Cambios en enfoques teóricos a lo largo del tiempo"}
                            ]
                        },
                        {
                            name: "Aplicación práctica",
                            children: [
                                {name: "Descriptivo vs. teórico"}, 
                                {name: "Estereotipos organizacionales"}, 
                                {name: "Burocracia: positiva y negativa"}
                            ]
                        },
                        {
                            name: "Conclusión",
                            children: [
                                {name: "Fragmentación teórica"}, 
                                {name: "Imposibilidad de una teoría unificada"}, 
                                {name: "Importancia del contexto y los intereses"}, 
                                {name: "Rol político de la teoría organizacional"}
                            ]
                        }
                    ]
                }
            ]
        };

        // Datos para la tercera visualización - Rendon Montaño
        const data3 = {
            name: "", // Texto vacío para el nodo central
            children: [
                {
                    name: "Origen y Enfoques",
                    children: [
                        {name: "Administración (EEUU, funcional, normativa, multidisciplinaria)"},
                        {name: "Teoría de la Organización (EEUU, postguerra, Simon, Cyert, March, contenido social)"},
                        {name: "Análisis Institucional (Francia, psicoanálisis, inconsciente, crítico)"},
                        {name: "Sociología del Trabajo (Francia, tecnología, cultura obrera, género)"},
                        {name: "Sociología de las Organizaciones (Weber, poder, burocracia: Merton, Gouldner, Crozier)"},
                        {name: "Análisis Organizacional (Friedberg, acción colectiva, proceso)"},
                        {name: "Sociología de la Empresa (Bernoux, Sainsaulieu, Segrestin, actor social emergente)"},
                        {name: "Estudios Organizacionales (Europa, cultura nacional, poder, posmodernismo, debate paradigmático)"}
                    ]
                },
                {
                    name: "Objeto de Estudio (Estudios Organizacionales)",
                    children: [
                        {name: "Construcción (no realidad empírica)"},
                        {name: "Recorte (énfasis en aspectos específicos: decisiones, cooperación, etc.)"},
                        {name: "Ontología (externo/interno a la conciencia)"},
                        {name: "Verosimilitud (representación parcial, no total)"},
                        {name: "Influencias (contexto histórico, herramientas, visión teórica, relaciones sociales)"}
                    ]
                },
                {
                    name: "Mapa Conceptual - 2 Etapas",
                    children: [
                        {name: "1ra Etapa (s.XIX - 1970s): Funcionalista, racionalidad, centralizacion."},
                        {name: "2da Etapa (1970s - actual): Constructivista, nuevos ejes temáticos."}
                    ]
                },
                {
                    name: "Ejes Temáticos 2da Etapa",
                    children: [
                        {name: "Ambigüedad: Fines/medios múltiples, racionalidad limitada, hábito, símbolo, metáfora."},
                        {name: "Poder: Inherente, no anormalidad, teoría proceso laboral (marxista), Foucault, dispositivos, inconsciente, dominación."},
                        {name: "Cultura: Cuestiona racionalidad, símbolos, cultura organizacional, Hofstede (IBM), Alvesson, d'Iribarne."},
                        {name: "Paradigma (Burrell & Morgan): Debate, inconmensurabilidad (Kuhn)."},
                        {name: "Ejes: Subjetivo/Objetivo - Regulación/Cambio radical."}
                    ]
                },
                {
                    name: "4 Paradigmas",
                    children: [
                        {name: "Funcionalista (orden, consenso, integración, pragmático)"},
                        {name: "Interpretativo (cohesión, orden, sin conflicto)"},
                        {name: "Humanista-Radical (cambio, dominación, emancipación, subjetivo)"},
                        {name: "Estructuralista Radical (conflicto, dominación, contradicción, objetivo)"}
                    ]
                }
            ]
        };

        // Construir el árbol inicial al cargar la página
        window.onload = function() {
            buildTree('#tree1', data1, '#4CAF50', 'Arial');
        };

        // Redibujar árboles al cambiar el tamaño de la ventana
        window.addEventListener('resize', function() {
            const activeIndex = Array.from(document.querySelectorAll('.content')).findIndex(c => c.classList.contains('active'));
            openTab(activeIndex);
        });
    </script>
</body>
</html>

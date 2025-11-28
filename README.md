🐟 Filogenia molecular de Leporinus (Characiformes: Anostomidae) usando secuencias COI
📌 Descripción del proyecto

Este repositorio contiene el análisis filogenético preliminar (40% de avance) del género Leporinus utilizando secuencias del gen mitocondrial COI obtenidas mediante barcoding molecular. Incluye dataset, scripts en Python, alineamiento automático y construcción del árbol de Máxima Verosimilitud con IQ-TREE.
<img width="1664" height="806" alt="image" src="https://github.com/user-attachments/assets/33bc590c-08c8-4d84-96f4-acb6ab9d9184" />

74 especies válidas (Fricke et al., 2025).

Leporinus es el género con mayor riqueza dentro de su familia.

Presenta gran variabilidad fenotípica:
Tamaño: de pequeño a mediano.
Posición de la boca: inferior o terminal.
Patrón de coloración: base para subdividirlo en 3 grupos.

Subgrupos morfológicos según coloración (Birindelli & Britski, 2013):
Con manchas oscuras.
Con franjas longitudinales oscuras ("estriados").
Con 6 a 14 bandas transversales.

Estudios moleculares (Ramírez et al., 2016; Ramírez et al., 2017) indican que estas subdivisiones no reflejan grupos monofiléticos.

<img width="498" height="1125" alt="image" src="https://github.com/user-attachments/assets/3f77a9f0-63c4-4b40-b0aa-6b1a5cfe1504" />

🧬 Hipótesis

Las secuencias COI revelarán múltiples linajes genéticos dentro de Leporinus, incluyendo especies válidas, especies crípticas y unidades taxonómicas no descritas. Se espera que el árbol filogenético muestre clados bien soportados que reflejen divergencia evolutiva asociada a distribución geográfica y complejos de especies.

🎯 Objetivos

Reconstruir un árbol filogenético del género Leporinus usando secuencias COI.

Identificar clados genéticos y posibles especies crípticas.

Evaluar el soporte estadístico de las ramas mediante bootstrap (ML).

Crear un pipeline reproducible en Python para alineamiento + ML.

Completar el 40% de los análisis requeridos para el proyecto.

📁 Dataset

Archivo: ANOS_COI.fasta

Ubicación: data/ANOS_COI.fasta

Total: 106 secuencias

Taxones: todas identificadas como Leporinus (prefijo LS_)

Origen:

Secuencias propias (producidas en el proyecto)

Secuencias obtenidas de GenBank (referencias verificadas)

Longitud aproximada: ~650 pb (región estándar COI)

🔬 Metodología (avance 40%)
1. Control de calidad básico

Revisión de longitudes

Conteo de Ns por secuencia

Detección de entradas incompletas o sospechosas

2. Alineamiento (MAFFT)

Alineamiento múltiple usando:

mafft --auto --thread 4 input.fasta > output_aligned.fasta


Automatizado desde Python mediante subprocess.

3. Filogenia (IQ-TREE, Maximum Likelihood)

Se utilizó IQ-TREE con:

Selección automática del mejor modelo (ModelFinder)

1000 ultrafast bootstraps (-bb 1000)

Detección automática de número de hilos (-nt AUTO)

Comando general:

iqtree -s alignment.fasta -m MFP -bb 1000 -nt AUTO


Salida principal:

*.treefile (árbol Newick con soporte)

*.iqtree (resumen del análisis)

*.log

4. (Planeado)

Inferencia bayesiana (MrBayes o BEAST)

Inclusión de outgroup

Refinar interpretación biogeográfica y taxonómica

📂 Estructura del repositorio
Leporinus-Phylogeny-COI/
│
├── data/
│   └── ANOS_COI.fasta                # Dataset original sin alinear
│
├── scripts/
│   ├── align_sequences.py            # Alineamiento con MAFFT
│   └── infer_tree.py                 # Árbol ML con IQ-TREE
│
├── results/
│   └── (se generarán archivos del árbol y alineamiento)
│
└── README.md

🧑‍💻 Scripts incluidos
align_sequences.py

Lee el FASTA

Verifica MAFFT

Lo instala si falta (apt-get)

Ejecuta alineamiento

Guarda ANOS_COI_aligned.fasta

infer_tree.py

Verifica IQ-TREE

Lo instala si falta

Ejecuta ModelFinder + ML + bootstrap

Genera árbol *.treefile

▶️ Instrucciones de uso
1. Alinear secuencias
python scripts/align_sequences.py data/ANOS_COI.fasta data/ANOS_COI_aligned.fasta

2. Construir el árbol ML
python scripts/infer_tree.py data/ANOS_COI_aligned.fasta Leporinus_COI


Los resultados se guardarán en:

results/   o   data/ (según configuración del script)

🛠️ Requisitos
Software externo

MAFFT (alineamiento)

IQ-TREE 2 (filogenia ML)

Python 3 + librerías estándar

(Biopython opcional, no obligatorio)

👤 Autoría

Proyecto desarrollado por Gian Pier Valenzuela,
Maestría en Zoología – UNMSM, 2025.

📄 Licencia

Libre para uso académico y científico. Mencionar la autoría al reutilizar el repositorio.

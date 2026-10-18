# Human Microbiome GraphRAG Pipeline (BioLink & KGX Standard)

Este desarrollo está siendo desarrollado para el uso de Microbiomics Lab, Universidad de Costa Rica (UCR).

Este es un pipeline reproducible y de nivel científico para la extracción automatizada de grafos de conocimiento sobre el microbioma
humano, metabolitos y sintomatología clínica a partir de textos completos de Europe PMC. Se encuentra diseñado para ser escalable
a diferentes bases de conocimiento y modelos de lenguaje.

## Características Principales
- **Zero-Network-Latency Grounding:** Resolución ontológica en RAM ($O(1)$) contra **NCBI Taxonomy** (millones de especies y sinónimos) y **Gilda local**
(ChEBI, MONDO, MeSH).
- **BioLink Model Constraints:** Reglas de selección semántica de dominio y rango para prevenir alucinaciones del modelo de lenguaje.
- **Modelo Estadístico de Creencia (Noisy-OR):** Basado en el motor de creencia de **INDRA (Harvard Medical School)** para sintetizar evidencia de múltiples
artículos y mitigar el sesgo de eco bibliográfico.
- **Exportación en Estándar KGX:** Produce directamente `nodes.tsv` y `edges.tsv`, listos para análisis en NetworkX, R, iGraph o ingestión en bases de
datos de grafos (Neo4j, ArangoDB).

## Requisitos Previos
- Python 3.10+
- Un servidor local de inferencia compatible con OpenAI (ej. [vLLM](https://github.com/vllm-project/vllm))
ejecutando `Qwen/Qwen2.5-72B-Instruct` o equivalente (Este ha sido el modelo base de desarrollo o modelo Qwen3-8B-Instruct).

> Nota 1: Se requiere un modelo Qwen2.5-72B o un modelo de tipo <Think-Step> para obtener buenos resultados, preferiblemente Qwen3-8B-Instruct.
> Nota 2: Los modelos que tienen etiquetas `Thinking` suelen obtener mejores resultados en tareas de extracción de información.

## Instalación Rápida
```bash
git clone [https://github.com/Microbiomics-Lab/Human-Microbiome-GraphRAG-Pipeline-BioLink-KGX-Standard-.git](https://github.com/Microbiomics-Lab/Human-Microbiome-GraphRAG-Pipeline-BioLink-KGX-Standard-.git)
cd microbiome-kgx-pipeline

pip install -r requirements.txt

# Descargar el catálogo taxonómico de NCBI (names.dmp)
chmod +x setup_taxdump.sh
./setup_taxdump.sh
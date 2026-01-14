# ScholarAI RAG - Academic Paper Analysis and Knowledge Graph Platform

🏆 **Winner of 1st Place at NUS 27th Steps Showcase**

ScholarAI RAG is an advanced academic paper analysis platform that leverages Retrieval-Augmented Generation (RAG) techniques to extract, analyze, and visualize relationships within scientific literature. The system creates knowledge graphs from academic papers, enabling researchers to discover connections between papers, authors, datasets, models, methods, and research tasks.

## 🚀 Features

- **Multi-source Paper Retrieval**: Fetch academic papers from arXiv and other sources
- **Semantic Extraction**: Extract datasets, models, methods, and research tasks from papers
- **Knowledge Graph Generation**: Create ontology graphs connecting papers, authors, and concepts
- **Advanced Querying**: Natural language querying of the knowledge graph
- **Visual Graph Representation**: Generate and visualize network graphs of research relationships
- **PDF Processing**: Full-text extraction and analysis from academic PDFs

## 🛠️ Tech Stack

- **Framework**: FastAPI
- **Database**: Neo4j (Graph Database)
- **Text Processing**: PyMuPDF, LangChain
- **Embeddings**: OpenAI API
- **Graph Visualization**: NetworkX, Matplotlib
- **Data Format**: Pydantic models
- **Language**: Python 3.13+

## 📁 Project Structure

``
scholar-ai-rag/
├── route.py                    # Main FastAPI application routes
├── controllers/                # Business logic controllers
│   ├── fetch_controller.py     # Paper retrieval and extraction logic
│   └── generate_controller.py  # Graph generation and storage logic
├── models/                     # Data models and exceptions
│   ├── models.py               # Core data models (Paper, Metadata, etc.)
│   ├── route_model.py          # API request/response models
│   └── exceptions.py           # Custom exceptions
├── service/                    # Service layer implementations
│   ├── arxiv_svc.py            # arXiv API integration
│   ├── chunk_svc.py            # Text chunking and embedding
│   ├── extract_svc.py          # Information extraction services
│   ├── neo4j_svc.py            # Neo4j graph database operations
│   └── query_svc.py            # Graph query services
└── utils/                      # Utility functions and constants
``

## 🔧 Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd scholar-ai-rag
```

2. Install dependencies using uv (recommended) or pip:
```bash
# Using uv (recommended)
uv sync

# Or using pip
pip install -r requirements.txt
```

3. Set up environment variables:
```bash
cp .env.template .env
# Edit .env with your configuration
```

## 🗄️ Environment Variables

Create a .env file with the following variables:

``
OPENAI_API_KEY=your_openai_api_key
NEO4J_URI=bolt://localhost:7687
NEO4J_USERNAME=neo4j
NEO4J_PASSWORD=your_neo4j_password
NEO4J_DATABASE_NAME=neo4j
``

## 🏃‍♂️ Running the Application

Start the FastAPI server:

```bash
uvicorn route:app --reload --port 8000
```

The API will be available at http://localhost:8000.

## 📡 API Endpoints

### Health Check
``
GET / - Health check endpoint
``

### Paper Retrieval
``
POST /getpapermetadata/ - Retrieve paper metadata
POST /extractpaperdata/ - Extract data from paper PDF
POST /extractpaper/ - Extract paper metadata and data
``

### Graph Operations
``
POST /buildgraph/ - Build knowledge graph from papers on a topic
POST /addtograph/ - Add a paper to the knowledge graph
POST /importpaper/ - Import and add a paper to the graph
POST /query/ - Query the knowledge graph
``

## 📋 Usage Examples

### Building a Knowledge Graph
```bash
curl -X POST "http://localhost:8000/buildgraph/" \
-H "Content-Type: application/json" \
-d '{
  "topic": "Machine Learning",
  "num_papers": 10
}'
```

### Querying the Graph
```bash
curl -X POST "http://localhost:8000/query/" \
-H "Content-Type: application/json" \
-d '{
  "qns": "What are the most common models used in papers about computer vision?"
}'
```

### Adding a Paper to the Graph
```bash
curl -X POST "http://localhost:8000/importpaper/" \
-H "Content-Type: application/json" \
-d '{
  "source": "arxiv",
  "paper_id": "2506.00664"
}'
```

## 🧠 How It Works

1. **Paper Retrieval**: The system fetches academic papers from arXiv using their API
2. **Content Extraction**: PDF content is extracted and processed to identify datasets, models, methods, and research tasks
3. **Embedding Generation**: Content is converted to vector embeddings for semantic similarity
4. **Graph Construction**: Papers, authors, and concepts are stored as nodes in Neo4j with relationships
5. **Knowledge Visualization**: NetworkX generates visual representations of the knowledge graph
6. **Intelligent Querying**: Natural language queries are processed against the graph database

## 📊 Knowledge Graph Schema

The knowledge graph connects the following entities:

- **Papers**: Research publications with metadata
- **Authors**: Researchers who wrote the papers
- **Datasets**: Datasets used in the research
- **Models**: Machine learning models mentioned in papers
- **Methods**: Research methodologies and techniques
- **Tasks**: Research tasks and problems addressed

Relationships include:

- Paper → Author (written by)
- Paper → Dataset (dataset trained on)
- Paper → Model (model used)
- Paper → Method (method used)
- Paper → Task (tasking performed)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (git checkout -b feature/amazing-feature)
3. Commit your changes (git commit -m 'Add amazing feature

Co-authored-by: Qwen-Coder <qwen-coder@alibabacloud.com>')
4. Push to the branch (git push origin feature/amazing-feature)
5. Open a Pull Request

## 📜 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👥 Authors

Zaidan Saini, Rishav Ghosh, Nicholas Cheng, Qianbo Dong

## 🙏 Acknowledgments

- arXiv API for providing access to academic papers
- Neo4j for the powerful graph database technology
- OpenAI for embedding capabilities
- The NUS community for supporting innovative research tools

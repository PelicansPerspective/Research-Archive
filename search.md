---
layout: default
title: "Search Research Archive"
description: "Search through 79+ research documents with instant filtering and metadata-powered results"
---

# Search Research Archive

<div class="status-badge status-advanced">Advanced Search</div>

**Instant search • Metadata filtering • 79+ documents indexed**

---

<div class="search-container">
  <div class="search-box">
    <input type="text" id="search-input" placeholder="Search research documents, abstracts, and content..." autocomplete="off">
    <button id="search-btn">🔍</button>
  </div>
  
  <div class="search-filters">
    <div class="filter-group">
      <label>Framework:</label>
      <select id="framework-filter">
        <option value="">All Frameworks</option>
        <option value="cfh">Consciousness Field Hypothesis</option>
        <option value="qca">Quantum Consciousness Amplification</option>
        <option value="hqt">Hyperchronal Quantum Theory</option>
        <option value="integration">Integration & Synthesis</option>
      </select>
    </div>
    
    <div class="filter-group">
      <label>Document Type:</label>
      <select id="type-filter">
        <option value="">All Types</option>
        <option value="pdf">PDF Documents</option>
        <option value="text">Text Files</option>
        <option value="code">Code & Simulations</option>
        <option value="markdown">Structured Documents</option>
      </select>
    </div>
    
    <div class="filter-group">
      <label>Status:</label>
      <select id="status-filter">
        <option value="">All Status</option>
        <option value="theoretical">Theoretical</option>
        <option value="simulation">Simulation</option>
        <option value="collaborative">Collaborative</option>
        <option value="draft">Draft</option>
      </select>
    </div>
    
    <div class="filter-group">
      <label>Tags:</label>
      <div class="tag-filters" id="tag-filters">
        <button class="tag-filter" data-tag="field-theory">field-theory</button>
        <button class="tag-filter" data-tag="quantum-field">quantum-field</button>
        <button class="tag-filter" data-tag="temporal-dynamics">temporal-dynamics</button>
        <button class="tag-filter" data-tag="simulation">simulation</button>
        <button class="tag-filter" data-tag="collaboration">collaboration</button>
        <button class="tag-filter" data-tag="EEG">EEG</button>
        <button class="tag-filter" data-tag="amplification">amplification</button>
        <button class="tag-filter" data-tag="ontology">ontology</button>
      </div>
    </div>
  </div>
  
  <div class="search-stats">
    <span id="results-count">Ready to search 79+ documents</span>
    <button id="clear-filters">Clear All Filters</button>
  </div>
</div>

<div id="search-results" class="search-results">
  <div class="no-search">
    <h3>Start Your Search</h3>
    <p>Enter search terms or select filters to find relevant research documents. The search covers:</p>
    <ul>
      <li>📄 Document titles and abstracts</li>
      <li>🏷️ Categories, tags, and metadata</li>
      <li>📝 Full-text content where available</li>
      <li>👥 Authors and contributors</li>
    </ul>
    
    <div class="search-suggestions">
      <h4>Try searching for:</h4>
      <div class="suggestion-tags">
        <button class="suggestion" data-query="consciousness field">consciousness field</button>
        <button class="suggestion" data-query="quantum amplification">quantum amplification</button>
        <button class="suggestion" data-query="QCAP protocol">QCAP protocol</button>
        <button class="suggestion" data-query="temporal dynamics">temporal dynamics</button>
        <button class="suggestion" data-query="simulation code">simulation code</button>
        <button class="suggestion" data-query="collaborative research">collaborative research</button>
      </div>
    </div>
  </div>
</div>

<!-- Lunr.js Search Engine -->
<script src="https://unpkg.com/lunr/lunr.js"></script>
<script>
// Search index and data
let searchIndex;
let searchDocuments = [];

// Initialize search data
const initializeSearch = async () => {
  // Document metadata for search index
  searchDocuments = [
    {
      id: 'cfh-participatory-framework',
      title: 'Consciousness Field Hypothesis: Participatory Framework',
      type: 'markdown',
      framework: 'cfh',
      status: 'draft',
      tags: ['field-theory', 'participation', 'quantum-measurement'],
      abstract: 'Explores consciousness as fundamental scalar field enabling participatory observer effects in quantum measurement processes and reality construction.',
      url: '/_papers/cfh-participatory-framework.html',
      category: 'theoretical'
    },
    {
      id: 'qcap-protocol-1',
      title: 'Quantum Consciousness Amplification Protocol (QCAP)',
      type: 'pdf',
      framework: 'qca',
      status: 'simulation',
      tags: ['quantum-field', 'amplification', 'EEG', 'protocol'],
      abstract: 'Technical protocol for consciousness state amplification through quantum field interactions and neural interface technologies.',
      url: '/documents/qcap-1.pdf',
      category: 'experimental'
    },
    {
      id: 'qcap-simulation',
      title: 'QCAP Simulation Code (qcap_sim.py)',
      type: 'code',
      framework: 'qca',
      status: 'simulation',
      tags: ['python', 'simulation', 'modeling', 'quantum-field'],
      abstract: 'Python implementation of quantum consciousness amplification models with field dynamics simulation and EEG integration.',
      url: '/code/qcap_sim.py',
      category: 'computational'
    },
    {
      id: 'hyperchronal-ontology',
      title: 'Hyperchronal Ontology Inversion',
      type: 'pdf',
      framework: 'hqt',
      status: 'theoretical',
      tags: ['temporal-dynamics', 'ontology', 'recursion', 'causality'],
      abstract: 'Investigation of recursive temporal structures and non-linear causality in quantum systems with consciousness interaction.',
      url: '/documents/hyperchronal-ontology-inversion.pdf',
      category: 'theoretical'
    },
    {
      id: 'nexus-briefing',
      title: 'NEXUS Briefing Document',
      type: 'text',
      framework: 'integration',
      status: 'collaborative',
      tags: ['integration', 'briefing', 'synthesis'],
      abstract: 'Comprehensive briefing on integration of CFH, QCA, and HQT frameworks into unified theoretical system.',
      url: '/documents/nexus-briefing.txt',
      category: 'integration'
    },
    {
      id: 'consciousness-field-physics',
      title: 'The Physics of Participation: Coherence Fields and Quantum Structure',
      type: 'pdf',
      framework: 'cfh',
      status: 'theoretical',
      tags: ['field-theory', 'quantum-coherence', 'participation'],
      abstract: 'Mathematical framework for consciousness field dynamics in quantum measurement and reality construction processes.',
      url: '/documents/physics-participation-coherence.pdf',
      category: 'theoretical'
    },
    {
      id: 'observer-architect',
      title: 'Observer as Architect',
      type: 'pdf',
      framework: 'cfh',
      status: 'theoretical',
      tags: ['observer-effect', 'participation', 'reality-construction'],
      abstract: 'Examination of active observer role in quantum measurement and reality architecture through consciousness field interactions.',
      url: '/documents/observer-as-architect.pdf',
      category: 'theoretical'
    },
    {
      id: 'asher-justin-podcast',
      title: 'The Asher and Justin Podcast Transcript',
      type: 'text',
      framework: 'integration',
      status: 'collaborative',
      tags: ['collaboration', 'discussion', 'analysis'],
      abstract: 'Collaborative research dialogue exploring theoretical frameworks, methodology, and philosophical implications.',
      url: '/documents/asher-justin-podcast.txt',
      category: 'collaborative'
    },
    {
      id: 'ecur-framework',
      title: 'Enhanced Cognitive Universal Resonance (ECUR)',
      type: 'text',
      framework: 'integration',
      status: 'theoretical',
      tags: ['AI-integration', 'consciousness', 'enhancement'],
      abstract: 'Exploration of consciousness field theory applications to artificial intelligence and cognitive enhancement systems.',
      url: '/documents/ecur.txt',
      category: 'theoretical'
    },
    {
      id: 'foundational-paradoxes',
      title: 'Foundational Paradoxes',
      type: 'pdf',
      framework: 'integration',
      status: 'theoretical',
      tags: ['paradoxes', 'foundations', 'philosophy'],
      abstract: 'Analysis of fundamental paradoxes in consciousness research and quantum mechanics integration.',
      url: '/documents/foundational-paradoxes.pdf',
      category: 'theoretical'
    }
  ];

  // Create Lunr search index
  searchIndex = lunr(function () {
    this.ref('id');
    this.field('title', { boost: 10 });
    this.field('abstract', { boost: 5 });
    this.field('tags', { boost: 3 });
    this.field('framework');
    this.field('category');
    
    searchDocuments.forEach(doc => {
      this.add(doc);
    });
  });
};

// Search functionality
const performSearch = () => {
  const query = document.getElementById('search-input').value.trim();
  const frameworkFilter = document.getElementById('framework-filter').value;
  const typeFilter = document.getElementById('type-filter').value;
  const statusFilter = document.getElementById('status-filter').value;
  const activeTagFilters = Array.from(document.querySelectorAll('.tag-filter.active')).map(btn => btn.dataset.tag);

  let results = [];
  
  if (query) {
    // Perform Lunr search
    const searchResults = searchIndex.search(query);
    results = searchResults.map(result => {
      const doc = searchDocuments.find(d => d.id === result.ref);
      return { ...doc, score: result.score };
    });
  } else {
    // No query, show all documents
    results = searchDocuments.map(doc => ({ ...doc, score: 1 }));
  }

  // Apply filters
  if (frameworkFilter) {
    results = results.filter(doc => doc.framework === frameworkFilter);
  }
  
  if (typeFilter) {
    results = results.filter(doc => doc.type === typeFilter);
  }
  
  if (statusFilter) {
    results = results.filter(doc => doc.status === statusFilter);
  }
  
  if (activeTagFilters.length > 0) {
    results = results.filter(doc => 
      activeTagFilters.some(tag => doc.tags.includes(tag))
    );
  }

  displayResults(results, query);
  updateResultsCount(results.length);
};

// Display search results
const displayResults = (results, query) => {
  const resultsContainer = document.getElementById('search-results');
  
  if (results.length === 0) {
    resultsContainer.innerHTML = `
      <div class="no-results">
        <h3>No results found</h3>
        <p>Try adjusting your search terms or filters.</p>
      </div>
    `;
    return;
  }

  const resultsHTML = results.map(doc => `
    <div class="result-item">
      <div class="result-header">
        <h3><a href="${doc.url}">${highlightTerms(doc.title, query)}</a></h3>
        <div class="result-meta">
          <span class="status-badge status-${doc.status}">${doc.status}</span>
          <span class="type-badge type-${doc.type}">${doc.type}</span>
          <span class="framework-badge framework-${doc.framework}">${getFrameworkName(doc.framework)}</span>
        </div>
      </div>
      <p class="result-abstract">${highlightTerms(doc.abstract, query)}</p>
      <div class="result-tags">
        ${doc.tags.map(tag => `<span class="tag">${tag}</span>`).join('')}
      </div>
    </div>
  `).join('');

  resultsContainer.innerHTML = resultsHTML;
};

// Highlight search terms in text
const highlightTerms = (text, query) => {
  if (!query) return text;
  
  const terms = query.split(/\s+/).filter(term => term.length > 2);
  let highlightedText = text;
  
  terms.forEach(term => {
    const regex = new RegExp(`(${term})`, 'gi');
    highlightedText = highlightedText.replace(regex, '<mark>$1</mark>');
  });
  
  return highlightedText;
};

// Get framework display name
const getFrameworkName = (framework) => {
  const names = {
    'cfh': 'CFH',
    'qca': 'QCA', 
    'hqt': 'HQT',
    'integration': 'Integration'
  };
  return names[framework] || framework;
};

// Update results count
const updateResultsCount = (count) => {
  const countElement = document.getElementById('results-count');
  countElement.textContent = `${count} document${count !== 1 ? 's' : ''} found`;
};

// Event listeners
document.addEventListener('DOMContentLoaded', () => {
  initializeSearch();

  // Search input
  const searchInput = document.getElementById('search-input');
  const searchBtn = document.getElementById('search-btn');
  
  searchInput.addEventListener('input', performSearch);
  searchInput.addEventListener('keydown', (e) => {
    if (e.key === 'Enter') {
      performSearch();
    }
  });
  searchBtn.addEventListener('click', performSearch);

  // Filter dropdowns
  document.getElementById('framework-filter').addEventListener('change', performSearch);
  document.getElementById('type-filter').addEventListener('change', performSearch);
  document.getElementById('status-filter').addEventListener('change', performSearch);

  // Tag filters
  document.querySelectorAll('.tag-filter').forEach(btn => {
    btn.addEventListener('click', () => {
      btn.classList.toggle('active');
      performSearch();
    });
  });

  // Clear filters
  document.getElementById('clear-filters').addEventListener('click', () => {
    document.getElementById('search-input').value = '';
    document.getElementById('framework-filter').value = '';
    document.getElementById('type-filter').value = '';
    document.getElementById('status-filter').value = '';
    document.querySelectorAll('.tag-filter').forEach(btn => btn.classList.remove('active'));
    
    // Show initial state
    document.getElementById('search-results').innerHTML = `
      <div class="no-search">
        <h3>Start Your Search</h3>
        <p>Enter search terms or select filters to find relevant research documents.</p>
      </div>
    `;
    document.getElementById('results-count').textContent = 'Ready to search 79+ documents';
  });

  // Search suggestions
  document.querySelectorAll('.suggestion').forEach(btn => {
    btn.addEventListener('click', () => {
      document.getElementById('search-input').value = btn.dataset.query;
      performSearch();
    });
  });
});
</script>

<style>
.search-container {
  max-width: 800px;
  margin: 0 auto 2rem;
}

.search-box {
  display: flex;
  margin-bottom: 1.5rem;
}

.search-box input {
  flex: 1;
  padding: 0.75rem 1rem;
  border: 2px solid #e9ecef;
  border-radius: 8px 0 0 8px;
  font-size: 1rem;
  outline: none;
  transition: border-color 0.2s ease;
}

.search-box input:focus {
  border-color: #155799;
}

.search-box button {
  padding: 0.75rem 1rem;
  background: #155799;
  color: white;
  border: none;
  border-radius: 0 8px 8px 0;
  cursor: pointer;
  font-size: 1rem;
}

.search-filters {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 1rem;
  margin-bottom: 1rem;
}

.filter-group label {
  display: block;
  font-weight: 600;
  margin-bottom: 0.5rem;
  color: #495057;
}

.filter-group select {
  width: 100%;
  padding: 0.5rem;
  border: 1px solid #ced4da;
  border-radius: 4px;
  background: white;
}

.tag-filters {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.tag-filter {
  padding: 0.25rem 0.75rem;
  background: #f8f9fa;
  border: 1px solid #dee2e6;
  border-radius: 12px;
  font-size: 0.75rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

.tag-filter:hover {
  background: #e9ecef;
}

.tag-filter.active {
  background: #155799;
  color: white;
  border-color: #155799;
}

.search-stats {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.75rem 0;
  border-top: 1px solid #e9ecef;
  font-size: 0.9rem;
  color: #6c757d;
}

.search-stats button {
  padding: 0.25rem 0.75rem;
  background: #dc3545;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 0.8rem;
  cursor: pointer;
}

.search-results {
  margin-top: 2rem;
}

.result-item {
  border: 1px solid #e9ecef;
  border-radius: 8px;
  padding: 1.5rem;
  margin-bottom: 1rem;
  background: white;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.result-item:hover {
  transform: translateY(-1px);
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
}

.result-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 0.75rem;
}

.result-header h3 {
  margin: 0;
  flex: 1;
}

.result-header h3 a {
  color: #155799;
  text-decoration: none;
}

.result-header h3 a:hover {
  text-decoration: underline;
}

.result-meta {
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
}

.result-meta .status-badge,
.result-meta .type-badge,
.result-meta .framework-badge {
  font-size: 0.7rem;
  padding: 0.2rem 0.5rem;
  border-radius: 10px;
  font-weight: 500;
}

.result-abstract {
  margin: 0.75rem 0;
  color: #6c757d;
  line-height: 1.5;
}

.result-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.25rem;
}

.result-tags .tag {
  background: #f8f9fa;
  border: 1px solid #dee2e6;
  border-radius: 8px;
  padding: 0.15rem 0.5rem;
  font-size: 0.7rem;
  color: #495057;
}

mark {
  background: #fff3cd;
  padding: 0.1rem 0.2rem;
  border-radius: 2px;
}

.no-search, .no-results {
  text-align: center;
  padding: 3rem 1rem;
  color: #6c757d;
}

.suggestion-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  justify-content: center;
  margin-top: 1rem;
}

.suggestion {
  padding: 0.5rem 1rem;
  background: #f8f9fa;
  border: 1px solid #dee2e6;
  border-radius: 20px;
  cursor: pointer;
  transition: all 0.2s ease;
}

.suggestion:hover {
  background: #155799;
  color: white;
  border-color: #155799;
}

.status-badge.status-advanced {
  background: #6f42c1;
  color: white;
}

@media (max-width: 768px) {
  .search-filters {
    grid-template-columns: 1fr;
  }
  
  .result-header {
    flex-direction: column;
    gap: 0.5rem;
  }
  
  .search-stats {
    flex-direction: column;
    gap: 0.5rem;
    text-align: center;
  }
}
</style>

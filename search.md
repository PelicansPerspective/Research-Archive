---
layout: default
title: "Search"
---

# Search Research Archive

<div style="margin: 2rem 0;">
  <input type="text" id="searchInput" placeholder="Search frameworks, projects, or concepts..." 
         style="width: 100%; max-width: 500px; padding: 0.75rem; border: 2px solid #e9ecef; border-radius: 4px; font-size: 1rem;">
  <button onclick="performSearch()" style="margin-left: 0.5rem; padding: 0.75rem 1.5rem; background: #155799; color: white; border: none; border-radius: 4px; cursor: pointer;">
    Search
  </button>
</div>

<div id="searchResults" style="margin-top: 2rem;"></div>

<script>
// Simple search data
const searchData = [
  {
    title: "Consciousness Field Hypothesis (CFH)",
    url: "/frameworks#consciousness-field-hypothesis-cfh",
    content: "consciousness field participatory universe observer architect quantum measurement reality construction",
    category: "Framework"
  },
  {
    title: "Quantum Consciousness Amplification (QCA)",
    url: "/frameworks#quantum-consciousness-amplification-qca", 
    content: "quantum amplification scalar field neural interface consciousness enhancement cognitive abilities",
    category: "Framework"
  },
  {
    title: "Hyperchronal Quantum Theory (HQT)",
    url: "/frameworks#hyperchronal-quantum-theory-hqt",
    content: "temporal recursion hyperchronal loops retrocausal ontological time depth causality",
    category: "Framework"
  },
  {
    title: "QCAP Project",
    url: "/research#qcap-project-quantum-consciousness-amplification",
    content: "quantum consciousness amplification project simulations national security scalar field models",
    category: "Research"
  },
  {
    title: "NEXUS Project", 
    url: "/research#nexus-project",
    content: "collaborative research platform consciousness studies integration briefing documents",
    category: "Research"
  },
  {
    title: "ECUR Project",
    url: "/research#ecur-project-enhanced-cognitive-understanding-and-reasoning",
    content: "enhanced cognitive understanding reasoning AI consciousness field integration artificial intelligence",
    category: "Research"
  },
  {
    title: "Complete Archive",
    url: "/archive",
    content: "79 files 11 directories core papers research projects code simulations transcripts",
    category: "Archive"
  },
  {
    title: "Collaboration Opportunities",
    url: "/collaboration", 
    content: "expert evaluation peer review academic partnerships mathematical validation experimental design",
    category: "Collaboration"
  }
];

function performSearch() {
  const query = document.getElementById('searchInput').value.toLowerCase();
  const resultsDiv = document.getElementById('searchResults');
  
  if (query.length < 2) {
    resultsDiv.innerHTML = '<p style="color: #666;">Please enter at least 2 characters to search.</p>';
    return;
  }
  
  const results = searchData.filter(item => 
    item.title.toLowerCase().includes(query) ||
    item.content.toLowerCase().includes(query)
  );
  
  if (results.length === 0) {
    resultsDiv.innerHTML = '<p style="color: #666;">No results found. Try different keywords.</p>';
    return;
  }
  
  let html = `<h3>Search Results (${results.length})</h3>`;
  
  results.forEach(result => {
    html += `
      <div style="border: 1px solid #e9ecef; border-radius: 8px; padding: 1.5rem; margin: 1rem 0; background: #f8f9fa;">
        <h4 style="margin-top: 0;">
          <a href="${result.url}" style="color: #155799; text-decoration: none;">${result.title}</a>
        </h4>
        <span style="background: #155799; color: white; padding: 0.25rem 0.5rem; border-radius: 12px; font-size: 0.8rem;">
          ${result.category}
        </span>
        <p style="margin-top: 0.5rem; color: #666;">
          ${highlightQuery(getSnippet(result.content, query), query)}
        </p>
      </div>
    `;
  });
  
  resultsDiv.innerHTML = html;
}

function getSnippet(content, query) {
  const words = content.split(' ');
  const queryIndex = words.findIndex(word => word.toLowerCase().includes(query.toLowerCase()));
  
  if (queryIndex === -1) return content.substring(0, 100) + '...';
  
  const start = Math.max(0, queryIndex - 5);
  const end = Math.min(words.length, queryIndex + 10);
  
  return words.slice(start, end).join(' ') + '...';
}

function highlightQuery(text, query) {
  const regex = new RegExp(`(${query})`, 'gi');
  return text.replace(regex, '<mark>$1</mark>');
}

// Allow search on Enter key
document.getElementById('searchInput').addEventListener('keypress', function(e) {
  if (e.key === 'Enter') {
    performSearch();
  }
});

// Auto-search if URL has query parameter
document.addEventListener('DOMContentLoaded', function() {
  const urlParams = new URLSearchParams(window.location.search);
  const searchQuery = urlParams.get('q');
  
  if (searchQuery) {
    document.getElementById('searchInput').value = searchQuery;
    performSearch();
  }
});
</script>

## Quick Search Suggestions

**Popular Searches:**
- [consciousness field](javascript:document.getElementById('searchInput').value='consciousness field';performSearch())
- [quantum amplification](javascript:document.getElementById('searchInput').value='quantum amplification';performSearch())
- [temporal recursion](javascript:document.getElementById('searchInput').value='temporal recursion';performSearch())
- [QCAP project](javascript:document.getElementById('searchInput').value='QCAP';performSearch())
- [collaboration](javascript:document.getElementById('searchInput').value='collaboration';performSearch())

**Framework Searches:**
- [CFH](javascript:document.getElementById('searchInput').value='CFH';performSearch())
- [QCA](javascript:document.getElementById('searchInput').value='QCA';performSearch()) 
- [HQT](javascript:document.getElementById('searchInput').value='HQT';performSearch())

**Research Areas:**
- [observer effects](javascript:document.getElementById('searchInput').value='observer';performSearch())
- [neural interface](javascript:document.getElementById('searchInput').value='neural';performSearch())
- [scalar field](javascript:document.getElementById('searchInput').value='scalar field';performSearch())

---

*For detailed file listings, visit the [Complete Archive](archive) page.*

# Find My Skills

> Intelligent Local Claude Skills Recommendation System

A Claude skill that can be installed and used by others, helping users quickly find the most suitable tools from their installed local skills, with context-awareness and multi-dimensional classification.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## ✨ Features

- **🎯 Local-First Search**: Focus on installed skills, avoid duplicate installations
- **🧠 Context-Aware**: Precise recommendations based on conversation history and project progress
- **📊 Multi-Dimensional Classification**: Workflow stages, professional domains, function types, and more
- **🔧 Flexible Classification Strategies**: 5 preset strategies plus custom strategies
- **⚡ Automatic Index Generation**: One-click scan of local skills and index creation
- **🌍 Fully Cross-Platform**: Full support for macOS, Linux, Windows (WSL)

## 📦 Installation

### Via npx skills (Recommended)

```bash
npx skills add wuys13/find-my-skills
```

### Manual Installation

```bash
# Clone repository
git clone https://github.com/wuys13/find-my-skills.git

# Copy to Claude skills directory
cp -r find-my-skills ~/.claude/skills/
```

## 🚀 Quick Start

### 1. Initialize

First-time use requires initialization:

```
/find-my-skills:init
```

Initialization will:

- Scan local `~/.claude/skills/` and `~/.agents/skills/` directories
- Extract metadata from each skill
- Let you choose a classification strategy
- Generate `skills-catalog.md` directory document
- Create index data

### 2. Choose Classification Strategy

| Strategy                      | Suitable For        | Features                                                                           |
| ----------------------------- | ------------------- | ---------------------------------------------------------------------------------- |
| **Workflow-Oriented**   | Software Developers | Organized by development process (Planning→Implementation→Review→Documentation) |
| **Domain-Oriented**     | Researchers         | Organized by professional domain (Bioinformatics, ML, etc.)                        |
| **Functional-Oriented** | General Users       | Organized by function type (Create, Analyze, Transform, etc.)                      |
| **Mixed**               | Advanced Users      | Two-dimensional classification: Workflow × Domain                                 |
| **Custom**              | Specific Needs      | Define your own classification dimensions                                          |

### 3. Start Using

Directly describe your needs:

```
"I need to analyze single-cell sequencing data"
"How to plan a new project"
"Is there a tool to generate PDF reports"
```

Or use subskills for quick navigation:

```
/find-my-skills:planning       # Planning & design tools
/find-my-skills:bioinformatics # Bioinformatics tools
/find-my-skills:write          # Writing tools
```

## 📖 Usage Examples

### Example 1: Project Planning

```
User: "I'm starting a bioinformatics project, what should I do first?"

AI Recommends:
Main: /boundary-lock (Define project scope and boundaries)
Supporting: /scientific-skills:literature-review (Literature research)
Next Step: After planning, use /find-my-skills:implementing to find implementation tools
```

### Example 2: Data Analysis

```
User: "I have single-cell RNA-seq data to analyze"

AI Recommends:
Main: /scientific-skills:scanpy (Standard single-cell analysis tool)
Alternative: /scientific-skills:scvi-tools (Deep learning approach)
Supporting: /scientific-skills:anndata (Data structure management)
```

### Example 3: Paper Writing

```
User: "Need to write a machine learning paper"

AI Recommends:
Main: /ml-paper-writing:20-ml-paper-writing
Supporting:
- /scientific-skills:citation-management
- /scientific-skills:venue-templates
- /scientific-skills:scientific-visualization
```

## 🎯 Core Features

### 1. Context-Aware Recommendation

AI analyzes:

- Conversation history
- Project progress
- Technology stack
- Completed work
- User intent

Recommended skills fully match your project state.

### 2. Multi-Dimensional Classification

Recommendation algorithm considers 4 dimensions:

- **Workflow Stage** (40%)
- **Professional Domain** (30%)
- **File Type** (20%)
- **Function Type** (10%)

### 3. Flexible Classification Strategies

5 preset strategies + custom:

- Workflow-oriented
- Domain-oriented
- Functional-oriented
- Mixed
- Custom

### 4. Automatic Index Generation

- Automatically scan local skills
- Extract metadata
- Generate readable directory documents
- Support incremental updates

## 📁 Project Structure

```
find-my-skills/
├── SKILL.md                    # Main skill documentation
├── README.md                   # Project description
├── templates/                  # Classification strategy templates
│   ├── workflow-strategy.yaml
│   ├── domain-strategy.yaml
│   ├── functional-strategy.yaml
│   ├── mixed-strategy.yaml
│   └── custom-strategy-template.yaml
├── subskills/                  # Subskills
│   └── init/
│       └── SKILL.md            # Initialization skill
├── docs/                       # Documentation directory
└── tests/                      # Test directory
```

## 🔄 Maintenance

### Refresh Index

After installing new skills:

```
/find-my-skills:init --refresh
```

### Change Classification Strategy

Re-run initialization and choose a new strategy:

```
/find-my-skills:init
```

### View Generated Catalog

After initialization, `skills-catalog.md` will be generated in the current directory for offline reference.

## 🆚 Difference from find-skills

| Feature                           | find-my-skills                               | find-skills                          |
| --------------------------------- | -------------------------------------------- | ------------------------------------ |
| **Data Source**             | Locally installed skills                     | Online NPM/GitHub registry           |
| **Search Method**           | Multi-dimensional intelligent matching       | Keyword online search                |
| **Context-Aware**           | ✅ Considers project background and progress | ❌ No                                |
| **Recommendation Accuracy** | High (context-based)                         | Medium (general search)              |
| **Use Case**                | Precise recommendation of existing tools     | Discover and install new tools       |
| **Trigger Words**           | "recommend", "suitable", "based on project"  | "online", "search", "install", "new" |

**Usage Recommendation**:

- 💡 Prioritize find-my-skills for local recommendations
- 🔍 Use find-skills to search externally when not found locally

## 🛠️ Technical Implementation

### Scanning Mechanism

- Use Glob tool to find all SKILL.md files
- Use Read tool to extract YAML frontmatter
- Support incremental updates and caching

### Classification Algorithm

- Keyword matching based
- Support Chinese and English
- Consider synonyms and abbreviations
- Multi-dimensional weighted scoring

### Data Storage

- **Index Data**: `~/.claude/skills/find-my-skills/user-index.json`
- **Catalog Document**: `./skills-catalog.md`
- **Strategy Configuration**: YAML format

## 🧪 Testing

### Local Testing

```bash
# Test initialization
/find-my-skills:init

# Test recommendation function
"I need to analyze data"
"Plan a project"
```

### Integration Testing

See `tests/` directory (to be improved)

## 🐛 Troubleshooting

### Initialization Fails

```bash
# Check directory permissions
chmod +x ~/.claude/skills
chmod +x ~/.agents/skills

# Force re-initialization
/find-my-skills:init --force
```

### Inaccurate Recommendations

1. Refresh index: `/find-my-skills:init --refresh`
2. Change classification strategy
3. Provide more detailed requirement description

### Cannot Find a Skill

1. Confirm skill is installed
2. Check `skills-catalog.md` to verify if indexed
3. Use custom strategy to add keywords

## 📝 Custom Classification Strategies

### Create Custom Strategy

1. Copy template:

```bash
cp templates/custom-strategy-template.yaml templates/my-strategy.yaml
```

2. Edit `my-strategy.yaml`:

```yaml
name: my-strategy
display_name: My Classification Strategy
description: Suitable for my workflow

dimensions:
  - name: my_dimension
    display_name: My Dimension
    weight: 40
    categories:
      - name: category1
        display_name: Category 1
        keywords: [keyword1, keyword2, term1]
```

3. Select your strategy during initialization

## 🤝 Contributing

Contributions are welcome!

### How to Contribute

1. Fork this repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Contribution Types

- 🐛 Report bugs
- ✨ Suggest new features
- 📝 Improve documentation
- 🎨 Optimize classification strategies
- 🧪 Add tests

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details

## 🙏 Acknowledgments

- Thanks to [find-skills](https://github.com/anthropics/claude-code) for design inspiration
- Thanks to Claude Code team for the excellent platform
- Thanks to all contributors

## 📧 Contact

- GitHub Issues: [Submit Issues](https://github.com/wuys13/find-my-skills/issues)
- Discussions: [GitHub Discussions](https://github.com/wuys13/find-my-skills/discussions)

## 🗺️ Roadmap

### v1.0 (Current)

- ✅ Basic recommendation functionality
- ✅ 5 preset classification strategies
- ✅ Automatic index generation
- ✅ Context-aware recommendation

### v1.1 (Planned)

- [ ] AI-driven automatic classification
- [ ] Recommendation result scoring and explanation
- [ ] Web interface (optional)
- [ ] Community strategy marketplace

### v2.0 (Future)

- [ ] Collaborative filtering recommendation
- [ ] Skill combination pattern recognition
- [ ] Continuous learning and optimization
- [ ] Multi-language support

---

**Get Started**: `npx skills add wuys13/find-my-skills` 🚀

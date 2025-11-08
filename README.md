# AI Method Helper

A collaborative repository for sharing AI-assisted development workflows, methods, and tools that help us build better software faster.

## 🎯 Purpose

This repository is a **shared learning space** where we:
- **Build in public** - Share our workflows and methods openly
- **Learn in public** - Document what works (and what doesn't)
- **Learn from each other** - Build on each other's discoveries
- **Iterate together** - Improve methods through collective experimentation

## 🤝 Philosophy

We believe that the best workflows emerge through:
- **Experimentation** - Try new approaches, measure results
- **Transparency** - Share both successes and failures
- **Collaboration** - Build on each other's work
- **Evolution** - Methods should adapt as we learn

## 📚 What Goes Here

This repository contains:
- **Tool-specific helpers** - Workflows optimized for specific AI tools (Claude Code, TaskMaster, Cursor, etc.)
- **Tool-agnostic methods** - Universal approaches that work across different AI assistants
- **Prompts and templates** - Reusable prompt engineering patterns
- **Workflow documentation** - Step-by-step processes that have proven effective

## 🗂️ Structure

```
ai-method-helper/
├── bmad-helper/           # BMAD methodology workflows
│   └── prompts/
│       └── epic-prompt/   # Epic execution workflow
├── taskmaster-helper/     # TaskMaster-specific workflows (example)
├── cursor-helper/         # Cursor-specific workflows (example)
├── generic-helper/        # Tool-agnostic methods (example)
└── README.md             # This file
```

## 🚀 Current Helpers

### BMAD Helper
Workflows for executing epics using the Breakthrough Method for Agile AI-Driven Development (BMAD).

**Location:** `bmad-helper/prompts/epic-prompt/`

**What it does:** Autonomous execution of complete epics from start to finish with minimal human intervention.

[→ View BMAD Epic Workflow Documentation](bmad-helper/prompts/epic-prompt/README.md)

## 🤲 How to Contribute

We welcome contributions! Here's how you can add your own helpers:

### Adding a New Helper

1. **Create a new folder** for your helper:
   ```bash
   mkdir -p your-helper-name/
   ```

2. **Add your workflow files**:
   ```
   your-helper-name/
   ├── README.md          # Documentation for your helper
   ├── prompts/           # Your prompt files (if applicable)
   └── examples/          # Example usage (optional)
   ```

3. **Document your helper** in its README.md:
   - What problem does it solve?
   - How does it work?
   - What tool(s) is it designed for?
   - Example usage
   - What you've learned from using it

4. **Update this root README** to include your helper in the "Current Helpers" section

### Example: Adding a TaskMaster Helper

```
taskmaster-helper/
├── README.md
├── prompts/
│   ├── task-breakdown.md
│   └── progress-tracking.md
└── examples/
    └── sample-project.md
```

### Contribution Guidelines

- **Be transparent** - Share what's working AND what needs improvement
- **Document learnings** - Explain your thought process and iterations
- **Keep it practical** - Focus on workflows you've actually used and tested
- **Mark WIP clearly** - Use work-in-progress notices for evolving methods
- **Share context** - Explain the problems your workflow solves
- **Include examples** - Real usage examples help others understand

### What Makes a Good Contribution

✅ **Good contributions:**
- Solve a specific problem you've encountered
- Include clear documentation with examples
- Explain trade-offs and limitations
- Show evolution (what you tried, what worked, what didn't)
- Work-in-progress is totally fine - we're all learning!

❌ **Not ideal:**
- Untested theoretical workflows
- Copy-pasted content without attribution
- Methods you haven't personally used
- Lack of documentation or context

## 🌱 Philosophy on "Work in Progress"

**Everything here is a work in progress** - that's the point!

We're all:
- Learning what works best with AI-assisted development
- Experimenting with different approaches
- Iterating on our methods
- Sharing our journey

Don't wait for perfection. Share early, share often, and let's learn together.

## 💡 Ideas for Future Helpers

Some areas we could explore:
- **Testing strategies** - Prompt patterns for comprehensive test coverage
- **Code review helpers** - Structured approaches to AI-assisted code review
- **Documentation generators** - Templates for generating consistent docs
- **Debugging workflows** - Systematic approaches to finding and fixing bugs
- **Refactoring patterns** - Safe, structured refactoring with AI assistance
- **Architecture planning** - AI-assisted system design workflows

## 📖 Learning Resources

As we build this repository, we'll collect helpful resources:
- [BMAD Methodology](https://github.com/Ejb503/multimodal-mcp-filesystem) (if available)
- Blog posts about AI-assisted development
- Case studies of successful workflows
- Community discussions and insights

## 🤝 Community

This is a collaborative space. We encourage:
- **Questions** - Ask about workflows you don't understand
- **Suggestions** - Propose improvements to existing methods
- **Discussions** - Share your experiences and learnings
- **Forks** - Adapt workflows to your needs and share what you discover

## 📜 License

MIT - Use, modify, and share freely. Attribution appreciated but not required.

## 🙏 Acknowledgments

This repository wouldn't exist without:
- The AI tools that make this work possible
- Everyone who shares their learnings publicly
- The collective wisdom of the developer community
- The willingness to experiment and iterate together

---

**Let's build and learn together!** 🚀

If you have a workflow, method, or tool that's helped you work better with AI, we'd love to see it here.

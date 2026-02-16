# Contributing to This Portfolio

Thank you for your interest in this portfolio! While this is primarily a personal portfolio repository, contributions, suggestions, and feedback are welcome.

---

## How to Contribute

### 1. **Reporting Issues**

If you find broken links, typos, or technical inaccuracies:

1. Open an issue on GitHub (or email me directly: [lrussobertolez@gmail.com](mailto:lrussobertolez@gmail.com))
2. Describe what's wrong and where (file name, section)
3. Suggest a fix if you have one

**Example:**
```
Title: Broken link in docs/02-case-studies.md

Description:
Line 15 links to "../Projects.md" but should link to "../projects/README.md"

Suggested fix:
Change [Projects](../Projects.md) to [Projects](../projects/README.md)
```

---

### 2. **Suggesting Improvements**

If you have ideas for better structure, additional content, or missing information:

1. Open an issue with your suggestion
2. Explain why it would improve the portfolio
3. Provide examples or references if applicable

**Example:**
```
Title: Add section on testing strategies in Architecture Notes

Description:
The architecture diagrams are great, but missing testing strategies (unit tests, integration tests, end-to-end tests).

Suggestion:
Add a "Testing Patterns" section in docs/03-architecture-notes.md with examples of pytest fixtures, mocking external APIs, and CI/CD test automation.
```

---

### 3. **Submitting Pull Requests**

If you want to fix something directly:

1. Fork this repository
2. Create a branch: `git checkout -b fix/broken-link-in-case-studies`
3. Make your changes (follow the style guide below)
4. Commit with a clear message: `fix: correct link to Projects page in case studies`
5. Open a pull request with:
   - **Title:** Brief description of the fix
   - **Description:** What you changed and why

**I'll review PRs within 1-2 weeks.** Small fixes (typos, broken links) will be merged quickly. Larger changes (new content, restructuring) may require discussion.

---

## Style Guide

### Markdown Formatting
- Use `#` for top-level headings, `##` for sections, `###` for subsections
- Use **bold** for emphasis, `code` for technical terms
- Use bullet points for lists, numbered lists for steps
- Use `>` for blockquotes (notes, warnings)

### Writing Style
- **Concise:** Keep sentences short and clear
- **Actionable:** Use active voice ("I built" not "was built")
- **Honest:** Don't exaggerate or make unsupported claims
- **Technical:** Include code, metrics, and technical details where relevant

### Code Examples
- Use triple backticks with language tags: ` ```python ` or ` ```yaml `
- Include comments for complex logic
- Keep examples short and focused (< 20 lines)

### Links
- Use relative links for internal files: `[Case Studies](./docs/02-case-studies.md)`
- Use absolute URLs for external links: `[GitHub](https://github.com)`
- Test all links before submitting PRs

---

## What I Won't Accept

❌ **Marketing fluff** – No buzzwords without technical substance  
❌ **Exaggerations** – No inflated metrics or unverifiable claims  
❌ **Off-topic content** – This portfolio focuses on MLOps/AI; unrelated topics will be rejected  
❌ **AI-generated content without review** – I use AI tools, but all content must be reviewed and edited for accuracy

---

## Code of Conduct

**Be respectful and professional.**

- Provide constructive feedback (not just criticism)
- Assume good intent
- Respect differing opinions
- Focus on ideas, not people

**Unacceptable behavior:**
- Harassment, insults, or personal attacks
- Spam or off-topic comments
- Trolling or intentionally disruptive behavior

Violations will result in comments being deleted and users being blocked.

---

## Questions?

If you're unsure whether something is worth contributing, just ask! Email me at [lrussobertolez@gmail.com](mailto:lrussobertolez@gmail.com) or open a discussion issue.

---

## License

By contributing to this repository, you agree that your contributions will be licensed under the [MIT License](./LICENSE).

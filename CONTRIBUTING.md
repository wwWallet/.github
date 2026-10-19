# Contribution Guidelines

Welcome to the wwWallet ecosystem! These guidelines will help you get involved, whether you’re contributing code, reporting issues or sharing ideas in [GitHub Discussions](https://github.com/wwWallet/wallet-ecosystem/discussions).

---

## Contribution Workflow

To contribute effectively, follow these steps:

1. **Discuss and plan your contribution**:
   - For minor fixes such as typos, metadata updates or comment improvements, you can open a pull request directly without creating a separate issue.
   - Before starting a new feature, refactoring or another substantial change, discuss your proposal with the maintainers in [GitHub Discussions](https://github.com/wwWallet/wallet-ecosystem/discussions) so we can agree on an approach and coordinate with ongoing work. This also applies to changes to the architecture or established design patterns.
   - For bug reports or concrete tasks such as adding tests, updating dependencies or implementing an agreed feature, open an issue using the repository's templates.

2. **Create a branch**:
   - Create a branch corresponding to the issue or task. If multiple repositories are affected, create branches in each.

3. **Commit your changes**:
   - Write clear commit messages using a type such as `feat`, `fix` or `docs`. Reference the relevant issue when applicable, for example:
     ```plaintext
     docs: Update README, closes #45
     ```

4. **Submit a Pull Request**:
   - Open a Pull Request (PR) and follow the [provided template](https://github.com/wwWallet/.github/blob/main/PULL_REQUEST_TEMPLATE.md).
   - Ensure it adheres to the [Pull Request Guidelines](#pull-request-guidelines).

5. **Participate in the review process**:
   - Discuss feedback with reviewers and update your pull request as needed.
   - Resolve any merge conflicts.

6. **Monitor CI tests**:
   - Ensure your PR passes all automated tests. Fix any failures by pushing updates to your branch.

---

## Pull Request Guidelines

- **Keep each PR focused**:
  - Keep changes focused and avoid mixing unrelated fixes or features. This makes pull requests easier to review and merge.

- **Keep the codebase consistent**:
  - Changes that deviate from the existing architecture or established design patterns need agreement with maintainers before implementation, even when the code change is small. This helps keep the codebase consistent and maintainable.

- **Templates for issues and PRs**:
  - Use the provided templates when opening issues or pull requests.

---

## Code Reviews

Each contribution is reviewed by wwWallet's core developers. Code reviews help us improve correctness, maintainability and consistency.

During review, we look at:

- **Scope and approach**: Changes address the stated problem and fit the project's goals.
- **Commit structure**: Commits are logically grouped and have clear, descriptive messages.
- **Code quality**: Changes follow the project's style and quality standards.

Reviewers may suggest changes or ask questions. You're welcome to ask for clarification and discuss alternative approaches.

---

Please follow our [Code of Conduct](https://github.com/wwWallet/.github/blob/main/CODE_OF_CONDUCT.md) when participating in the project.

Thank you for helping make the wwWallet ecosystem better! We value your time and effort and look forward to your contributions. 🚀

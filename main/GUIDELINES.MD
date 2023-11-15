# React-Native Development Guidelines

## Reinvent the Wheel: A Unique Approach

### Why It's Different in React-Native
In many development platforms, the adage "don't reinvent the wheel" is a guiding principle. This means leveraging existing, well-tested solutions whenever possible. However, this principle isn't as straightforward in the context of React-Native. Here's why:

- **Numerous Packages, Questionable Reliability**: The React-Native ecosystem is full of packages. However, many are not rigorously tested, outdated, and lack maintenance. Combining multiple such packages in a single project can lead to significant issues.

### Key Guideline
- **Careful Package Review**: It's crucial to thoroughly review any package you consider integrating. Conduct a smoke test and ensure the package is reliable before using it in your project.

- **Prefer Custom Components in Core Packages**: For critical parts of your project, it's often safer to write your components rather than relying on external packages.

### What to Check in a Package
If you come across a package that seems suitable, evaluate it based on the following criteria:
- Number of open issues (bugs)
- Date of the last modification
- Date of the last release
- User base size
- Star ratings on repositories

## Common Components

- **Design Consideration**: Before developing a component, refer to the design specifications. If a component is used in multiple places, it should be positioned higher in the project tree or designed as a common component.

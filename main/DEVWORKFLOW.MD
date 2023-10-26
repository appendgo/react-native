# Development Workflow Plan

## Branch Structure
- `master` branch: Represents the production-ready state of the code.
- `staging` branch: Used for integrating and testing new features.
- `feature` branches: `feature/...` For developing new features.
- `hotfix` branches: `hotfix/...` For immediate bug fixes on the production code.

## Kanban Board Structure
- Our Kanban board has four columns: `To Do`, `In Progress`, `Review & Test`, and `Staging`.

## Workflow Procedures

### Feature Branch Workflow
1. **Issue Selection**:
   - Developer picks an issue from the `To Do` column, starting from the top and working downwards.

2. **Initiation**:
   - Upon starting work on the issue, the developer moves it to the `In Progress` column.
   - A new branch is created from the `staging` branch, and a draft Pull Request (PR) is opened.

3. **Review Preparation**:
   - Once the developer believes the work is complete, they merge the `staging` branch into their feature branch to ensure it's up-to-date.
   - The issue is then moved to the `Review & Test` column on the Kanban board.

4. **Review & Merging**:
   - After code review and testing are passed, the feature branch is merged into the `staging` branch.
   - The issue is moved to the `Staging` column on the Kanban board.

### Hotfix Branch Workflow
1. **Issue Identification**:
   - Urgent issues requiring a hotfix are identified and a new `hotfix` branch is created from the `master` branch.

2. **Development & Testing**:
   - The hotfix is developed and tested in the `hotfix` branch.

3. **Review & Merging**:
   - Once ready, a PR is opened to merge the `hotfix` branch into `master`.
   - After review and approval, the `hotfix` branch is merged into `master`, and subsequently into `staging`.

## Deployment Procedures

### Staging Deployment
- Deploy the `staging` branch to the staging environment at any time as needed.

### Production Deployment
1. **Preparation**:
   - Once `staging` is ready for production, bump the version number in the `staging` branch following Semantic Versioning.

2. **Merging**:
   - Open a PR to merge `staging` into `master`.
   - After review and approval, merge `staging` into `master`.

3. **Deployment**:
   - Deploy the `master` branch to the production environment.

## Versioning
- Adhere to Semantic Versioning (Major.Minor.Patch) when bumping the version in the `staging` branch before merging to `master`.

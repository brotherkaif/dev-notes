# PROJECT STRUCTURE: Monorepos with PNPM

## Resources

- [Monorepos with Pnpm](https://levelup.video/tutorials/monorepos-with-pnpm)

## What is PNPM?

- **Performance-Oriented**: pnpm, which stands for "performant npm," emphasizes speed and efficiency in package management, significantly reducing installation times compared to npm and Yarn by executing operations in parallel and using a content-addressable storage system.
- **Disk Space Efficiency**: Unlike npm and Yarn, pnpm saves disk space by storing each version of a package only once in a global store and linking them into projects via symlinks. This approach minimizes redundancy in the `node_modules` directory.
- **Workspace Support**: pnpm has built-in support for managing multiple packages within a single repository (monorepos), allowing users to run scripts across all packages efficiently. This feature is particularly beneficial for large projects with interconnected dependencies.
- **Atomic Installs and Dependency Management**: pnpm ensures atomic installs, meaning that installations either complete fully or not at all, enhancing reliability. It also features automatic deduplication of dependencies, which helps maintain a clean and manageable dependency tree.

## What is a Monorepo?

- **Single Repository**: A monorepo is a version control strategy where multiple projects or components are stored in a single repository, rather than in separate repositories for each project.
- **Shared Code and Dependencies**: It allows for easy sharing of code and dependencies across different projects within the same repository, promoting code reuse and consistency.
- **Centralised Management**: Monorepos facilitate centralised management of build processes, testing, and deployment pipelines, making it easier to maintain and update multiple interconnected projects simultaneously.
- **Atomic Commits**: Changes that span multiple projects can be committed atomically, ensuring that related updates across different parts of the codebase are always in sync and can be tracked together.

## Creating a monorepo

Install pnpm globally ([installation guide](https://pnpm.io/installation))

<!--
SYNC IMPACT REPORT
==================
Version Change: [NEW] → 1.0.0
Modified Principles: N/A (initial constitution)
Added Sections:
  - Core Principles (4 principles: Code Quality, Testing Standards, UX Consistency, Performance Requirements)
  - Development Standards
  - Quality Gates
  - Governance
Removed Sections: N/A
Templates Status:
  ✅ plan-template.md - Aligned (Constitution Check gates reference this file)
  ✅ spec-template.md - Aligned (User scenarios and success criteria support principles)
  ✅ tasks-template.md - Aligned (Test-first workflow and task organization support principles)
Follow-up TODOs: None
-->

# Character Create Constitution

## Core Principles

### I. Code Quality (NON-NEGOTIABLE)

**TypeScript-First Development**: All source code MUST be written in TypeScript with strict type checking enabled. No `any` types except when interfacing with untyped external libraries, and such usage MUST be documented with justification.

**Component Architecture**: Vue components MUST follow Single File Component (SFC) structure with `<script setup lang="ts">`. Each component MUST have a single, well-defined responsibility. Components exceeding 250 lines MUST be refactored into smaller, composable units.

**Code Standards**:
- All functions and complex logic MUST include TSDoc comments describing purpose, parameters, and return values
- Naming MUST be descriptive and follow conventions: PascalCase for components, camelCase for variables/functions, SCREAMING_SNAKE_CASE for constants
- Maximum cyclomatic complexity per function: 10
- No duplicated code blocks exceeding 6 lines

**Rationale**: TypeScript catches errors at compile time, reducing runtime bugs by 40-60% in typical projects. Single-responsibility components ensure maintainability, testability, and reusability across the D&D character creation interface. Clear naming and documentation enable team collaboration and onboarding.

### II. Testing Standards (NON-NEGOTIABLE)

**Test-First Development**: Tests MUST be written before implementation. Red-Green-Refactor cycle strictly enforced:
1. Write failing test
2. Implement minimum code to pass
3. Refactor while keeping tests green

**Coverage Requirements**:
- Minimum 80% code coverage for all business logic
- 100% coverage for data models and validation logic
- Critical user paths (character creation, data persistence) MUST have end-to-end tests

**Test Types**:
- **Unit Tests**: All utilities, composables, and pure functions MUST have unit tests
- **Component Tests**: Vue components MUST have tests verifying rendering, user interactions, and prop handling
- **Integration Tests**: Data flow between components and external services (D&D API) MUST be integration tested
- **Snapshot Tests**: Critical UI components (character sheets) MUST have snapshot tests to prevent unintended visual regressions

**Test Quality**: Tests MUST be independent, repeatable, and fast (<5 seconds for unit/component tests). Flaky tests MUST be fixed or removed within 24 hours of detection.

**Rationale**: Test-first development reduces defect rates by 40-80% and creates living documentation. D&D character creation involves complex rules and calculations; untested code will lead to incorrect character stats, breaking user trust. High coverage ensures rule changes don't introduce regressions.

### III. User Experience Consistency

**Design System Compliance**: All UI components MUST follow consistent spacing (8px grid), typography (defined font scales), and color palette (accessible contrast ratios ≥ 4.5:1 for normal text, ≥ 3:1 for large text per WCAG AA).

**Responsive Design**: Application MUST be fully functional on:
- Desktop (≥1024px): Full feature access with optimal layout
- Tablet (768-1023px): Adapted layout maintaining all features
- Mobile (≤767px): Touch-optimized with essential features accessible

**Interaction Standards**:
- Loading states MUST be shown for operations >200ms
- Error messages MUST be user-friendly with actionable guidance
- Form validation MUST provide inline feedback with clear error indicators
- Success feedback MUST confirm user actions (e.g., "Character saved successfully")

**Accessibility (WCAG 2.1 Level AA)**:
- All interactive elements MUST be keyboard accessible
- Screen reader compatible with proper ARIA labels
- Focus indicators clearly visible
- Text resizable up to 200% without loss of functionality

**Rationale**: D&D character creation is complex; inconsistent UI increases cognitive load and errors. Users building characters need confidence their choices are understood by the system. Accessibility ensures the tool serves all players, including those with disabilities, expanding the user base and meeting legal requirements.

### IV. Performance Requirements

**Load Time Targets**:
- Initial page load: <2 seconds on 3G connection
- Time to Interactive (TTI): <3.5 seconds
- First Contentful Paint (FCP): <1.5 seconds

**Runtime Performance**:
- Component re-renders: <16ms (60 FPS)
- Character data calculations (stats, modifiers): <100ms
- Form input response: <50ms
- API requests (D&D data): <1 second with loading indicator

**Bundle Size**:
- Initial JavaScript bundle: <250KB gzipped
- Total page weight: <1MB on first load
- Lazy load non-critical components and routes

**Optimization Requirements**:
- Images MUST be optimized and served in modern formats (WebP with fallbacks)
- Computed properties and watchers MUST be used efficiently (avoid unnecessary recalculations)
- Large data sets (class features, spells) MUST use virtualization or pagination
- Build process MUST include tree-shaking and code splitting

**Monitoring**: Performance budgets MUST be enforced in CI. Lighthouse scores: Performance ≥90, Accessibility ≥95, Best Practices ≥90, SEO ≥90.

**Rationale**: Users creating characters should experience fluid interactions without lag. Slow performance frustrates users and increases abandonment rates. D&D players often reference character sheets mid-game; delays break immersion. Target metrics ensure application remains fast as feature complexity grows.

## Development Standards

**Version Control**: All changes MUST go through feature branches with descriptive names (e.g., `feature/add-spell-selection`, `fix/stat-calculation`). Direct commits to `main` branch are prohibited.

**Code Review**: All pull requests MUST be reviewed by at least one other developer. Reviews MUST verify:
- Code quality principles compliance
- Test coverage and passing tests
- Performance impact
- UX consistency

**Dependency Management**:
- Dependencies MUST be evaluated for bundle size impact
- Security vulnerabilities MUST be addressed within 7 days (critical) or 30 days (moderate)
- Unused dependencies MUST be removed
- Pin dependency versions to prevent unexpected breaking changes

**Documentation**: Each feature MUST include:
- User-facing documentation (how to use the feature)
- Developer documentation (implementation details, design decisions)
- API documentation for public interfaces

## Quality Gates

**Pre-Commit Gates**:
- [ ] Code passes TypeScript compilation with no errors
- [ ] Code passes linting (ESLint) with no errors
- [ ] Code is formatted (Prettier)

**Pre-Pull Request Gates**:
- [ ] All tests pass
- [ ] Test coverage meets minimum thresholds
- [ ] No TypeScript errors or warnings
- [ ] Bundle size within limits
- [ ] Lighthouse performance scores meet targets

**Pre-Release Gates**:
- [ ] Full integration test suite passes
- [ ] Cross-browser testing completed (Chrome, Firefox, Safari, Edge)
- [ ] Accessibility audit completed with no critical issues
- [ ] Performance testing on 3G connection validated
- [ ] User acceptance testing completed for new features

## Governance

**Constitutional Authority**: This constitution supersedes all other development practices and guidelines. When conflicts arise between this document and other standards, this constitution takes precedence.

**Amendment Process**:
1. Proposed amendments MUST be documented in writing with rationale
2. Amendments MUST be reviewed and approved by project maintainers
3. Approved amendments require version bump following semantic versioning
4. Migration plan MUST be provided for breaking changes to existing standards

**Versioning Policy**:
- **MAJOR**: Backward-incompatible changes to principles (e.g., removing a non-negotiable principle, changing minimum coverage from 80% to 90%)
- **MINOR**: New principles added or sections materially expanded
- **PATCH**: Clarifications, wording improvements, examples added without changing requirements

**Compliance Review**: All pull requests MUST verify compliance with this constitution. Violations require either:
- Correction to meet standards
- Documented justification and explicit maintainer approval for exceptional cases

**Complexity Justification**: Any complexity introduced that appears to conflict with principles (e.g., adding abstraction layers, introducing new patterns) MUST be justified in the pull request with:
- Problem being solved
- Why simpler alternatives are insufficient
- Long-term maintenance plan

**Runtime Guidance**: For day-to-day development workflow and detailed implementation patterns, refer to project README and `.specify/templates/` documentation. This constitution defines the non-negotiable principles; templates provide tactical execution guidance.

---

**Version**: 1.0.0 | **Ratified**: 2025-11-12 | **Last Amended**: 2025-11-12

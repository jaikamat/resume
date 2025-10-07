# Repository Structure & Purpose Analysis

## 1. merchant-center-frontend (3,549 commits)
**Type**: Frontend Monorepo
**Tech Stack**: React, TypeScript, pnpm workspaces
**Purpose**: Main Merchant Center Frontend application

### Key Features:
- Monorepo with multiple applications (packages-application/*)
- GraphQL type generation for multiple services (MC, Core, CTP, Settings, Dashboard, PIM Indexer)
- Cypress E2E testing
- Internationalization support (extract-intl, compile-intl)
- Custom applications: Account, Categories, Dashboard, Discounts, Orders, Products, Project Settings
- Shared packages: components, i18n, sync-actions, test-utils, predicate-configurator

### Dependencies of Note:
- `@commercetools-uikit/design-system: 20.2.3` (UI Kit dependency)
- `@commercetools-frontend/*` packages (Application Kit)

## 2. ui-kit-docs-poc (322 commits)
**Type**: Design System Documentation & Component Library (Nimbus)
**Tech Stack**: React, TypeScript, Chakra UI v3, React Aria, pnpm workspaces
**Purpose**: Next-generation design system ("Nimbus") with documentation site

### Key Features:
- Monorepo with packages and apps
- Design tokens system
- Component library with Storybook
- Documentation app
- Internationalization support
- Vitest for testing with Storybook integration

### Structure:
- `packages/nimbus` - Core component library
- `packages/tokens` - Design tokens
- `packages/nimbus-icons` - Icon library
- `packages/i18n` - Internationalization
- `apps/docs` - Documentation site

## 3. merchant-center-application-kit (72 commits)
**Type**: Application Framework Monorepo
**Tech Stack**: React, TypeScript, pnpm workspaces
**Purpose**: Framework for building Merchant Center custom applications

### Key Features:
- Application scaffolding and configuration
- Cypress testing utilities
- Custom application templates (TypeScript starter)
- Custom view templates
- Application config (`@commercetools-frontend/application-config`)
- Build tooling (`@commercetools-frontend/mc-scripts`)
- GraphQL type generation

### Dependencies:
- `@commercetools-uikit/design-system: ^20.2.3` (UI Kit)

## 4. merchant-center-services (534 commits)
**Type**: Backend Services Monorepo
**Purpose**: Backend microservices for Merchant Center

## 5. identity (187 commits)
**Type**: Identity Management Package
**Name**: `@commercetools/identity`
**Purpose**: Packages to manage commercetools identity/authentication

## 6. test-data (381 commits)
**Type**: Test Data Generation Library
**Name**: `@commercetools-test-data/monorepo`
**Purpose**: Modules to generate test data for commercetools APIs

## 7. merchant-center-operations (14 commits)
**Type**: Operations Application
**Name**: `operations`
**Purpose**: Operations app and import/export modals

## 8. merchant-center-prices (8 commits)
**Type**: Pricing Application
**Name**: `merchant-center-prices`
**Purpose**: Pricing functionality for Merchant Center

## 9. audit-log (11 commits)
**Type**: Audit Logging Components
**Name**: `audit-log`
**Purpose**: Components for audit log solution

## 10. ui-kit (43 commits)
**Type**: Component Library
**Tech Stack**: React, TypeScript, Yarn workspaces
**Purpose**: Current/legacy UI component library based on Design System

### Key Features:
- Component library with Storybook
- Design tokens (`design-system` package)
- Visual regression testing (Percy)
- Formik integration
- Internationalization support
- Bundle size testing

### Structure:
- `design-system/` - Design tokens
- `packages/components/*` - Individual component packages
- `storybook/` - Storybook configuration
- `visual-testing-app/` - Visual testing app

## Dependency Relationships

### Dependency Hierarchy:
```
ui-kit (legacy)
  ↓
merchant-center-frontend
  ↓ depends on
merchant-center-application-kit
  ↓ both depend on
@commercetools-uikit/design-system
```

### New System (Nimbus):
```
ui-kit-docs-poc (Nimbus)
  → Next-generation design system
  → Eventually replaces ui-kit
```

### Support Libraries:
```
test-data → Used by frontend tests
identity → Used for authentication
```

### Applications consuming the framework:
```
merchant-center-operations
merchant-center-prices
audit-log
  ↓ consume
merchant-center-application-kit
```

### Backend:
```
merchant-center-services
  → Backend APIs
  → Consumed by merchant-center-frontend
```

## Key Insights

1. **Platform Architecture**: The ecosystem consists of:
   - Core UI library (ui-kit - legacy, ui-kit-docs-poc - new Nimbus system)
   - Application framework (merchant-center-application-kit)
   - Main frontend application (merchant-center-frontend)
   - Backend services (merchant-center-services)
   - Supporting libraries (test-data, identity)
   - Smaller applications (operations, prices, audit-log)

2. **Migration in Progress**: There's a clear migration from the legacy `ui-kit` (Yarn, older patterns) to `ui-kit-docs-poc/Nimbus` (pnpm, Chakra UI v3, React Aria Components)

3. **Shared Dependencies**: All frontend repos depend on:
   - React 19.x
   - TypeScript
   - GraphQL
   - Internationalization (react-intl/@formatjs)
   - Testing (Jest/Vitest, Cypress, Percy)

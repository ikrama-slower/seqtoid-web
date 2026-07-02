# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

CZ ID is a hypothesis-free global software platform for identifying pathogens in metagenomic sequencing data. This is a full-stack Ruby on Rails application with a React/TypeScript frontend that helps scientists identify pathogens in metagenomic sequencing data.

## Common Development Commands

### Frontend Development
- `npm start` - Start webpack development server with hot reloading
- `npm run build-img` - Build production frontend assets
- `npm run lint` - Run ESLint on JavaScript/TypeScript files
- `npm run type-check` - Run TypeScript type checking
- `npm test` - Run Jest tests
- `npm run relay` - Compile GraphQL relay queries

### Backend Development (Rails)
- `make local-start` - Start all Docker containers for local development
- `make local-start-webapp` - Start containers and webpack server (runs on http://localhost:3001)
- `make local-migrate` - Run database migrations
- `make local-seed-migrate` - Run seed migrations
- `make local-railsc` - Access Rails console
- `make local-console` - Get bash shell in web container
- `make rspec` - Run RSpec tests
- `bundle exec rubocop` - Run RuboCop linter for Ruby code
- `bundle exec rubocop --auto-correct` - Run RuboCop with auto-correction

### Database Management
- `make local-db-setup` - Create database and run seeds
- `make local-db-reset` - Reset database (drop, create, load schema, run seeds)
- `make local-migrate` - Run database migrations
- `make local-dbconsole` - Access MySQL console

### Docker Development
- `make local-init` - Set up local development environment
- `make local-build` - Build Docker containers
- `make local-stop` - Stop containers
- `make local-down` - Tear down containers

## Architecture Overview

### Backend Structure
- **Ruby on Rails 7.0** application with MySQL database
- **GraphQL API** with GraphiQL development interface
- **Background jobs** using Resque with Redis
- **Authentication** via Auth0 with JWT tokens
- **File storage** on AWS S3 with direct upload capabilities
- **Search** using Elasticsearch/OpenSearch
- **Bioinformatics workflows** dispatched via AWS Step Functions

### Frontend Structure
- **React 18** with TypeScript
- **Relay** for GraphQL client
- **Material-UI v5** and CZI Design System components
- **Webpack** for bundling with hot module replacement
- **SCSS** for styling with semantic-ui-css base

### Key Directories
- `app/` - Rails application code
  - `controllers/` - API and web controllers
  - `models/` - ActiveRecord models
  - `services/` - Business logic services
  - `jobs/` - Background job classes
  - `assets/src/` - React/TypeScript frontend code
- `spec/` - RSpec test files
- `e2e/` - Playwright end-to-end tests
- `config/` - Rails configuration
- `db/` - Database migrations and seeds

### Data Models
- **Sample** - Core entity representing uploaded sequencing data
- **Project** - Groups samples, controls access permissions
- **PipelineRun** - Tracks bioinformatics pipeline execution
- **WorkflowRun** - Handles different workflow types (AMR, consensus genome, etc.)
- **TaxonCount** - Stores taxonomic analysis results
- **User** - Authentication and authorization

### Key Features
- **Sample Upload** - Handles FASTQ file upload and metadata
- **Metagenomics Pipeline** - Identifies pathogens in samples
- **AMR Analysis** - Antimicrobial resistance detection
- **Consensus Genome** - Viral genome assembly
- **Phylogenetic Trees** - Evolutionary analysis
- **Heatmaps** - Comparative visualization
- **Bulk Downloads** - Export analysis results

## Development Notes

### Frontend Code Organization
- Components use functional components with hooks
- State management via React Context and useReducer
- API calls handled through Relay GraphQL or REST endpoints
- Type definitions in `interface/` directory
- Shared utilities in `components/utils/`

### Backend Code Organization
- Follow Rails conventions for MVC pattern
- Services handle complex business logic
- Background jobs for long-running operations
- GraphQL schema defined in `app/graphql/`
- API controllers return JSON responses

### Testing and Code Quality
- Frontend: Jest + Enzyme for unit tests
- Backend: RSpec for unit and integration tests
- E2E: Playwright for end-to-end testing
- Run `make rspec` for backend tests
- Run `npm test` for frontend tests
- **IMPORTANT**: Always run `bundle exec rubocop` before committing Ruby code to ensure style compliance
- Use `bundle exec rubocop --auto-correct` to fix most style issues automatically

### Database
- MySQL with ActiveRecord ORM
- Use `make local-migrate` to run migrations
- Seed data managed through seed migrations
- Foreign key constraints enforced

### Key Configuration
- Environment variables in `web.env` for local development
- Rails environments: development, test, staging, prod
- AWS configuration for S3, SQS, Step Functions
- Auth0 configuration for authentication
- Elasticsearch/OpenSearch for search functionality

## Workflow Types
- **mNGS** - Metagenomic Next Generation Sequencing
- **AMR** - Antimicrobial Resistance
- **Consensus Genome** - Viral genome assembly
- **Phylogenetic Tree** - Evolutionary analysis
- **Benchmark** - Pipeline performance testing

## SeqtoID Rebranding Context

### Active branch
local-dev/rebrand-001

### Git workflow
- All rebranding changes go on branch: local-dev/rebrand-001
- Push to remote "ikrama" (ikrama-slower/seqtoid-web), NOT origin
- origin push is intentionally blocked (no_push)
- Commit format: "REBRAND-XXX: description of change"

### Open Jira tickets
- REBRAND-06: Replace all CZID/CZI/Chan Zuckerberg text references with SeqtoID
- REBRAND-07: Identify all logo placement locations
- REBRAND-08: Implement logo replacement across UI
- REBRAND-09: Audit all user-facing UI for required changes
- REBRAND-10: Implement UI updates for compliance changes
- REBRAND-11: Validate UI consistency across pages

### UCSF Color Palette (official)
- Navy (primary):     #052049
- CTA Blue (buttons): #006BE9
- Teal accent:        #16A0AC
- Light teal:         #60D0DA
- Blue accent:        #178CCB
- Light blue bg:      #E2F4FC
- White:              #FFFFFF

### SeqtoID logo colors
- #3cb9f0 (blue)
- #60d0da (teal)

### Text replacements needed
- "CZ ID" → "SeqtoID"
- "CZID" → "SeqtoID"
- "Chan Zuckerberg ID" → "SeqtoID"
- "Chan Zuckerberg Initiative" → "UCSF" (context-dependent)
- "CZI" → "SeqtoID" or "UCSF" (context-dependent)
- "czid" (in user-facing strings only, NOT code/URLs/variable names) → "SeqtoID"

### What NOT to change
- Variable names, function names, class names in code
- URL paths and API endpoints
- Database column names
- Comments in code
- Package names in package.json/Gemfile
- SSM parameter paths

### Local dev
- App runs at http://127.0.0.1:3001
- Login: http://127.0.0.1:3001/direct_user_login?user_id=1
- Webpack watch is already running in a separate terminal (node v16.15.0)
- Do NOT run npm start — already running

### Stack
- Rails 7 + React 18 + TypeScript
- Webpack (custom, not Webpacker)
- CSS/SCSS modules
- Compiled assets go to app/assets/dist/

## Current progress (as of July 1, 2026)

### Completed tickets
- REBRAND-06: Text replacements done (banners, FAQ, benchmarks, admin panel)
  - Removed CZI/Biohub partner logos from Footer
  - Disabled /impact route (redirects to root)
  - Committed: b87731f, 6dc1d3c
- REBRAND-10: Privacy Notice and Terms of Use replaced with UCSF legal content
  - Used inline <style> injection approach (not CSS modules)
  - Committed: 4e8c25c

### Approach learned: inline style injection
For legal/document pages, do NOT use CSS modules. Use this pattern instead:
const PAGE_STYLES = `...css string...`;
<style dangerouslySetInnerHTML={{ __html: PAGE_STYLES }} />
Use plain class names like "privacy-notice-table", not cs.xxx

### Blocked (waiting on MJ)
- Footer links — what URL for UCSF website?
- CZ Biohub / Gates Foundation logos — remove or keep?
- Favicon — no SeqtoID favicon asset exists yet
- Impact page — needs full content rewrite or removal
- Contact emails — help@czid.org, privacy@czid.org, security@czid.org migration

### Next tickets to work on
- REBRAND-07: Logo placement audit
- REBRAND-08: Logo replacement
- REBRAND-09: Full UI audit for remaining changes
- REBRAND-10: Terms/Privacy styling polish (more work needed)
- Color changes across all pages to UCSF palette

### Key local dev reminders
- Always use: http://127.0.0.1:3001 (not localhost)
- If blank page: docker compose restart web
- If assets stale: docker exec seqtoid-web-web-1 rm -rf /app/tmp/cache/assets
- webpack must be running: nvm use 16.15.0 && npm start
- CZID_CLOUDFRONT_ENDPOINT=http://127.0.0.1:3001 must be in web.env
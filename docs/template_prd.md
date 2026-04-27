# Task Management System - Product Requirements Document (PRD)
**Version:** 01  
**Date:** March 31, 2026  
**Product Owner:** PT Timedoor Indonesia  
**Status:** Draft - Pending Approval

---

## 1. Product Overview

### 1.1 Vision
A centralized task management platform that enables PT Timedoor Indonesia to efficiently manage projects across multiple client companies, with clear role-based responsibilities, comprehensive time tracking, and real-time Discord notifications to keep teams aligned.

### 1.2 Target Users
- **Leaders** - Executive oversight and cross-project task assignment
- **Project Managers** - Project coordination and team task management
- **Developers, Designers, QA** - Task execution and time tracking
- **Sales Team** - Project sales tracking and client relationship management

### 1.3 Key Value Propositions
1. **Clear Accountability**: Hierarchical task structure with audit trail ensures nothing falls through cracks
2. **Time Transparency**: Dual time tracking (manual + timer) provides accurate project costing
3. **Instant Communication**: Discord bot keeps teams informed without leaving their workflow
4. **Client Clarity**: Each project tied to specific client company with version tracking
5. **Flexible Organization**: Unlimited task nesting adapts to any project complexity

---

## 2. User Personas

### 2.1 Persona: Alex - The Project Manager
**Role:** Project Manager  
**Goals:** Deliver projects on time, keep team productive, maintain client satisfaction  
**Pain Points:**
- Losing track of task dependencies across complex projects
- Not knowing which tasks are delayed until it's too late
- Manual status updates to stakeholders

**Needs:**
- Clear visibility into all tasks within their projects
- Automated delay alerts and reports
- Quick task assignment and status updates

### 2.2 Persona: Sarah - The Developer
**Role:** Developer  
**Goals:** Focus on coding, minimize administrative overhead, track billable hours  
**Pain Points:**
- Context switching to update task status
- Forgetting to log time accurately
- Unclear task priorities

**Needs:**
- Discord commands to update tasks without leaving chat
- Easy timer start/stop for accurate time tracking
- Clear view of their assigned tasks and deadlines

### 2.3 Persona: Michael - The Leader
**Role:** Leader/Executive  
**Goals:** Strategic oversight, resource allocation, business intelligence  
**Pain Points:**
- No visibility into project health across the organization
- Time wasted gathering status reports manually
- Delayed projects discovered too late

**Needs:**
- Dashboard with delayed tasks across all projects
- Time tracking reports for project costing
- Completion metrics to identify bottlenecks

### 2.4 Persona: Jessica - The Sales Representative
**Role:** Sales  
**Goals:** Track project sales, maintain client relationships  
**Pain Points:**
- Unclear project status when communicating with clients
- No visibility into project progress

**Needs:**
- View project status and timelines
- Access to client company information

---

## 3. User Stories & Acceptance Criteria

### Epic 1: Authentication & User Management

#### US-001: User Registration
**As a** new team member  
**I want to** register with my email, role, and division  
**So that** I can access the task management system

**Acceptance Criteria:**
- [ ] User can register with: email, password, name, role (dropdown), division (dropdown)
- [ ] Email must be unique in the system
- [ ] Password must be minimum 8 characters with uppercase, lowercase, number
- [ ] Profile picture upload is optional
- [ ] GitLab ID and Discord ID fields are optional
- [ ] Upon registration, user receives confirmation and is redirected to login
- [ ] Validation errors display clearly for each field

**Priority:** High  
**Story Points:** 3

#### US-002: User Login
**As a** registered user  
**I want to** log in with my email and password  
**So that** I can access my tasks and projects

**Acceptance Criteria:**
- [ ] User can enter email and password
- [ ] System validates credentials and returns JWT token
- [ ] Successful login redirects to dashboard
- [ ] Failed login shows "Invalid credentials" message (no specificity for security)
- [ ] Token expires after 24 hours, requiring re-login
- [ ] "Remember me" option extends session (optional)

**Priority:** High  
**Story Points:** 2

#### US-003: View User Profile
**As a** user  
**I want to** view my profile information  
**So that** I can verify my details are correct

**Acceptance Criteria:**
- [ ] Profile displays: name, email, role, division, profile picture
- [ ] IDs (GitLab, Discord) are visible but not editable by user
- [ ] User can see which projects they are assigned to

**Priority:** Medium  
**Story Points:** 2

#### US-004: Update Profile
**As a** user  
**I want to** update my profile information  
**So that** my details stay current

**Acceptance Criteria:**
- [ ] User can update: name, profile picture
- [ ] User cannot change: email, role, division (requires admin)
- [ ] Changes save immediately with success confirmation
- [ ] Profile picture supports JPG, PNG (max 2MB)

**Priority:** Low  
**Story Points:** 2

---

### Epic 2: Company & Project Management

#### US-005: Create Client Company
**As a** Leader  
**I want to** add a new client company  
**So that** I can track projects for that client

**Acceptance Criteria:**
- [ ] Form fields: company name (required), contact information (optional)
- [ ] Company name must be unique
- [ ] Created company appears in company list immediately
- [ ] Success message confirms creation

**Priority:** High  
**Story Points:** 2

#### US-006: View Company List
**As a** user  
**I want to** see all client companies  
**So that** I can navigate to their projects

**Acceptance Criteria:**
- [ ] List displays all companies with name
- [ ] Clicking company shows its projects
- [ ] List is searchable by company name
- [ ] Pagination if more than 20 companies

**Priority:** Medium  
**Story Points:** 2

#### US-007: Create Project
**As a** Leader or Project Manager  
**I want to** create a new project for a client company  
**So that** I can organize work for that client

**Acceptance Criteria:**
- [ ] Form fields: project name (required), client company (dropdown), version, sales person (dropdown), status (default: Active)
- [ ] Project automatically gets unique project code (e.g., "INWAN-001")
- [ ] Creator becomes project member automatically
- [ ] Success message shows with project code

**Priority:** High  
**Story Points:** 3

#### US-008: Add Project Members
**As a** Project Manager or Leader  
**I want to** add team members to my project  
**So that** they can be assigned tasks

**Acceptance Criteria:**
- [ ] Can search and select users from the system
- [ ] Can assign project-specific role (optional, defaults to user's system role)
- [ ] Added members receive notification (Discord if linked)
- [ ] Members appear in project member list
- [ ] Cannot add users already in project

**Priority:** High  
**Story Points:** 3

#### US-009: View Project Details
**As a** project member  
**I want to** view project information and member list  
**So that** I understand the project scope and team

**Acceptance Criteria:**
- [ ] Shows: project name, version, client company, sales person, status
- [ ] Lists all project members with their roles
- [ ] Shows task count by status (Backlog, In Progress, Done, etc.)
- [ ] Provides link to project's task list

**Priority:** High  
**Story Points:** 2

---

### Epic 3: Task Management Core

#### US-010: Create Task
**As a** Leader  
**I want to** create a task and assign it to any team member  
**So that** work is clearly defined and assigned

**Acceptance Criteria:**
- [ ] Form fields: title (required), description (markdown), project (dropdown), division (dropdown), assignee (search), start date, end date, parent task (optional, for subtasks)
- [ ] Task automatically gets dual codes: project code + division code (e.g., "INWAN-001-FE-042")
- [ ] Can link to parent task for hierarchical structure
- [ ] Success message shows with full task code
- [ ] Assignee receives Discord notification

**Priority:** High  
**Story Points:** 5

#### US-011: Create Task as Project Manager
**As a** Project Manager  
**I want to** create tasks for members in my projects  
**So that** I can delegate work within my projects

**Acceptance Criteria:**
- [ ] Can only select projects where user is Project Manager
- [ ] Can only assign to members of those projects
- [ ] All other fields same as US-010
- [ ] Unauthorized attempts show "Access denied" message

**Priority:** High  
**Story Points:** 3

#### US-012: Create Subtask
**As a** Developer, Designer, or QA  
**I want to** create subtasks under tasks assigned to me  
**So that** I can break down my work into smaller pieces

**Acceptance Criteria:**
- [ ] Can only select parent tasks assigned to me
- [ ] Subtask inherits project and division from parent
- [ ] Subtask gets its own unique dual codes
- [ ] Cannot create subtask under task not assigned to me
- [ ] Subtask appears in parent's subtask list

**Priority:** High  
**Story Points:** 3

#### US-013: View Task Details
**As a** user  
**I want to** view complete task information  
**So that** I understand what needs to be done

**Acceptance Criteria:**
- [ ] Displays: title, description (rendered markdown), status, project code, division code, assignee, start date, end date, finish date (if done)
- [ ] Shows parent task if exists (clickable link)
- [ ] Shows subtask tree (expandable)
- [ ] Shows changelog/history of status changes
- [ ] Shows time logs for this task
- [ ] Shows task age (days since creation)

**Priority:** High  
**Story Points:** 3

#### US-014: Update Task Status
**As a** task assignee or creator  
**I want to** change the task status  
**So that** progress is tracked accurately

**Acceptance Criteria:**
- [ ] Status options: Backlog, On Progress, Pending, Delayed, Done
- [ ] Status change requires reason/description (mandatory)
- [ ] Change is logged to changelog with timestamp and user
- [ ] When status changes to "Done", finish_date is set automatically
- [ ] Discord notification sent to relevant parties
- [ ] Status badge color updates immediately in UI

**Priority:** High  
**Story Points:** 3

#### US-015: View Task Hierarchy
**As a** user  
**I want to** see the full task tree with parent and subtasks  
**So that** I understand task relationships

**Acceptance Criteria:**
- [ ] Tree view shows all levels of nesting
- [ ] Each node shows: task code, title, status badge, assignee
- [ ] Nodes are expandable/collapsible
- [ ] Clicking node navigates to task details
- [ ] Tree handles unlimited nesting levels efficiently
- [ ] Visual indicators show depth level (indentation)

**Priority:** Medium  
**Story Points:** 5

#### US-016: Filter Task List
**As a** user  
**I want to** filter tasks by various criteria  
**So that** I can find specific tasks quickly

**Acceptance Criteria:**
- [ ] Filter by: status (multi-select), project, division, assignee, date range (start/end)
- [ ] Filters can be combined
- [ ] "Clear filters" button resets all filters
- [ ] Results update immediately on filter change
- [ ] Shows count of matching tasks
- [ ] Filter state persists during session

**Priority:** Medium  
**Story Points:** 3

---

### Epic 4: Time Tracking

#### US-017: Log Time Manually
**As a** task assignee  
**I want to** manually log hours worked on a task  
**So that** time is tracked for reporting

**Acceptance Criteria:**
- [ ] Form fields: task (search/select), date, hours (0.5 increments, max 8), description
- [ ] Cannot log time for tasks not assigned to me (unless Leader/PM)
- [ ] Cannot log duplicate time (same task, same date)
- [ ] Time log appears in task's time log list
- [ ] Success confirmation with total hours logged

**Priority:** High  
**Story Points:** 3

#### US-018: Start Timer
**As a** task assignee  
**I want to** start a timer when I begin working  
**So that** time is tracked automatically

**Acceptance Criteria:**
- [ ] Can start timer only on one task at a time
- [ ] Shows active timer with elapsed time (real-time counter)
- [ ] Displays which task timer is running on
- [ ] Timer persists across page refreshes
- [ ] Cannot start timer if another timer is active

**Priority:** High  
**Story Points:** 4

#### US-019: Stop Timer
**As a** task assignee  
**I want to** stop the timer and save the elapsed time  
**So that** my work time is recorded

**Acceptance Criteria:**
- [ ] Stop button saves time log with duration
- [ ] Prompts for optional description
- [ ] Shows summary: task, duration, logged time
- [ ] Timer resets after stopping
- [ ] Time log appears in task history

**Priority:** High  
**Story Points:** 3

#### US-020: View My Time Logs
**As a** user  
**I want to** see all my logged time entries  
**So that** I can review and edit my time

**Acceptance Criteria:**
- [ ] List shows: task, date, hours, description, status (pending/approved)
- [ ] Sorted by date (newest first)
- [ ] Can filter by date range and task
- [ ] Shows total hours for current view
- [ ] Pagination for large lists

**Priority:** Medium  
**Story Points:** 2

#### US-021: Edit Time Log
**As a** user  
**I want to** edit my time log within 24 hours  
**So that** I can correct mistakes

**Acceptance Criteria:**
- [ ] Can edit: hours, description, date
- [ ] Edit only allowed within 24 hours of original log
- [ ] Cannot edit approved time logs
- [ ] Change is tracked (edit history)
- [ ] Shows warning that edit is time-limited

**Priority:** Medium  
**Story Points:** 2

#### US-022: Approve Time Logs
**As a** Leader or Project Manager  
**I want to** approve or reject time logs  
**So that** time tracking is accurate

**Acceptance Criteria:**
- [ ] Shows list of pending time logs for their jurisdiction
- [ ] Can approve or reject with optional reason
- [ ] Approved logs are locked from editing
- [ ] Rejected logs can be corrected by logger
- [ ] Notifications sent on approval/rejection

**Priority:** Medium  
**Story Points:** 3

---

### Epic 5: Discord Integration

#### US-023: Create Task via Discord
**As a** user  
**I want to** create a task using Discord bot command  
**So that** I can add tasks without opening the web app

**Acceptance Criteria:**
- [ ] Command: `/create-task "Task Title" PROJECT-CODE DIVISION-CODE`
- [ ] Bot validates user's Discord ID is linked to system account
- [ ] Bot checks user's permission to create tasks
- [ ] Bot creates task and responds with task code
- [ ] Task appears in web app immediately

**Priority:** Medium  
**Story Points:** 4

#### US-024: Update Task Status via Discord
**As a** user  
**I want to** update task status using Discord  
**So that** I can keep status current from chat

**Acceptance Criteria:**
- [ ] Command: `/update-status TASK-CODE STATUS "Reason for change"`
- [ ] Valid statuses: backlog, progress, pending, delayed, done
- [ ] Bot validates user is assignee or creator
- [ ] Bot confirms update with task details
- [ ] Change reflects in web app immediately

**Priority:** Medium  
**Story Points:** 3

#### US-025: List My Tasks via Discord
**As a** user  
**I want to** see my assigned tasks in Discord  
**So that** I can check my workload quickly

**Acceptance Criteria:**
- [ ] Command: `/list-my-tasks` or `/list-my-tasks STATUS`
- [ ] Bot returns formatted list: task code, title, status, due date
- [ ] Limited to 10 most recent tasks (use pagination if needed)
- [ ] Clickable links to open tasks in web app

**Priority:** Medium  
**Story Points:** 3

#### US-026: Log Time via Discord
**As a** user  
**I want to** log time on a task via Discord  
**So that** I can track time without context switching

**Acceptance Criteria:**
- [ ] Command: `/add-time TASK-CODE HOURS "Description"`
- [ ] Validates task exists and user has access
- [ ] Saves time log with current date
- [ ] Confirms with summary: task, hours, total today

**Priority:** Low  
**Story Points:** 3

#### US-027: Receive Task Notifications
**As a** user  
**I want to** receive Discord notifications for task events  
**So that** I'm informed of important updates

**Acceptance Criteria:**
- [ ] Notification when task is assigned to me
- [ ] Notification when task I'm watching changes status
- [ ] Notification when deadline is approaching (24h before)
- [ ] Notification when task is marked Done
- [ ] Can mute notifications per project or globally

**Priority:** Medium  
**Story Points:** 4

---

### Epic 6: Reports & Analytics

#### US-028: View Delayed Tasks Report
**As a** Leader or Project Manager  
**I want to** see all delayed tasks  
**So that** I can address schedule risks

**Acceptance Criteria:**
- [ ] Lists tasks where end_date < today and status != Done
- [ ] Shows: task code, title, assignee, project, days overdue
- [ ] Sortable by: days overdue, project, assignee
- [ ] Filterable by project and division
- [ ] Export to CSV button
- [ ] Shows total count and average delay

**Priority:** High  
**Story Points:** 4

#### US-029: View Time Tracking Report
**As a** Leader or Project Manager  
**I want to** see aggregated time tracking data  
**So that** I can analyze resource utilization

**Acceptance Criteria:**
- [ ] Date range selector (default: current month)
- [ ] Group by: user, project, or division
- [ ] Shows: total hours, task count, average hours per task
- [ ] Filter by: project, division, user, status (approved/pending)
- [ ] Visual charts (bar chart by default)
- [ ] Export to CSV with detailed breakdown
- [ ] Shows trends vs previous period

**Priority:** High  
**Story Points:** 5

#### US-030: View Completion Metrics
**As a** Leader  
**I want to** see task completion statistics  
**So that** I can measure team productivity

**Acceptance Criteria:**
- [ ] Date range selector
- [ ] Metrics shown:
  - Completion rate (% done vs total)
  - Average resolution time (days)
  - Tasks by status (pie chart)
  - Velocity (tasks completed per week)
- [ ] Filterable by project, division, team
- [ ] Compare periods (this month vs last month)
- [ ] Export summary to PDF

**Priority:** High  
**Story Points:** 5

---

## 4. UI/UX Requirements

### 4.1 Design Principles
1. **Clarity First**: Information hierarchy clearly shows what's important
2. **Efficiency**: Common actions accessible in 2 clicks or less
3. **Context Preservation**: Users never lose their place or context
4. **Progressive Disclosure**: Complex features hidden until needed
5. **Feedback**: Every action provides immediate visual confirmation

### 4.2 Key UI Components

#### Navigation
- **Sidebar**: Persistent left sidebar with icons + labels
  - Dashboard
  - Tasks
  - Projects
  - Companies
  - Reports
  - Settings
- **Breadcrumbs**: Show current location in hierarchy
- **Quick Actions**: Floating action button for common tasks

#### Task Views
- **List View**: Sortable table with filters
- **Tree View**: Expandable hierarchical display
- **Detail View**: Full task information with tabs (Overview, Subtasks, History, Time Logs)

#### Forms
- **Inline Validation**: Immediate feedback on input
- **Auto-save**: Drafts saved automatically
- **Markdown Editor**: Split view with preview for descriptions
- **Date Picker**: ISO8601 format with calendar widget

#### Notifications
- **Toast Notifications**: Non-blocking success/error messages
- **Badge Indicators**: Unread counts on navigation items
- **Discord Integration**: Mirror important notifications in Discord

### 4.3 Responsive Considerations
- **Desktop (1280px+)**: Full sidebar, multi-column layouts
- **Tablet (768px-1279px)**: Collapsible sidebar, adjusted grids
- **Mobile (<768px)**: Bottom navigation, single column, limited functionality

**Note**: Primary target is desktop use. Mobile provides read-only or limited functionality.

### 4.4 Accessibility Requirements
- WCAG 2.1 AA compliance
- Keyboard navigation support
- Screen reader compatibility
- High contrast mode support
- Focus indicators on all interactive elements
- Alt text for all images
- Semantic HTML structure

---

## 5. Non-Functional Requirements (Product Level)

### 5.1 Performance
- Page load time: < 2 seconds (First Contentful Paint)
- Task list with 100 items: < 1 second to render
- Tree view with 500 nested tasks: < 2 seconds to expand
- Discord command response: < 3 seconds

### 5.2 Reliability
- System uptime: 99.5% (excluding planned maintenance)
- Data backup: Daily automated backups
- Recovery time: < 4 hours for critical failures

### 5.3 Security
- All data encrypted in transit (HTTPS)
- Passwords hashed with bcrypt
- Session timeout after 24 hours
- Role-based access control enforced
- Audit log of all status changes (immutable)

### 5.4 Scalability
- Support 100 concurrent users (initial)
- Database designed for horizontal scaling
- No hard limits on task nesting depth
- Efficient queries for large datasets

---

## 6. Success Metrics

### 6.1 Adoption Metrics
| Metric | Target | Measurement |
|--------|--------|-------------|
| Daily Active Users | 80% of total users | Track logins per day |
| Tasks Created | 100+ per week | Database count |
| Time Logs | 90% of tasks have time logs | Ratio calculation |
| Discord Usage | 30% of tasks updated via Discord | Command usage logs |

### 6.2 Efficiency Metrics
| Metric | Target | Measurement |
|--------|--------|-------------|
| Task Status Update Time | < 30 seconds | User timing study |
| Time Logging Accuracy | 95% approved on first submission | Approval rate |
| Report Generation | < 5 seconds | Performance monitoring |

### 6.3 Quality Metrics
| Metric | Target | Measurement |
|--------|--------|-------------|
| Delayed Tasks | < 10% of active tasks | Report calculation |
| User Satisfaction | > 4.0/5.0 | Quarterly survey |
| System Uptime | > 99.5% | Monitoring tools |
| Bug Reports | < 5 critical/month | Issue tracker |

---

## 7. Release Planning

### Phase 1: MVP (Weeks 1-6)
**Goal**: Core functionality for basic task management

**Features:**
- US-001 to US-004: Authentication
- US-005 to US-006: Company management (basic)
- US-007 to US-009: Project management (basic)
- US-010 to US-014: Task CRUD and status
- US-017, US-020: Basic time logging

**Success Criteria:**
- Users can create and manage tasks
- Basic hierarchy (2 levels)
- Time tracking functional

### Phase 2: Enhanced Task Management (Weeks 7-10)
**Goal**: Advanced task features and hierarchy

**Features:**
- US-015: Task hierarchy/tree view
- US-016: Task filtering
- US-012: Subtask creation
- US-018 to US-019: Timer functionality
- US-021 to US-022: Time log management

**Success Criteria:**
- Unlimited nesting works efficiently
- Time tracking complete (manual + timer)
- Task navigation is intuitive

### Phase 3: Discord Integration (Weeks 11-13)
**Goal**: Bot commands and notifications

**Features:**
- US-023 to US-026: Discord bot commands
- US-027: Discord notifications
- Discord ID linking in user profile

**Success Criteria:**
- 4 bot commands working reliably
- Notifications deliver promptly
- Bot handles errors gracefully

### Phase 4: Reporting & Analytics (Weeks 14-16)
**Goal**: Management visibility and insights

**Features:**
- US-028: Delayed tasks report
- US-029: Time tracking report
- US-030: Completion metrics
- Dashboard with key metrics

**Success Criteria:**
- All 3 report types functional
- Reports export to CSV
- Metrics help identify bottlenecks

### Phase 5: Polish & Scale (Weeks 17-20)
**Goal**: Performance, bug fixes, and preparation for full rollout

**Activities:**
- Performance optimization
- Security audit
- User acceptance testing
- Documentation completion
- Training materials
- Bug fixes from feedback

**Success Criteria:**
- All acceptance criteria met
- Performance targets achieved
- Users trained and ready
- Production deployment successful

---

## 8. Open Questions

1. **Data Migration**: Is there existing task data to migrate from current tools?
2. **Discord Channels**: Which Discord channels should receive notifications?
3. **Email Fallback**: Should email notifications be implemented as fallback to Discord?
4. **Custom Fields**: Do tasks need custom fields beyond the current specification?
5. **Integrations**: Priority of GitLab integration vs other potential integrations?
6. **Mobile Priority**: Is mobile app needed within first year?

---

## 9. Approval

**Product Owner Approval:**
- [ ] Specification reviewed and approved
- [ ] Scope confirmed
- [ ] Priority alignment confirmed
- [ ] Success metrics agreed upon

**Sign-off:**
| Role | Name | Signature | Date |
|------|------|-----------|------|
| Product Owner | | | |
| Technical Lead | | | |
| Stakeholder | | | |

---

## 10. Appendix

### A. Glossary
- **Task Code**: Unique identifier combining project and division codes
- **Changelog**: Audit trail of all task status changes
- **PIC**: Person In Charge (user who made the change)
- **MVP**: Minimum Viable Product
- **US**: User Story

### B. Reference Documents
- Technical Specification: `task_management_version01_spec.md`
- Risk Assessment: `task_management_version01_risks.md`

### C. Revision History
| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 0.1 | 2026-03-31 | System | Initial draft |

---

*End of PRD v01*

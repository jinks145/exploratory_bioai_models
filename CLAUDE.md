# Claude Code Instructions - Pharmacoepigenomics Project

## Project Context

This is a biomedical machine learning project for predicting cancer drug response using DNA methylation and gene expression data. Read `.claude/template.md` for full session history and current status.

## Session Management Triggers

When the user says any of these phrases, execute the corresponding workflow:

### Save Progress Triggers
**Trigger phrases**: "save progress", "checkpoint", "save state", "save session", "update progress"

**Actions**:
1. Update `.claude/template.md` with a new session section:
   - What was accomplished (with checkmarks)
   - Current data status
   - Key technical details
   - What needs to be done next
   - File locations for next session
   - Known issues/notes
2. Verify git status (ensure large files are gitignored)
3. Provide brief summary to user

### End Session Triggers
**Trigger phrases**: "prepare for next session", "end session", "wrap up", "finish session", "done for today"

**Actions**:
1. Follow full workflow in `.claude/SESSION_WORKFLOW.md`:
   - Update `.claude/template.md` with comprehensive session summary
   - Check `.gitignore` for new data files
   - Create placeholder files for new directories
   - Update TODO list
   - Verify git status (large files ignored)
2. Create handoff summary with:
   - What was completed
   - What's ready to commit
   - Next session starter prompt
3. Display the next session starter prompt for the user to copy

### Resume Session Triggers
**Trigger phrases**: "continue session", "resume", "pick up where we left off", "what's the status"

**Actions**:
1. Read `.claude/template.md` for previous session summary
2. Read context files in `.claude/context/` folder
3. Summarize current project state
4. List immediate next steps
5. Ask user what they'd like to work on

### Progress Check Triggers
**Trigger phrases**: "summarize progress", "what have we done", "progress report", "status update"

**Actions**:
1. Read current `.claude/template.md`
2. Provide concise summary of:
   - Completed tasks
   - Current data status
   - Pending items
3. Do NOT update files (read-only check)

## Data Files Policy

- **Always gitignore**: `.csv.gz`, `.csv` data files, `.pdf`, figures, model files
- **Track in git**: Source code, notebooks (without large outputs), markdown documentation
- **Data location**: `data/processed/` contains ML-ready datasets
- **Never commit files > 1MB** without user approval

## Key File Locations

- **Session state**: `.claude/template.md`
- **Workflow instructions**: `.claude/SESSION_WORKFLOW.md`
- **Quick reference**: `.claude/SESSION_COMMANDS.md`
- **Project context**: `.claude/context/project_details.md`
- **Coding standards**: `.claude/context/coding_standards.md`
- **Main datasets**: `data/processed/ml_with_gene_expr.csv.gz`
- **Active notebooks**: Root directory (`.ipynb` files)
- **Reference notebooks**: `notebooks/reference/`

## Coding Standards

- Use NumPy-style docstrings
- Type hints for function parameters
- Naming: `df_` prefix for DataFrames, `arr_` for arrays
- Random seed = 42 for reproducibility
- Follow existing patterns in `src/` modules

## Research Context

- **Primary dataset**: 987 cancer cell lines with methylation + gene expression
- **Features**: 10K CpG sites + 5K genes
- **Targets**: IC50 drug response for 375 compounds
- **Current focus**: Model generalization across cancer types
- **Evaluation**: Random splits, histology-based splits, site-based splits

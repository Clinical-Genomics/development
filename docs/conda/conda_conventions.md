# Conda conventions

This document describes how to name your conda environments.

Examples:

Production environment for microsalt:
```
P_usalt
```

Stage environment for microsalt:
```
S_usalt
```

A development environment for microsalt:
```
D_fix-microbial-coverage_190517_IS
```

## Naming conventions 

   - Production: `P_[name]`
   - Stage: `S_[name]`
   - Development: `D_[name]_[creation_date]_[signature]`
   - Archive: `A_[name]_[timestamp]_[signature]`

With:

   - creation_date: `%y%m%d`
   - timestamp: `%y%m%d %H%M%S`.
   - name: whatever makes sense.
   - signature: showing who created the environment. Use the two- or three letter name acronyms assigned to you.

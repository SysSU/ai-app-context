# Execute BASE PRP

## PRP File: $ARGUMENTS

## Mission: One-Pass Implementation Success

PRPs enable working code on the first attempt through:

- **Context Completeness**: Everything needed, nothing guessed
- **Progressive Validation**: 4-level gates catch errors early
- **Pattern Consistency**: Follow existing codebase approaches
- Read PRPs/README.md to understand PRP concepts

**Your Goal**: Transform the PRP into working code that passes all validation gates.

## Execution Process

1. **Load PRP**
   - Read the specified PRP file completely
   - Absorb all context, patterns, requirements and gather codebase intelligence
   - Follow all instructions in the PRP and extend the research if needed
   - Use the provided documentation references and file patterns, consume the right documentation before the appropriate todo/task
   - Trust the PRP's context and guidance - it's designed for one-pass success
   - Ensure you have all needed context to implement the PRP fully
   - Do more web searches and codebase exploration as needed

2. **ULTRATHINK & Plan**
   - Ultrathink before you execute the plan. Create a comprehensive plan addressing all requirements
   - Break down into clear todos using TodoWrite tool
   - Use agents, subagents and batchtool to enhance the process
   - **Important**: YOU MUST ENSURE YOU HAVE EXTREMELY CLEAR TASKS FOR SUBAGENTS AND REFERENCE CONTEXT AND MAKE SURE EACH SUBAGENT READS THE PRP AND UNDERSTANDS ITS CONTEXT
   - Identify implementation patterns from existing code to follow
   - Follow the patterns referenced in the PRP
   - Use specific file paths, class names, and method signatures from PRP context
   - Never guess about imports, file names, function names etc - ALWAYS be based in reality and real context gathering

3. **Execute Implementation**
   - Follow the PRP's Implementation Tasks sequence, add more detail as needed, especially when using subagents
   - Use the patterns and examples referenced in the PRP
   - Follow TypeScript/JavaScript best practices (when applicable)
   - Ensure proper type safety and error handling
   - Follow existing codebase patterns and conventions
   - Create files in locations specified by the desired codebase tree
   - Apply naming conventions from the task specifications and CLAUDE.md

4. **Progressive Validation**

   **Execute the level validation system from the PRP:**
   - **Level 1**: Run syntax & style validation commands from PRP
   - **Level 2**: Execute unit test validation from PRP
   - **Level 3**: Run integration testing commands from PRP
   - **Level 4**: Execute specified validation from PRP

   **Each level must pass before proceeding to the next.**
   
   - Run each validation command from the PRP
   - The better validation that is done, the more confident we can be that the implementation is correct
   - Fix any failures (type errors, linting issues, test failures)
   - Re-run until all pass
   - Always re-read the PRP to validate and review the implementation to ensure it meets the requirements

5. **Completion Verification**
   - Work through the Final Validation Checklist in the PRP
   - Verify all Success Criteria from the "What" section are met
   - Confirm all Anti-Patterns were avoided
   - Ensure all checklist items done
   - Run final validation suite
   - Report completion status
   - Read the PRP again to ensure you have implemented everything
   - Implementation is ready and working

6. **Reference the PRP**
   - You can always reference the PRP again if needed

**Failure Protocol**: When validation fails, use error patterns and gotchas from the PRP to fix issues, then re-run validation until passing.

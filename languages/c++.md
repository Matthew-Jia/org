# Assembly

## Section keyword

In assembly, a Section is a way of categorizing data and instructions so the linker and the CPU know how to treat different parts of your binary. There are three main sections:

- .text: Contains the actual machine code instructions and must include a global entry point label (usually \_start) for the linker.
- .data + .rodata: This section is used for declaring initialized data (.data) that might change over the program's execution, or constants (.rodata, or ``Read-Only" data) that do not change during the program's execution.
- .bss (Block Started by Symbol): This section is used for uninitialized global or static variables (local variables are on the stack). It essentially takes up zero bytes in the binary and is zeroed out by the OS at program start time. The only thing that remains in the .bss section in the binary is the virtual address that it starts (important because the linker has made assembly the relies on where it believes the .bss section starts) and the size (so the OS knows how much space it needs to zero out).

The System V ABI defines a specific ``priority list" for integer and pointer arguments. When you call a function, the compiler (or you, in assembly) must place the arguments in this exact order:

\begin{tabular}{lc}
	\toprule
	Argument # & Register \\
	\midrule
	1st & RDI\\
	2nd & RSI\\
	3rd & RDX\\
	4th & RCX\\
	5th & R8\\
	6th & R9\\
	\bottomrule
\end{tabular}~\\

If a function has more than 6 arguments, the rest are pushed onto the stack in reverse order.

# Keywords

## Restrict Keyword 

C++ doesn't not have standard support for restrict, but many compilers have equivalents that usually work in both C++ and C, such as GCC's and Clang's \_\_restrict\_\_. Restrict is a type qualifier that hints to the compiler a pointer will not be aliased during its lifetime, aiding optimizations like vectorization that would not otherwise be possible. If the declaration of intent is not followed (i.e. the object is accessed by an independent pointer), this will result in undefined behavior.

## Inline Keyword

- Indicates to the compiler that ``inline substitution of a function" is preferred over normal function call, that is, instead of jumping to the funciton body stored in a seperate location in memory, replace the call to the function with a copy of the contents of the function body directly in the binary. The decision to actually execute inline substitution of a function is still up to the compiler.
    - Pros: 
        - Eliminates the overhead of funciton call (passing args from callee to caller, and vice verca + jump instruction to function)
    - Cons: 
        - Increases binary size since function bodys are duplicated in the binary rather than kept out-of-line in one location in memory.
        - Since inline instructions aren't stored in the same spot in memory, execessive use of inline and specific cases of inlined functions could put pressure on the icache whereas an out-of-line function will like in the same spot in memory and always take up the same cache lines in the icache. Some examples of this happening might be an inline function called in an unrolled loop, or frequent calls to the inline function in multiple different areas of the code.

- An inline entity with external linkage can be defined more than once as long as all definitions are identical. In this case, the language-level guarantee is that the program behaves as though there is one shared entity.
    - Great for header files that want to define an entity with external linkage, as each include of that header file in a different translation unit, once linked together, would cause a violation of the ODR.

- Inline static data members is a definition rather than just a declaration. This allows you to define a static member variable on the same line as its declaration in the class rather than needing a seperate line for the definition of the static data member.

- Inline const variables at namespace scope have external linkage by default, unlike the non-inline non-volatile const-qualified variables, which have internal linkage. 
    - Reasoning: before C++17 inline variables existed, C++ wanted const qualified variables in header files to work naturally. Since you couldn't inline variables back then, a simple const variable in a header file would cause ODR violations between linked translation units that both include this header file (alternatively, you would need to use the extern keyword to declare the variable without definiting it, and define the variable in a src file). With the introduction if inline variables, this is no longer a problem, so inline const variables were changed back to the intuitive external linkage.
    - This is actually significant. An internally linked variable means that the same const variable across translation units are completely different in memory and thus are their own seperate objects (constructors are called multiple times, mutable member variable states are different, etc.), wheinline reas an externally linked variable means that the same inline const variable across translation units are the exact same location in memory, making them the same object (one constructor is run, all member variables are shared, etc).

- Inline static entities at the namespace scope are internally linked due to the static keyword. This is useless for variables but not entirely useless for functions (since they still hint to the compiler to use ``inline substitution of a function").

Note: If an inline variable that is externally linked must be evaluated at runtime, the compiler will generate locks/guards to ensure that its initialization runs exactly once, even if multiple threads attempt to access it before main() begins.

## Extern Keyword

Extern is a linkage specifier used to declare a variable or function without defining it. It is mainly useful for solving ODR violations, especially in header files, but can also be used to declare variables at block scope. This works exactly the same way as declaring an extern variable at the namespace scope, but with the obvious fact that the extern variable is only useable within the block scope its declared in.

\textbf{Note:} extern and static cannot be used together for the same variable declaration, but extern can be used to declare a variable following a static definition of the same varaible at namespace scope, causing the varaible declared extern to refer to the same object as the one declared static and continue to have internal linkage. This is considered bad practice and highly confusing.

# Linkage Types

A name in C++ can have 4 different types of linkage

## Internal Linkage:
Names that can be used by declarations within the same translation unit to refer to the same entity, but declarations in other translation units cannot refer to that entity. 

- Done through the static keyword, global const variables (non-inline non-volatile const-qualified variables), unnamed namespaces, and data members of an anonymous union.
- Defining an internal-linkage entity in a header does not ordinarily cause an ODR violation by itself, because each translation unit receives a distinct entity. However, they can still lead to undefined behavior expecially when used in an inline function shared across multiple translation units. In this case, the inline function would violate the ``must be identical defintions" requirement, since they would access their own internally linked entity. This is not allowed for inline functions since the standard requires each defintion to be identical. See (\ref{inline}) for more. 

## External Linkage
Names that can be used by declarations within all linked translation units to refer to the same entity.
- An name decalared at namespace scope has external linkage by default, unless a rule changes it to internal linkage or module linkage. These rules are:
    - static $\rightarrow$ internal linkage
    - Non-volatile Const variables $\rightarrow$ internal linkage
    - inside unnamed namespace $\rightarrow$ internal linkage
    - attatched to a named module but not exported $\rightarrow$ module linkage
    - otherwise $\rightarrow$ external linkage
- If more than one translation unit has its own definition of this externally linked name, then two such entities exist and symbols across these linked translation unit will not know which entity to bind to. The ``Inline" keyword can be used to fix this, see (\ref{inline}) for more.

## Module Linkage
TODO

## No Linkage:
An name that cannot be redeclared in another scope in a way that reconnects to the same entity.

- Names declared at the block scope with the following have no linkage:
    - variables that are not explicitly declared extern
    - local classes (classes declared at block scope) and their methods 
    - other names declared at block scope such as typedefs, enums, and enumerators.
    - funcitons cannot have no linkage, since they are by default external linkage, unless declared static, in which case it has internal linkage, and functions cannot be nested within functions (unlike classes), meaning it can't be declared at block scope.

Another way to think about linkage is to think about what symbols can bind to which entity. An name defined with no linkage creates entities that can only be bound to by symbols within its scope. A name defined with internal (external) linkage creates an object that can be bound to by symbols within its translation unit (its linked translation unit). 

# One Definition Rule (ODR)}

A fundamental rule in C++ stating that no variable, function, class, or template can have more than one definition within a specific scope, ensuring identical definitions exist across files.

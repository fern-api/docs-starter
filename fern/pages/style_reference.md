# C++ Library Docs Style Reference

This document captures micro-level formatting decisions extracted from the 12 golden pages. It complements the Rendering Rules document with exact spacing, prop patterns, and stylistic conventions.

---

## Blank Line Conventions

### Between top-level elements in the preamble

One blank line between each preamble element (summary, include header, callouts, see also, template params, inherits from).

**Example** (from `pointer_v4.mdx`):
```mdx
`pointer` stores a pointer to an object allocated in memory.

Like [`device_ptr`](/library/api/thrust::device_ptr), this type ensures type safety ...

```cpp showLineNumbers={false}
#include <thrust/pointer.h>
```

<Note>
`pointer` is not a smart pointer; ...
</Note>

**See also:**
[device_ptr](/library/api/thrust::device_ptr),
reference,
[raw_pointer_cast](/library/api/thrust::raw_pointer_cast)

<AccordionGroup>
```

### Inside Tabs

One blank line after `<Tab title="...">` before content. One blank line before `</Tab>`.

**Example** (from `block_reduce_v3.mdx`):
```mdx
<Tab title="Single item">

Computes a block-wide reduction for thread<sub>0</sub> ...

<CodeBlock links={{...}}>
```cpp showLineNumbers={false}
...
```
</CodeBlock>

*Added in v2.2.0. First appears in CUDA Toolkit 12.3.*

- The return value is undefined ...

**Template parameters**

<ParamField path="ReductionOp" type="typename">
...
</ParamField>

**Parameters**

<ParamField path="input" type="T">
...
</ParamField>

**Example**

The code snippet below ...

```cpp showLineNumbers={false}
...
```

</Tab>
```

### Between ParamFields

One blank line between consecutive `<ParamField>` components.

**Example** (from `block_reduce_v3.mdx`):
```mdx
<ParamField path="input" type="T">
Calling thread's input
</ParamField>

<ParamField path="reduction_op" type="ReductionOp">
Binary reduction functor
</ParamField>
```

### Between heading and content

One blank line between an H3 heading and the following content (description or Tabs).

**Example** (from `device_vector_v3.mdx`):
```mdx
### size <Badge intent="note" minimal>const</Badge>

Returns the number of elements in this vector.
```

### Between method sections (same H2)

One blank line after the last element of one method, then the next H3 heading. When methods within the same H2 section are separated by `---`, the pattern is:

```mdx
(end of method content)

---

### NextMethodName <Badge ...>
```

### Between CodeBlock and version annotation

One blank line between `</CodeBlock>` and the italic version annotation.

```mdx
</CodeBlock>

*Added in v2.2.0. First appears in CUDA Toolkit 12.3.*
```

### Between version annotation and callouts/bullets

One blank line between the version annotation and callout components or bullet lists.

```mdx
*Added in v2.2.0. First appears in CUDA Toolkit 12.3.*

- The return value is undefined ...
```

### Between callouts/bullets and Parameters heading

One blank line between callout content and `**Parameters**`.

### Between Returns and Parameters

`**Returns:**` comes BEFORE `**Parameters**` when both are present (only seen in assignment operators). More commonly, `**Returns:**` comes AFTER `**Parameters**`. Actually, looking at the golden pages:

Standard order within a method/tab:
1. Description text
2. CodeBlock (signature)
3. Version annotation (italic)
4. Callouts / behavioral notes
5. `**Template parameters**` + ParamFields
6. `**Parameters**` + ParamFields
7. `**Returns:**` line
8. `**Throws:**` line
9. `**Example**` + code block

**Exception for assignment operators and short methods** (from `device_vector_v3.mdx`):
```mdx
**Returns:** `device_vector &`

**Parameters**

<ParamField ...>
```
Here, Returns comes BEFORE Parameters. This pattern is used when the return value is short and the parameters are the main content.

**The canonical order depends on the golden pages.** Analyzing all instances:
- In `device_vector_v3.mdx` (operator=, operator[], front, back, data, iterators, etc.): **Returns** comes BEFORE **Parameters**
- In `block_reduce_v3.mdx` (Reduce, Sum): **Returns** is absent (returns the value directly, described in prose), Parameters come after Template parameters
- In `simple_struct_v4.mdx` (operator()): **Returns** comes AFTER **Parameters**
- In `pointer_v4.mdx` (get, base, base_reference): **Returns** comes after CodeBlock, no Parameters
- In `group_member_example_v4.mdx` (do_allocate): **Returns** comes BEFORE **Parameters**

**Rule:** `**Returns:**` comes immediately after the behavioral callouts/notes, BEFORE `**Parameters**`. If there are template parameters, the order is: Returns, then Template parameters, then Parameters. However, this is not consistent -- some pages put Returns after Parameters. The most common pattern across golden pages is:

**Returns before Parameters** when the method is primarily characterized by its return value.
**Returns after Parameters** when the method is primarily characterized by what it does with its parameters.

For consistency, adopt the most common golden page pattern: **Returns BEFORE Parameters**.

---

## Component Prop Patterns

### CodeBlock

```mdx
<CodeBlock links={{"ShortName": "/path/to/api"}}>
```cpp showLineNumbers={false}
signature
```
</CodeBlock>
```

- Always `showLineNumbers={false}` on the inner code fence
- `links` prop is a JSON object mapping identifier strings to path strings
- Multiple links separated by commas: `{{"A": "/path/a", "B": "/path/b"}}`

### ParamField

```mdx
<ParamField path="param_name" type="ParamType">
Description text.
</ParamField>
```

With default:
```mdx
<ParamField path="param_name" type="ParamType" default="default_value">
Description text.
</ParamField>
```

- `path`: The parameter name exactly as it appears in the signature
- `type`: The full type string (may include `const`, `&`, `*`, template parameters)
- `default` (optional): The default value as a string

### Badge

Qualifier badge:
```mdx
<Badge intent="note" minimal>qualifier_text</Badge>
```

Entity-kind badge:
```mdx
<Badge intent="info">C++20 concept</Badge>
```

- Qualifier badges always use `intent="note"` and `minimal`
- Entity-kind badges use `intent="info"` without `minimal`
- Multiple badges separated by a single space on the same line

### Accordion

```mdx
<AccordionGroup>
<Accordion title="Template parameters">

(ParamField components)

</Accordion>
</AccordionGroup>
```

- Always wrapped in `<AccordionGroup>`
- Title is always `"Template parameters"`
- Blank line after `<Accordion title="...">` and before `</Accordion>`

### Callouts

```mdx
<Note>
Content text.
</Note>

<Warning>
Content text with **bold** or `code`.
</Warning>

<Error title="Deprecated">
Use `alternative` instead.
</Error>

<Info title="Postconditions">
State description.
</Info>
```

- `<Error>` always has `title="Deprecated"` for deprecation notices
- `<Info>` uses `title="Postconditions"` for postconditions, or other custom titles
- `<Note>` and `<Warning>` typically have no `title` prop
- Blank line after opening tag, content, blank line before closing tag (or content directly between tags with no extra blank lines -- both patterns appear)

---

## Tab Title Conventions

### Constructor Tab Titles

| Scenario | Title |
|---|---|
| No-argument default | `"Default"` or `"Default constructor"` |
| From nullptr | `"From nullptr"` |
| From raw pointer | `"From raw pointer"` |
| From other pointer/type | `"From other pointer"`, `"From other device_vector type"` |
| From specific type | `"From std::vector"`, `"From vector_base"`, `"From initializer_list"` |
| With an allocator | `"With allocator"` |
| With a config object | `"With TempStorage"`, `"With upstream and bookkeeper"`, `"With default resources"` |
| Move | `"Move"`, `"Move with allocator"` |
| Copy | `"Copy constructor"`, `"From device_vector"` |
| Copy with allocator | `"From device_vector with allocator"` |
| Size variants | `"Value-initialized"`, `"Default-initialized"`, `"No-init"` |
| Fill variants | `"n copies of value"`, `"n copies with allocator"` |
| Range | `"From iterator range"`, `"From iterator range with allocator"` |
| Deleted | `"Copy (deleted)"` |

### Method Overload Tab Titles

| Scenario | Title |
|---|---|
| Single item vs array | `"Single item"`, `"Multiple items per thread"` |
| Partial operation | `"Partial tile"`, `"Partial warp"` |
| Full vs partial | `"Full warp"`, `"Partial warp"` |
| With aggregate output | `"With aggregate"`, `"With prefix callback"` |
| Const/Mutable | `"Mutable"`, `"Const"` |
| Copy/Move assign | `"Copy assign"`, `"Move assign"` |
| Functional | `"Fill"`, `"Range"`, `"Single element"` |
| Pre/Post | `"Pre-increment"`, `"Post-increment"`, `"Pre-decrement"`, `"Post-decrement"` |
| With/without stream | `"With stream"`, `"Default stream"` |
| Deprecated variant | `"Deprecated (no args)"` |
| Deleted | `"Copy assign (deleted)"`, `"Deleted overloads"` |

---

## Heading Hierarchy

| Level | Usage | Examples |
|---|---|---|
| **H1** | Never used | -- |
| **H2** (`##`) | Top-level body sections | `## Constructors`, `## Methods`, `## Types`, `## Member variables`, `## Inner classes`, `## Performance considerations`, `## Example`, `## Description`, `## Related concepts`, `## Collective constructors`, `## Generic reductions`, `## Summation reductions`, `## Exclusive prefix sum operations`, `## Assignment operators`, `## Element access`, `## Iterators`, `## Capacity`, `## Modifiers`, `## Allocator`, `## Static methods`, `## Friend functions`, `## Pool management`, `## Allocation`, `## Comparison`, `## Ownership`, `## Accessors`, `## Synchronization`, `## Query methods`, `## Event recording`, `## Device information`, `## Increment operators`, `## Compound assignment operators`, `## Resource and stream management`, `## Segmented reductions`, `## Max reductions`, `## Min reductions`, `## Utility methods` |
| **H3** (`###`) | Individual members | Method names, constructor names, destructor label, inner class names, `### Typedefs`, `### Destructor` |
| **H4** (`####`) | Never used | Use `**Bold text**` instead |

---

## Cross-Ref Path Format

### Per-Library Path Patterns

| Pattern | Path format | Example |
|---|---|---|
| CUB classes | `/library/api/cub::ClassName` | `/library/api/cub::BlockReduce` |
| CUB nested types | `/library/api/cub::ClassName::TypeName` | `/library/api/cub::BlockReduce::TempStorage` |
| CUB enums | `/library/api/cub::EnumValue` | `/library/api/cub::BLOCK_REDUCE_WARP_REDUCTIONS` |
| CUB methods | `/library/api/cub::ClassName::MethodName` | `/library/api/cub::BlockReduce::_TempStorage` |
| Thrust classes | `/library/api/thrust::ClassName` | `/library/api/thrust::device_vector` |
| Thrust nested types | `/library/api/thrust::ClassName::TypeName` | `/library/api/thrust::device_vector::size` |
| Thrust free functions | `/library/api/thrust::FunctionName` | `/library/api/thrust::raw_pointer_cast` |
| Thrust nested namespaces | `/library/api/thrust::mr::ClassName` | `/library/api/thrust::mr::memory_resource` |
| libcudacxx classes | `/libcudacxx/api/cuda::ClassName` | `/libcudacxx/api/cuda::counting_iterator` |
| libcudacxx nested | `/libcudacxx/api/cuda::ClassName::Member` | `/libcudacxx/api/cuda::stream::sync` |
| libcudacxx cross-ref from other pages | `/libcudacxx/api/cuda::ClassName` | `/libcudacxx/api/cuda::stream_ref` |
| cuda::mr concepts | `/library/api/cuda::mr::ConceptName` | `/library/api/cuda::mr::resource` |
| cuda:: concepts/traits | `/library/api/cuda::ConceptName` | `/library/api/cuda::has_property` |

**Key distinction:** `cuda::` entities that are part of libcudacxx use `/libcudacxx/api/` prefix. `cuda::mr::` concepts referenced from the concept_example page use `/library/api/` prefix. This distinction maps to the library the entity belongs to.

### In-Signature Links

Links in `<CodeBlock links={{...}}>` map short identifiers to full paths:

```mdx
<CodeBlock links={{"BlockReduce": "/library/api/cub::BlockReduce"}}>
```

```mdx
<CodeBlock links={{"device_vector": "/library/api/thrust::device_vector"}}>
```

```mdx
<CodeBlock links={{"counting_iterator": "/libcudacxx/api/cuda::counting_iterator"}}>
```

```mdx
<CodeBlock links={{"buffer": "/libcudacxx/api/cuda::buffer", "stream_ref": "/libcudacxx/api/cuda::stream_ref"}}>
```

### In-Text Links

Markdown link format: `[display text](/path/to/api)`

**Example** (from `device_vector_v3.mdx`):
```mdx
[size()](/library/api/thrust::device_vector::size)
```

**Example** (from `concept_example_v3.mdx`):
```mdx
[`cuda::mr::resource`](/library/api/cuda::mr::resource)
```

---

## Badge Conventions

### Which intent for which purpose

| Badge text | Intent | Minimal | When used |
|---|---|---|---|
| `inline` | `note` | yes | Method/constructor qualifier |
| `const` | `note` | yes | Method qualifier |
| `static` | `note` | yes | Method qualifier, member variable qualifier |
| `virtual` | `note` | yes | Method qualifier |
| `explicit` | `note` | yes | Constructor/conversion qualifier |
| `constexpr` | `note` | yes | Method/variable qualifier |
| `noexcept` | `note` | yes | Method qualifier |
| `nodiscard` | `note` | yes | Method qualifier |
| `final` | `note` | yes | Class qualifier |
| `C++20 concept` | `info` | no | Entity-kind indicator |

### Badge ordering on H3 headings

Badges appear in a consistent order. The observed canonical order is:

1. `inline`
2. `static`
3. `constexpr`
4. `explicit`
5. `const`
6. `noexcept`
7. `nodiscard`
8. `virtual`
9. `final`

**Example** (from `deep_template_class_v4.mdx`):
```mdx
### operator* <Badge intent="note" minimal>inline</Badge> <Badge intent="note" minimal>constexpr</Badge> <Badge intent="note" minimal>const</Badge> <Badge intent="note" minimal>noexcept</Badge> <Badge intent="note" minimal>nodiscard</Badge>
```

**Example** (from `group_member_example_v4.mdx`):
```mdx
### do_allocate <Badge intent="note" minimal>inline</Badge> <Badge intent="note" minimal>nodiscard</Badge> <Badge intent="note" minimal>virtual</Badge>
```

**Example** (from `pointer_v4.mdx`):
```mdx
### operator bool <Badge intent="note" minimal>inline</Badge> <Badge intent="note" minimal>explicit</Badge> <Badge intent="note" minimal>const</Badge>
```

### Badge placement in member variable tables

Badges for `static` and `constexpr` go in the Name cell, after the variable name:

```mdx
| `BLOCK_THREADS` <Badge intent="note" minimal>static</Badge> <Badge intent="note" minimal>constexpr</Badge> | `int` | The thread block size in threads. |
```

---

## Signature Formatting

### General rules

- Signatures are always inside `<CodeBlock>` with `showLineNumbers={false}`
- Fully-qualified name: `namespace::ClassName<TemplateParams>::MethodName`
- Template prefix on its own line when present
- Parameters indented with 4 spaces when multi-line
- Closing `)` on same line as last parameter, or on its own line for `const`/`noexcept` qualifiers

### Template prefix

When a method has its own template parameters, the template line comes first:

```cpp
template <typename ReductionOp>
T cub::BlockReduce<T, BlockDimX, Algorithm, BlockDimY, BlockDimZ>::Reduce(
    T input,
    ReductionOp reduction_op
)
```

### Multi-parameter line breaking

Parameters are each on their own line, indented with 4 spaces:

```cpp
void cub::BlockScan<T, BlockDimX, Algorithm, BlockDimY, BlockDimZ>::ExclusiveSum(
    T input,
    T &output,
    T &block_aggregate
)
```

### Single-parameter or no-parameter signatures

May be on one line:

```cpp
T cub::WarpReduce<T, LogicalWarpThreads>::Sum(
    T input
)
```

Or inline:

```cpp
size_type thrust::device_vector<T, Alloc>::size() const
```

### Const/noexcept qualifiers on signatures

Appear after the closing `)`:

```cpp
const_reference thrust::device_vector<T, Alloc>::front() const
```

```cpp
void cuda::buffer<_Tp, _Properties>::swap(
    buffer &__other
) noexcept
```

### SFINAE / enable_if in signatures

Rendered as-is in the signature:

```cpp
template <typename InputType,
          ::cuda::std::enable_if_t<
              detail::is_fixed_size_random_access_range_v<InputType>, int> = 0>
T cub::WarpReduce<T, LogicalWarpThreads>::Sum(
    const InputType &input
)
```

### Deleted functions

```cpp
cuda::stream::stream(
    const stream &
) = delete
```

### Default arguments in signatures

```cpp
thrust::mr::disjoint_unsynchronized_pool_resource< Upstream, Bookkeeper >::disjoint_unsynchronized_pool_resource(
    Upstream *upstream,
    Bookkeeper *bookkeeper,
    pool_options options = get_default_options()
)
```

---

## Description Segment Rendering

The IR contains description segments of various types. Here is how each renders in MDX:

### Plain text (DocTextSegment)

Rendered as-is in markdown.

### Code references (DocCodeSegment)

Wrapped in backticks: `` `code_here` ``

### Bold text (DocBoldSegment)

Wrapped in `**bold**`.

### Italic text (DocItalicSegment)

Wrapped in `*italic*`.

### Links/references (DocRefSegment)

Rendered as markdown links: `[display text](/path/to/target)`

### Subscript

Using HTML: `thread<sub>0</sub>`, `lane<sub>0</sub>`

### Superscript

Using HTML: `*i*<sup>th</sup>`

### Inline math / special formatting

Rendered using HTML tags or markdown as appropriate.

---

## Separator Usage

### Where `---` goes

1. After the preamble (before first H2 body section)
2. Between each H2 body section
3. Between distinct H3 methods within the same H2 section (when they are different method names, not overloads)

### Where `---` does NOT go

1. Between overloads of the same method (use Tabs instead)
2. Between the `### Destructor` label and `### ~ClassName`
3. After the very last section on the page

### Example structure (from `warp_reduce_v4.mdx`)

```mdx
## Segmented reductions

### HeadSegmentedSum <Badge intent="note" minimal>inline</Badge>

(content)

---

### TailSegmentedSum <Badge intent="note" minimal>inline</Badge>

(content)

---

### HeadSegmentedReduce <Badge intent="note" minimal>inline</Badge>

(content)

---

### TailSegmentedReduce <Badge intent="note" minimal>inline</Badge>

(content)

---

## Types
```

---

## Version Annotation Format

**Format:** Italic text, standalone line.

**Full form:**
```mdx
*Added in v2.2.0. First appears in CUDA Toolkit 12.3.*
```

**Rules:**
- Always italic (wrapped in `*...*`)
- Period after each sentence
- Appears on its own line immediately after `</CodeBlock>`
- One blank line before and after
- If no version info is available, omit entirely

---

## Table Formatting

### Column headers and alignment

Always use `|---|` (no alignment colons) between header and body:

```mdx
| Name | Definition | Description |
|---|---|---|
| `TypeName` | `Definition` | Description text. |
```

### When to use 2 vs 3 columns for typedefs

**3-column** (Name | Definition | Description): When ANY typedef in the table has a description.

**Example** (from `block_reduce_v3.mdx`):
```mdx
| Name | Definition | Description |
|---|---|---|
| `InternalBlockReduce` | `...` | Internal specialization type. |
| `_TempStorage` | `...` | Shared memory storage layout type for ... |
| `WarpReductions` | `...` | |
```

**2-column** (Name | Definition): When NO typedefs have descriptions.

**Example** (from `device_vector_v3.mdx`):
```mdx
| Name | Definition |
|---|---|
| `Parent` | `detail::vector_base< T, Alloc >` |
```

**Example** (from `deep_template_class_v4.mdx`):
```mdx
| Name | Definition |
|---|---|
| `value_type` | `_Start` |
| `difference_type` | `_IotaDiffT<_Start>` |
```

### Member variable table format

Always 3-column: Name | Type | Description.

```mdx
| Name | Type | Description |
|---|---|---|
| `variable_name` | `type` | Description. |
```

Badges in Name column:
```mdx
| `default_priority` <Badge intent="note" minimal>static</Badge> <Badge intent="note" minimal>constexpr</Badge> | `int` | The default stream priority. |
```

Types with links:
```mdx
| `m_options` | [`pool_options`](/library/api/thrust::mr::pool_options) | |
```

Types with reference qualifiers:
```mdx
| `temp_storage` | [`_TempStorage`](/library/api/cub::BlockReduce::_TempStorage) `&` | Shared storage reference. |
```

### Related concepts table format (concept pages only)

2-column: Concept | Description. Concept names are linked.

```mdx
| Concept | Description |
|---|---|
| [`cuda::mr::resource`](/library/api/cuda::mr::resource) | Verifies that a type satisfies ... |
```

### Inner class member tables

3-column (same as member variable tables). Appear directly after the inner class CodeBlock.

```mdx
### chunk_descriptor

<CodeBlock links={{...}}>
```cpp showLineNumbers={false}
struct namespace::ClassName::chunk_descriptor
```
</CodeBlock>

| Name | Type | Description |
|---|---|---|
| `size` | `std::size_t` | |
| `pointer` | `void_ptr` | |
```

---

## Callout Usage

### Which callout type for which IR field

| IR field / concept | Callout component |
|---|---|
| Deprecated flag | `<Error title="Deprecated">` |
| Behavioral notes / preconditions | `<Note>` (or inline bullet list per golden pages, but resolved to use `<Note>`) |
| Warnings about user responsibility | `<Warning>` |
| Postconditions | `<Info title="Postconditions">` |
| Memory allocation notes | `<Note>` |
| Thread safety notes | `<Note>` |
| Destroyed/moved-from state warnings | `<Warning>` |

### Callout placement in method tabs

Callouts appear AFTER the CodeBlock and version annotation, BEFORE template parameters and regular parameters.

**Example order within a Tab** (from `raises_example_v4.mdx`):
```mdx
<Tab title="No-init">

<Badge intent="note" minimal>explicit</Badge> <Badge intent="note" minimal>noexcept</Badge>

Construct a new [`stream`](/libcudacxx/api/cuda::stream) object into the moved-from state.

<CodeBlock links={{...}}>
```cpp showLineNumbers={false}
...
```
</CodeBlock>

<Info title="Postconditions">
[`stream()`](/libcudacxx/api/cuda::stream::stream) returns an invalid stream handle.
</Info>

</Tab>
```

### Callout placement in preamble

Callouts in the preamble appear after the include header, before See Also:

```mdx
```cpp showLineNumbers={false}
#include <thrust/pointer.h>
```

<Note>
`pointer` is not a smart pointer; ...
</Note>

**See also:**
...
```

For deprecated classes, the `<Error>` callout appears after the include header:

```mdx
```cpp showLineNumbers={false}
#include <thrust/strided_iterator.h>
```

<Error title="Deprecated">
Use `cuda::strided_iterator` instead.
</Error>
```

---

## Empty State Rules

### What to omit

| Missing data | Action |
|---|---|
| No summary text | Omit summary paragraph(s); frontmatter description is still present |
| No include header | Omit the include code block |
| No deprecation | Omit `<Error>` callout |
| No see-also refs | Omit `**See also:**` line |
| No class-level example | Omit `## Example` section |
| No performance considerations | Omit `## Performance considerations` section |
| No template parameters | Omit `<AccordionGroup>` entirely |
| No base classes | Omit `**Inherits from:**` line |
| No methods in a category | Omit that H2 section entirely |
| No member variables | Omit `## Member variables` section |
| No inner classes | Omit `## Inner classes` section |
| No typedefs | Omit `### Typedefs` and its table |
| No version annotation | Omit the italic version line |
| No return value (void) | Omit `**Returns:**` line |
| No throws | Omit `**Throws:**` line |
| No method-level example | Omit `**Example**` and code block |
| No parameters | Omit `**Parameters**` heading and ParamFields |
| No template params (method) | Omit `**Template parameters**` heading and ParamFields |
| No description on ParamField | Omit the ParamField component entirely (resolved decision #10) |
| No description on method | Omit description paragraph; keep CodeBlock and other fields |

### What to keep even when seemingly empty

| Element | Always keep |
|---|---|
| Frontmatter `description` | Always present, even if body has no summary |
| `---` separators | Always present between H2 sections |
| CodeBlock for signature | Always present for every method/constructor/destructor |
| H3 heading for method | Always present even with no description |
| `### Destructor` label | Always present before `### ~ClassName` |
| `### Typedefs` heading | Present when there are typedefs to show |

---

## Method Content Ordering Within a Tab

The canonical order of elements inside a `<Tab>` (or for a non-tabbed method):

1. **Overload-specific badges** (standalone line, if any)
2. **Description text** (one or more paragraphs)
3. **CodeBlock** (signature)
4. **Version annotation** (italic, if present)
5. **Callouts** (`<Note>`, `<Warning>`, `<Info>`, `<Error>`)
6. **Returns** (`**Returns:**` line, if present)
7. **Template parameters** (`**Template parameters**` + ParamFields, if present)
8. **Parameters** (`**Parameters**` + ParamFields, if present)
9. **Throws** (`**Throws:**` line, if present)
10. **Example** (`**Example**` + code block, if present)

**Note on Returns placement:** In many golden pages (especially `device_vector_v3.mdx`), **Returns** appears BEFORE **Parameters**. In others (like `simple_struct_v4.mdx`), it appears AFTER. The predominant pattern is Returns before Parameters.

**Alternate observed order (from block_reduce_v3.mdx within Tabs):**
1. Description
2. CodeBlock
3. Version annotation
4. Behavioral bullet points / callouts
5. Template parameters
6. Parameters
7. Example

(No explicit Returns line in block_reduce pages because the return is described in the method description.)

# C++ Library Docs Rendering Rules

This document is the formal rendering specification for generating MDX pages from the C++ Library Docs IR. Every rule is extracted from the 12 golden pages and the resolved inconsistency decisions.

---

## Frontmatter

Every page begins with YAML frontmatter containing exactly two fields: `title` and `description`.

**Rule:**
- `title`: The fully-qualified C++ name (e.g., `cub::BlockReduce`, `thrust::device_vector`, `cuda::counting_iterator`).
  - For names containing angle brackets or special characters, wrap in double quotes.
- `description`: A one-sentence summary of the entity, wrapped in double quotes.

**Example** (from `block_reduce_v3.mdx`):
```yaml
---
title: cub::BlockReduce
description: "Collective methods for computing parallel reductions across a CUDA thread block."
---
```

**Example with special chars** (from `concept_example_v3.mdx`):
```yaml
---
title: "cuda::mr::resource_with"
description: "A concept that verifies a memory resource satisfies both the resource concept and a set of property requirements."
---
```

**Edge cases:**
- If the title contains `::` only (no angle brackets), quoting is optional but recommended for consistency.
- Always quote the description.

---

## Page Layout -- Class/Struct Pages

The canonical section order for class/struct pages is:

### Preamble (before the first `---` separator)

1. **Summary paragraph(s)** -- plain text describing the entity
2. **Include header** -- a bare `cpp` code block (no CodeBlock component)
3. **Callouts** -- `<Error>`, `<Warning>`, `<Note>`, `<Info>` for deprecated/behavioral notes
4. **See also** -- bold label `**See also:**` followed by comma-separated links
5. **Example** -- class-level example with optional introductory sentence + code block
6. **Performance considerations** -- `## Performance considerations` section (only for CUB classes)
7. **Template parameters** -- wrapped in `<AccordionGroup><Accordion title="Template parameters">`
8. **Inherits from** -- bold text `**Inherits from:**` followed by type and access specifier
9. Additional notes (e.g., "This class is marked `<Badge intent="note" minimal>final</Badge>`.")

**Important:** The `---` horizontal rule separates the preamble from the body sections.

### Body Sections (after first `---`)

Sections appear as `## SectionLabel` headings, separated by `---` horizontal rules. The order follows the IR's `sections` array. Common section orderings observed:

1. `## Constructors` (or `## Collective constructors`)
2. `## Assignment operators`
3. `## Element access`
4. `## Iterators`
5. `## Capacity`
6. `## Modifiers`
7. `## Static methods`
8. `## Friend functions`
9. `## Types` (typedefs)
10. `## Member variables`
11. `## Inner classes`

**Example section order** (from `device_vector_v3.mdx`):
```
## Constructors
---
## Assignment operators
---
## Element access
---
## Iterators
---
## Capacity
---
## Modifiers
---
## Allocator
---
## Types
```

**Edge cases:**
- If a class has no members in a category, that section is omitted entirely.
- The `Performance considerations` and `Example` sections in the preamble are H2 headings (part of the preamble, before the first `---`).

---

## Page Layout -- Concept Pages

Concept pages have a different structure since concepts have no constructors, methods, or member variables.

### Preamble

1. **Entity-kind Badge** -- `<Badge intent="info">C++20 concept</Badge>` on its own line
2. **Summary paragraph(s)**
3. **Concept definition signature** -- in a `<CodeBlock>` with links
4. **Template parameters** -- in `<AccordionGroup><Accordion>`

### Body Sections

1. `## Description` -- detailed explanation
2. `## Related concepts` -- table of related concepts

**Example** (from `concept_example_v3.mdx`):
```mdx
<Badge intent="info">C++20 concept</Badge>

The `resource_with` concept verifies that ...

<CodeBlock links={{"resource": "/library/api/cuda::mr::resource", "has_property": "/library/api/cuda::has_property"}}>
```cpp showLineNumbers={false}
template <class _Resource, class... _Properties>
concept resource_with = /* see description */;
```
</CodeBlock>

<AccordionGroup>
<Accordion title="Template parameters">
...
</Accordion>
</AccordionGroup>

---

## Description

...

---

## Related concepts

| Concept | Description |
|---|---|
| [`cuda::mr::resource`](/library/api/cuda::mr::resource) | ... |
```

---

## Page Layout -- Simple Struct Pages

Simple structs (like `cub::ArgMax` from `simple_struct_v4.mdx`) omit sections that don't apply. They follow the same canonical order but only include what's present.

**Example** (from `simple_struct_v4.mdx`):
```
Preamble: summary only (no include header, no template params)
---
## Methods
```

---

## Preamble Sections

### Summary

**Rule:** One or more paragraphs of plain text. The first paragraph should be a concise description. Subsequent paragraphs provide additional detail. Inline code uses backticks. Cross-references use markdown links.

**Example** (from `device_vector_v3.mdx`):
```mdx
A `device_vector` is a container that supports random access to elements, constant time removal of elements at the end, and linear time insertion and removal of elements at the beginning or in the middle.

The number of elements in a `device_vector` may vary dynamically; memory management is automatic. The memory associated with a `device_vector` resides in the memory accessible to devices.
```

**Example with numbered list** (from `block_reduce_v3.mdx`):
```mdx
`BlockReduce` can be optionally specialized by algorithm to accommodate different latency/throughput workload profiles:

1. [`cub::BLOCK_REDUCE_RAKING_COMMUTATIVE_ONLY`](/library/api/cub::BLOCK_REDUCE_RAKING_COMMUTATIVE_ONLY):
   An efficient "raking" reduction algorithm that only supports commutative reduction operators.
2. [`cub::BLOCK_REDUCE_RAKING`](/library/api/cub::BLOCK_REDUCE_RAKING):
   ...
```

### Include Header

**Rule:** Render as a bare fenced code block with `cpp showLineNumbers={false}`. No `<CodeBlock>` component. Appears after the summary paragraphs.

**Example** (from `device_vector_v3.mdx`):
```mdx
```cpp showLineNumbers={false}
#include <thrust/device_vector.h>
```
```

**Edge cases:**
- Not all entities have include headers. If absent, omit entirely.
- Simple structs (like `cub::ArgMax`) may not have include headers.

### Callouts (Deprecated, Warnings, Notes)

**Rule:** Always use callout components. Never use plain bullet points for behavioral notes, warnings, or deprecation notices.

| Callout type | Usage |
|---|---|
| `<Error title="Deprecated">` | Deprecation notices |
| `<Warning>` | Dangerous behavior, user responsibility warnings |
| `<Note>` | Important behavioral notes, clarifications |
| `<Info title="Postconditions">` | Postcondition descriptions |
| `<Info title="...">` | Other informational callouts with custom titles |

**Deprecated example** (from `deprecated_example_v4.mdx`):
```mdx
<Error title="Deprecated">
Use `cuda::strided_iterator` instead.
</Error>
```

**Note example** (from `pointer_v4.mdx`):
```mdx
<Note>
`pointer` is not a smart pointer; it is the client's responsibility to deallocate memory pointer to by `pointer`.
</Note>
```

**Warning example** (from `empty_docstring_class_v4.mdx` / `raises_example_v4.mdx`):
```mdx
<Warning>
This constructor does **NOT** initialize any elements. It is the user's responsibility to ensure that the elements within `[vec.begin(), vec.end())` are properly initialized.
</Warning>
```

**Info/Postconditions example** (from `raises_example_v4.mdx`):
```mdx
<Info title="Postconditions">
`__other` is in moved-from state.
</Info>
```

**Edge cases:**
- Callouts appear in the preamble AND inside method/overload tabs.
- Within tabs, callouts appear after the CodeBlock and before **Parameters**.

### See Also

**Rule:** Render as `**See also:**` (bold) followed by a line of comma-separated links. External URLs use full markdown links. Internal refs use relative link paths.

**Example** (from `device_vector_v3.mdx`):
```mdx
**See also:**
[https://en.cppreference.com/w/cpp/container/vector](https://en.cppreference.com/w/cpp/container/vector),
[device_allocator](/library/api/thrust::device_allocator),
[host_vector](/library/api/thrust::host_vector),
[universal_vector](/library/api/thrust::universal_vector)
```

**Example** (from `pointer_v4.mdx`):
```mdx
**See also:**
[device_ptr](/library/api/thrust::device_ptr),
reference,
[raw_pointer_cast](/library/api/thrust::raw_pointer_cast)
```

**Edge cases:**
- If a see-also item has no link target, render as plain text (e.g., `reference` in the pointer example).
- Each link on its own line, comma-separated.

### Example (class-level)

**Rule:** Render as an `## Example` H2 heading followed by an optional introductory sentence and a fenced code block (`cpp showLineNumbers={false}`). Class-level examples use a bare code block (no `<CodeBlock>` component).

**Example** (from `block_reduce_v3.mdx`):
```mdx
## Example

The code snippet below illustrates a sum reduction of 512 integer items that are partitioned in a blocked arrangement across 128 threads where each thread owns 4 consecutive items.

```cpp showLineNumbers={false}
#include <cub/cub.cuh>   // or equivalently <cub/block/block_reduce.cuh>

__global__ void ExampleKernel(...)
{
    ...
}
```
```

**Edge cases:**
- Some pages place the example before template parameters, some after. The canonical order is: example comes before template parameters when it's a class-level example in the preamble.
- `## Performance considerations` if present comes before `## Example`.

### Template Parameters

**Rule:** Wrapped in `<AccordionGroup><Accordion title="Template parameters">`. Each parameter uses a `<ParamField>` component.

**Example** (from `block_reduce_v3.mdx`):
```mdx
<AccordionGroup>
<Accordion title="Template parameters">

<ParamField path="T" type="typename">
Data type being reduced
</ParamField>

<ParamField path="BlockDimX" type="int">
The thread block length in threads along the X dimension
</ParamField>

<ParamField path="Algorithm" type="BlockReduceAlgorithm" default="BLOCK_REDUCE_WARP_REDUCTIONS">
**[optional]** [cub::BlockReduceAlgorithm](/library/api/cub::BlockReduceAlgorithm) enumerator specifying the underlying algorithm to use (default: [cub::BLOCK_REDUCE_WARP_REDUCTIONS](/library/api/cub::BLOCK_REDUCE_WARP_REDUCTIONS))
</ParamField>

</Accordion>
</AccordionGroup>
```

**Edge cases:**
- Optional parameters start their description with `**[optional]**`.
- Default values use the `default` prop on `<ParamField>`.

### Base Classes / Inherits From

**Rule:** Render as `**Inherits from:**` (bold) followed by the base class type and access specifier in parentheses.

**Example** (from `device_vector_v3.mdx`):
```mdx
**Inherits from:** `detail::vector_base< T, thrust::device_allocator< T > >` (public)
```

**Example with link** (from `pointer_v4.mdx`):
```mdx
**Inherits from:** [`thrust::iterator_adaptor< Derived, Base, Value, System, Traversal, Reference, Difference >`](/library/api/thrust::iterator_adaptor) (public)
```

**Example with multiple bases** (from `group_member_example_v4.mdx`):
```mdx
**Inherits from:** [`thrust::mr::memory_resource< Upstream::pointer >`](/library/api/thrust::mr::memory_resource) (public), [`thrust::mr::validator2< Upstream, Bookkeeper >`](/library/api/thrust::mr::validator2) (private)
```

**Edge cases:**
- If a base class has a known API page, link it.
- Multiple base classes are comma-separated.
- If the class is `final`, add a separate line: `This class is marked <Badge intent="note" minimal>final</Badge>.`

---

## Method Rendering

### Method Heading (H3 + Badges)

**Rule:** Methods are rendered as H3 headings. Qualifier badges that apply to ALL overloads of the method go on the H3 heading line. Qualifiers specific to individual overloads go inside the corresponding Tab.

**Format:** `### MethodName <Badge intent="note" minimal>qualifier</Badge>`

**Example -- all-overload qualifiers on H3** (from `block_reduce_v3.mdx`):
```mdx
### Reduce <Badge intent="note" minimal>inline</Badge>
```

**Example -- multiple qualifiers** (from `pointer_v4.mdx`):
```mdx
### get <Badge intent="note" minimal>inline</Badge> <Badge intent="note" minimal>const</Badge>
```

**Example -- overload-specific qualifier inside Tab** (from `device_vector_v3.mdx`):
```mdx
<Tab title="Const">

<Badge intent="note" minimal>const</Badge>

Subscript read access to the data contained in this vector.
```

**Example -- overload-specific qualifier inside Tab** (from `deprecated_example_v4.mdx`):
```mdx
<Tab title="From iterator and stride">

<Badge intent="note" minimal>inline</Badge>

Creates a [strided_iterator](/library/api/thrust::strided_iterator) from an existing iterator and a stride.
```

**Badge placement decision rule:**
- If a qualifier (e.g., `inline`, `const`, `static`, `virtual`, `noexcept`, `nodiscard`, `explicit`, `constexpr`) applies to every overload of the method, place it on the H3.
- If it applies only to some overloads, place it as a standalone Badge line at the top of the relevant Tab (before the description text).

### Signature (CodeBlock with links)

**Rule:** Method signatures are always wrapped in a `<CodeBlock links={{...}}>` component. The links prop maps identifier names to their API page paths.

**Format:**
```mdx
<CodeBlock links={{"ClassName": "/library/api/namespace::ClassName", "OtherType": "/library/api/namespace::OtherType"}}>
```cpp showLineNumbers={false}
ReturnType namespace::ClassName<Params>::MethodName(
    ParamType1 param1,
    ParamType2 param2
)
```
</CodeBlock>
```

**Example** (from `block_reduce_v3.mdx`):
```mdx
<CodeBlock links={{"BlockReduce": "/library/api/cub::BlockReduce"}}>
```cpp showLineNumbers={false}
template <typename ReductionOp>
T cub::BlockReduce<T, BlockDimX, Algorithm, BlockDimY, BlockDimZ>::Reduce(
    T input,
    ReductionOp reduction_op
)
```
</CodeBlock>
```

**Rules for the links prop:**
- Include the owning class short name (e.g., `"BlockReduce"`, `"device_vector"`).
- Include any parameter types or return types that have known API pages.
- If a method is inherited, include both the current class and the base class in links.

**Example -- inherited method with two link targets** (from `pointer_v4.mdx`):
```mdx
<CodeBlock links={{"pointer": "/library/api/thrust::pointer", "iterator_adaptor": "/library/api/thrust::iterator_adaptor"}}>
```cpp showLineNumbers={false}
Base const & thrust::iterator_adaptor< Derived, Base, Value, System, Traversal, Reference, Difference >::base() const
```
</CodeBlock>
```

### Parameters

**Rule:** Always use `**Parameters**` (bold text), never `#### Parameters` (H4).

**Format:**
```mdx
**Parameters**

<ParamField path="param_name" type="ParamType">
Description of the parameter.
</ParamField>
```

**Example** (from `block_reduce_v3.mdx`):
```mdx
**Parameters**

<ParamField path="input" type="T">
Calling thread's input
</ParamField>

<ParamField path="reduction_op" type="ReductionOp">
Binary reduction functor
</ParamField>
```

**Edge cases:**
- If a parameter has a default value, use the `default` prop: `<ParamField path="x" type="const value_type &" default="value_type()">`.
- Empty ParamFields (no description text) should be omitted entirely. However, if the parameter must be listed but genuinely has no description, render with empty content: `<ParamField path="param" type="Type">\n</ParamField>`.

### Template Parameters (method-level)

**Rule:** Same format as Parameters but with `**Template parameters**` heading.

**Example** (from `block_reduce_v3.mdx`):
```mdx
**Template parameters**

<ParamField path="ReductionOp" type="typename">
**[inferred]** Binary reduction functor type having member `T operator()(const T &a, const T &b)`
</ParamField>
```

**Edge cases:**
- Inferred template parameters start with `**[inferred]**`.

### Returns

**Rule:** Always use prose description format: `**Returns:** Description text`. Include type in backticks or as a link within the prose. Never use bare type-only returns.

**Examples:**

Prose with type (from `block_reduce_v3.mdx`):
```mdx
**Returns:** Reference to [_TempStorage](/library/api/cub::BlockReduce::_TempStorage)
```

Prose with inline type (from `device_vector_v3.mdx`):
```mdx
**Returns:** Read/write reference to data.
```

Type with dash separator (from `device_vector_v3.mdx`):
```mdx
**Returns:** `size_type` -- the number of elements.
```

Short type returns (from `raises_example_v4.mdx`):
```mdx
**Returns:** `stream &`
```

Link-based returns (from `raises_example_v4.mdx`):
```mdx
**Returns:** [`stream_ref`](/libcudacxx/api/cuda::stream_ref)
```

Boolean returns (from `device_vector_v3.mdx`):
```mdx
**Returns:** `true` if [size()](/library/api/thrust::device_vector::size) == 0; `false`, otherwise.
```

### Throws

**Rule:** Render as `**Throws:**` followed by the exception type and condition.

**Example** (from `device_vector_v3.mdx`):
```mdx
**Throws:** `std::length_error` if `n` exceeds [max_size()](/library/api/thrust::device_vector::max_size).
```

**Example** (from `raises_example_v4.mdx`):
```mdx
**Throws:** `cuda_error` if stream creation fails.
```

### Callouts (preconditions, postconditions, notes, warnings)

**Rule:** Use callout components within method bodies/tabs. These appear AFTER the CodeBlock and version annotation, BEFORE **Parameters**.

**Behavioral notes as bullet list with callout components:**

Actually, looking at the golden pages, behavioral notes within method tabs are rendered as plain bullet lists (not callouts). The resolved decision says to use callout components. However, in many golden pages, behavioral notes within overload tabs use plain bullet lists:

**Current golden page pattern** (from `block_reduce_v3.mdx`):
```mdx
- The return value is undefined in threads other than thread<sub>0</sub>.
- Assumes threads are in row-major order.
- The block-wide aggregate of `temp_storage` is undefined after calling this method ...
```

**Resolved decision:** Standardize on callout components everywhere. However, for method-level behavioral notes that are short lists, the golden pages use plain bullet lists. The resolved decision (#1) says to use callout components (`<Note>`, `<Warning>`, etc.) and never plain bullet points. Apply this decision:

- Method-level behavioral notes --> wrap in `<Note>` callout
- Warnings --> `<Warning>`
- Postconditions --> `<Info title="Postconditions">`
- Deprecation --> `<Error title="Deprecated">`

**Postconditions example** (from `raises_example_v4.mdx`):
```mdx
<Info title="Postconditions">
`__other` is in moved-from state.
</Info>
```

**Note within Tab** (from `empty_docstring_class_v4.mdx`):
```mdx
<Note>
No memory is allocated.
</Note>
```

### Examples (method-level)

**Rule:** Render as `**Example**` (bold text) followed by an optional intro sentence and a bare fenced code block (`cpp showLineNumbers={false}`). Method-level examples do NOT use the `<CodeBlock>` component.

**Example** (from `block_reduce_v3.mdx`):
```mdx
**Example**

The code snippet below illustrates a max reduction of 128 integer items that are partitioned across 128 threads.

```cpp showLineNumbers={false}
#include <cub/cub.cuh>   // or equivalently <cub/block/block_reduce.cuh>

__global__ void ExampleKernel(...)
{
    ...
}
```
```

---

## Overloads

### Tab Structure

**Rule:** When a method has multiple overloads, wrap them in `<Tabs><Tab title="...">...</Tab></Tabs>`. Each Tab contains the full rendering of one overload: description, CodeBlock, version annotation, callouts, template parameters, parameters, returns, throws, example.

**Format:**
```mdx
<Tabs>
<Tab title="Overload 1 name">

Description of this overload.

<CodeBlock links={{...}}>
```cpp showLineNumbers={false}
...
```
</CodeBlock>

*Version annotation*

**Parameters**

<ParamField ...>
...
</ParamField>

</Tab>
<Tab title="Overload 2 name">
...
</Tab>
</Tabs>
```

### Tab Titles Convention

**Rule:** Tab titles should be short, descriptive labels. Conventions:

| Pattern | Title format | Examples |
|---|---|---|
| Default constructor | `"Default"` or `"Default constructor"` | `"Default"`, `"Default constructor"` |
| Copy constructors | `"From X"` where X describes the source | `"From device_vector"`, `"From std::vector"`, `"From other device_vector type"`, `"From initializer_list"` |
| Move constructors | `"Move"` or `"Move with allocator"` | `"Move"`, `"Move with allocator"` |
| Constructors with config | `"With X"` where X is the config | `"With TempStorage"`, `"With allocator"`, `"With upstream and bookkeeper"`, `"With default resources"` |
| Const/Mutable pairs | `"Mutable"` / `"Const"` | `"Mutable"`, `"Const"` |
| Size variants | `"Single item"` / `"Multiple items per thread"` / `"Partial tile"` | as shown |
| Functional description | Short phrase | `"Fill"`, `"Range"`, `"Value-initialized"`, `"Default-initialized"`, `"No-init"` |
| Pre/Post increment | `"Pre-increment"` / `"Post-increment"` | as shown |
| Assignment variants | `"Copy assign"` / `"Move assign"` | as shown |
| Deleted overloads | `"Copy (deleted)"` / `"Copy assign (deleted)"` / `"Deleted overloads"` | as shown |

**Key rules:**
- Be concise but clear.
- Use noun phrases, not sentences.
- When there are Mutable/Const pairs, always use exactly `"Mutable"` and `"Const"`.

---

## Constructors

### Grouping

**Rule:** Always use a single H3 with one `<Tabs>` group for all constructor overloads in a logical group. Do NOT subdivide into named H3 groups per overload.

However, when a class has MANY constructors with clearly distinct categories (like `device_vector` with 20+ constructors), they MAY be split into multiple named H3 groups, each with its own `<Tabs>`:

**Example of multiple constructor groups** (from `device_vector_v3.mdx`):
```mdx
### Default and allocator constructors
<Tabs>...</Tabs>

### Size constructors
<Tabs>...</Tabs>

### Fill constructors
<Tabs>...</Tabs>

### Copy constructors
<Tabs>...</Tabs>

### Move constructors
<Tabs>...</Tabs>

### Initializer list constructors
<Tabs>...</Tabs>

### Range constructors
<Tabs>...</Tabs>
```

**Resolution clarification:** The resolved decision (#9) says "Always use a single H3 with one Tabs group." However, the `device_vector` golden page uses multiple named H3 groups. The rule is: **prefer a single H3 with one Tabs group.** Only use multiple H3 groups when there are so many constructors (>6) that a single Tabs group would be unwieldy, AND the constructors fall into clearly distinct semantic categories. When using multiple H3 groups, the H3 title describes the category (e.g., "Copy constructors"), not individual overloads.

**Example of single H3 with Tabs** (from `block_reduce_v3.mdx`):
```mdx
### BlockReduce <Badge intent="note" minimal>inline</Badge>

<Tabs>
<Tab title="Default constructor">
...
</Tab>
<Tab title="With TempStorage">
...
</Tab>
</Tabs>
```

### Destructor

**Rule:** Always include `### Destructor` as a label heading before the `### ~ClassName` heading.

**Example** (from `device_vector_v3.mdx`):
```mdx
### Destructor

### ~device_vector <Badge intent="note" minimal>inline</Badge>

The destructor erases the elements.

<CodeBlock links={{"device_vector": "/library/api/thrust::device_vector"}}>
```cpp showLineNumbers={false}
thrust::device_vector<T, Alloc>::~device_vector()
```
</CodeBlock>
```

**Example** (from `group_member_example_v4.mdx`):
```mdx
### Destructor

### ~disjoint_unsynchronized_pool_resource <Badge intent="note" minimal>inline</Badge>

Destructor. Releases all held memory to upstream.

<CodeBlock links={{"disjoint_unsynchronized_pool_resource": "/library/api/thrust::mr::disjoint_unsynchronized_pool_resource"}}>
```cpp showLineNumbers={false}
thrust::mr::disjoint_unsynchronized_pool_resource< Upstream, Bookkeeper >::~disjoint_unsynchronized_pool_resource()
```
</CodeBlock>
```

**Edge cases:**
- The destructor appears at the end of the Constructors section, after all constructor tabs.
- If the destructor has no description, still include the `### Destructor` label and the `### ~ClassName` heading with the CodeBlock.
- Destructors without overloads do NOT use Tabs.
- The `### ~ClassName` heading on the destructor line (from `raises_example_v4.mdx`):
```mdx
### ~stream <Badge intent="note" minimal>inline</Badge>

Destroy the [`stream`](/libcudacxx/api/cuda::stream) object.
```
Note: In the `raises_example_v4.mdx` golden page, the destructor is rendered WITHOUT the `### Destructor` label heading. The resolved decision (#5) says to ALWAYS include it. So the canonical form is to always add `### Destructor` before `### ~ClassName`.

---

## Components

### Callout Types and When to Use Each

| Component | When to use |
|---|---|
| `<Note>` | General informational notes, behavioral clarifications, non-critical operational details |
| `<Warning>` | Dangerous behavior, user responsibility, potential misuse consequences |
| `<Error title="Deprecated">` | Deprecation notices (always with `title="Deprecated"`) |
| `<Info>` | Postconditions, pre-conditions, general informational callouts |
| `<Info title="Postconditions">` | Specifically for method postconditions |

### Badge -- Qualifier Badges vs Entity-Kind Badges

**Qualifier badges** use `intent="note" minimal`:
```mdx
<Badge intent="note" minimal>inline</Badge>
<Badge intent="note" minimal>const</Badge>
<Badge intent="note" minimal>static</Badge>
<Badge intent="note" minimal>virtual</Badge>
<Badge intent="note" minimal>explicit</Badge>
<Badge intent="note" minimal>constexpr</Badge>
<Badge intent="note" minimal>noexcept</Badge>
<Badge intent="note" minimal>nodiscard</Badge>
<Badge intent="note" minimal>final</Badge>
```

**Entity-kind badges** use `intent="info"` (NOT minimal):
```mdx
<Badge intent="info">C++20 concept</Badge>
```

**Placement:**
- Qualifier badges on H3 headings: separated by spaces, on the same line
- Qualifier badges inside Tabs: standalone line at the top of the Tab, before description
- Entity-kind badges: in the preamble, on their own line before the summary

**Static/constexpr in member variable tables** (from `block_reduce_v3.mdx`):
```mdx
| `BLOCK_THREADS` <Badge intent="note" minimal>static</Badge> <Badge intent="note" minimal>constexpr</Badge> | `int` | The thread block size in threads. |
```

### AccordionGroup / Accordion

**Rule:** Used exclusively for class-level template parameters.

```mdx
<AccordionGroup>
<Accordion title="Template parameters">

<ParamField path="T" type="typename">
Description
</ParamField>

</Accordion>
</AccordionGroup>
```

### CodeBlock with Links

**Rule:** Used for all method/constructor/destructor signatures and concept definition signatures.

**Format:**
```mdx
<CodeBlock links={{"Identifier1": "/path/to/api", "Identifier2": "/path/to/api"}}>
```cpp showLineNumbers={false}
signature here
```
</CodeBlock>
```

**Rules for the `links` prop:**
- Keys are short identifiers that appear in the signature
- Values are the API page paths
- Always include the owning class as a link
- Include parameter types and return types that have known pages
- For inherited methods, include both the declaring class and the owning class

### ParamField

**Rule:** Used for parameters and template parameters.

**Props:**
- `path` (required): Parameter name
- `type` (required): Parameter type as string
- `default` (optional): Default value

**Example:**
```mdx
<ParamField path="options" type="pool_options" default="get_default_options()">
Pool options to use.
</ParamField>
```

**Empty ParamField rule (resolved decision #10):** Omit ParamField components entirely when there is no description text. Do not render empty ParamFields.

However, some golden pages do include ParamFields with no description (from `pointer_v4.mdx`):
```mdx
<ParamField path="r" type="typename detail::pointer_traits_detail::pointer_to_param< Element >::type">
</ParamField>
```
The resolved decision says to omit these. The canonical rule is: **omit ParamField components when there is no description text.**

### Tabs

**Rule:** Used for method overloads, const/mutable pairs, and any other multi-variant rendering.

```mdx
<Tabs>
<Tab title="Title 1">
Content for variant 1
</Tab>
<Tab title="Title 2">
Content for variant 2
</Tab>
</Tabs>
```

---

## Tables

### Typedef Tables

**Rule:** Use either 2-column or 3-column format depending on whether descriptions are available.

**3-column format** (Name | Definition | Description) -- when at least some typedefs have descriptions:

**Example** (from `block_reduce_v3.mdx`):
```mdx
| Name | Definition | Description |
|---|---|---|
| `InternalBlockReduce` | `::cuda::std::_If< ... >` | Internal specialization type. |
| `_TempStorage` | `typename InternalBlockReduce::TempStorage` | Shared memory storage layout type for [BlockReduce](/library/api/cub::BlockReduce). |
| `WarpReductions` | `detail::BlockReduceWarpReductions< T, BlockDimX, BlockDimY, BlockDimZ >` | |
```

**2-column format** (Name | Definition) -- when NO typedefs have descriptions:

**Example** (from `device_vector_v3.mdx`):
```mdx
| Name | Definition |
|---|---|
| `Parent` | `detail::vector_base< T, Alloc >` |
```

**Decision rule:** If ANY typedef in the table has a description, use 3-column. If NONE have descriptions, use 2-column.

### Member Variable Tables

**Rule:** Always 3-column: Name | Type | Description.

**Example** (from `block_reduce_v3.mdx`):
```mdx
| Name | Type | Description |
|---|---|---|
| `BLOCK_THREADS` <Badge intent="note" minimal>static</Badge> <Badge intent="note" minimal>constexpr</Badge> | `int` | The thread block size in threads. |
| `temp_storage` | [`_TempStorage`](/library/api/cub::BlockReduce::_TempStorage) `&` | Shared storage reference. |
| `linear_tid` | `unsigned int` | Linear thread-id. |
```

**Edge cases:**
- Static/constexpr badges go in the Name column.
- Types that have API pages are linked.
- If a member has no description, leave the Description cell empty.

### Inner Class Member Tables

**Rule:** Inner classes that have only member variables (no methods) render a member variable table directly after the CodeBlock.

**Example** (from `group_member_example_v4.mdx`):
```mdx
### chunk_descriptor

<CodeBlock links={{"disjoint_unsynchronized_pool_resource": "/library/api/thrust::mr::disjoint_unsynchronized_pool_resource"}}>
```cpp showLineNumbers={false}
struct thrust::mr::disjoint_unsynchronized_pool_resource::chunk_descriptor
```
</CodeBlock>

| Name | Type | Description |
|---|---|---|
| `size` | `std::size_t` | |
| `pointer` | `void_ptr` | |
| `pool_idx` | `std::size_t` | |
```

### Related Concepts Table (Concept Pages)

**Rule:** 2-column: Concept | Description. Each concept name is a link.

**Example** (from `concept_example_v3.mdx`):
```mdx
| Concept | Description |
|---|---|
| [`cuda::mr::resource`](/library/api/cuda::mr::resource) | Verifies that a type satisfies the basic requirements of a memory resource with stream-ordered allocations. |
```

---

## Cross-References

### Link Path Convention per Namespace

**Rule:** Cross-reference paths follow the pattern `/library/api/fully::qualified::name` for CUB and Thrust entities, and `/libcudacxx/api/fully::qualified::name` for libcudacxx (cuda::) entities.

| Library/Namespace | Path prefix | Example |
|---|---|---|
| `cub::` | `/library/api/cub::` | `/library/api/cub::BlockReduce` |
| `thrust::` | `/library/api/thrust::` | `/library/api/thrust::device_vector` |
| `thrust::mr::` | `/library/api/thrust::mr::` | `/library/api/thrust::mr::memory_resource` |
| `cuda::` | `/libcudacxx/api/cuda::` | `/libcudacxx/api/cuda::counting_iterator` |
| `cuda::mr::` | `/library/api/cuda::mr::` | `/library/api/cuda::mr::resource` |
| `cuda::std::` | N/A (no API pages) | (not linked) |

**Member references** use `::` separators:
- `/library/api/cub::BlockReduce::TempStorage`
- `/library/api/thrust::device_vector::size`

**Method references:**
- `/library/api/thrust::device_vector::size` (links to the method on the class page)
- `/libcudacxx/api/cuda::stream::sync`
- `/libcudacxx/api/cuda::stream_ref::sync`
- `/libcudacxx/api/cuda::buffer::set_stream`

### Same-Page Anchors vs Cross-Page Links

**Rule:** Cross-page links always use the path format above. Same-page anchors are not used in the golden pages -- all references link to the full path even for items on the same page.

---

## Empty State Handling

### Missing Summary

**Rule:** If the IR provides no summary/description for the class, omit the summary paragraph entirely. The page starts with the include header or template parameters.

**Example** (from `empty_docstring_class_v4.mdx` -- `cuda::buffer`):
```mdx
---
title: "cuda::buffer"
description: "A memory-safe buffer for managing typed, property-annotated device memory with stream-ordered allocation."
---

```cpp showLineNumbers={false}
#include <cuda/buffer.h>
```

<AccordionGroup>
...
```
(Note: the frontmatter description is always present even if the body has no summary paragraph.)

### Missing Parameters

**Rule:** If a method has no parameters, omit the `**Parameters**` heading and all ParamField components entirely.

### Missing Returns

**Rule:** If a method returns `void`, omit the `**Returns:**` line entirely. Never write `**Returns:** void`.

**Exception:** If the return type is meaningful (e.g., `void_ptr`), include it.

### Missing Examples

**Rule:** If a method has no example, simply omit the `**Example**` heading and code block.

### Missing Member Variables

**Rule:** If a class has no member variables, omit the `## Member variables` section entirely.

### Missing Description on ParamField

**Rule (resolved decision #10):** Omit ParamField components entirely when there is no description text. Do not render empty ParamFields.

### Methods with No Description

**Rule:** If a method has no description text, render just the signature CodeBlock (and any badges, parameters, returns). Omit the description paragraph.

**Example** (from `pointer_v4.mdx`):
```mdx
### operator-> <Badge intent="note" minimal>inline</Badge> <Badge intent="note" minimal>const</Badge>

<CodeBlock links={{"pointer": "/library/api/thrust::pointer"}}>
```cpp showLineNumbers={false}
Element * thrust::pointer< Element, Tag, Reference, Derived >::operator->() const
```
</CodeBlock>
```

---

## Version Annotations

**Rule:** Version annotations appear as italic text on their own line, immediately after the CodeBlock.

**Format:** `*Added in vX.Y.Z. First appears in CUDA Toolkit X.Y.*`

**Example** (from `block_reduce_v3.mdx`):
```mdx
*Added in v2.2.0. First appears in CUDA Toolkit 12.3.*
```

**Edge cases:**
- Not all methods have version annotations. If absent, omit.
- Always italic (wrapped in `*...*`).
- Appears between the CodeBlock and the callouts/parameters.

---

## Separator Usage

**Rule:** Horizontal rules (`---`) separate:
1. The preamble from the first body section
2. Each top-level H2 section from the next

A `---` appears BEFORE each `## SectionHeading` (except the very first one after the preamble, where the `---` serves double duty).

**Example structure:**
```mdx
(preamble content)

---

## Constructors

### ClassName
...

---

## Methods

### methodName
...

---

## Types

### Typedefs
...
```

**Edge cases:**
- Within a section, methods are NOT separated by `---`. Only H2 sections get separators.
- Exception: segmented methods in `warp_reduce_v4.mdx` -- individual non-overloaded methods within the same H2 section ARE separated by `---` when they are distinct methods (not overloads).

**Example of method-level separators** (from `warp_reduce_v4.mdx`):
```mdx
### HeadSegmentedSum <Badge intent="note" minimal>inline</Badge>
...

---

### TailSegmentedSum <Badge intent="note" minimal>inline</Badge>
...

---

### HeadSegmentedReduce <Badge intent="note" minimal>inline</Badge>
```

The pattern: `---` between distinct H3 methods within the same H2 section when the methods are semantically separate (not overloads of the same function name).

---

## Section Heading Rules

| Level | Usage |
|---|---|
| H2 (`##`) | Top-level body sections: Constructors, Methods, Types, Member variables, etc. Also: Performance considerations, Example, Description (in preamble/concept pages) |
| H3 (`###`) | Individual methods, constructors, destructors, inner classes, "Typedefs" label, "Destructor" label |
| Never H1 | H1 is never used (the page title from frontmatter serves as H1) |
| Never H4 | H4 is never used. Use `**Bold text**` instead (e.g., `**Parameters**`) |

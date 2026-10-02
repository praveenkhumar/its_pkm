# Python for AI Engineers - Course Curriculum Architecture

## Phase 1: Modern Python Foundations & Dynamic Type Systems
*   **Lesson 1:** Modern Python Environment & Dependency Management (pyproject.toml, uv, venv vs Poetry)
*   **Lesson 2:** Static Typing & Advanced Type Annotations (typing module, generics, TypeVar, ParamSpec, Protocols)
*   **Lesson 3:** Functional Paradigms for Data Streams (Generators, yield, yield from, Iterators, and Itertools)
*   **Lesson 4:** Metaprogramming & Decorators (Function decorators, Class decorators, functools.wraps, Context Managers with contextlib)
*   **Lesson 5:** Memory Management & Data Internals (CPython memory model, reference counting, gc, `__slots__`, shallow vs deep copy)

## Phase 2: High-Performance Asyncio & Concurrency for AI
*   **Lesson 6:** CPython Concurrency Architecture (GIL internals, Threads vs Processes vs Coroutines)
*   **Lesson 7:** Asyncio Core Mechanics (Event loop lifecycle, Tasks, Futures, async/await internals)
*   **Lesson 8:** Concurrent Execution Patterns (asyncio.gather, asyncio.as_completed, TaskGroups in Python 3.11+)
*   **Lesson 9:** Async Resource Throttling & Synchronization (asyncio.Semaphore, Queues, Locks, shielding against timeouts)
*   **Lesson 10:** Bridging Sync and Async (anyio.to_thread, loop.run_in_executor, ProcessPoolExecutor for CPU-heavy tasks)

## Phase 3: Data Contracts, Parsing & Validation with Pydantic V2
*   **Lesson 11:** Pydantic V2 Architecture (pydantic-core, Rust validation engine, BaseModel internals)
*   **Lesson 12:** Field Engineering & Custom Constraints (Field metadata, Annotated types, regex constraints, default factories)
*   **Lesson 13:** Advanced Serialization & Deserialization (model_validate, model_dump_json, computed_fields, alias generators)
*   **Lesson 14:** Complex Validations (field_validator vs model_validator, mode='before' vs mode='after', cross-field validation)
*   **Lesson 15:** Type Adapters & Dynamic Validation (TypeAdapter for raw lists/primitives without BaseModel boilerplate)

## Phase 4: Async Networking, Streaming & Resilient HTTP with HTTPX
*   **Lesson 16:** HTTPX vs Requests (httpx.AsyncClient connection pooling, HTTP/2 multiplexing)
*   **Lesson 17:** Token & Event Streaming (Server-Sent Events, async chunk iteration, handling broken streams)
*   **Lesson 18:** Fault-Tolerant Networking (Exponential backoff, retries with tenacity, circuit breaker patterns)
*   **Lesson 19:** High-Throughput Batch Ingestion (Parallel async API consumers with concurrency limits)
*   **Lesson 20:** Secure API Authentication & Dynamic Headers (Custom Auth flows, proxy rotations, token refreshes)

## Phase 5: Tensor Primitives & Vector Computations (NumPy & Embeddings)
*   **Lesson 21:** Vector Math Essentials for AI Engineers (Dot products, Cosine Similarity, Euclidean distances)
*   **Lesson 22:** NumPy Array Internals (Strides, broadcasting rules, memory contiguity, C-order vs F-order)
*   **Lesson 23:** Batch Vector Operations (Vectorizing distance calculations across 100k embeddings without loops)
*   **Lesson 24:** Tensor Operations & Data Pipelines (PyTorch tensor basics, GPU tensor offloading, float16 vs bfloat16 memory footprints)
*   **Lesson 25:** Efficient Serialization & Storage (Safetensors, Parquet, pickle pitfalls and security vulnerabilities)

## Phase 6: Profiling, Optimization & Production Readiness
*   **Lesson 26:** Performance Bottleneck Profiling (cProfile, py-spy, memray for memory leaks in long-running AI apps)
*   **Lesson 27:** Packaging & Dockerizing Python AI Apps (Minimal slim multi-stage builds, non-root execution, cache mounts)
*   **Lesson 28:** Senior AI Python Technical Interviews & Production Scenarios (Debugging async deadlocks, memory bloat during inference, GIL bottlenecks)
# LangSmith Cookbook

This repository stores code tutorials showing different ways to get more out of [LangSmith](https://smith.langchain.com/). LangSmith is a platform that helps you debug, test, evaluate, and monitor your LLM applications.

These cookbook recipes are meant to complement the [LangSmith Documentation](https://docs.smith.langchain.com/) by showing common use cases and tactics within "end-to-end" examples, which you can take and adapt to your needs.

If you have any specific requests or common patterns you'd like to see highlighted, create a GitHub issue or let one of the core LangChain devs know. We also welcome contributions!


## Tracing your code

Setting up tracing in LangChain is as simple as setting a couple environment variables. We've also added support through the LangSmith SDK to trace applications that don't rely on LangChain. The following walkthroughs address common questions around tracing your code!
- The [Tracing without LangChain](./tracing-examples/traceable/tracing_without_langchain.ipynb) notebook uses the Python SDK's `@traceable` decorator to trace and tag run in an app that does not use depend on LangChain.
- The [REST API](./tracing-examples/rest/rest.ipynb) notebook walks through logging runs to LangSmith directly using the REST API, covering how to log LLM and chat model runs for token counting, and how to nest runs. The run logging spec can be found in the [LangSmith SDK repository](https://github.com/langchain-ai/langsmith-sdk/blob/main/openapi/openapi.yaml).
- The [Customing Run Names](./tracing-examples/runnable-naming/run-naming.ipynb) notebook demonstrates how to assign custom names to LangSmith chain runs for better traceability and clarity in the UI. It covers custom naming for chains, lambda functions, and agents, offering practical examples for each.

## LangChain Hub

Managing multiple versions of LLM components can be tough. The [LangChain Hub](https://smith.langchain.com/hub) provides tools to keep everything organized. The following walkthroughs relate how to incporate it in your workflows. For more information, please consult the [docs](https://docs.smith.langchain.com/category/hub).

- The [RetrievalQA Chain](./hub-examples/retrieval-qa-chain/retrieval-qa.ipynb) notebook shows how to version prompts for retrieval QA chain.
- The [Prompt Versioning](./hub-examples/retrieval-qa-chain-versioned/prompt-versioning.ipynb) notebook whows how to ensure deployment stability by using specific prompt versions from the Hub instead of the 'latest'.
- The [Runnable PromptTemplate](./hub-examples/runnable-prompt/edit-in-playground.ipynb) notebook explains how to save prompts to the hub directly from the playground. It also reviews how to use these prompts in runnable chains.

## Testing & Evaluation

### Python Examples
The following walkthroughs demonstrate ways to evaluate common application scenarios.
- The [Q&A System Correctness](./testing-examples/qa-correctness/qa-correctness.ipynb) notebook walks through creating a dataset for a retrieval-augmented Q&A pipeline, evaluating the responses for correctness, and using LangSmith to iterate and improve.
- The [Evaluating Q&A Systems with Dynamic Data](./testing-examples/dynamic-data/testing_dynamic_data.ipynb) notebook shows how to evaluate a Q&A pipeline when the underlying data may change over time by using an evaluator that dereferences a label at evaluation time.
- The [Comparison Evals](./testing-examples/comparing-runs/comparing-qa.ipynb) notebook shows how to use labeled preference scoring to help compare two versions of a system and choose the preferred outputs.
- For examples using LangSmith in your testing framework, such as with pytest, you can reference the following:
    - The [LangSmith in Pytest](./testing-examples/pytest/) recipe shows how to directly evaluate your chain or LLM on a dataset and then define your own pass/fail criteria.
    - The [Unit Testing with Pytest](./testing-examples/pytest-ut/) recipe shows how to write individual unit tests so that feedback and traces are all organized by test suite.
- The [Evaluating Existing Runs](./testing-examples/evaluate-existing-test-project/evaluate_runs.ipynb) notebook demonstrates how to evaluate or add automated feedback to existing run traces. This is useful for adding additional evaluation metrics after already conducting a test run, for adding AI-assisted feedback in monitoring projects, and for evaluating runs logged outside of python.
#### Testing FAQs

We include some smaller snippets to answer common questions.
- The [Naming Test Projects](./testing-examples/naming-test-projects/naming-test-projects.md) example demonstrates how to customize the test run with `run_on_dataset(..., project_name='my-project-name')`

### TypeScript / JS Testing Examples

LangSmith supports logging evaluation feedback to any run. The following walkthroughs show how to incorporate LangSmith in your TS/JS testing and evaluation workflows.
- The [Evaluating JS Chains in Python](./typescript-testing-examples/eval-in-python/) walkthrough shows how to run your JS chain over a LangSmith dataset and then evaluate the resulting traces in python, using a custom evaluator to test the structured results. This applies the technique presented in [Evaluating Existing Runs](./testing-examples/evaluate-existing-test-project/evaluate_runs.ipynb).
- The [Logging Assertions as Feedback](./typescript-testing-examples/simple-test/) example shows a how to quickly store your existing CI test assertions as LangSmith feedback. This lets you store annotated traces of your test runs in LangSmith without requiring many changes to your existing test system.

## Using Feedback

The following walkthroughs show ways to capture and use [feedback](https://docs.smith.langchain.com/evaluation/capturing-feedback) on runs using LangSmith. This is useful for anything from app monitoring, to personalization, to evaluation and finetuning.

- [Streamlit Chat App](./feedback-examples/streamlit/README.md) contains a minimal example of a Chat application that captures user feedback and shares traces of the chat application.
    - The [vanilla_chain.py](./feedback-examples/streamlit/vanilla_chain.py) contains an LLMChain that powers the chat application.
    - The [expression_chain.py](./feedback-examples/streamlit/expression_chain.py) contains an equivalent chat chain defined exclusively with [LangChain expressions](https://python.langchain.com/docs/guides/expression_language/). 
- [Next.js Chat App](./feedback-examples/nextjs/README.md) contains a TypeScript tracing and user feedback example.
    - You can [check out a deployed demo version here](https://langsmith-cookbook.vercel.app/).
- The [Building an Algorithmic Feedback Pipeline](./feedback-examples/algorithmic-feedback/algorithmic_feedback.ipynb) notebook guides you through automating feedback metrics for your LLM deployment, enabling advanced monitoring and performance tuning with LangSmith.

## Exploratory Data Analysis

Once you've logged your trace data, there is a wealth of insight you can glean from analyzing the logs. Use them for fine-tuning, to build better eval suites, to drive product insights, and more. The following are some example notebooks showing how you can export the data to other tools for analysis.
- The [Lilac](./exploratory-data-analysis/lilac/lilac.ipynb) notebook demonstrates how you can enrich a dataset by defining custom patterns, check for PII, and performing near-duplicate detection using the open-source unstructured data analytics tool, [Lilac](https://github.com/lilacai/lilac).
## Exporting data for fine-tuning

The [LangSmith docs](https://docs.smith.langchain.com/tracing/use-cases/export-runs/local) contains examples of ways to filter and query the runs database for downstream tasks. The examples below share recipes on how to then use that data for fine-tuning.
- The [OpenAI Fine-Tuning](./fine-tuning-examples/export-to-openai/fine-tuning-on-chat-runs.ipynb) recipe shows a fast, simple way to list LLM runs in a project and convert them to OpenAI's fine-tuning format.
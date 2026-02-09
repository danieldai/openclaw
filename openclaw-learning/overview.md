# OpenClaw Project Overview

I've completed a comprehensive exploration of the OpenClaw project, and here's a detailed guide to help you understand its architecture and build new agents using its capabilities.

## 1. Project Architecture & Structure

OpenClaw is a multi-channel AI gateway with extensible messaging integrations. Its codebase is organized as follows:

- **Source code**: `src/` (CLI wiring, commands, web provider, infra, media pipeline)
- **Tests**: Colocated `*.test.ts` files
- **Docs**: `docs/` (images, queue, Pi config)
- **Plugins/extensions**: `extensions/` (workspace packages)
- **Build output**: `dist/`

The project uses TypeScript (ESM) with strict typing and follows a modular architecture. It supports both Node.js and Bun runtimes.

## 2. Agent System

OpenClaw's agent system is one of its core features:

- **Agent Architecture**: The system uses a modular approach with support for multiple agents, each with its own configuration, workspace, and model settings.
- **Agent Execution**: Agents are executed through `agent-runner.ts` and `agent-runner-execution.ts`, which handle session management, model fallbacks, and error handling.
- **Session Management**: Each agent maintains sessions with unique IDs, handling context overflow and session corruption automatically.
- **Model Fallbacks**: The system supports model fallbacks to ensure continuous operation even if the primary model fails.

## 3. Plugin SDK & Extension System

OpenClaw provides a comprehensive plugin SDK for extending functionality:

- **Plugin SDK**: Exposed as `openclaw/plugin-sdk`, providing types, helpers, and config utilities.
- **Plugin Runtime**: Injected via `OpenClawPluginApi.runtime` to access core runtime behavior.
- **Channel Plugins**: Messaging connectors implemented as plugins using the SDK/runtime.
- **Extension Structure**: Extensions live under `extensions/` as workspace packages.

## 4. Messaging Channels

OpenClaw supports multiple messaging channels:

- **Core Channels**: Telegram, WhatsApp, Discord, Google Chat, Slack, Signal, iMessage
- **Channel Registry**: Maintains metadata for each channel, including docs links and configuration options.
- **Channel Adapters**: Pluggable adapters for each channel, handling authentication, messaging, and events.
- **Channel Bindings**: Routes messages from specific channels to designated agents.

## 5. Browser Automation

OpenClaw includes browser automation capabilities:

- **Browser Control Server**: Express-based server for controlling browsers.
- **Playwright Integration**: Uses Playwright for browser automation.
- **Chrome Extension Support**: Includes a relay server for Chrome extension integration.
- **Multiple Profiles**: Supports multiple browser profiles with different configurations.

## 6. CLI Commands

The CLI is a key interface for interacting with OpenClaw:

- **Command Structure**: Built with Commander.js, organized into command registrations.
- **Core Commands**: `agents`, `message`, `config`, `status`, `onboard`, `setup`
- **Agent Commands**: `agents add`, `agents list`, `agents delete`, `agents identity`
- **Interactive Mode**: Provides a wizard-based interface for complex commands.

## 7. Configuration & Deployment

OpenClaw uses a flexible configuration system:

- **Config Structure**: Split into focused modules covering agents, channels, browser, messaging, etc.
- **Validation**: Uses Zod schemas for config validation.
- **Migration**: Supports migration from legacy config formats.
- **Runtime Overrides**: Allows overriding config values at runtime.
- **Deployment Options**: Supports local, cloud, and containerized deployments.

## 8. Building New Agents

To build new agents with OpenClaw, follow these steps:

1. **Create an Agent**: Use `openclaw agents add` command with a name and workspace directory.
2. **Configure the Agent**: Set up model, skills, memory search, and other parameters.
3. **Bind Channels**: Route messages from specific channels to your agent.
4. **Customize Workspace**: Set up the agent's workspace directory for file operations.
5. **Test the Agent**: Use `openclaw agent` command to test your agent's functionality.

## 9. Key Takeaways & Best Practices

- **Modularity**: OpenClaw's modular architecture makes it easy to extend and customize.
- **Plugin System**: Use the plugin SDK to create custom channels and extensions.
- **Multi-Agent Architecture**: Leverage multiple agents for different tasks or channels.
- **Error Handling**: The system includes robust error handling and automatic recovery mechanisms.
- **Testing**: Write comprehensive tests using the colocated `*.test.ts` pattern.
- **Documentation**: Follow the project's documentation guidelines for clear, consistent docs.

## 10. Getting Started

1. **Install Dependencies**: `pnpm install` or `bun install`
2. **Build the Project**: `pnpm build`
3. **Run the CLI**: `pnpm openclaw ...` or `pnpm dev`
4. **Create Your First Agent**: `pnpm openclaw agents add`
5. **Configure Channels**: Set up messaging channels for your agent
6. **Start the Gateway**: Run the gateway to process messages

OpenClaw provides a powerful foundation for building AI agents with multi-channel messaging capabilities. Its modular architecture and plugin system make it highly extensible, allowing you to create custom agents tailored to your specific needs.

For more detailed information, refer to the project's documentation at [https://docs.openclaw.ai/](https://docs.openclaw.ai/).

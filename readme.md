# Semantic Kernel Sample Project

This repository contains sample code and examples demonstrating how to use Microsoft's Semantic Kernel in both Python and C#. The samples showcase key concepts and features of Semantic Kernel, providing a practical guide to building AI-powered applications.

## Repository Structure

```
sematinc-kernel-sample/
│
├── python/              # Python examples
│   ├── kernel.ipynb     # Basic Kernel operations in Python
│   ├── plugins.ipynb    # Plugin system examples in Python
│   └── planner.ipynb    # Planner functionality examples in Python
│
└── c#/                  # C# examples
    ├── kernel.ipynb     # Basic Kernel operations in C#
    ├── plugins.ipynb    # Plugin system examples in C#
    └── config/          # Configuration files for C#
        ├── Settings.cs  # Settings handling class
        └── settings.json # Configuration values
```

## Key Concepts

### Kernel

The Kernel is the central orchestrator in Semantic Kernel that manages:

- Integration with AI models
- Execution of plugins and functions
- Context and memory management
- Orchestration of workflows

See the kernel notebooks in both Python and C# for detailed examples of how to initialize and use the Kernel.

### Plugins

Plugins enhance the capabilities of language models (LLMs) through modular execution, allowing you to:

1. **Execute Deterministic Logic**: Each plugin contains specific and well-defined logic to perform concrete tasks.
2. **Extend Functionality**: Expand LLM capabilities by integrating with different tools and services.
3. **Custom Tailoring**: Adapt functionality according to specific user or application needs.

The plugins notebooks demonstrate how to create, register, and invoke plugins in both Python and C#.

### Planners

Planners in Semantic Kernel provide functionality for:

- **Organizing and Coordinating Functions**: Create efficient workflows by coordinating different functions.
- **Evaluating and Optimizing Tasks**: Establish optimal execution order and prioritize tasks.
- **Modifying Execution Plans**: Adapt plans in real-time based on user input or changing conditions.

The planner notebooks show how to implement and use different planning strategies.

## Getting Started

### Prerequisites

#### Python
- Python 3.8+
- Semantic Kernel Python SDK
- Jupyter Notebook or compatible environment
- Azure OpenAI service or OpenAI API access

#### C#
- .NET 6.0+
- Semantic Kernel NuGet packages
- Jupyter Notebook with .NET Kernel

### Setup

1. Clone this repository:
   ```
   git clone https://github.com/yourusername/sematinc-kernel-sample.git
   cd sematinc-kernel-sample
   ```

2. Configure your AI service:
   - For C#: Update `c#/config/settings.json` with your API credentials
   - For Python: Set environment variables as referenced in the notebooks

3. Install required packages:
   - Python: `pip install semantic-kernel azure-cosmos azure-identity requests`
   - C#: The notebooks will automatically install the required NuGet packages

## Usage Examples

### Basic Kernel Operations

```python
# Python example
from semantic_kernel import Kernel
from semantic_kernel.functions import kernel_function

# Create kernel instance
kernel = Kernel()

# Define and register a function
@kernel_function(name="greet")
async def greet(name: str) -> str:
    return f"Hello, {name}!"

kernel.add_plugin(greet, "example")

# Invoke the function
result = await kernel.invoke("example.greet", name="World")
print(result)  # Output: Hello, World!
```

```csharp
// C# example
using Microsoft.SemanticKernel;

// Create kernel instance
var kernel = Kernel.CreateBuilder().Build();

// Define and register a function
public class GreetingSkill
{
    [KernelFunction]
    public string Greet(string name)
    {
        return $"Hello, {name}!";
    }
}

kernel.ImportPluginFromObject(new GreetingSkill(), "greeting");

// Invoke the function
var result = await kernel.InvokeAsync("greeting", "Greet", new() { ["name"] = "World" });
Console.WriteLine(result);  // Output: Hello, World!
```

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- [Microsoft Semantic Kernel](https://github.com/microsoft/semantic-kernel)
- Azure OpenAI Service

# Parallel Performance Tool

A command-line utility written in C++ for calculating and analyzing parallel computing performance metrics.

The tool provides calculations for **Speedup** and **Parallel Efficiency**, individually or together. It automatically generates text reports containing the input values and calculation results.

Its command structure is similar to Git: users execute commands followed by the required arguments directly from the terminal.

## Features

- **Speedup Calculation (`spd`)** – Calculates speedup using sequential and parallel execution times.
- **Parallel Efficiency Calculation (`efc`)** – Calculates efficiency using speedup and the number of processors.
- **Combined Calculation (`spdefc`)** – Calculates both speedup and parallel efficiency.
- **Automatic Report Generation** – Generates `.txt` reports containing input values and calculation results.
- **Automatic Directory Creation** – Creates a `Reports` directory if it does not exist.
- **Timestamped Reports** – Uses timestamps in report filenames.
- **Input Validation and Error Handling** – Validates arguments, numerical values, and report-generation operations.

## Dependencies

The project uses standard C++ libraries and does not require external third-party dependencies.

| Dependency | Description |
|---|---|
| C++17 compatible compiler | Required to compile the program. |
| C++ Standard Library | Provides filesystem operations, input/output, and string manipulation. |
| C++17 support | Required for `std::filesystem`. |

Recommended compilers:
- GCC
- Clang
- Microsoft Visual C++ (MSVC)

**Compatibility note:** The current timestamp implementation uses Microsoft's `localtime_s()` convention and requires adaptation for GCC and Clang. Its return-value check also needs correction.

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/KevenPaulinoFerrer/Command-Line-Tools.git
```

### 2. Navigate to the project directory

```bash
cd Command-Line-Tools
```

### 3. Compile the program

Using Microsoft Visual C++:

```bash
cl /std:c++17 /EHsc src/main.c++ /Fe:main.exe
```

The resulting executable will be generated in the current directory.

## Usage

The program is designed to be executed through the terminal.

General command structure:

```bash
main.exe <command> [arguments]
```

### Available Commands

| Command | Arguments | Description |
|---|---|---|
| `help` | None | Displays available commands and usage instructions. |
| `spd` | `<sequential_time> <parallel_time>` | Calculates speedup. |
| `efc` | `<speedup> <processors>` | Calculates parallel efficiency. |
| `spdefc` | `<sequential_time> <parallel_time> <processors>` | Calculates both metrics. |

### 1. Help

```bash
main.exe help
```

Displays the available commands and their descriptions.

### 2. Calculate Speedup

Calculates how many times faster parallel execution is compared to sequential execution.

**Formula:**

```text
Speedup = Sequential Time / Parallel Time
```

**Example:**

```bash
main.exe spd 100 25
```

Expected result:

```text
Speedup = 100 / 25 = 4
```

### 3. Calculate Parallel Efficiency

Calculates how efficiently the available processors are being utilized.

**Formula:**

```text
Efficiency = Speedup / Number of Processors
```

**Example:**

```bash
main.exe efc 4 8
```

Expected result:

```text
Efficiency = 4 / 8 = 0.5
```

This represents 50% parallel efficiency.

### 4. Calculate Speedup and Efficiency

Calculates both metrics using sequential execution time, parallel execution time, and the number of processors.

**Example:**

```bash
main.exe spdefc 100 25 8
```

Expected results:

```text
Speedup = 100 / 25 = 4

Efficiency = 4 / 8 = 0.5
```

## Report Generation

After successfully executing a calculation, the program automatically generates a text report.

Reports are stored in a `Reports` directory located alongside the executable.

Example directory structure:

```text
Command-Line-Tools/
│
├── src/
│   └── main.c++
│
├── main.exe
│
└── Reports/
    ├── Report_2026-11-17_19-30-00.txt
    └── Report_2026-11-17_19-35-00.txt
```

Each report contains the calculation inputs and their corresponding results.

**Example report:**

```text
Sequential Time: 100.000000
Parallel Time: 25.000000
Processors: 8.000000
Speedup: 4.000000
Efficiency: 0.500000
```

The timestamp in the filename identifies when the report was generated.

## Error Handling

The program validates user input and provides descriptive error messages when an operation cannot be completed.

| Error | Description |
|---|---|
| Missing command | No command was provided. |
| Unknown command | The specified command does not exist. |
| Invalid arguments | An incorrect number of arguments was provided. |
| Invalid number | An argument contains an invalid numerical value. |
| Sequential time error | Sequential execution time must be greater than zero. |
| Parallel time error | Parallel execution time must be greater than zero. |
| Processor error | Number of processors must be greater than zero. |
| Speedup error | Speedup must be greater than zero. |
| Report error | The program could not create or write the report. |
| Directory error | The program could not create the Reports directory. |

## License

No license has been specified for this project.

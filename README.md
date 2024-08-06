
# 🧙 Vendordep Wizard for FRC

Vendor Wizard is a tool designed to simplify the management of vendor dependencies (vendordeps) in FRC (FIRST Robotics Competition) projects. It provides both a CLI script and a GUI tool to help teams easily update and maintain their project dependencies.

## Important Note

**The files from this repository MUST be placed in a folder named `tools` at the root of your robot project for the tool to function correctly.**

## Features

- List all vendordeps and their status
- Update outdated vendordeps
- CLI script for automation and integration with build processes
- Gradle integration for automatic updates during builds

## Installation

### Prerequisites

- Python 3.7+
- Bash (for the CLI script)

### Setup

1. Clone this repository:
   ```
   git clone https://github.com/WindingMotor/Vendor-Wizard.git
   ```

2. Create a new folder named `tools` at the root of your robot project if it doesn't already exist.

3. Move all the cloned files into the `tools` folder in your robot project.

4. Navigate to your the `tools` folder.

5. Create a virtual environment:
   ```
   python -m venv venv
   ```

6. Activate the virtual environment:
   - On Windows:
     ```
     venv\Scripts\activate
     ```
   - On macOS and Linux:
     ```
     source venv/bin/activate
     ```

7. Install the required Python packages:
   ```
   pip install -r tools/requirements.txt
   ```

## Usage

### CLI Tool

The CLI tool is located in the `tools` directory and is named `vendor_wizard.sh`. To use it:

1. Make sure you're in your robot project's root directory.

2. Make the script executable:
   ```
   chmod +x tools/vendor_wizard.sh
   ```

3. Run the script with the desired command:
   ```
   ./tools/vendor_wizard.sh list
   ./tools/vendor_wizard.sh update
   ```

### GUI Tool

To launch the GUI tool:

1. Ensure you're in the `tools` directory and your virtual environment is activated.

2. Run the Python script:
   ```
   python tools/vendor_wizard_gui.py
   ```

## Gradle Integration

To integrate Vendor Wizard with your Gradle build process, add the following task to your `build.gradle` file:

```groovy
task updateVendordeps(type: Exec) {
    workingDir "${rootDir}/tools"
    commandLine './vendor_wizard.sh', 'update', '--gradle'
    standardOutput = new ByteArrayOutputStream()
    errorOutput = new ByteArrayOutputStream()
    ignoreExitValue = true
    doLast {
        def output = standardOutput.toString()
        def errorOutput = errorOutput.toString()
        println output
        println errorOutput
    }
}
tasks.build.dependsOn updateVendordeps
```

This will automatically update your vendordeps when you run the Gradle build.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

---

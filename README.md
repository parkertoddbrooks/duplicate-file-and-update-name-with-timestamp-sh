# Duplicate File and Update Name with Timestamp (Shell Script & App)

This project provides a shell script and Automator app that monitors specified directories for file duplication events and automatically updates the names of duplicated files with a timestamp format.

## Features

- Monitors specified directories (Desktop and Documents) for file duplication events
- Automatically renames duplicated files with a timestamp
- Handles multiple duplications by appending additional timestamps
- Works with files ending in " copy" (case insensitive) or files already renamed by this script

When a file is duplicated:

- If the file ends with " copy" (case insensitive), it will be renamed to `filename-copy-YYYY-MM-DD-HHMMSS.extension`
- If the file already has a timestamp (from a previous duplication), a new timestamp will be appended: `filename-copy-YYYY-MM-DD-HHMMSS--YYYY-MM-DD-HHMMSS.extension`

### Key Considerations

- The script is designed to run continuously in the background, monitoring specified directories for file duplication events. 
- By default, the script monitors the user's Desktop and Documents folders, providing a convenient out-of-the-box experience. However, users can still specify a different directory if needed.
- This project was developed and tested on macOS Sonoma 14.5. The script is specifically designed for macOS and may require modifications for use on other Unix-like systems.
- Choose between using the script directly (for more control and customization) or the Automator app (for ease of use and integration with macOS).

## Directory Structure

```
/duplicate-file-and-update-name-with-timestamp-sh/
├── ai-insights
├── automator-set-up.sh
├── DuplicateFileManager.sh
├── DuplicateWithTimestamp.app
├── DuplicateWithTimestamp.sh
├── install.sh
└──README.md
```

## AI-Assisted Development Insights

Our project was developed with Claude.ai and Claude Engineer CLI. The `/ai_insight/` directory contains valuable information about this AI-assisted development approach:

### cli-dump
Complete transcripts of Claude Engineering CLI sessions.

### dev-summaries
Comprehensive project progress updates that allow any AI or developer to quickly understand the current state of the project. This serves as a continuity mechanism to preserve context beyond various model and system limitations, including token limits, context windows, session boundaries, rate limits, stateless API interactions, parsing complexities, and cross-model compatibility issues. 

### error-logs
CLI outputs for each encountered bug. These are submitted to Claude via Markdown files rather than direct paste to prevent formatting issues caused by multiple carriage returns. This method helps maintain Claude Engineer's stability when processing large blocks of text.

### PRDs
Product requirement documents generated by both OpenAI and Anthropic, outlining the specifications for this project or PRDs we for features we created as we developed the software.

### prompts
Prompts designed to efficiently bring Claude Engineering CLI back up to speed after any connection or context loss, ensuring continuity in the development process.

### steps
A continuously updated file containing Claude's recommendations for next steps in the project, providing a clear roadmap for development.

## Installation and Usage

### Prerequisites
- macOS or Unix-based operating system
- bash or zsh shell
- fswatch utility (can be installed via Homebrew: `brew install fswatch`)

### Installation Steps

1. Install fswatch (if not already installed):
   On macOS, you can use Homebrew:
   ```
   brew install fswatch
   ```
   For other Unix-based systems, use your system's package manager or install from source: https://github.com/emcrisostomo/fswatch
   
   
2. Add ~/.local/bin/ to your PATH:
   Add the following line to your ~/.bashrc or ~/.zshrc file:
   ```
   export PATH="$HOME/.local/bin:$PATH"
   ```
   Then, reload your shell configuration:
   ```
   source ~/.bashrc  # or source ~/.zshrc if you're using zsh
   
   ```

3. Clone the repository:
   ```
   git clone https://github.com/parkertoddbrooks/duplicate-file-and-update-name-with-timestamp-sh.git
   ```
   ```
   cd duplicate-file-and-update-name-with-timestamp-sh
   ```

4. Run the installer script:
   ```
   ./install.sh
   ```
   This will copy the necessary scripts to ~/.local/bin/ and make them executable.

### Using from the Command Line (background process)

1. Start the service:
   ```
   ~/.local/bin/DuplicateFileManager.sh start
   ```

2. Stop the service:
   ```
   ~/.local/bin/DuplicateFileManager.sh stop
   ```

3. Check the status of the service:
   ```
   ~/.local/bin/DuplicateFileManager.sh status
   ```

4. Toggle the service (start if stopped, stop if running):
   ```
   ~/.local/bin/DuplicateFileManager.sh toggle
   ```
   
### Using from the Command Line (foreground process)

Run the shell script without arguments to monitor your Desktop and Documents folders. Use Ctrl+C to stop the script.

```
~/.local/bin/DuplicateWithTimestamp.sh
```

### Using the App

The DuplicateWithTimestamp.app is a macOS Automator application that provides a user-friendly graphical interface for managing the Duplicate File and Update Name with Timestamp service. This app simplifies the process of starting and stopping the file monitoring and renaming service without the need to use command-line instructions.

Key features of the Automator app:

1. Easy toggle functionality: Double-clicking the app alternates between starting and stopping the service.
2. Visual feedback: The app uses macOS notifications to inform you when the service starts or stops.
3. Seamless integration: It integrates smoothly with macOS, allowing you to add it to your login items for automatic startup.
4. Background operation: Once started, the app runs the service in the background, allowing you to continue with your work without interruption.

The Automator app is ideal for users who prefer a graphical interface or are less comfortable with command-line operations. It provides the same functionality as the command-line interface but in a more accessible format, making it easier to manage the file duplication and renaming service on your Mac.

1. Double-click the DuplicateWithTimestamp.app in Finder to start the service.
2. Double-click the app again to stop the service.

### Setting Up Automatic Start on Login

1. Open "System Preferences" on your Mac.
2. Go to "Users & Groups".
3. Select your user account.
4. Click on the "Login Items" tab.
5. Click the "+" button below the list of login items.
6. Navigate to and select the DuplicateWithTimestamp.app.
7. Click "Add".

The app will now start automatically when you log in to your Mac.

## Troubleshooting

- If the service doesn't start, check the log files in ~/.local/log/ for error messages.
- Ensure fswatch is installed and in your PATH.
- Verify that ~/.local/bin/ is in your PATH.
- If the renaming doesn't work as expected, check the permissions of the monitored directories.
- For issues with the Automator app, try running the script directly from the command line to isolate the problem.

For any issues not covered here, please check the debug output or submit an issue on the project's GitHub page at https://github.com/parkertoddbrooks/duplicate-file-and-update-name-with-timestamp-sh

## Uninstall

To uninstall the Duplicate File and Update Name with Timestamp tool:

1. Stop the service if it's running:
   ```
   ~/.local/bin/DuplicateFileManager.sh stop
   ```

2. Remove the installed scripts:
   ```
   rm ~/.local/bin/DuplicateWithTimestamp.sh
   rm ~/.local/bin/DuplicateFileManager.sh
   ```

3. Remove the Automator app:
   ```
   rm -rf /Applications/DuplicateWithTimestamp.app
   ```

4. Remove the log directory:
   ```
   rm -rf ~/.local/log
   ```

5. If you added the app to your login items, remove it from System Preferences > Users & Groups > Login Items.

After these steps, the tool will be completely removed from your system.

## Version History

- v1.0.0 (Current)
  - Initial release
  - Basic functionality for renaming duplicated files
  - Command-line interface and Automator app support

## Contributing

We welcome contributions to improve the Duplicate File and Update Name with Timestamp project. 

# License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.


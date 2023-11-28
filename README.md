
# UE5-EOS-Config

This GitHub Action is designed to prepare Unreal Engine 5 (UE5) configuration files for use with Epic Online Services (EOS). It automates the process of updating the `DefaultEngine.ini` and optionally creates a `DedicatedServerEngine.ini` based on the provided inputs.

## How it Works

The action performs the following steps:

- Updates `DefaultEngine.ini` with provided Sandbox and Deployment IDs, Build ID, Client ID, Client Secret, Server Public Key, and Player Data Encryption Key.
- Conditionally creates a `DedicatedServerEngine.ini` file with provided content when the `SERVER` input is set to `true`.

## Requirements

- PowerShell must be available in the runner environment as the scripts are PowerShell commands.
- The configuration directory and `DefaultEngine.ini` must be present at the specified location.
- If creating `DedicatedServerEngine.ini`, the content for it must be provided.

## Inputs

| Input                       | Description                                      | Required |
| --------------------------- | ------------------------------------------------ | :------: |
| `CONFIG_DIR_PATH`           | Path to the configuration directory              |   Yes    |
| `SANDBOX_ID`                | Sandbox ID                                       |   Yes    |
| `DEPLOYMENT_ID`             | Deployment ID                                    |   Yes    |
| `BUILD_ID`                  | Build ID                                         |   Yes    |
| `CLIENT_ID`                 | Client ID                                        |   Yes    |
| `CLIENT_SECRET`             | Client secret                                    |   Yes    |
| `SERVER_PUBLIC_KEY`         | Server Public Key                                |   Yes    |
| `PLAYER_DATA_ENCRYPTION_KEY`| Player Data Encryption Key                       |   Yes    |
| `SERVER`                    | Flag to create `DedicatedServerEngine.ini`       |   No     |
| `DEDICATED_SERVER_INI`      | Content for `DedicatedServerEngine.ini`          |   Yes    |

## Using the Action

To use this action in your workflow, add the following step:

```yaml
- name: Configure UE5 Project for EOS
  uses: OrchidIsle/UE5-EOS-Config@latest
  with:
    CONFIG_DIR_PATH: ${{ github.workspace }}/MyGameFolder/Config
    SANDBOX_ID: YourSandboxID
    DEPLOYMENT_ID: YourDeploymentID
    BUILD_ID: YourBuildID
    CLIENT_ID: YourClientID
    CLIENT_SECRET: YourClientSecret
    SERVER_PUBLIC_KEY: YourServerPublicKey
    PLAYER_DATA_ENCRYPTION_KEY: YourPlayerDataEncryptionKey
    SERVER: 'true' # Optional, only if you want to create DedicatedServerEngine.ini
    DEDICATED_SERVER_INI: 'YourDedicatedServerConfigContent' # Required if SERVER is 'true'
```
## Outputs

There are no outputs for this action as it performs file operations directly.

## Typical Usage

Use this action anytime you need to prepare your UE5 project's configuration files for EOS, such as during a build process or when setting up environments. Make sure to provide all the necessary inputs for the configuration files you are updating or creating.

## Additional Information

-   Ensure that the `actions/checkout` step is used before this action to clone the repository into the GitHub Actions runner.
-   This action is created by Orchid Isle Games and is part of our suite of tools for Unreal Engine 5 projects.

For more information on using Epic Online Services with Unreal Engine, refer to the [EOS Documentation](https://dev.epicgames.com/docs/services/en-US/index.html).

----------

This action is maintained by [Orchid Isle Games](https://github.com/OrchidIsle). For support, please open an issue in the repository.

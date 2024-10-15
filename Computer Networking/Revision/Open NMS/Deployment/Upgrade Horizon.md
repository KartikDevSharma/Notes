# OpenNMS Horizon Upgrade, Backup, and Restore: A Simple Summary

## Upgrade Horizon

Upgrading Horizon is like updating an app on your phone, but a bit more complex because it's a crucial system for your network.

### 1. Identify Changed Configuration Files

#### What is it?
This step is about finding out which settings files have been modified since you last installed or upgraded OpenNMS.

#### How it works:
1. OpenNMS compares your current configuration files with the default ones.
2. It identifies which files you've customized.

#### Why it's important:
- It prevents your custom settings from being overwritten during the upgrade.
- It helps you know which settings you might need to update for the new version.

#### In simple terms:
It's like checking which settings you've changed on your phone before updating its operating system, so you don't lose your preferences.

### 2. Manage Configuration Changes with Git

#### What is it?
Git is a tool that helps keep track of changes in files over time.

#### How it works:
1. You use Git to create a record of your configuration files.
2. Each change you make is saved as a separate version.
3. You can easily see what changed, when, and why.

#### Why use it:
- It provides a history of all changes.
- You can easily revert changes if something goes wrong.
- It helps manage configurations across multiple OpenNMS installations.

#### In simple terms:
It's like having a time machine for your OpenNMS settings. You can see how they changed over time and go back to previous versions if needed.

### 3. Basic Upgrade Steps

#### What is it?
These are the fundamental steps to upgrade OpenNMS Horizon.

#### How it works:
1. Back up your current system.
2. Download the new version of OpenNMS.
3. Stop the current OpenNMS service.
4. Install the new version.
5. Update the database schema if necessary.
6. Start the new OpenNMS service.

#### Why it's important:
- It ensures a smooth transition to the new version.
- It minimizes the risk of losing data or functionality.

#### In simple terms:
It's like following a recipe to cook a complex dish. Each step is important to ensure everything turns out right.

### 4. Upgrade Horizon with Git

#### What is it?
This is a more advanced method of upgrading that uses Git to manage the process.

#### How it works:
1. Your configuration is stored in a Git repository.
2. You merge the new version's changes into your Git repository.
3. Git helps identify and resolve any conflicts between your changes and the new version's changes.

#### Why use it:
- It provides better control over the upgrade process.
- It makes it easier to handle complex configurations.
- It creates a clear record of what changed during the upgrade.

#### In simple terms:
It's like having a smart assistant that helps you compare your current settings with the new version's settings, making sure everything fits together properly.

## Back up OpenNMS Horizon

#### What is it?
Creating a safety copy of your OpenNMS system and data.

#### How it works:
1. Stop the OpenNMS service.
2. Copy all configuration files.
3. Export the database.
4. Save any custom scripts or plugins.
5. Document the current version and any special settings.

#### Why it's important:
- It protects against data loss.
- It allows you to recover if something goes wrong during an upgrade or if there's a system failure.

#### In simple terms:
It's like taking a snapshot of your entire OpenNMS system. If anything goes wrong, you can use this snapshot to recreate the system exactly as it was.

## Restore OpenNMS Horizon

#### What is it?
The process of bringing back a previous version of OpenNMS from a backup.

#### How it works:
1. Install the same version of OpenNMS that was backed up.
2. Stop the OpenNMS service.
3. Replace the configuration files with the backed-up versions.
4. Import the backed-up database.
5. Restore any custom scripts or plugins.
6. Start the OpenNMS service.

#### Why it's important:
- It allows you to recover from major issues or failed upgrades.
- It minimizes downtime in case of system failures.

#### In simple terms:
It's like using the snapshot you took earlier to rebuild your OpenNMS system. This ensures you can always get back to a working state, even if something goes seriously wrong.

﻿# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).



## Version [2.9.2] - 2024-12-12 🚀

### Fixed 🐛

- [Issue #85](https://github.com/I-am-PUID-0/pd_zurg/issues/85) - Updated the default plex_debrid files to the latest changes from the [elfhosted](https://github.com/elfhosted/plex_debrid)


## Version [2.9.1] - 2024-09-03 🚀

### Fixed 🐛

- [Issue #68](https://github.com/I-am-PUID-0/pd_zurg/issues/68) Docker Compose fetches incorrect architecture binary on Raspbian arm64 🛠️
- [Issue #69](https://github.com/I-am-PUID-0/pd_zurg/issues/69) Dockerfile pulling the wrong zurg architecture, when running on aarch64 🛠️


## Version [2.9.0] - 2024-08-09 🚀

### Changed 🔄

- plex_debrid: Pulled in [elfhosted](https://github.com/elfhosted/plex_debrid) fork of plex_debrid as the base plex_debrid within the pd_zurg image 🔄

### Added ✨

- TRAKT_CLIENT_ID: Environment variable to set the trakt client ID for plex_debrid 📊 - when not set, it will use **[itsToggle's](https://github.com/itsToggle)** trakt client ID and secret
- TRAKT_CLIENT_SECRET: Environment variable to set the trakt client secret for plex_debrid 📊 - when not set, it will use **[itsToggle's](https://github.com/itsToggle)** trakt client ID and secret

### Notes 📝

- Per [elfhosted](https://github.com/elfhosted/plex_debrid/tree/main#improvements), below are the improvements made to the plex_debrid fork:

* ✅ Support [ElfHosted internal URLs](https://elfhosted.com/how-to/connect-apps/) for [Plex](https://elfhosted.com/app/plex/), [Jellyfin](https://elfhosted.com/app/jellyfin/), [Overseerr](https://elfhosted.com/app/overseerr/), [Jackett](https://elfhosted.com/app/jackett/), [Prowlarr](https://elfhosted.com/app/prowlarr/) by default.
* ✅ Trakt OAuth [fixed](https://github.com/elfhosted/plex_debrid/commit/c678fa1e5974a5c666b2fe70d65228c6fdfb4047) (*by passing your own client ID / secret in ENV vars*).
* ✅ Integrated with [Zilean](https://github.com/iPromKnight/zilean/) for scraping [DebridMediaManager](https://debridmediamanager.com/) (DMM) public hashes, defaults to ElfHosted internal Zilean service.
* ✅ Parametize watchlist loop interval (*defaults to 30s instead of hard-coded 30 min*)
* ✅ Single episode downloads [fixed](https://github.com/elfhosted/plex_debrid/pull/1)

- **Zilean support is not yet implemented in pd_zurg, but will be in a future release**

## Version [2.8.1] - 2024-08-09 🚀

## Fixed 🐛

- healthcheck: Fixed healthcheck for zurg w/ armv7 🛠️


## Version [2.8.0] - 2024-08-09 🚀

### Changed 🔄

- plex_debrid: Debug printing for plex_debrid no longer linked to PDZURG_LOG_LEVEL 🐞
- Downloader: Add linux-arm-7 to get_architecture function 📦

### Added ✨

- PD_LOG_LEVEL: Environment variable to set the log level for plex_debrid - Only DEBUG and INFO are supported for plex_debrid ; Default is INFO 📊
- Suppress Logs: If the LOG_LEVEL for a process is set to OFF, then logs will be suppressed for the process 🤫
- Zurg: Check for arm-7 architecture for compatibility with armv7 devices and set `ln -sf /lib/ld-musl-armhf.so.1 /lib/ld-linux-armhf.so.3` 🛠️

### Notes 📝

- Setting RCLONE_LOG_LEVEL to OFF will break rclone - will patch in future release
- Thank you @barneyphife for the support with the armV7 compatibility 🙏


## Version [2.7.0] - 2024-07-30 🚀

### Changed 🔄

- Refactored to use additional common functions under utils 🛠️
- Update process: Refactored update process to apply updates to Zurg and plex_debrid before starting the processes 🔄

### Added ✨

- Ratelimit for GitHub API requests ⏳
- Retries for GitHub API requests 🔁
- plex_debrid: Debug printing for plex_debrid linked to PDZURG_LOG_LEVEL 🐞
- Zurg: Add plex_update.sh from Zurg to working directory for Zurg use 📦
- Shutdown: Added a shutdown function to gracefully stop the pd_zurg container; e.g., unmount the rclone mounts 🛑
- ffmpeg: Added ffmpeg to the Dockerfile for Zurg use of ffprobe to extract media information from files, enhancing media metadata accuracy. 🎞️
- COLOR_LOG_ENABLED: Environment variable to enable color logging; Default is false 🌈

### Fixed 🐛

[PR #62](https://github.com/I-am-PUID-0/pd_zurg/pull/62) - Allow nightly release custom versions for ZURG_VERSION


## Version [2.6.0] - 2024-07-26

### Changed

- [PR #62](https://github.com/I-am-PUID-0/pd_zurg/pull/62) - Allow nightly release custom versions for ZURG_VERSION


## Version [2.5.0] - 2024-07-22

### Added

- [Issue #59](https://github.com/I-am-PUID-0/pd_zurg/issues/59): Added PDZURG_LOG_SIZE environment variable to set the maximum size of the log file; Default is 10MB
- [Issue #60](https://github.com/I-am-PUID-0/pd_zurg/issues/60): Added PD_REPO environment variable to set the plex_debrid repository to pull from; Default is `None`

### Changed

- Refactored to use common functions under utils 
- Dockerfile: Updated to use the python:3.11-alpine image
- plex_debrid: Updates for plex_debrid are now enabled with PD_UPDATE when PD_REPO is used

### Notes

- The PDZURG_LOG_SIZE environment variable only applies to the pd_zurg log file; not the Zurg or plex_debrid log files. 

- The PD_REPO environment variable is used to set the plex_debrid repository to pull from. If used, the value must be a comma seperated list for the GitHub username,repository_name,and optionally the branch; e.g., PD_REPO=itsToggle,plex_debrid,main - the branch is defaulted to main if not specified

- PD_UPDATE is only functional when PD_REPO is used


## Version [2.4.3] - 2024-07-17

### Fixed

- Rclone: Fixed WebDAV URL check for Zurg startup processes to accept all 2xx status codes


## Version [2.4.2] - 2024-07-16

### Fixed

- Rclone: Fixed WebDAV URL check for Zurg startup processes when Zurg user and password are set in config.yml


## Version [2.4.1] - 2024-07-16

### Fixed

- Zurg: Fixed the removal of Zurg user and password if previously set in config.yml
- Rclone: Introduced a Rclone startup check for the Zurg WebDAV URL to ensure the Zurg startup processes have finished before starting Rclone


## Version [2.4.0] - 2024-06-26

### Added

- Zurg: GITHUB_TOKEN environment variable to use for access to the private sponsored zurg repository


## Version [2.3.0] - 2024-06-19

### Changed
- plex_debrid: The original plex_debird repository files are now stored within this repository. This is to ensure that if the original repository is deleted or removed from GitHub, this repository will still function. It's also simpler than maintaining a forked repository.


## Version [2.2.0] - 2024-06-19

### Changed

- plex_debrid: Updates for plex_debrid are disabled, as plex_debrid is no longer maintained.


## Version [2.1.5] - 2024-05-09

### Fixed
 
- [Issue #666](https://github.com/itsToggle/plex_debrid/issues/666) - Fixed issue with trakt sync not working properly in plex_debrid. Thanks to @mash2k3 for the fix!


## Version [2.1.4] - 2024-02-27

### Changed

- plex_debrid: plex_debrid setup process automatically checks for existing Plex libraries and adds them to settings.json for Library update services

### Fixed

- [Issue #2](https://github.com/I-am-PUID-0/pd_zurg/issues/2)
- [Issue #35](https://github.com/I-am-PUID-0/pd_zurg/issues/35)


## Version [2.1.3] - 2024-02-10

### Changed

- Zurg: Zurg setup process uncomments appropriate lines in config.yml for Zurg setup


## Version [2.1.2] - 2024-02-09

### Changed

- plex_debrid: plex_debrid setup process now checks for existing additional Plex users


## Version [2.1.1] - 2024-02-01

### Changed

- Zurg: Download release version parsing using GitHub release tags

### Fixed

- Healthcheck: Fixed healthcheck for rclone serve NFS  


## Version [2.1.0] - 2024-01-29

### Added

- ZURG_USER: ZURG_USER env var added to enable Zurg username for Zurg endpoints
- ZURG_PASS: ZURG_PASS env var added to enable Zurg password for Zurg endpoints
- NFS_ENABLED: NFS_ENABLED env var added to enable NFS mount for rclone w/ Zurg
- NFS_PORT: NFS_PORT env var added to define the NFS mount port for rclone w/ Zurg
- ZURG_PORT: ZURG_PORT env var added to define the Zurg port for Zurg endpoints

## Version [2.0.5] - 2024-01-29

### Fixed

- Healthcheck: Fixed healthcheck for Zurg and plex_debrid services to ensure they are checked for "true" or "false" values


## Version [2.0.4] - 2024-01-23

### Fixed

- Zurg: Fixed AllDebrid setup process for Zurg


## Version [2.0.3] - 2024-01-22

### Fixed

- plex_debrid: Fixed Plex users for Jellyfin deployments


## Version [2.0.2] - 2024-01-22

### Fixed

- PLEX_REFRESH: Fixed Plex library refresh w/ Zurg when using docker secrets

## Version [2.0.1] - 2024-01-16

### Fixed

- logging: Fixed logging for subprocesses


## Version [2.0.0] - 2024-01-04

### Breaking Change

- PD_ENABLED: Added PD_ENABLED env var to enable/disable plex_debrid service
- PLEX_USER: PLEX_USER env var no longer enables plex_debrid service

### Added

- JF_API_KEY: JF_API_KEY env var added to enable Jellyfin integration
- JF_ADDRESS: JF_ADDRESS env var added to enable Jellyfin integration
- SEERR_API_KEY: SEERR_API_KEY env var added to enable Overseerr/Jellyseerr integration
- SEERR_ADDRESS: SEERR_ADDRESS env var added to enable Overseerr/Jellyseerr integration
- PLEX_REFRESH: PLEX_REFRESH env var added to enable Plex library refresh w/ Zurg
- PLEX_MOUNT_DIR: PLEX_MOUNT_DIR env var added to enable Plex library refresh w/ Zurg

### Changed

- plex_debrid setup: plex_debrid setup process now allows for selection of Plex or Jellyfin

### Removed

- ZURG_LOG_LEVEL: Removed the need for ZURG_LOG_LEVEL env var - now set by PDZURG_LOG_LEVEL
- RCLONE_LOG_LEVEL: Removed the need for RCLONE_LOG_LEVEL env var - now set by PDZURG_LOG_LEVEL


## Version [1.1.0] - 2024-01-04

### Added

- Docker Secrets: Added support for the use of docker secrets


## Version [1.0.3] - 2024-01-03

### Changed

- Zurg: Increased read timeout to 10 seconds for GitHub repository checks
- Zurg: Setup process now checks for existing config.yml in debrid service directory
- Zurg: Setup process now checks for existing zurg app in debrid service directory
- Logging: Cleaned up logging and added additional logging details

## Version [1.0.2] - 2024-01-02

### Changed

- Zurg: Download release version parsing


## Version [1.0.1] - 2023-12-21

### Changed

- plex_debrid: increased read timeout to 5 seconds for GitHub repository checks 


## Version [1.0.0] - 2023-12-21

### Breaking Change

- Automatic Updates: AUTO_UPDATE env var renamed to PD_UPDATE

### Changed

- Automatic Updates: Refactored update process to allow for scaling of update process
- Healthcheck: Refactored healthcheck process to allow for scaling of healthcheck process
- Healthcheck: rclone mount check now uses rclone process instead of rclone mount location
- Rclone: Subprocess logs are now captured and logged to the pd_zurg logs

### Added

- ZURG_UPDATE: ZURG_UPDATE env var added to enable automatic update process for ZURG
- Zurg: Added automatic update process for Zurg
- Healthcheck: Added healthcheck for Zurg process


## Version [0.2.0] - 2023-12-13

### Added

- ZURG_LOG_LEVEL: The log level to use for Zurg as defined with the ZURG_LOG_LEVEL env var


## Version [0.1.0] - 2023-12-12

### Added

- ZURG_VERSION: The version of ZURG to use as defined with the ZURG_VERSION env var 

### Changed

- Zurg: Container pulls latest or user-defined version of ZURG from github upon startup


## Version [0.0.5] - 2023-12-06

### Fixed

- Duplicate Cleanup: Process not called correctly


## Version [0.0.4] - 2023-12-06

### Changed

- Dockerfile: Pull latest config.yml from zurg repo for base file


## Version [0.0.3] - 2023-12-05

### Fixed

- Zurg: config.yml override


## Version [0.0.2] - 2023-12-05

### Changed

- base: Update envs
- main.py: Order of execution
- healthcheck.py: Order of execution


## Version [0.0.1] - 2023-12-05

### Added

- Initial Push 

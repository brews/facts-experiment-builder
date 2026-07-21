# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.5.0] - 2026-07-20 

### Fixed
- Added two fields to module yamls of sea-level modules: 1) `pass_to_total`, true by default; set to false to prevent auxiliary outputs (such as `quantiles.nc`) from being passed to totaling step, 2) `climate_output_type`, used to specify which outptus from the climate step is expected by a sea-level module (ie.`gsat.nc` or `ohc.nc`) ([PR #83](https://github.com/fact-sealevel/facts-experiment-builder/pull/83),  [@e-marshall](https://github.com/e-marshall))
- Remove hard-coding of `"experiments/"` as parent directory of `--experiment-name`. A parent directory is not required but is recommended and should be included in `--experiment-name`. FEB resolves path based on `--root` and `--experiment-name` using `FileSystemExperimentStorage` obj ([PR #86](https://github.com/fact-sealevel/facts-experiment-builder/pull/86),  [@e-marshall](https://github.com/e-marshall))

### Added
- FEB recognizes and handles module schemas with entries in inputs section that are directories instead of files ([PR #82](https://github.com/fact-sealevel/facts-experiment-builder/pull/82),  [@e-marshall](https://github.com/e-marshall))
- Added Pydantic models for structure of individual entries in each section (top-level params, options, inputs, outputs,...) of a module yaml file ([PR #83](https://github.com/fact-sealevel/facts-experiment-builder/pull/83),  [@e-marshall](https://github.com/e-marshall))
- Add `module-registry` args to CLI commands that use registry and use `FileSystemModuleRegistry objs ([PR #86](https://github.com/fact-sealevel/facts-experiment-builder/pull/86),  [@e-marshall](https://github.com/e-marshall))
- Add `root` arg to CLI commands that write files (`setup-experiment`, `generate-compose`) to give option of specifying alternative working directory ([PR #86](https://github.com/fact-sealevel/facts-experiment-builder/pull/86),  [@e-marshall](https://github.com/e-marshall))


### Changed
- `feb generate-compose` fails loudly if service creation fails for individual module or workflow ([PR #82](https://github.com/fact-sealevel/facts-experiment-builder/pull/82), [@e-marshall](https://github.com/e-marshall))
- Small change to `InputArgSpec` to allow list of filenames to be passed in cases where multiple files may be passed for one input arg (ie. ssp-landwaterstorage). ([PR #85](https://github.com/fact-sealevel/facts-experiment-builder/pull/85),  [@e-marshall](https://github.com/e-marshall))
- Refactor module registry and how it is used in codebase ([PR #86](https://github.com/fact-sealevel/facts-experiment-builder/pull/86),  [@e-marshall](https://github.com/e-marshall))


## [0.4.1] - 2026-06-09 

### Fixed
- Bug related to `check-data` CLI command ([PR #77](https://github.com/fact-sealevel/facts-experiment-builder/pull/77), [@e-marshall](https://github.com/e-marshall))
- Added missing tlm-sterodynamics input data to setup guide instructions ([PR #78](https://github.com/fact-sealevel/facts-experiment-builder/pull/78),  [@e-marshall](https://github.com/e-marshall))

## [0.4.0] - 2026-06-09

### Added
- `feb init` command that initializes a facts workspace directory by creating a blank `experiments/` dir and cloning the module registry repo ([PR #72](https://github.com/fact-sealevel/facts-experiment-builder/pull/72), [@e-marshall](https://github.com/e-marshall))
- `feb check-data` command that checks to see which modules have input data downloaded at a provided location and if the contents match the expected structure and the files expected (as specified in the module registry) ([PR #72](https://github.com/fact-sealevel/facts-experiment-builder/pull/72), [@e-marshall](https://github.com/e-marshall)).
- Initial support for emulandice2. Still does not correctly handle all region options or write localized outputs ([PR #72](https://github.com/fact-sealevel/facts-experiment-builder/pull/72), [@e-marshall](https://github.com/e-marshall)).
- Expanded documentation surrounding experiments and downloading module input data ([PR #74](https://github.com/fact-sealevel/facts-experiment-builder/pull/74),  [@e-marshall](https://github.com/e-marshall)).
- New component of `feb init` that checks if there are more recent remote changes in the facts-module-registry repo that is cloned locally in the workspace, automatically creates .gitignore in workspace if not present and adds facts-module-registry to it ([PR #74](https://github.com/fact-sealevel/facts-experiment-builder/pull/74),  [@e-marshall](https://github.com/e-marshall)).

### Fixed
- Correct outputs now passed to totaling step ([PR #67](https://github.com/fact-sealevel/facts-experiment-builder/pull/67), [@e-marshall](https://github.com/e-marshall))

### Changed
- Changed quickstart guide name to setup guide in docs ([PR #75](https://github.com/fact-sealevel/facts-experiment-builder/pull/75), [@e-marshall](https://github.com/e-marshall))

## [0.3.1] - 2026-05-05

### Fixed
- Small typos in README ([7d984f7](7d984f72f740539850a4e42c8c6f683fbe647f5f), [@e-marshall](https://github.com/e-marshall))


## [0.3.0] - 2026-05-03

### Changed

- Move module registry to external repository; rename `setup-new-experiment` -> `setup-experiment` ([PR #60](https://github.com/fact-sealevel/facts-experiment-builder/pull/60), [@e-marshall](https://github.com/e-marshall))


## [0.2.0] - 2026-04-28

### Changed
- Containers associated with all modules in module registry now point to 'latest' tag, previously some pointed at specific versions ([PR 43](https://github.com/fact-sealevel/facts-experiment-builder/pull/43), [@e-marshall](https://github.com/e-marshall))
- Reformat CLI to `feb setup` and `feb generate` ([PR #44](https://github.com/fact-sealevel/facts-experiment-builder/pull/44), [@brews](https://github.com/brews))
- Rename `general-inputs` to `shared-in` and `experiment-metadata.yml` to `experiment-config.yml` ([PR #45](https://github.com/fact-sealevel/facts-experiment-builder/pull/45), [@e-marshall](https://github.com/e-marshall))
- Modules no longer have separate yaml files with default values, this information is now stored in the module yaml itself under `default_value` and `filename` keys. ([PR #55](https://github.com/fact-sealevel/facts-experiment-builder/pull/55), [@e-marshall](https://github.com/e-marshall))
- `setup-new-experiment` CLI command did have a `--framework-step` arg that accepted `'facts-total'` module. this was redundant and now removed. `'facts-total'` called if multiple sea-level modules are specified in experiment. ([PR #55](https://github.com/fact-sealevel/facts-experiment-builder/pull/55), [@e-marshall](https://github.com/e-marshall))
- Undo 43 ([PR #58](https://github.com/fact-sealevel/facts-experiment-builder/pull/58),[@e-marshall](https://github.com/e-marshall))
### Added
- Added option to automatically pass all modules instead of specifying them all in a workflow ([PR #48](https://github.com/fact-sealevel/facts-experiment-builder/commit/ee08b23759b8dec5141323c2886d634113c26f4e), [@e-marshall](https://github.com/e-marshall))

### Fixed
- Solved issues that prevented FEB from creating modules that include the [emulandice](https://github.com/fact-sealevel/emulandice) module ([PR #50](https://github.com/fact-sealevel/facts-experiment-builder/pull/50), [@e-marshall](https://github.com/e-marshall))
- Seed is no longer the same across all modules in an experiment. Instead of an experiment-level (`top-level`) argument passed in `setup-new-experiment` and spec. in `experiment-config.yml`, it is hard-coded in each module's ModuleRegistry yaml to match its value in Facts1 development branch ([PR #57](https://github.com/fact-sealevel/facts-experiment-builder/pull/57), [@e-marshall](https://github.com/e-marshall)).

## [0.1.0] - 2026-04-08

- Initial release

[0.5.0]: https://github.com/fact-sealevel/facts-experiment-builder/compare/v0.4.1...v0.5.0
[0.4.1]: https://github.com/fact-sealevel/facts-experiment-builder/compare/v0.4.0...v0.4.1
[0.4.0]: https://github.com/fact-sealevel/facts-experiment-builder/compare/v0.3.1...v0.4.0
[0.3.1]: https://github.com/fact-sealevel/facts-experiment-builder/compare/v0.3.0...v0.3.1
[0.3.0]: https://github.com/fact-sealevel/facts-experiment-builder/compare/v0.2.0...v0.3.0
[0.2.0]: https://github.com/fact-sealevel/facts-experiment-builder/compare/v0.1.0...v0.2.0
[0.1.0]: https://github.com/fact-sealevel/facts-experiment-builder/tag/v0.1.0

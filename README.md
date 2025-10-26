<p align="center">
  <a href="https://github.com/Flow-Scanner">
    <img src="https://raw.githubusercontent.com/Flow-Scanner/lightning-flow-scanner-core/main/assets/media/bannerslim.png" style="width: 41%;" />
  </a>
</p>
<p align="center">Scans for unsafe contexts, hardcoded IDs, and other issues to optimize your Flows.</p>

<p align="center">
<img src="https://raw.githubusercontent.com/Flow-Scanner/lightning-flow-scanner-copado/main/assets/Copado-LFS.gif" style="width: 88%;" />
</p>

- [Usage](#usage)
- [Installation](#installation)
  - [Set-up Picklist Values](set-up-picklist-values)
  - [Create The Job Templates](create-the-job-templates)
  - [Configure Threshold Criteria](configure-threshold-criteria)
- [Configuration](#configuration)
  - [Create a Quality Gate(Rule)](#create-the-quality-gate-rule)
  - [Create a Quality Gate(Condition)](#create-the-quality-gate-rule-condition)

## Usage
A Copado Plugin for automated analysis and optimization of Salesforce Flow in User Stories. Scans metadata for 20+ issues such as hardcoded IDs, unsafe contexts, inefficient SOQL/DML operations, recursion risks, and missing fault handling. View comprehensive results directly within Copado for confident releases. For more information on the default rules and configurations, please review the [flow scanner documentation](https://flow-scanner.github.io/lightning-flow-scanner-core/). To watch a full Demo, [click here](https://www.loom.com/share/d5fc87459e714e94b72abcd5511be5d8)

##### Maintainers
* Maintained by [@abhisheksaxena7](https://github.com/abhisheksaxena7)

##### Pre-Requisites
* Copado v21.14 or higher
* Copado Quality Tools extension v1.42 or higher

##### Scanner Version
* Lightning Flow Scanner Core v.2.6.0

##### Warning
This plugin is running on Lightning Flow Scanner Core [v2.6.0](https://www.npmjs.com/package/lightning-flow-scanner-core/v/2.6.0), which contains known vulnerabilities and is no longer supported. For more information on a fix, please see [the related pull request](https://github.com/Flow-Scanner/lightning-flow-scanner-copado/pull/2).

## Installation

### Set-up Picklist Values

Create the Following Picklist values

* **Object: Extension Configuration** > Field: Extension Tool, Value: `flow-scanner`
* **Picklist Value Set** > Copado Test Tool, Value: `flow-scanner`

### Create The Job Templates

Navigate to the “Copado Extensions” tab, select “CopadoFlowScanner” and press the button “Generate Extension Records”.

<p align="center">
<img src="./assets/images/generate-extension-records.png" style="width: 88%;" />
</p>

### Configure Threshold Criteria

<p align="center">
<img src="./assets/images/function-parameter.png" />
</p>

`fail_on` - This parameter can take one of three rule severity values - `error`, `note` or `warning`. The default value of it is `error`. This parameter decides when should the Quality Gate fail.

- Setting it to `error` means - Succeed the Quality Gate, if their are no violations or they are only of type `warning` or `note`. Fail on violations of severity `error`.
- Setting it to `warning` means - Succeed the Quality Gate, if their are no violations or they are only of type or `note`. Fail on violations of severity `error` or `warning`.
- Setting it to `note` means - Succeed the Quality Gate, if their are no violations. Fail on any violations irrespective of severity.

By default, all rules have a severity of `error`. To customize behaviour, check the [core documentation](https://flow-scanner.github.io/lightning-flow-scanner-core/) on how to create a  `.flow-scanner.json` configuration file.

## Configuration

### Create the Quality Gate Rule

Navigate to the Quality Gate Rules tab and create a new record as follows. Note that the Type field will be populated automatically upon save. The global value set Test Tool should have a value for `Flow Scanner` as part of this package. It can be created manually if necessary.

<p align="center">
<img src="./assets/images/create-quality-gate-rule.png" style="width: 88%;" />
</p>

### Create the Quality Gate Rule Condition

Set the conditions so that it only applies to `Pipelines/Stages/Environments` with Platform = `SFDX`. This picklist value can be added manually if necessary.
Once saved, press the “Activate” button on the Quality Gate Rule record. To run Flow Scanner only when Flows are committed, add Filter Logic as demonstrated below:

<p align="center">
<img src="./assets/images/quality-gate-rule-condition.png" style="width: 88%;" />
</p>

**You are all set.** To test the configuration, just perform a commit, and the Commit Action will call `Flow Scanner` after every commit.

If you'd like to help us enhance Flow Scanner, please consider having a look at the [Contributing Guidelines](https://github.com/Flow-Scanner/lightning-flow-scanner-core/blob/main/CONTRIBUTING.md).

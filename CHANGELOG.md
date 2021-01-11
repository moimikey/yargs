# Changelog

All notable changes to this project will be documented in this file. See [standard-version](https://github.com/conventional-changelog/standard-version) for commit guidelines.

## [15.2.0](https://www.github.com/moimikey/yargs/compare/v6.0.0...v15.2.0) (2021-01-11)


### ⚠ BREAKING CHANGES

* #1823 contains the following breaking API changes:
    * now returns a promise if handler is async.
    * onFinishCommand removed, in favor of being able to await promise.
    * getCompletion now invokes callback with err and `completions, returns promise of completions.
* tweaks to ESM/Deno API surface: now exports yargs function by default; getProcessArgvWithoutBin becomes hidBin; types now exported for Deno.
* find-up replaced with escalade; export map added (limits importable files in Node >= 12); yarser-parser@19.x.x (new decamelize/camelcase implementation).
* **usage:** single character aliases are now shown first in help output
* **ts:** yargs now ships with its own types
* drop support for EOL Node 8 (#1686)
* **deps:** yargs-parser@17.0.0 no longer implicitly creates arrays out of boolean arguments when duplicates are provided
* **deps:** yargs-parser now throws on invalid combinations of config (#1470)
* yargs-parser@16.0.0 drops support for Node 6
* drop Node 6 support (#1461)
* remove package.json-based parserConfiguration (#1460)
* previously to this fix methods like `yargs.getOptions()` contained the state of the last command to execute.
* do not allow additional positionals in strict mode
* options with leading '+' or '0' now parse as strings
* dropping Node 6 which hits end of life in April 2019
* see [yargs-parser@12.0.0 CHANGELOG](https://github.com/yargs/yargs-parser/blob/master/CHANGELOG.md#breaking-changes)
* we now warn if the yargs stanza package.json is used.
* Options absent from `argv` (not set via CLI argument) are now absent from the parsed result object rather tahn being set with `undefined`
* drop Node 6 from testing matrix, such that we'll gradually start drifting away from supporting Node 4.
* yargs-parser does not populate 'false' when boolean flag is not passed
* tests that assert against help output will need to be updated
* requiresArg now has significantly different error output, matching nargs.
* .usage() no longer accepts an options object as the second argument. It can instead be used as an alias for configuring a default command.
* previously hidden options were simply implied using a falsy description
* help command now only executes if it's the last positional in argv._
* version() and help() are now enabled by default, and show up in help output; the implicit help command can no longer be enabled/disabled independently from the help command itself (which can now be disabled).
* environment variables will now override config files, '--' is now populated rather than '_' when parsing is stopped.
* extends functionality now always loads the JSON provided, rather than reading from a specific key
* this pull requests introduces language features that require Node 4+.
* the first argument to strict() is now used to enable/disable its functionality, rather than controlling whether or not it is global.
* `extends` key in config file is now used for extending other config files
* environment variables now take precedence over config files.
* context now takes precedence over argv and defaults
* there's a good chance this will throw exceptions for a few folks who are using the API in an unexpected way.
* by default options, and many of yargs' parsing helpers will now default to being applied globally; such that they are no-longer reset before being passed into commands.
* yargs will no longer aggressively supress errors, allowing errors that are not generated internally to bubble.

### Features

* .usage() can now be used to configure a default command ([#975](https://www.github.com/moimikey/yargs/issues/975)) ([7269531](https://www.github.com/moimikey/yargs/commit/72695316e02ae7e5cd0a78897dd0748068e345fc))
* Add `.parserConfiguration()` method, deprecating package.json config ([#1262](https://www.github.com/moimikey/yargs/issues/1262)) ([3c6869a](https://www.github.com/moimikey/yargs/commit/3c6869aae7b488d2416f66c19a801c06243c075c))
* add applyBeforeValidation, for applying sync middleware before validation ([5be206a](https://www.github.com/moimikey/yargs/commit/5be206ac9ecd096531ed1726032484e7884293a8))
* add conflicts and implies shorthands. ([#753](https://www.github.com/moimikey/yargs/issues/753)) ([bd1472b](https://www.github.com/moimikey/yargs/commit/bd1472ba3da6a6cbae521559b9c662416d1bac12))
* add missing simple chinese locale strings ([#1004](https://www.github.com/moimikey/yargs/issues/1004)) ([3cc24ec](https://www.github.com/moimikey/yargs/commit/3cc24ecd49b2c29ee70af6cdab5a3f014d613576))
* add new pt_BR translations ([#674](https://www.github.com/moimikey/yargs/issues/674)) ([5615a82](https://www.github.com/moimikey/yargs/commit/5615a82ed7b7246e9f5e7441ad853a17b8f71ebd))
* add Norwegian Nynorsk translations ([#1028](https://www.github.com/moimikey/yargs/issues/1028)) ([a5ac213](https://www.github.com/moimikey/yargs/commit/a5ac2133f712a546c88bb00e2443bb9aeb82d0ac))
* add support for global middleware, useful for shared tasks like metrics ([#1119](https://www.github.com/moimikey/yargs/issues/1119)) ([9d71ac7](https://www.github.com/moimikey/yargs/commit/9d71ac745baeaf5f5277dd5aef6b4b4316acfafb))
* add support for numeric commands ([#825](https://www.github.com/moimikey/yargs/issues/825)) ([fde0564](https://www.github.com/moimikey/yargs/commit/fde0564f4d7275e8ed09684ebf02d606d2ad8569))
* add traditional Chinese translation ([#780](https://www.github.com/moimikey/yargs/issues/780)) ([6ab6a95](https://www.github.com/moimikey/yargs/commit/6ab6a95de6358f8e42466c424567a28ed0bd45cf))
* add usage for single-digit boolean aliases ([#1580](https://www.github.com/moimikey/yargs/issues/1580)) ([6014e39](https://www.github.com/moimikey/yargs/commit/6014e39bca3a1e8445aa0fb2a435f6181e344c45))
* adds config option for sorting command output ([#1256](https://www.github.com/moimikey/yargs/issues/1256)) ([6916ce9](https://www.github.com/moimikey/yargs/commit/6916ce9a548c4f0ccd80740a0d85c6e7c567ff84))
* adds deprecation option for commands ([027a636](https://www.github.com/moimikey/yargs/commit/027a6365b737e13116811a8ef43670196e1fa00a))
* adds strictOptions() ([#1738](https://www.github.com/moimikey/yargs/issues/1738)) ([b215fba](https://www.github.com/moimikey/yargs/commit/b215fba0ed6e124e5aad6cf22c8d5875661c63a3))
* adds support for ESM and Deno ([#1708](https://www.github.com/moimikey/yargs/issues/1708)) ([ac6d5d1](https://www.github.com/moimikey/yargs/commit/ac6d5d105a75711fe703f6a39dad5181b383d6c6))
* adds support for multiple epilog messages ([#1384](https://www.github.com/moimikey/yargs/issues/1384)) ([07a5554](https://www.github.com/moimikey/yargs/commit/07a5554c480ff3aa43cdc37b1d4ecbaf2687c779))
* allow completionCommand to be set via showCompletionScript ([#1385](https://www.github.com/moimikey/yargs/issues/1385)) ([5562853](https://www.github.com/moimikey/yargs/commit/55628535a242979adcf189d917082083edb2ad56))
* allow extends to inherit from a module ([#865](https://www.github.com/moimikey/yargs/issues/865)) ([89456d9](https://www.github.com/moimikey/yargs/commit/89456d994216466da2be929d81d3fb936005ae96))
* allow hidden options to be displayed with --show-hidden ([#1061](https://www.github.com/moimikey/yargs/issues/1061)) ([ea862ae](https://www.github.com/moimikey/yargs/commit/ea862ae551b8e973534c1fc0248bc85fd8a01c7a))
* allow implies and conflicts to accept array values ([#922](https://www.github.com/moimikey/yargs/issues/922)) ([abdc7da](https://www.github.com/moimikey/yargs/commit/abdc7da9d60e48b105034a255f62e3d6f10c6650))
* allow parse with no arguments as alias for yargs.argv ([#944](https://www.github.com/moimikey/yargs/issues/944)) ([a9f03e7](https://www.github.com/moimikey/yargs/commit/a9f03e712a2176d348c34def80d7107adda2ba0e))
* allow provided config object to extend other configs ([#779](https://www.github.com/moimikey/yargs/issues/779)) ([3280dd0](https://www.github.com/moimikey/yargs/commit/3280dd02ce125e00f2e4d02ae26fcb59e82a55a7))
* allow setting scriptName $0 ([#1143](https://www.github.com/moimikey/yargs/issues/1143)) ([a2f2eae](https://www.github.com/moimikey/yargs/commit/a2f2eae2235fa9b10ce221aea1320b1dfc564efa))
* allow strict mode to be disabled ([#840](https://www.github.com/moimikey/yargs/issues/840)) ([6f78c05](https://www.github.com/moimikey/yargs/commit/6f78c05a3a719f3c40e3b8197dd1ea2e85afd627))
* async command handlers ([#1001](https://www.github.com/moimikey/yargs/issues/1001)) ([241124b](https://www.github.com/moimikey/yargs/commit/241124ba4bfad505363433453c51e22c4e4f2baf))
* command() now accepts an array of modules ([f415388](https://www.github.com/moimikey/yargs/commit/f415388cc454d02786c65c50dd6c7a0cf9d8b842))
* **command:** add camelcase commands to argv ([#658](https://www.github.com/moimikey/yargs/issues/658)) ([b1cabae](https://www.github.com/moimikey/yargs/commit/b1cabae60ca1ae715ee9bc8ad10f7ce69f644048))
* complete short options with a single dash ([#1507](https://www.github.com/moimikey/yargs/issues/1507)) ([99011ab](https://www.github.com/moimikey/yargs/commit/99011ab5ba90232506ece0a17e59e2001a1ab562))
* **completion:** takes negated flags into account when boolean-negation is set ([#1509](https://www.github.com/moimikey/yargs/issues/1509)) ([7293ad5](https://www.github.com/moimikey/yargs/commit/7293ad50d20ea0fb7dd1ac9b925e90e1bd95dea8))
* deprecateOption ([#1559](https://www.github.com/moimikey/yargs/issues/1559)) ([8aae333](https://www.github.com/moimikey/yargs/commit/8aae3332251d09fa136db17ef4a40d83fa052bc4))
* **deps:** introduce yargs-parser with support for unknown-options-as-args ([#1440](https://www.github.com/moimikey/yargs/issues/1440)) ([4d21520](https://www.github.com/moimikey/yargs/commit/4d21520ca487b65f2ace422c323aaecb2be1c8a6))
* **deps:** pull in yargs-parser@17.0.0 ([#1553](https://www.github.com/moimikey/yargs/issues/1553)) ([b9409da](https://www.github.com/moimikey/yargs/commit/b9409da199ebca515a848489c206b807fab2e65d))
* **deps:** yargs-parser now throws on invalid combinations of config ([#1470](https://www.github.com/moimikey/yargs/issues/1470)) ([c10c38c](https://www.github.com/moimikey/yargs/commit/c10c38cca04298f96b55a7e374a9a134abefffa7))
* **deps:** yargs-parser with 'greedy-array' configuration ([#1569](https://www.github.com/moimikey/yargs/issues/1569)) ([a03a320](https://www.github.com/moimikey/yargs/commit/a03a320dbf5c0ce33d829a857fc04a651c0bb53e))
* **deps:** yargs-parser with support for collect-unknown-options ([#1421](https://www.github.com/moimikey/yargs/issues/1421)) ([d388a7c](https://www.github.com/moimikey/yargs/commit/d388a7cbb03b5e74bc07b4b48789511fe1306a0a))
* display appropriate $0 for electron apps ([#1536](https://www.github.com/moimikey/yargs/issues/1536)) ([d0e4379](https://www.github.com/moimikey/yargs/commit/d0e437912917d6a66bb5128992fa2f566a5f830b))
* drop support for EOL Node 8 ([#1686](https://www.github.com/moimikey/yargs/issues/1686)) ([863937f](https://www.github.com/moimikey/yargs/commit/863937f23c3102f804cdea78ee3097e28c7c289f))
* enable .help() and .version() by default ([#912](https://www.github.com/moimikey/yargs/issues/912)) ([1ef44e0](https://www.github.com/moimikey/yargs/commit/1ef44e03ef1a2779f92bd979984a6bab3a671ee9))
* expose `Parser` from `require('yargs/yargs')` ([#1477](https://www.github.com/moimikey/yargs/issues/1477)) ([1840ba2](https://www.github.com/moimikey/yargs/commit/1840ba22f1a24c0ece8e32bbd31db4134a080aee))
* expose hideBin helper for CJS ([#1768](https://www.github.com/moimikey/yargs/issues/1768)) ([63e1173](https://www.github.com/moimikey/yargs/commit/63e1173bb47dc651c151973a16ef659082a9ae66))
* extend *.rc files in addition to json ([#1080](https://www.github.com/moimikey/yargs/issues/1080)) ([11691a6](https://www.github.com/moimikey/yargs/commit/11691a670b384e3dce2ee61fc92e6b6965079708))
* function argument validation ([#773](https://www.github.com/moimikey/yargs/issues/773)) ([22ed9bb](https://www.github.com/moimikey/yargs/commit/22ed9bb8b4be48c52fe0e3e965460954d07f8f80))
* **helpers:** rebase, Parser, applyExtends now blessed helpers ([#1733](https://www.github.com/moimikey/yargs/issues/1733)) ([c7debe8](https://www.github.com/moimikey/yargs/commit/c7debe8eb1e5bc6ea20b5ed68026c56e5ebec9e1))
* hidden options are now explicitly indicated using "hidden" flag ([#962](https://www.github.com/moimikey/yargs/issues/962)) ([280d0d6](https://www.github.com/moimikey/yargs/commit/280d0d6bd1035b91254db876281c1ae755520f07))
* i18n for ESM and Deno ([#1735](https://www.github.com/moimikey/yargs/issues/1735)) ([c71783a](https://www.github.com/moimikey/yargs/commit/c71783a5a898a0c0e92ac501c939a3ec411ac0c1))
* **i18n:** swap out os-locale dependency for simple inline implementation ([#1356](https://www.github.com/moimikey/yargs/issues/1356)) ([4dfa19b](https://www.github.com/moimikey/yargs/commit/4dfa19b3275cbd74ed686c437d392c4612e237a4))
* if only one column is provided for examples, allow it to take up the entire line ([#749](https://www.github.com/moimikey/yargs/issues/749)) ([7931652](https://www.github.com/moimikey/yargs/commit/793165278bcccdd4f67c2656b4bd12e2d80ee421))
* implement conflicts() for defining mutually exclusive arguments; thanks [@madcampos](https://www.github.com/madcampos)! ([#741](https://www.github.com/moimikey/yargs/issues/741)) ([5883779](https://www.github.com/moimikey/yargs/commit/5883779b1a3fc6a88b12fa9abe45c82f2ab79a2e))
* improve support for async/await ([#1823](https://www.github.com/moimikey/yargs/issues/1823)) ([169b815](https://www.github.com/moimikey/yargs/commit/169b815df7ae190965f04030f28adc3ab92bb4b5))
* initial support for command aliases ([#647](https://www.github.com/moimikey/yargs/issues/647)) ([127a040](https://www.github.com/moimikey/yargs/commit/127a0407a51817b8dd048c282f7ad6dc59f8b53f))
* introduce .positional() for configuring positional arguments ([#967](https://www.github.com/moimikey/yargs/issues/967)) ([cb16460](https://www.github.com/moimikey/yargs/commit/cb16460bffeb13d54215de45c09dbe4708aee770))
* introduce custom yargs error object ([#765](https://www.github.com/moimikey/yargs/issues/765)) ([8308efa](https://www.github.com/moimikey/yargs/commit/8308efab74bb2734248accc17429cfc163a7d463))
* introduces strictCommands() subset of strict mode ([#1540](https://www.github.com/moimikey/yargs/issues/1540)) ([1d4cca3](https://www.github.com/moimikey/yargs/commit/1d4cca395a98b395e6318f0505fc73bef8b01350))
* introduces support for default commands, using the '*' identifier ([#785](https://www.github.com/moimikey/yargs/issues/785)) ([d78a0f5](https://www.github.com/moimikey/yargs/commit/d78a0f5b42d41f3959c451b8e2f81e8fdbac845e))
* Italian translations for 'did you mean' and 'aliases' ([#673](https://www.github.com/moimikey/yargs/issues/673)) ([81984e6](https://www.github.com/moimikey/yargs/commit/81984e69e4d6ebfd1a6155a56e4248da7f54c2f5))
* **lang:** add Finnish localization (language code fi) ([222c8fe](https://www.github.com/moimikey/yargs/commit/222c8fef2e2ad46e314c337dec96940f896bec35))
* **locales:** add Hindi translations ([9290912](https://www.github.com/moimikey/yargs/commit/9290912f77767534d603a66666545326009b3553))
* **locales:** add Hungarian translations ([be92327](https://www.github.com/moimikey/yargs/commit/be92327fad6c2af52fb52a3e9de52baa58a4800a))
* **locales:** Add Thai locale file ([#679](https://www.github.com/moimikey/yargs/issues/679)) ([c05e36b](https://www.github.com/moimikey/yargs/commit/c05e36b4ad991bc8f7d771e8612e5d057cf6dd9a))
* **locales:** Added Belarusian translation ([#690](https://www.github.com/moimikey/yargs/issues/690)) ([68dac1f](https://www.github.com/moimikey/yargs/commit/68dac1f7740649f56df51e0655ff509b85e33756))
* **locales:** Create nl.json ([#687](https://www.github.com/moimikey/yargs/issues/687)) ([46ce1bb](https://www.github.com/moimikey/yargs/commit/46ce1bb3f980d30355a0b52d83c0d1f995a4996a))
* **locales:** Japanese translations for 'did you mean' and 'aliases'  ([#651](https://www.github.com/moimikey/yargs/issues/651)) ([5eb78fc](https://www.github.com/moimikey/yargs/commit/5eb78fcfe1d6c838bbd54a0c318de68e2d853d5a))
* **locales:** Polish translations for 'did you mean' and 'aliases' ([#650](https://www.github.com/moimikey/yargs/issues/650)) ([c951c0e](https://www.github.com/moimikey/yargs/commit/c951c0e1769c3de689d95e0d79d2aadab6bfeda9))
* make it possible to merge configurations when extending other config. ([#1411](https://www.github.com/moimikey/yargs/issues/1411)) ([5d7ad98](https://www.github.com/moimikey/yargs/commit/5d7ad989a851398587a0349cdd15344769b4cd79))
* middleware ([#881](https://www.github.com/moimikey/yargs/issues/881)) ([77b8dbc](https://www.github.com/moimikey/yargs/commit/77b8dbc495b926ef2dbc9d839882c828b8dad29b))
* multiple usage calls are now collected, not replaced ([#958](https://www.github.com/moimikey/yargs/issues/958)) ([74a38b2](https://www.github.com/moimikey/yargs/commit/74a38b2646478c301a17498afa36a832277e5b9c))
* onFinishCommand handler ([#1473](https://www.github.com/moimikey/yargs/issues/1473)) ([fe380cd](https://www.github.com/moimikey/yargs/commit/fe380cd356aa33aef0449facd59c22cab8930ac9))
* options/positionals with leading '+' and '0' no longer parse as numbers ([#1286](https://www.github.com/moimikey/yargs/issues/1286)) ([e9dc3aa](https://www.github.com/moimikey/yargs/commit/e9dc3aaf7b9d0fe07bfbe28ec347db7d959cbf0b))
* pull in yargs-parser introducing additional settings ([#688](https://www.github.com/moimikey/yargs/issues/688)), and fixing [#716](https://www.github.com/moimikey/yargs/issues/716) ([#722](https://www.github.com/moimikey/yargs/issues/722)) ([702995a](https://www.github.com/moimikey/yargs/commit/702995a04648460ac5a4c7c531e26c6b4750f38f))
* remove `setPlaceholderKeys` ([#1105](https://www.github.com/moimikey/yargs/issues/1105)) ([6ee2c82](https://www.github.com/moimikey/yargs/commit/6ee2c82df515cb1b062e4135a5dd9c386fed2b21))
* replace /bin/bash with file basename ([#983](https://www.github.com/moimikey/yargs/issues/983)) ([20bb99b](https://www.github.com/moimikey/yargs/commit/20bb99b25630594542577133d51e38a4c6712d31))
* requiresArg is now simply an alias for nargs(1) ([#1054](https://www.github.com/moimikey/yargs/issues/1054)) ([a3ddacc](https://www.github.com/moimikey/yargs/commit/a3ddacc87e6cbb8a275f97d746511fe1d1f93044))
* rethink how options are inherited by commands ([#766](https://www.github.com/moimikey/yargs/issues/766)) ([ab1fa4b](https://www.github.com/moimikey/yargs/commit/ab1fa4b355cbf75506b18f27cb1ae4bf8b646c39))
* reworking yargs API to make it easier to run in headless environments, e.g., Slack ([#646](https://www.github.com/moimikey/yargs/issues/646)) ([f284c29](https://www.github.com/moimikey/yargs/commit/f284c2968c2f8b818b0737dc09c94a44ef8afc25))
* split demand() into demandCommand()/demandOption() ([#740](https://www.github.com/moimikey/yargs/issues/740)) ([66573c8](https://www.github.com/moimikey/yargs/commit/66573c82ed1479eb6ba9bf654463e3ca2d99c6dc))
* support array of examples ([#1682](https://www.github.com/moimikey/yargs/issues/1682)) ([225ab82](https://www.github.com/moimikey/yargs/commit/225ab8271938bed3a48d23175f3d580ce8cd1306))
* support defaultDescription for positional arguments ([812048c](https://www.github.com/moimikey/yargs/commit/812048ccaa31ac0db072d13589ef5af8cd1474c6))
* support for positional argument aliases ([#727](https://www.github.com/moimikey/yargs/issues/727)) ([27e1a57](https://www.github.com/moimikey/yargs/commit/27e1a57825bc949cec0f33c802124046499953a4))
* support promises in middleware ([f3a4e4f](https://www.github.com/moimikey/yargs/commit/f3a4e4f7531d74668a07be87f45dc497d4d08c4b))
* to allow both undefined and nulls, for benefit of TypeScript  ([#945](https://www.github.com/moimikey/yargs/issues/945)) ([792564d](https://www.github.com/moimikey/yargs/commit/792564d954d5143b2b57b05aaca4007780f5b728))
* **translation:** Update pl-PL translations ([#985](https://www.github.com/moimikey/yargs/issues/985)) ([5a9c986](https://www.github.com/moimikey/yargs/commit/5a9c98643333799e04fc78c5797fad0ecfefde86))
* Turkish translations for 'did you mean' and 'aliases' ([#660](https://www.github.com/moimikey/yargs/issues/660)) ([072fd45](https://www.github.com/moimikey/yargs/commit/072fd45f9c5266eb4833b35075c7eb6ed7d31dae))
* tweaks to API surface based on user feedback ([#1726](https://www.github.com/moimikey/yargs/issues/1726)) ([4151fee](https://www.github.com/moimikey/yargs/commit/4151fee4c33a97d26bc40de7e623e5b0eb87e9bb))
* update to yargs-parser that addresses [#598](https://www.github.com/moimikey/yargs/issues/598), [#617](https://www.github.com/moimikey/yargs/issues/617) ([#700](https://www.github.com/moimikey/yargs/issues/700)) ([54cb31d](https://www.github.com/moimikey/yargs/commit/54cb31db8510f6b9dcae0939a6c36c028f454bea))
* **usage:** single char aliases first in help ([#1574](https://www.github.com/moimikey/yargs/issues/1574)) ([a552990](https://www.github.com/moimikey/yargs/commit/a552990c120646c2d85a5c9b628e1ce92a68e797))
* yargs is now passed as the third-argument to fail handler ([#613](https://www.github.com/moimikey/yargs/issues/613)) ([21b74f9](https://www.github.com/moimikey/yargs/commit/21b74f91ca63df2eb885de1f8926f92d702faf51))
* **yargs-parser:** introduce single-digit boolean aliases ([#1576](https://www.github.com/moimikey/yargs/issues/1576)) ([3af7f04](https://www.github.com/moimikey/yargs/commit/3af7f04cdbfcbd4b3f432aca5144d43f21958c39))
* zsh auto completion ([#1292](https://www.github.com/moimikey/yargs/issues/1292)) ([16c5d25](https://www.github.com/moimikey/yargs/commit/16c5d25c00d2cd1c055987837601f7154a7b41b3)), closes [#1156](https://www.github.com/moimikey/yargs/issues/1156)


### Bug Fixes

* __proto__ will now be replaced with ___proto___ in parse ([#1591](https://www.github.com/moimikey/yargs/issues/1591)) ([2474c38](https://www.github.com/moimikey/yargs/commit/2474c3889dcae42ddc031f0ac3872d306bf99e6b))
* --help with default command should print top-level help ([#810](https://www.github.com/moimikey/yargs/issues/810)) ([9c03fa4](https://www.github.com/moimikey/yargs/commit/9c03fa497bd15111fac9d0592f14a89cc7982ddf))
* .argv and .parse() now invoke identical code path ([#1126](https://www.github.com/moimikey/yargs/issues/1126)) ([f13ebf4](https://www.github.com/moimikey/yargs/commit/f13ebf4314225bdd9abb2b117cfb7fec0efaf1a3))
* 'undefined' default value for choices resulted in validation failing ([782b896](https://www.github.com/moimikey/yargs/commit/782b89690ecc22f969f381f8eff7e69413f2cbc5))
* 'undefined' should be taken to mean no argument was provided ([#1015](https://www.github.com/moimikey/yargs/issues/1015)) ([c679e90](https://www.github.com/moimikey/yargs/commit/c679e907d1a19d0858698fdd9fa882d10c4ba5a3))
* [object Object] was accidentally being populated on options object ([#736](https://www.github.com/moimikey/yargs/issues/736)) ([f755e27](https://www.github.com/moimikey/yargs/commit/f755e2756b227555e0f11e58ecfb6bc1a38cbca0))
* $0 contains first arg in bundled electron apps ([#1206](https://www.github.com/moimikey/yargs/issues/1206)) ([567820b](https://www.github.com/moimikey/yargs/commit/567820b4eed518ffc3651ffb206a03e12ba10eff))
* accept single function for middleware ([66fd6f7](https://www.github.com/moimikey/yargs/commit/66fd6f7e9831008eab6742c7782f2e255b838ea7))
* Add `dirname` sanity check on `findUp` ([#1036](https://www.github.com/moimikey/yargs/issues/1036)) ([331d103](https://www.github.com/moimikey/yargs/commit/331d10305af3991bd225fbd7a1060bf43cff22d3))
* add package.json to module exports ([#1818](https://www.github.com/moimikey/yargs/issues/1818)) ([d783a49](https://www.github.com/moimikey/yargs/commit/d783a49a7f21c9bbd4eec2990268f3244c4d5662)), closes [#1817](https://www.github.com/moimikey/yargs/issues/1817)
* add zsh script to files array ([3180224](https://www.github.com/moimikey/yargs/commit/318022499b2d35d1bf4448cd1dbb313fb4c30764))
* address ambiguity between nargs of 1 and requiresArg ([#1572](https://www.github.com/moimikey/yargs/issues/1572)) ([a5edc32](https://www.github.com/moimikey/yargs/commit/a5edc328ecb3f90d1ba09cfe70a0040f68adf50a))
* address bug with handling of arrays of implications ([c240661](https://www.github.com/moimikey/yargs/commit/c240661c27a69fdd2bae401919a9ad31ccd1be01))
* address issues with dutch translation ([#1316](https://www.github.com/moimikey/yargs/issues/1316)) ([0295132](https://www.github.com/moimikey/yargs/commit/02951325c6ea93865b9eeb426828350cc595ed3f))
* address min/max validation message regression ([#750](https://www.github.com/moimikey/yargs/issues/750)) ([2e5ce0f](https://www.github.com/moimikey/yargs/commit/2e5ce0fa711446c99f2ec3c2741e63bb656189a8))
* address positional argument strict() bug introduced in [#766](https://www.github.com/moimikey/yargs/issues/766) ([#784](https://www.github.com/moimikey/yargs/issues/784)) ([a8528e6](https://www.github.com/moimikey/yargs/commit/a8528e6a6cace86b240c6a7e9245e8ca636161b2))
* allows camel-case, variadic arguments, and strict mode to be combined ([#1247](https://www.github.com/moimikey/yargs/issues/1247)) ([eacc035](https://www.github.com/moimikey/yargs/commit/eacc03568e0ecb9fa1f2224e77d2ad2ba38d7960))
* async middleware was called twice ([#1422](https://www.github.com/moimikey/yargs/issues/1422)) ([9a42b63](https://www.github.com/moimikey/yargs/commit/9a42b6380c92a3528a1e47ebf2ed0354e723fea2))
* better bash path completion ([#1272](https://www.github.com/moimikey/yargs/issues/1272)) ([da75ea2](https://www.github.com/moimikey/yargs/commit/da75ea2a5bac2bca8af278688785298054f54bd3))
* calling parse multiple times now appropriately maintains state ([#1137](https://www.github.com/moimikey/yargs/issues/1137)) ([#1369](https://www.github.com/moimikey/yargs/issues/1369)) ([026b151](https://www.github.com/moimikey/yargs/commit/026b1514d47d92f8ea1a3811862013500ff12b57))
* choose correct config directory when require.main does not exist ([#1056](https://www.github.com/moimikey/yargs/issues/1056)) ([a04678c](https://www.github.com/moimikey/yargs/commit/a04678ca0ab9ac7119e6e72b2a657a8a3eaf7818))
* code was not passed to process.exit ([#1742](https://www.github.com/moimikey/yargs/issues/1742)) ([d1a9930](https://www.github.com/moimikey/yargs/commit/d1a993035a2f76c138460052cf19425f9684b637))
* **command:** Run default cmd even if the only cmd ([#950](https://www.github.com/moimikey/yargs/issues/950)) ([7b22203](https://www.github.com/moimikey/yargs/commit/7b22203934966d35ec38020ce6893682dea0dac4))
* commands are now applied in order, from left to right ([#857](https://www.github.com/moimikey/yargs/issues/857)) ([baba863](https://www.github.com/moimikey/yargs/commit/baba863f9889b92e6e8a15d8b321b3392ed3b7be))
* **command:** subcommands via commandDir() now supported for parse(msg, cb) ([#678](https://www.github.com/moimikey/yargs/issues/678)) ([6b85cc6](https://www.github.com/moimikey/yargs/commit/6b85cc61930289bec6c6fcf63f20a973289181ff))
* **completion:** Avoid default command and recommendations during completion ([#1123](https://www.github.com/moimikey/yargs/issues/1123)) ([036e7c5](https://www.github.com/moimikey/yargs/commit/036e7c5dfc6f0bb91a7609aac69d529a5e6cfb9f))
* config and normalise can be disabled with false ([#952](https://www.github.com/moimikey/yargs/issues/952)) ([3bb8771](https://www.github.com/moimikey/yargs/commit/3bb8771876e6c62e7e44b64d62f12a8ede9120ab))
* console.warn() rather than throwing errors when api signatures are incorrect ([#804](https://www.github.com/moimikey/yargs/issues/804)) ([a607061](https://www.github.com/moimikey/yargs/commit/a6070619b85d8d1662afbb26ca45585dae2620ec))
* context should override parsed argv ([#786](https://www.github.com/moimikey/yargs/issues/786)) ([0997288](https://www.github.com/moimikey/yargs/commit/09972884e18e3dd7f29a1267dfa690503c4a40f0))
* context variables are now recognized in strict() mode ([#796](https://www.github.com/moimikey/yargs/issues/796)) ([48575cd](https://www.github.com/moimikey/yargs/commit/48575cd50d53818491d48aeaec84436be51c4085))
* defaulting keys to 'undefined' interfered with conflicting key logic ([a8e0cff](https://www.github.com/moimikey/yargs/commit/a8e0cffbdd36eda0b6f93ca48f0ccfcf6e4af355))
* **deno:** get yargs working on deno@1.5.x ([#1799](https://www.github.com/moimikey/yargs/issues/1799)) ([cb01c98](https://www.github.com/moimikey/yargs/commit/cb01c98c44e30f55c2dc9434caef524ae433d9a4))
* **deno:** update types for deno ^1.4.0 ([#1772](https://www.github.com/moimikey/yargs/issues/1772)) ([0801752](https://www.github.com/moimikey/yargs/commit/080175207d281be63edf90adfe4f0568700b0bf5))
* **dependencies:** upgrade yargs-parser to fix [#1602](https://www.github.com/moimikey/yargs/issues/1602)  ([#1603](https://www.github.com/moimikey/yargs/issues/1603)) ([c67c257](https://www.github.com/moimikey/yargs/commit/c67c257cdf2b79af117cfd1b3938881c8f3e0677))
* **deps:** cliui, find-up, and string-width, all drop Node 6 support ([#1479](https://www.github.com/moimikey/yargs/issues/1479)) ([6a9ebe2](https://www.github.com/moimikey/yargs/commit/6a9ebe2d955e3e979e76c07ffbb1c17fef64cb49))
* **deps:** fix enumeration for normalized path arguments ([#1567](https://www.github.com/moimikey/yargs/issues/1567)) ([0b5b1b0](https://www.github.com/moimikey/yargs/commit/0b5b1b0e5f4f9baf393c48e9cc2bc85c1b67a47a))
* **deps:** Update os-locale to avoid security vulnerability ([#1270](https://www.github.com/moimikey/yargs/issues/1270)) ([27bf739](https://www.github.com/moimikey/yargs/commit/27bf73923423dbe84dd2fd282fdd31d26bdb6cee))
* **deps:** upgrade cliui for compatibility with latest chalk. ([#1330](https://www.github.com/moimikey/yargs/issues/1330)) ([b20db65](https://www.github.com/moimikey/yargs/commit/b20db651cdfe6c8899e11295b43cae694b91e744))
* **deps:** use decamelize from npm instead of vendored copy ([#1377](https://www.github.com/moimikey/yargs/issues/1377)) ([015eeb9](https://www.github.com/moimikey/yargs/commit/015eeb9eec7f89c74140722c9587e334e6596f82))
* **deps:** yargs-parser update addressing several parsing bugs ([#1357](https://www.github.com/moimikey/yargs/issues/1357)) ([e230d5b](https://www.github.com/moimikey/yargs/commit/e230d5bfd947fcc1bc6007cad59973cbd3f49b01))
* detect zsh when zsh isnt run as a login prompt ([#1395](https://www.github.com/moimikey/yargs/issues/1395)) ([8792d13](https://www.github.com/moimikey/yargs/commit/8792d13445458c51bdff6612b1edda5aa344b6a0))
* do not allow additional positionals in strict mode ([35d777c](https://www.github.com/moimikey/yargs/commit/35d777c8db9548763a8f00c95bbd56a9c0f31084))
* do not use cwd when resolving package.json for yargs parsing config ([#726](https://www.github.com/moimikey/yargs/issues/726)) ([9bdaab7](https://www.github.com/moimikey/yargs/commit/9bdaab7ebffbfb70e76fa4067c3cafb4a700ef10))
* **docs:** broken markdown link ([#1426](https://www.github.com/moimikey/yargs/issues/1426)) ([236e24e](https://www.github.com/moimikey/yargs/commit/236e24ef74cb32ff22f3d82a808333ec666d3c22))
* **docs:** describe usage of `.check()` in more detail ([932cd11](https://www.github.com/moimikey/yargs/commit/932cd1177e93f5cc99edfe57a4028e30717bf8fb))
* **docs:** fix incorrect parserConfiguration documentation ([2a99124](https://www.github.com/moimikey/yargs/commit/2a99124d2b388fb32e34886898efc4b624f4e26e))
* **docs:** formalize existing callback argument to showHelp ([#1386](https://www.github.com/moimikey/yargs/issues/1386)) ([d217764](https://www.github.com/moimikey/yargs/commit/d2177645834007a03ecc1a5163b1cd248b3eaf1f))
* **docs:** TypeScript import to prevent a future major release warning ([#1441](https://www.github.com/moimikey/yargs/issues/1441)) ([b1b156a](https://www.github.com/moimikey/yargs/commit/b1b156a3eb4ddd6803fbbd56c611a77919293000))
* **docs:** update boolean description and examples in docs ([#1474](https://www.github.com/moimikey/yargs/issues/1474)) ([afd5b48](https://www.github.com/moimikey/yargs/commit/afd5b4871bfeb90d58351ac56c5c44a83ef033e6))
* **docs:** use recommended cjs import syntax for ts examples ([#1513](https://www.github.com/moimikey/yargs/issues/1513)) ([f9a18bf](https://www.github.com/moimikey/yargs/commit/f9a18bfd624a5013108084f690cd8a1de794c430))
* don't bother calling JSON.stringify() on string default values ([#891](https://www.github.com/moimikey/yargs/issues/891)) ([628be21](https://www.github.com/moimikey/yargs/commit/628be21f4300852fb3f905264b222673fbd160f3))
* don't load config when processing positionals ([5d0dc92](https://www.github.com/moimikey/yargs/commit/5d0dc9249551afa32d699394902e9adc43624c68))
* errors were not bubbling appropriately from sub-commands to top-level ([#802](https://www.github.com/moimikey/yargs/issues/802)) ([8a992f5](https://www.github.com/moimikey/yargs/commit/8a992f535e395e0994afdfebf5c40b5838b5280d))
* **examples:** fix usage-options.js to reflect current API ([#1375](https://www.github.com/moimikey/yargs/issues/1375)) ([6e5b76b](https://www.github.com/moimikey/yargs/commit/6e5b76b3a0c2a0abf9e5b1b7273ffd4427352c2d))
* exclude positional arguments from completion output ([#927](https://www.github.com/moimikey/yargs/issues/927)) ([71c7ec7](https://www.github.com/moimikey/yargs/commit/71c7ec72bc18ff8a449522c3b9b4ee293cf25e49))
* **exports:** node 13.0-13.6 require a string fallback ([#1776](https://www.github.com/moimikey/yargs/issues/1776)) ([b45c43a](https://www.github.com/moimikey/yargs/commit/b45c43a5f64b565c3794f9792150eaeec4e00b69))
* expose helpers for legacy versions of Node.js ([#1801](https://www.github.com/moimikey/yargs/issues/1801)) ([107deaa](https://www.github.com/moimikey/yargs/commit/107deaa4f68b7bc3f2386041e1f4fe0272b29c0a))
* fix demandOption no longer treats 'false' as truthy ([#829](https://www.github.com/moimikey/yargs/issues/829)) ([c748dd2](https://www.github.com/moimikey/yargs/commit/c748dd21ff090db1ce636dae5c5cdf1d867692aa))
* fix promise check to accept any spec conform object ([#1424](https://www.github.com/moimikey/yargs/issues/1424)) ([0be43d2](https://www.github.com/moimikey/yargs/commit/0be43d2e1bfa0a485a13d0bbf4aa02bd4a05d4dd))
* fix tiny spacing issue with usage ([#992](https://www.github.com/moimikey/yargs/issues/992)) ([7871327](https://www.github.com/moimikey/yargs/commit/78713274d5b911bfa8638544a33cd826c792a5b6))
* freeze was not resetting configObjects to initial state; addressed performance issue raised by [@nexdrew](https://www.github.com/nexdrew). ([#670](https://www.github.com/moimikey/yargs/issues/670)) ([ae4bcd4](https://www.github.com/moimikey/yargs/commit/ae4bcd446281674e22dcfcabe7a7b014f32856f8))
* get terminalWidth in non interactive mode no longer causes a validation exception ([#837](https://www.github.com/moimikey/yargs/issues/837)) ([360e301](https://www.github.com/moimikey/yargs/commit/360e3019de266ee04f85e2baf21ce18f8b48cdc1))
* getCompletion() was not working for options ([#1495](https://www.github.com/moimikey/yargs/issues/1495)) ([463feb2](https://www.github.com/moimikey/yargs/commit/463feb2870158eb9df670222b0f0a40a05cf18d0))
* groups were not being maintained for nested commands ([#1430](https://www.github.com/moimikey/yargs/issues/1430)) ([d38650e](https://www.github.com/moimikey/yargs/commit/d38650e45b478ef0104af40281df54b41a50f12f))
* help always displayed for the first command parsed having an async handler ([#1535](https://www.github.com/moimikey/yargs/issues/1535)) ([d585b30](https://www.github.com/moimikey/yargs/commit/d585b303a43746201b05c9c9fda94a444634df33))
* help now takes precedence over command recommendation ([#866](https://www.github.com/moimikey/yargs/issues/866)) ([17e3567](https://www.github.com/moimikey/yargs/commit/17e356700bfacbb88f98ab2006ed5c43bd04c5dc))
* help strings for nested commands were missing parent commands ([#990](https://www.github.com/moimikey/yargs/issues/990)) ([cd1ca15](https://www.github.com/moimikey/yargs/commit/cd1ca1587910b98a0edf7457f9682e8ea998769d))
* hide `hidden` options from help output even if they are in a group ([#1221](https://www.github.com/moimikey/yargs/issues/1221)) ([da54028](https://www.github.com/moimikey/yargs/commit/da54028bbb5cf13739c7fa1eb5d5f00811915696))
* **i18n:** Japanese translation phrasing ([#1619](https://www.github.com/moimikey/yargs/issues/1619)) ([0894175](https://www.github.com/moimikey/yargs/commit/089417550ef5a5b8ce3578dd2a989191300b64cd))
* **i18n:** rename unclear 'implication failed' to 'missing dependent arguments' ([#1317](https://www.github.com/moimikey/yargs/issues/1317)) ([bf46813](https://www.github.com/moimikey/yargs/commit/bf468136724a0903cdc37c3e0788dc7f8131ef03))
* implications fails only displayed once ([#954](https://www.github.com/moimikey/yargs/issues/954)) ([ac8088b](https://www.github.com/moimikey/yargs/commit/ac8088bf70bd27aa10268afb0d63bcf3a4a8016f))
* improve Norwegian Bokmål translations ([#1208](https://www.github.com/moimikey/yargs/issues/1208)) ([a458fa4](https://www.github.com/moimikey/yargs/commit/a458fa42d4cdc80c54072d8838c4bee436c6cb72))
* improve Norwegian Nynorsk translations ([#1207](https://www.github.com/moimikey/yargs/issues/1207)) ([d422eb5](https://www.github.com/moimikey/yargs/commit/d422eb504898ec2f7464952fbed45e810294c9b8))
* less eager help command execution ([#972](https://www.github.com/moimikey/yargs/issues/972)) ([8c1d7bf](https://www.github.com/moimikey/yargs/commit/8c1d7bfd4b907677fa3915c78e09587ab1cbfb72))
* **locales:** change some translations ([#667](https://www.github.com/moimikey/yargs/issues/667)) ([aa966c5](https://www.github.com/moimikey/yargs/commit/aa966c53220a6c8c5f06921f53b4d629e5f1d5bd))
* **locales:** conform hi locale to y18n.__n expectations ([#666](https://www.github.com/moimikey/yargs/issues/666)) ([22adb18](https://www.github.com/moimikey/yargs/commit/22adb188e4baca0701d853497a8b19466ce74d45))
* **locales:** correct some Russian translations ([#691](https://www.github.com/moimikey/yargs/issues/691)) ([a980671](https://www.github.com/moimikey/yargs/commit/a980671ceae7b8895f120026c9eb243d262cc5d0))
* **locales:** only translate default option group name ([acc16de](https://www.github.com/moimikey/yargs/commit/acc16de6b846ea7332db753646a9cec76b589162))
* **locales:** remove extra space in French for 'default' ([#1564](https://www.github.com/moimikey/yargs/issues/1564)) ([ecfc2c4](https://www.github.com/moimikey/yargs/commit/ecfc2c474575c6cdbc6d273c94c13181bd1dbaa6))
* make positionals in -- count towards validation ([#1752](https://www.github.com/moimikey/yargs/issues/1752)) ([eb2b29d](https://www.github.com/moimikey/yargs/commit/eb2b29d34f1a41e0fd6c4e841960e5bfc329dc3c))
* middleware added multiple times due to reference bug ([#1282](https://www.github.com/moimikey/yargs/issues/1282)) ([64af518](https://www.github.com/moimikey/yargs/commit/64af518f3aa91239c56983dc57c674f1ad097f1d))
* middleware should work regardless of when method is called  ([664b265](https://www.github.com/moimikey/yargs/commit/664b265de038b80677fb2912f8840bc3c7fb98c8)), closes [#1178](https://www.github.com/moimikey/yargs/issues/1178)
* misspelling of package.json `engines` field ([0891d0e](https://www.github.com/moimikey/yargs/commit/0891d0ed35b30c83a6d9e9f6a5c5f84d13c546a0))
* **modules:** module path was incorrect ([#1759](https://www.github.com/moimikey/yargs/issues/1759)) ([95a4a0a](https://www.github.com/moimikey/yargs/commit/95a4a0ac573cfe158e6e4bc8c8682ebd1644a198))
* move yargs.cjs to yargs to fix Node 10 imports ([#1747](https://www.github.com/moimikey/yargs/issues/1747)) ([5bfb85b](https://www.github.com/moimikey/yargs/commit/5bfb85b33b85db8a44b5f7a700a8e4dbaf022df0))
* parse array rather than string, so that quotes are safe ([#993](https://www.github.com/moimikey/yargs/issues/993)) ([c351685](https://www.github.com/moimikey/yargs/commit/c3516851f21f0321c44b73048da38546335c7356))
* populate correct value on yargs.parsed and stop warning on access ([#1412](https://www.github.com/moimikey/yargs/issues/1412)) ([bb0eb52](https://www.github.com/moimikey/yargs/commit/bb0eb528ce6ecfd90a9cb1eaf0221fd326b3aeca))
* populate positionals when unknown-options-as-args is set ([#1508](https://www.github.com/moimikey/yargs/issues/1508)) ([bb0f2eb](https://www.github.com/moimikey/yargs/commit/bb0f2eb996fa4e19d330b31a01c2036cafa99a7e)), closes [#1444](https://www.github.com/moimikey/yargs/issues/1444)
* populating placeholder arguments broke validation ([b3eb2fe](https://www.github.com/moimikey/yargs/commit/b3eb2fe5d994b8273f10fe7cbca80d26bc0459a7))
* positional arguments now work if no handler is provided to inner command ([#864](https://www.github.com/moimikey/yargs/issues/864)) ([e28ded3](https://www.github.com/moimikey/yargs/commit/e28ded33339b2a140530280ee5a698eef2bd9369))
* positional arguments of sub-commands threw strict() exception ([#805](https://www.github.com/moimikey/yargs/issues/805)) ([f3f074b](https://www.github.com/moimikey/yargs/commit/f3f074bd983e9b2dea6df94e21febfeef27b6de4))
* **positional:** positional strings no longer drop decimals ([#1761](https://www.github.com/moimikey/yargs/issues/1761)) ([e1a300f](https://www.github.com/moimikey/yargs/commit/e1a300f1293ad821c900284616337f080b207980))
* prefer user supplied script name in usage ([#1383](https://www.github.com/moimikey/yargs/issues/1383)) ([28c74b9](https://www.github.com/moimikey/yargs/commit/28c74b9e584d30cf6a6c6c31dad967fd81fc5077))
* properties accessed on singleton now reflect current state of instance ([#1366](https://www.github.com/moimikey/yargs/issues/1366)) ([409d35b](https://www.github.com/moimikey/yargs/commit/409d35bfb10928b34b2a6b29492878d42c4825df))
* pull in yargs-parser with modified env precedence ([#787](https://www.github.com/moimikey/yargs/issues/787)) ([e0fbbe5](https://www.github.com/moimikey/yargs/commit/e0fbbe58281f6cd722d49fcf6c61f5176a35dd2b))
* remove the trailing white spaces from the help output ([#1090](https://www.github.com/moimikey/yargs/issues/1090)) ([3f0746c](https://www.github.com/moimikey/yargs/commit/3f0746c0e212d2049e3c1d6633a824382d2ec165))
* requiresArg should only be enforced if argument exists ([#1043](https://www.github.com/moimikey/yargs/issues/1043)) ([fbf41ae](https://www.github.com/moimikey/yargs/commit/fbf41ae672ea967f80c2f8ec8efd4317e4d70a1d))
* running parse() multiple times on the same yargs instance caused exception if help() enabled ([#790](https://www.github.com/moimikey/yargs/issues/790)) ([07e39b7](https://www.github.com/moimikey/yargs/commit/07e39b79dbaf64cb03d05ea23e0741b3b80b1fcb))
* Set implicit nargs=1 when type=number requiresArg=true ([#1050](https://www.github.com/moimikey/yargs/issues/1050)) ([2b56812](https://www.github.com/moimikey/yargs/commit/2b5681233a0d9406e362ce2ddd434a47117755db))
* show 2 dashes on help for single digit option key or alias ([#1493](https://www.github.com/moimikey/yargs/issues/1493)) ([63b3dd3](https://www.github.com/moimikey/yargs/commit/63b3dd31a455d428902220c1992ae930e18aff5c))
* showCompletionScript was logging script twice ([#1388](https://www.github.com/moimikey/yargs/issues/1388)) ([07c8537](https://www.github.com/moimikey/yargs/commit/07c8537aa727d3c9b026523ee255758d76939cb3))
* still freeze/unfreeze if parse() is called in isolation ([#717](https://www.github.com/moimikey/yargs/issues/717)) ([30a9492](https://www.github.com/moimikey/yargs/commit/30a94921d6a551a05f4dfa82d1ddc722f3028957))
* stop applying parser to context object ([#675](https://www.github.com/moimikey/yargs/issues/675)) ([3fe9b8f](https://www.github.com/moimikey/yargs/commit/3fe9b8fdbd53da8841cc001cffe7f7794100031a))
* stop-parse was not being respected by commands ([#1459](https://www.github.com/moimikey/yargs/issues/1459)) ([12c82e6](https://www.github.com/moimikey/yargs/commit/12c82e62663e928148a7ee2f51629aa26a0f9bb2))
* strict mode should not fail for hidden options ([#949](https://www.github.com/moimikey/yargs/issues/949)) ([0e0c58d](https://www.github.com/moimikey/yargs/commit/0e0c58dd737f856ee4b3d595ddfb835247db9503))
* **strict mode:** report default command unknown arguments ([#1626](https://www.github.com/moimikey/yargs/issues/1626)) ([69f29a9](https://www.github.com/moimikey/yargs/commit/69f29a9cd429d4bb99481238305390107ac75b02))
* strict() should not ignore hyphenated arguments ([#1414](https://www.github.com/moimikey/yargs/issues/1414)) ([b774b5e](https://www.github.com/moimikey/yargs/commit/b774b5e4834735f7b730a27c4b7bf6e7544ee224))
* support merging deeply nested configuration ([#1423](https://www.github.com/moimikey/yargs/issues/1423)) ([bae66fe](https://www.github.com/moimikey/yargs/commit/bae66feee45cb59241facc978c8fdd2bb4d4c751))
* support options/sub-commands in zsh completion ([0a96394](https://www.github.com/moimikey/yargs/commit/0a96394f3b3125332eeaaa6c7a5beeffb3c3a27f))
* temporary fix for libraries that call Object.freeze() ([#1483](https://www.github.com/moimikey/yargs/issues/1483)) ([99c2dc8](https://www.github.com/moimikey/yargs/commit/99c2dc850e67c606644f8b0c0bca1a59c87dcbcd))
* the positional argument parse was clobbering global flag arguments ([#984](https://www.github.com/moimikey/yargs/issues/984)) ([7e58453](https://www.github.com/moimikey/yargs/commit/7e58453e6a46c59d3f51c0c3ccc933ca68089b4a))
* tolerate null prototype for config objects with `extends` ([#1376](https://www.github.com/moimikey/yargs/issues/1376)) ([3d26d11](https://www.github.com/moimikey/yargs/commit/3d26d114148118763b37886da32ee2ee2af2d8dc)), closes [#1372](https://www.github.com/moimikey/yargs/issues/1372)
* translation not working when using __ with a single parameter ([#1183](https://www.github.com/moimikey/yargs/issues/1183)) ([f449aea](https://www.github.com/moimikey/yargs/commit/f449aead59f44f826cbcf570cf849c4a59c79c81))
* **translations:** add French translation for unknown command ([#1563](https://www.github.com/moimikey/yargs/issues/1563)) ([18b0b75](https://www.github.com/moimikey/yargs/commit/18b0b752424bf560271e670ff95a0f90c8386787))
* **translations:** fix pluralization in error messages. ([#1557](https://www.github.com/moimikey/yargs/issues/1557)) ([94fa38c](https://www.github.com/moimikey/yargs/commit/94fa38cbab8d86943e87bf41d368ed56dffa6835))
* **typescript:** yargs-parser was breaking @types/yargs ([#1745](https://www.github.com/moimikey/yargs/issues/1745)) ([2253284](https://www.github.com/moimikey/yargs/commit/2253284b233cceabd8db677b81c5bf1755eef230))
* update to yargs-parser with fix for array default values ([#1463](https://www.github.com/moimikey/yargs/issues/1463)) ([ebee59d](https://www.github.com/moimikey/yargs/commit/ebee59d9022da538410e69a5c025019ed46d13d2))
* upgrade os-locale to version that addresses license issue ([#1195](https://www.github.com/moimikey/yargs/issues/1195)) ([efc0970](https://www.github.com/moimikey/yargs/commit/efc0970bc8f91359905882b6990ffc0786193068))
* **usage:** translate 'options' group only when displaying help ([#1600](https://www.github.com/moimikey/yargs/issues/1600)) ([e60b39b](https://www.github.com/moimikey/yargs/commit/e60b39b9d3a912c06db43f87c86ba894142b6c1c))
* use correct completion command in generated completion script ([#988](https://www.github.com/moimikey/yargs/issues/988)) ([3c8ac1d](https://www.github.com/moimikey/yargs/commit/3c8ac1ddd79cc7adc2fc0214318c7b23d98f613c))
* use path.resolve() to support node 0.10 ([#797](https://www.github.com/moimikey/yargs/issues/797)) ([49a93fc](https://www.github.com/moimikey/yargs/commit/49a93fc392e952b83adda37465d90e7d2321d05e))
* **validation:** Use the error as a message when none exists otherwise ([#1268](https://www.github.com/moimikey/yargs/issues/1268)) ([0510fe6](https://www.github.com/moimikey/yargs/commit/0510fe6a617fc8af77aa205e44feaa5226e9643c))
* we shouldn't output help if we've printed a prior help-like message ([#847](https://www.github.com/moimikey/yargs/issues/847)) ([17e89bd](https://www.github.com/moimikey/yargs/commit/17e89bdd0a59455d1c34d028f1cf6a9e591f71cf))
* **yargs:** add missing command(module) signature ([#1707](https://www.github.com/moimikey/yargs/issues/1707)) ([0f81024](https://www.github.com/moimikey/yargs/commit/0f810245494ccf13a35b7786d021b30fc95ecad5)), closes [#1704](https://www.github.com/moimikey/yargs/issues/1704)
* **yargs:** correct support of bundled electron apps ([#1554](https://www.github.com/moimikey/yargs/issues/1554)) ([a0b61ac](https://www.github.com/moimikey/yargs/commit/a0b61ac21e2b554aa73dbf1a66d4a7af94047c2f))


### Performance Improvements

* normalizing package data is an expensive operation ([#705](https://www.github.com/moimikey/yargs/issues/705)) ([49cf533](https://www.github.com/moimikey/yargs/commit/49cf53390290c79c573fee45eb5557756f75629d))


### Miscellaneous Chores

* drop Node 6 from testing matrix ([#1287](https://www.github.com/moimikey/yargs/issues/1287)) ([ef16792](https://www.github.com/moimikey/yargs/commit/ef167921e9f8d03e4bd08604480e1458cbf861e9))
* drop Node 6 support ([#1461](https://www.github.com/moimikey/yargs/issues/1461)) ([2ba8ce0](https://www.github.com/moimikey/yargs/commit/2ba8ce05e8fefbeffc6cb7488d9ebf6e86cceb1d))
* test Node.js 6, 8 and 10 ([#1160](https://www.github.com/moimikey/yargs/issues/1160)) ([84f9d2b](https://www.github.com/moimikey/yargs/commit/84f9d2b07b48b675277f6500551dacaf69379a4c))
* update dependencies ([#1284](https://www.github.com/moimikey/yargs/issues/1284)) ([f25de4f](https://www.github.com/moimikey/yargs/commit/f25de4fc8b4ad4bfd48080439492e6af50596940))
* upgrade to version of yargs-parser that does not populate value for unset boolean ([#1104](https://www.github.com/moimikey/yargs/issues/1104)) ([d4705f4](https://www.github.com/moimikey/yargs/commit/d4705f474e0243271b307ea880e8c4e4866218eb))
* upgrade yargs-parser ([#867](https://www.github.com/moimikey/yargs/issues/867)) ([8f9c6c6](https://www.github.com/moimikey/yargs/commit/8f9c6c6954b51f6e22d772ba2c7dfbbac5cb504b))


### Code Refactoring

* remove package.json-based parserConfiguration ([#1460](https://www.github.com/moimikey/yargs/issues/1460)) ([0d3642b](https://www.github.com/moimikey/yargs/commit/0d3642b6f829b637938774c0c6ce5f6bfe1afa51))
* **ts:** ship yargs.d.ts ([#1671](https://www.github.com/moimikey/yargs/issues/1671)) ([c06f886](https://www.github.com/moimikey/yargs/commit/c06f886142ad02233db2b2ba82f2e606cbf57ccd))

## [16.2.0](https://www.github.com/yargs/yargs/compare/v16.1.1...v16.2.0) (2020-12-05)


### Features

* command() now accepts an array of modules ([f415388](https://www.github.com/yargs/yargs/commit/f415388cc454d02786c65c50dd6c7a0cf9d8b842))


### Bug Fixes

* add package.json to module exports ([#1818](https://www.github.com/yargs/yargs/issues/1818)) ([d783a49](https://www.github.com/yargs/yargs/commit/d783a49a7f21c9bbd4eec2990268f3244c4d5662)), closes [#1817](https://www.github.com/yargs/yargs/issues/1817)

### [16.1.1](https://www.github.com/yargs/yargs/compare/v16.1.0...v16.1.1) (2020-11-15)


### Bug Fixes

* expose helpers for legacy versions of Node.js ([#1801](https://www.github.com/yargs/yargs/issues/1801)) ([107deaa](https://www.github.com/yargs/yargs/commit/107deaa4f68b7bc3f2386041e1f4fe0272b29c0a))
* **deno:** get yargs working on deno@1.5.x ([#1799](https://www.github.com/yargs/yargs/issues/1799)) ([cb01c98](https://www.github.com/yargs/yargs/commit/cb01c98c44e30f55c2dc9434caef524ae433d9a4))

## [16.1.0](https://www.github.com/yargs/yargs/compare/v16.0.3...v16.1.0) (2020-10-15)


### Features

* expose hideBin helper for CJS ([#1768](https://www.github.com/yargs/yargs/issues/1768)) ([63e1173](https://www.github.com/yargs/yargs/commit/63e1173bb47dc651c151973a16ef659082a9ae66))


### Bug Fixes

* **deno:** update types for deno ^1.4.0 ([#1772](https://www.github.com/yargs/yargs/issues/1772)) ([0801752](https://www.github.com/yargs/yargs/commit/080175207d281be63edf90adfe4f0568700b0bf5))
* **exports:** node 13.0-13.6 require a string fallback ([#1776](https://www.github.com/yargs/yargs/issues/1776)) ([b45c43a](https://www.github.com/yargs/yargs/commit/b45c43a5f64b565c3794f9792150eaeec4e00b69))
* **modules:** module path was incorrect ([#1759](https://www.github.com/yargs/yargs/issues/1759)) ([95a4a0a](https://www.github.com/yargs/yargs/commit/95a4a0ac573cfe158e6e4bc8c8682ebd1644a198))
* **positional:** positional strings no longer drop decimals ([#1761](https://www.github.com/yargs/yargs/issues/1761)) ([e1a300f](https://www.github.com/yargs/yargs/commit/e1a300f1293ad821c900284616337f080b207980))
* make positionals in -- count towards validation ([#1752](https://www.github.com/yargs/yargs/issues/1752)) ([eb2b29d](https://www.github.com/yargs/yargs/commit/eb2b29d34f1a41e0fd6c4e841960e5bfc329dc3c))

### [16.0.3](https://www.github.com/yargs/yargs/compare/v16.0.2...v16.0.3) (2020-09-10)


### Bug Fixes

* move yargs.cjs to yargs to fix Node 10 imports ([#1747](https://www.github.com/yargs/yargs/issues/1747)) ([5bfb85b](https://www.github.com/yargs/yargs/commit/5bfb85b33b85db8a44b5f7a700a8e4dbaf022df0))

### [16.0.2](https://www.github.com/yargs/yargs/compare/v16.0.1...v16.0.2) (2020-09-09)


### Bug Fixes

* **typescript:** yargs-parser was breaking @types/yargs ([#1745](https://www.github.com/yargs/yargs/issues/1745)) ([2253284](https://www.github.com/yargs/yargs/commit/2253284b233cceabd8db677b81c5bf1755eef230))

### [16.0.1](https://www.github.com/yargs/yargs/compare/v16.0.0...v16.0.1) (2020-09-09)


### Bug Fixes

* code was not passed to process.exit ([#1742](https://www.github.com/yargs/yargs/issues/1742)) ([d1a9930](https://www.github.com/yargs/yargs/commit/d1a993035a2f76c138460052cf19425f9684b637))

## [16.0.0](https://www.github.com/yargs/yargs/compare/v15.4.2...v16.0.0) (2020-09-09)


### ⚠ BREAKING CHANGES

* tweaks to ESM/Deno API surface: now exports yargs function by default; getProcessArgvWithoutBin becomes hideBin; types now exported for Deno.
* find-up replaced with escalade; export map added (limits importable files in Node >= 12); yarser-parser@19.x.x (new decamelize/camelcase implementation).
* **usage:** single character aliases are now shown first in help output
* rebase helper is no longer provided on yargs instance.
* drop support for EOL Node 8 (#1686)

### Features

* adds strictOptions() ([#1738](https://www.github.com/yargs/yargs/issues/1738)) ([b215fba](https://www.github.com/yargs/yargs/commit/b215fba0ed6e124e5aad6cf22c8d5875661c63a3))
* **helpers:** rebase, Parser, applyExtends now blessed helpers ([#1733](https://www.github.com/yargs/yargs/issues/1733)) ([c7debe8](https://www.github.com/yargs/yargs/commit/c7debe8eb1e5bc6ea20b5ed68026c56e5ebec9e1))
* adds support for ESM and Deno ([#1708](https://www.github.com/yargs/yargs/issues/1708)) ([ac6d5d1](https://www.github.com/yargs/yargs/commit/ac6d5d105a75711fe703f6a39dad5181b383d6c6))
* drop support for EOL Node 8 ([#1686](https://www.github.com/yargs/yargs/issues/1686)) ([863937f](https://www.github.com/yargs/yargs/commit/863937f23c3102f804cdea78ee3097e28c7c289f))
* i18n for ESM and Deno ([#1735](https://www.github.com/yargs/yargs/issues/1735)) ([c71783a](https://www.github.com/yargs/yargs/commit/c71783a5a898a0c0e92ac501c939a3ec411ac0c1))
* tweaks to API surface based on user feedback ([#1726](https://www.github.com/yargs/yargs/issues/1726)) ([4151fee](https://www.github.com/yargs/yargs/commit/4151fee4c33a97d26bc40de7e623e5b0eb87e9bb))
* **usage:** single char aliases first in help ([#1574](https://www.github.com/yargs/yargs/issues/1574)) ([a552990](https://www.github.com/yargs/yargs/commit/a552990c120646c2d85a5c9b628e1ce92a68e797))


### Bug Fixes

* **yargs:** add missing command(module) signature ([#1707](https://www.github.com/yargs/yargs/issues/1707)) ([0f81024](https://www.github.com/yargs/yargs/commit/0f810245494ccf13a35b7786d021b30fc95ecad5)), closes [#1704](https://www.github.com/yargs/yargs/issues/1704)

[Older CHANGELOG Entries](https://github.com/yargs/yargs/blob/master/docs/CHANGELOG-historical.md)

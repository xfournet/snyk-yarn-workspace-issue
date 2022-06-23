# Pre requisite
* yarn installed
* execute `yarn install`

# Tests
## Test with --all-projects
`yarn dlx snyk test --all-projects`

❌ Complains about missing `my-wks\node_modules` folder

```
✗ 1/2 potential projects failed to get dependencies.
D:\sources\github\snyk-yarn-workspace-issue\my-wks\package.json:
  Missing node_modules folder: we can't test without dependencies.
Please run 'npm install' first.

Testing D:\sources\github\snyk-yarn-workspace-issue...

Organization:      xfournet
Package manager:   yarn
Target file:       package.json
Project name:      root
Open source:       no
Project path:      D:\sources\github\snyk-yarn-workspace-issue
Licenses:          enabled

✔ Tested D:\sources\github\snyk-yarn-workspace-issue for known issues, no vulnerable paths found.
```

✅ If `my-wks/node_modules` empty directory is manually created, then it works as expected

```
Testing D:\sources\github\snyk-yarn-workspace-issue...

Organization:      xfournet
Package manager:   yarn
Target file:       package.json
Project name:      root
Open source:       no
Project path:      D:\sources\github\snyk-yarn-workspace-issue
Licenses:          enabled

✔ Tested D:\sources\github\snyk-yarn-workspace-issue for known issues, no vulnerable paths found.

Next steps:
- Run `snyk monitor` to be notified about new related vulnerabilities.
- Run `snyk test` as part of your CI/test.

-------------------------------------------------------

Testing D:\sources\github\snyk-yarn-workspace-issue...

Organization:      xfournet
Package manager:   npm
Target file:       my-wks\package.json
Project name:      my-wks
Open source:       no
Project path:      D:\sources\github\snyk-yarn-workspace-issue
Licenses:          enabled

✔ Tested 1 dependencies for known issues, no vulnerable paths found.

Next steps:
- Run `snyk monitor` to be notified about new related vulnerabilities.
- Run `snyk test` as part of your CI/test.


Tested 2 projects, no vulnerable paths were found.
```

## Test with --all-projects + --strict-out-of-sync=false 
`yarn dlx snyk test --all-projects --strict-out-of-sync=false`

❌ Complains about `trim@0.0.1` dependency while this is not the dependency that is installed (`trim@1.0.1`)

```
Testing D:\sources\github\snyk-yarn-workspace-issue...

Organization:      xfournet
Package manager:   yarn
Target file:       package.json
Project name:      root
Open source:       no
Project path:      D:\sources\github\snyk-yarn-workspace-issue
Licenses:          enabled

✔ Tested D:\sources\github\snyk-yarn-workspace-issue for known issues, no vulnerable paths found.

Next steps:
- Run `snyk monitor` to be notified about new related vulnerabilities.
- Run `snyk test` as part of your CI/test.

-------------------------------------------------------

Testing D:\sources\github\snyk-yarn-workspace-issue...

Tested 2 dependencies for known issues, found 1 issue, 1 vulnerable path.


Issues with no direct upgrade or patch:
  ✗ Regular Expression Denial of Service (ReDoS) [High Severity][https://snyk.io/vuln/SNYK-JS-TRIM-1017038] in trim@0.0.1
    introduced by window-classlist@0.0.4 > trim@0.0.1
  This issue was fixed in versions: 0.0.3



Organization:      xfournet
Package manager:   yarn
Target file:       my-wks\package.json
Project name:      my-wks
Open source:       no
Project path:      D:\sources\github\snyk-yarn-workspace-issue
Licenses:          enabled


Tested 2 projects, 1 contained vulnerable paths.
```

❌ Creating `my-wks/node_modules` directory doesn't change the result

## Test with --yarn-workspaces
`yarn dlx snyk test --yarn-workspaces`

❌ Complains about out of sync lock file

`Dependency trim@0.0.1 was not found in yarn.lock. Your package.json and yarn.lock are probably out of sync. Please run "yarn install" and try again.`

❌ Creating `my-wks/node_modules` directory doesn't change the result

## Test with --yarn-workspaces + --strict-out-of-sync=false
`yarn dlx snyk test --yarn-workspaces --strict-out-of-sync=false`

❌ Complains about `trim@0.0.1` dependency while this is not the dependency that is installed (`trim@1.0.1`)

```
Testing D:\sources\github\snyk-yarn-workspace-issue...

Organization:      xfournet
Package manager:   yarn
Target file:       package.json
Project name:      root
Open source:       no
Project path:      D:\sources\github\snyk-yarn-workspace-issue
Licenses:          enabled

✔ Tested D:\sources\github\snyk-yarn-workspace-issue for known issues, no vulnerable paths found.

Next steps:
- Run `snyk monitor` to be notified about new related vulnerabilities.
- Run `snyk test` as part of your CI/test.

-------------------------------------------------------

Testing D:\sources\github\snyk-yarn-workspace-issue...

Tested 2 dependencies for known issues, found 1 issue, 1 vulnerable path.


Issues with no direct upgrade or patch:
  ✗ Regular Expression Denial of Service (ReDoS) [High Severity][https://snyk.io/vuln/SNYK-JS-TRIM-1017038] in trim@0.0.1
    introduced by window-classlist@0.0.4 > trim@0.0.1
  This issue was fixed in versions: 0.0.3



Organization:      xfournet
Package manager:   yarn
Target file:       my-wks\package.json
Project name:      my-wks
Open source:       no
Project path:      D:\sources\github\snyk-yarn-workspace-issue
Licenses:          enabled


Tested 2 projects, 1 contained vulnerable paths.
```

❌ Creating `my-wks/node_modules` directory doesn't change the result

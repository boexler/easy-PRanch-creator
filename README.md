# easy-branch-creator
Use Easy Branch Creator in Azure DevOps to create branches directly from within workitems using fields from the workitem for the branch name.

## Overview
When you want to create a new branch, it is often good to have a branch naming convention in place. With the convention in place, branches are more structure and it's easier to find the correct branch. You can group branches also in subfolders based on a category like *feature* or *bugfix*.  
In Azure DevOps you often create a branch on the basis of a workitem and then use some information from the workitem for the name of the branch. To be able to do so, you often need to copy several fields of the workitem to construct the actual branch name.  

### Create branch
The `easy-branch-creator` is an extension for Azure DevOps that eases this process. `easy-branch-creator` adds a menu action on a workitem to automatically create a branch using fields from the given workitem.  
When clicking the actions, `easy-branch-creator` will create a new branch, using the configured naming convention, based on the default branch.

![Create Branch Screen Shot][create-branch-action]

### Settings
`easy-branch-creator` can be configured in several ways. The settings can be found in `Project Settings` under the `Extensions` section. 
- Template Branch Name
  - This is the template being used to create the branch name. The template can use **any** field from a workitem. Validation is in place to ensure a valid template is entered.
- Non-alphanumeric characters replacement
  - Any non-alphanumeric character in a workitem field will be replaced by this character.
- Lowercase branch name
  - When checked, the entire branch name will be lowercased.
- Update workitem state
  - If enabled for a workitem type, when creating a new branch, the workitem is also updated to the selected state.

![Settings][settings]

## Extension permissions

When you install the extension from the Visual Studio Marketplace, Azure DevOps lists **permission scopes** and may show a warning about “high privilege scopes.” That text is standard for extensions that declare OAuth scopes of this level. It does not mean the extension performs hidden operations; it reflects what the declared APIs are allowed to do if the extension code calls them.

The extension manifest declares two scopes (see `vss-extension.json`):

| Scope             | Shown in Marketplace (typical)           | Why it is required |
|-------------------|------------------------------------------|----------------------|
| `vso.work_write`  | Work items (read and write)              | Read work item fields for branch/PR name templates; add relations linking branches and pull requests to work items; optionally update work item state when configured. |
| `vso.code_manage` | Code (read, write, and manage)           | List repositories and branches, read refs, create new branches (Git ref updates), create pull requests, and optionally read `.azuredevops/pull_request_template.md` from the repo. |

Azure Repos extensions that **create branches or pull requests via the REST API** generally need `vso.code_manage`. Finer-grained manifest scopes do not usually allow “only create a branch/PR” without the broader code scope; the Marketplace label “read, write, and manage” is how that scope is summarized for administrators.

**Trust:** Only install this extension if your organization trusts the publisher and the code in this repository—the granted tokens could perform any operation those scopes allow, so the install screen reminds you to verify the source.

[create-branch-action]: marketplace/create-branch-action.png
[settings]: marketplace/settings.png

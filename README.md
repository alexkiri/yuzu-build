# yuzu-build
Merge yuzu's 'early-access-merge' and 'mainline-merge' pr to master branch.

The build process is completely transparent, with source code from the official yuzu repo.

Download build from ['Action'](https://github.com/alexkiri/yuzu-build/actions) tab, in the "Artifacts" section of a finished action, or from the ['Releases'](https://github.com/alexkiri/yuzu-build/releases) section

# Additional functionality
The workflow includes logic that can:
- build either `yuzu-ea` or `yuzu-mainline`
- include any custom PR in the build, even it doesn't have the `early-access-merge` label. This is done by specifying a comma separated list of PR IDs in the workflow input. Closed PRs will can also be included. Use this with caution, as it might cause merge conflicts, build errors, or other unwanted consequences. Can be left empty, and it only works for `yuzu-ea` build type
- make the build enable / disable various cmake flags. You can find some description for each flag in the [CMakeLists.txt](https://github.com/yuzu-emu/yuzu/blob/master/CMakeLists.txt) file
- apply custom optimization flag for any selectable CPU extension. This is experimental, and it probably has little to not effect
- apply custom fixes in the form of `.patch` files. There are now 2 folders, 
`optionalPatches` and `defaultPatches`. The optional ones are applied based on the input flags of the workflow, the default ones are applied regardless. In this way, you can include your own patch file(s) in the `defaultPatches` folder, and they will be applied automatically without any changes to the workflow

## Tips
- This workflow will release build files with 'release' tag. If you want to release files,please go to repo's setting → Action → General → Workflow permissions, choose 'Read and write permissions' and click 'save'. If you don't want to do this, just ignore the error about release failed.

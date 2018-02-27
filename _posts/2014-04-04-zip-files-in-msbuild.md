---
layout: post
title: Zipping files in MSBuild using Community Tasks
categories: build
description: How to use MSBuild Community Tasks to create a Zip file containing outputs from a build
---

We use this for packaging up PDB files for each release.

~~~ xml
  <UsingTask AssemblyName="MSBuild.Community.Tasks" TaskName="MSBuild.Community.Tasks.Zip" />
  <Target Name="ZipPDBs">
    <Message Text="Zipping PDB files in $(BasePath)" />
    <CreateItem Include="$(BasePath)\*.pdb" >
        <Output ItemName="PDBFiles" TaskParameters="Include" />
    </CreateItem>
    <MSBuildCommunity.Tasks.Zip ZipFileName="$(BasePath)\pdbs-$(VersionNumber).zip" WorkingDirectory="$(BasePath)" Files="@PDBFiles" />
  </Target>
~~~

$(BasePath) and $(VersionNumber) need to be defined elsewhere.

MSBuild.Community.Tasks.dll needs to be accessible.


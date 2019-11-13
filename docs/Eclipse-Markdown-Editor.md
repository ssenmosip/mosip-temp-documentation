# Eclipse Markdown Editor

### Markdown editor plugin for eclipse 

Search and Install **“ Markdown Text Editor “**  form Eclipse Marketplace.


![Eclimh](_images/ecl_markdown/0_ecl_plugin_markdown_editor.PNG)
 
 

[**Web Link**](//marketplace.eclipse.org/content/markdown-text-editor)


### GitHub Flavored Markdown viewer plugin

Search and Install **“ GitHub Flavored Markdown “** form Eclipse Marketplace.


 ![](_images/ecl_markdown/0_gfm_viewr_plugin.PNG)


[**Web Link**](//marketplace.eclipse.org/content/github-flavored-markdown-viewer-plugin)




# MOSIP WIKI Local Setup

**MOSIP wiki will have architecture, API specs and developer documentation only. To access the Low level design documents, follow the steps mentioned in the [**link**](/mosip/mosip-platform/wiki/MOSIP-Platform-Detailed-Design)**


**Step1:** Access MOSIP wiki at [**link**](/mosip/mosip-docs/wiki)


**Step2:** Copy repository URL and Git clone the `https://github.com/mosip/mosip-docs.wiki.git`


![](_images/ecl_markdown/1_mosip_wiki.PNG)
 

**Step3:** Import it in Eclipse From File -> Open Projects form File System.. 
 

![](_images/ecl_markdown/2_wiki_imort_eclipse.PNG)



![](_images/ecl_markdown/3_mosip_wiki_content.PNG)



**Start4:** Edit ****.md file (Markdown Source tab) and Preview your changes (Preview tab)


 ![](_images/ecl_markdown/4_markdown_source_view.PNG)



 ![](_images/ecl_markdown/5.0_markdown_preview.PNG)
 

**Step5:** If you are using GitHub Flavored Markdown Syntax, Right-click .md file then select ''Show in GFM view".
Remember to delete generated “.xxx.md.html” preview file after using this option. 



 ![](_images/ecl_markdown/5.1_markdown_preview.PNG)



**Start6:** Commit and Push back to GitHub.


**NOTE:** 

- Create SubFolder/Add Images inside “_images/SubFolderName/”


- Add MDs files prefixed with SectionNumber.SubSectionNumber

![](_images/ecl_markdown/6_section-subsection.PNG)







# Editing Code Repository MD Files (Repository for low level design for sequence diagrams and class diagrams)

**NOTE:** 

- Each module has own README.md files for installation, runtime environment and setup instructions.

- Each module has own UML design MD files inside “design/module” folder and respective diagrams inside “design/module/_images” 

 

![](_images/ecl_markdown/7_mosip_code_repo_design.PNG)
  


![](_images/ecl_markdown/8_module_design.PNG)




**Refer to this [**link**](//guides.github.com/features/mastering-markdown) for Markdown Syntax guide**


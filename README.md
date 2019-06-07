## Vue-Salesforce Widget Scaffold

### 1. Introduction
- This is a repository to show how vue.js framework used to build a salesforce widget. By using lighting container, we can embed the static resource (assets that developed in vue) to the Lightning component. 
- The `todo_widget` directory is a sample of how vue.js can be use to develop the widget. 
- You can create a new project by using this scaffold project (details in section 4.)

### 2. Prerequisite
- You have installed `sfdx` to pull the metadata from your Salesforce org
- You have installed `node.js, npm or yarn & vue cli`

### 3. Description of Files and Directories
- The files and directories inside `vue_salesforce_widget` is a common project generated by SFDX `sfdx force:project:create`
- The `vue-sf-projects` is an additional directory to ease the widget development.

### 4. You Can Create New Vue-Sf Widget Project!
- Go to the `vue-sf-projects` directory by:
  ```
  cd vue-sf-projects
  ```
- Create your new project by typing this command:
  ```
  vue create new_widget_component_name
  ```
- Create a lightining component to host your vue project
  ```
  sfdx force:lightning:component:create -n new_widget_name
  ```
- After your vue project is done, you should build and then upload the assets to static resource (Please refer to Deploy The Widget Section) 
- In `new_widget_name.cmp` file, add the lightning container element as below:
  ```
  <aura:component access="global" implements="flexipage:availableForAllPageTypes" >
    <lightning:container src="{!$Resource.new_widget_name + '/index.html'}"/>
  </aura:component>
  ```
- Add the new widget to your Salesfroce Page and you're done, yeay!

### 5. Deploy The Widget
- Build your vue project by typing (make sure you are in the `your-new-widget-project-name` directory)
  ```
  npm run build
  ```
- After the build stage is success, Copy the dist directory to `force-app/main/default/staticresources` directory
- Change the `dist` folder name to `your-new-widget-project-name`
- Create new xml metadata for your new static resource named it as `your-new-widget-project-name.resource-meta.xml`
- Add this config in the xml file:
```
<?xml version="1.0" encoding="UTF-8"?>
<StaticResource xmlns="http://soap.sforce.com/2006/04/metadata">
    <cacheControl>Public</cacheControl>
    <contentType>application/x-zip-compressed</contentType>
    <description>Sample Apps created using vue.js technology, embedded in the lighting component.</description>
</StaticResource>
```
- Push your change to your SF Environment
`sfdx force:source:deploy -x manifest/package.xml`

### 6. Resources
- **[Lightning Container Guidance](https://developer.salesforce.com/docs/atlas.en-us.lightning.meta/lightning/container_overview.htm)**
- **[Salesforce Lightning application with Vue.js and Webpack](https://medium.com/@ennoucas/salesforce-lightning-application-with-vue-js-and-webpack-part-2-af0071347274)**
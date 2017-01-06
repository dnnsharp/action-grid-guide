# **Sync with URL **

The **Sync URL **option is available under General Settings and comes enabled by default. Basically, it synchronize with URL, without a page load, all changes for the current capabilities, namely: sort, pagination, search and filter. It is useful for navigating back using browser button, bookmarking, sharing and integrating with other modules. 

The new URL will be similar with the following: http://domain.com/ActionGridPage?pageModuleId=Value&sizeModuleId=Value&searchModuleId=Value&sortModuleId=Value&sortdirModuleId=asc&filterModuleID-GridField=Value. Copy pasting the URL in other browsers/tabs should open the grid with exact same data.

### **Update Datasource without postback**

The Action Grid supports the possibility to update its Datasource without postback, using JavaScript from any other Module \(eg: HTML Module\). This feature uses the HTML5 push state mechanism.   


The most common scenario can be achieved making the following steps:   
  
 - Add a HTML Module which contains a similar Source: 

`<ul>`

` <li><a href="#" onclick="window.history.pushState('{ }','','?id=1');">Analyst</a></li>`

` <li><a href="#" onclick="window.history.pushState('{ }','','?id=2');">Sales Rep</a></li>`

` <li><a href="#" onclick="window.history.pushState('{ }','','?id=3');">Manager</a></li>`

` <li><a href="#" onclick="window.history.pushState('{ }','','?id=4');">Designer</a></li>`

`</ul>`  
  
- Use the \[Get:id\] token to filter the Grid's Datasource by adding it in a where condition from the SQL Query for retrieving Items, like: `Select * from Table5 where id='[Get:id]'`

-for every time when clicking an item from the HTML Module \(such as: Analyst, Sales Rep, Manager, Designer\) the Action Grid will update its datasource without a page load. 


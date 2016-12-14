# Item Picker \(Tree View\) field

This fields was especially designed for choosing items from a dropdown where the data source and the display should be structured as a tree. There are now 3 data sources that where redesigned to work properly with this new field in Action Form and Action Grid \(Form Builder\). Those are: **PortalPages**, **PortalFolderList** and the most powerful **SQL Query.**

# PortalPages & PortalFolderList

Those datasources will bind all the the data and you will be able to select a page or a node \(a page with subpages or folder\). There are no restriction applied for those data sources and you can select only one.

The result should be something like this:

![](assets/1f2143bdb9[1].png)

# SQL Query

This field is more customizable than other fields that are at the moment so an custom more powerful SQL Query is need it to use all the features.

Here is an example of  query and will look below of what is new:

> `SELECT TOP 1000`
>
> `[Text]`
>
> `,[Value]`
>
> `, CASE WHEN ParentId = 0 THEN CAST([EntryID] as nvarchar(50)) ELSE  CAST(ParentID as nvarchar(50)) + '/' + CAST([EntryID] as nvarchar(50)) END as 'Path'`
>
> `, CASE WHEN ParentId != 0 THEN 'true' ELSE 'false' END as IsSelectable`
>
> `, CASE WHEN text = 'Argentina' THEN null ELSE 11 END ParentPath`
>
> `, CASE WHEN 0 = 0 THEN -1 ELSE ParentID END ParentId`
>
> `, EntryID as ItemId`
>
> `, CASE WHEN ParentId = 0 and EntryID != 12 THEN 'true' ELSE 'false' END as HasChildren`
>
> `FROM [Lists]`
>
> `where`
>
> `--condition for getting descendents of an item`
>
> `ParentID = @parentId`
>
> `--condition for getting the root items`
>
> `or`
>
> `(@parentId = -1 And   EntryID = 11)`
>
> `or`
>
> `(@parentId = -1 And   EntryID = 12)`
>
> `--condition for search`
>
> `or`
>
> `(`
>
> `@searchText != ''`
>
> `AND`
>
> `-- this condition should bring all items when searchText has a value`
>
> `(ParentID = 11  or EntryID = 11 or EntryID = 12)`
>
> `)`

The SQL Header should look like this :

![](assets/5a6b68bbe6[1].png)

The result should be something like this:

![](assets/4e4079e584[1].png)

### Fields:

**Text: ** This will be displayed for the user to select and/or expand.

**Value:** This will be the value that for further processing, if you have any, this field will return as token.

**Path & ParentPath**_\(!\)_**: ** Those Fields are used create the logic behind the arborescent view where the **Path **is the whole path to item including him and the **ParrentPath ** is only the parent path if the item. _\(Use only one of those two\)\(!\)_

**ItemId & ParentId**_\(!\)_**: ** Those Fields are used create the logic behind the arborescent view where the **ItemId **is the whole path to item including him and the **ParrentId ** is only the parent path if the item. _\(Use only one of those two\)\(!\)_

**HasChildren: **Tell the fields if it has children there for is expandable. We need this info because this control has lazy loading so we can keep the traffic and the database at a minimum.

**IsSelectable: **Tell the item if it can be selectable _\(can be a leaf or a node\)_

### Note:

**If the columns name is not provided as above the control will not work. **

# IsSelectable \(SQL Query Only\)

When this value is 'true' than the leaf or node can be selected and chosen as an option. When 'false' the mouse pointer will be change and let you know that you can't click that item and choose it as an option.

# Expanding & Collapsing

Because mainly the data sources require the nodes to be selectable the expanding and collapsing is made from the plus \( ![](assets/folder-closed.png) \) and minus \( ![](assets/folder.png) \) where the file \( ![](assets/file.png) \) mean that there is a leaf and can't be expanded.

# Search

The search works with by pressing the button on the right of the textbox \( ![](assets/cfb6ed253e[1].png) \) or by pressing Enter key._ It will not search when the input is changed._

# Initially Selected

### PortalPages: _TabID_

### PortalFolderList: _Path_

### SQL Query: _value from Value Column_




# 管理环境访问权限

环境可以按[组](groups.md)进行组织管理。如果环境和单个用户位于同一组中，用户将在**管理访问**页面上标记为`inherited`。这意味着用户从组继承其访问权限，而不是直接从环境继承。

如果您手动将用户分配到环境，而该用户已通过组分配，则他们将在**管理访问**页面上标记为`override`，表示在此特定环境下，他们的个人访问权限将覆盖组的权限。您可以针对此特殊情况修改他们的访问权限。

从菜单展开**环境相关**，然后选择**环境**。找到您要授予用户访问权限的环境，然后选择行尾的**管理访问**。

<figure><img src="..//assets/2.20-environments-access.gif" alt=""><figcaption></figcaption></figure>

接下来，使用下拉菜单选择要添加的用户或团队。然后使用**角色**下拉菜单选择您希望此用户或团队拥有的角色。

<figure><img src="..//assets/2.20-environments-access-create.png" alt=""><figcaption></figcaption></figure>

选择完成后，点击**创建访问权限**。

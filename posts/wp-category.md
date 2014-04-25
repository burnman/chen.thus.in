#wordpress自定义分类目录模版

最近在使用wordpress搭建企业网站，在这里会把一些经验分享出来，供大家交流交流。

wordpress后台是无法直接设置分类目录的模版的，只能调用默认的category.php模版。这就不符合企业站的分类要求，一般的企业站点至少要有About,News,Products,Service四个大类。其中About可以使用文章页代替，其它三个就必须使用不同的分类目录模版。在这里提供两种方法：

**方法一**

复制模板根目录下的category.php文件，将其重命名为对应的名称。例如：category-news.php,category-products.php,category-service.php

命名方式有两种

第一种，根据分类目录的ID来命名。例如"News"这个分类目录的ID是2，则将文件名重命名为category-2.php ，修改其文件中的代码，则可以实现模板内容的自定义调整。

如果不知道分类目录ID的，可以在wordpress后台点击“文章”-“分类目录”，然后点击对应分类的 “查看” 然后浏览器顶部就会出现类似下面的一个地址，其中tag_ID=2就是你分类目录ID。

`http://127.0.0.1/wp/wp-admin/edit-tags.php?action=edit&taxonomy=category&tag_ID=2&post_type=post`

第二种，根据分类目录的别名来命名，需要把category.php重命名为对应的别名。比如“News”列表页面栏目别名为news，重命名为category-news.php。

**方法二**

在模板的index.php文件中增加对应的文件引用判断，代码如下：

```php
<?php
if (in_category('1') || post_is_in_descendant_category(1) ){
include(TEMPLATEPATH.`/category-1.php`); //判断当前分类目录ID是否为1，为1则调用对应的分类模板
}
elseif(in_category('2') || post_is_in_descendant_category(2) ){
include(TEMPLATEPATH.`/category-2.php`); //判断当前分类目录ID是否为2，为2则调用对应的分类模板
}else{
include(TEMPLATEPATH.`/category.php`); //如果当前分类目录，ID不是1和2的话，则调用默认的分类目录
}
?>
```


我用的是第一种方法，因为更符合企业的命名规范。大家可以根据自己需求选择使用哪种方法。


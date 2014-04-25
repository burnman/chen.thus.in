#WordPress不同分类模版使用不同文章模版

上一篇写了WordPress怎样自定义分类目录模版，接下来就是怎样让不同的分类模版使用适合自身分类的文章模板。

这里同样介绍两种方法

**方法一**

1.将下面的代码添加到当前主题的functions.php文件中：

```c
/**
* 不同分类使用不同的文章模板
*/
//定义模板文件所在目录为 single 文件夹
define(SINGLE_PATH, TEMPLATEPATH . '/single');
//自动选择模板的函数
function wpdaxue_single_template($single) {
    global $wp_query, $post;
    //通过分类别名或ID选择模板文件
    foreach((array)get_the_category() as $cat) :
        if(file_exists(SINGLE_PATH . '/single-cat-' . $cat->slug . '.php'))
            return SINGLE_PATH . '/single-cat-' . $cat->slug . '.php';
        elseif(file_exists(SINGLE_PATH . '/single-cat-' . $cat->term_id . '.php'))
            return SINGLE_PATH . '/single-cat-' . $cat->term_id . '.php';
    endforeach;
}
//通过 single_template 钩子挂载函数
add_filter('single_template', 'wpdaxue_single_template');
```

2.在当前 主题的根目录新建一个名为single的文件夹，然后根据不同的分类创建不同的文件命名格式为 single-cat-[分类别名或ID].php。例如：上篇讲的分类News，ID为2、别名为news，所以我们为它新建一个模版文件名为single-cat-news.php或者single-cat-2.php。你可以按自身的需求创建不同文章模板，但是你要记得你的每个分类模板都应有文章模板。

**方法二**

第二种方法可以使用wordpress的in_category()函数，这个函数可以通过分类别名或分类ID来判断当前文章的所属分类。

通过别名判断

```c
in_category('news')
in_category(array('news','products','service'))    //多个分类别名
```

通过ID判断

```c
in_category(2)
in_category(array(2,3,4))
```

下面就举个例子，分别为分类目录news、products、service建三个文章模板，命名为single-news.php,single-products.php,single-service.php。然后在主题的根目录下找到single.php，写入一下代码。

```php
<?php 
if ( in_category(array('news','products','service')) )
{
    include(TEMPLATEPATH . '/single-news.php');
} elseif ( in_category( 7 )) {
    include(TEMPLATEPATH . '/single-products.php');
} else {
    include(TEMPLATEPATH . '/single-service.php');
}
?>
```

你也可以在主题的根目录下新建一个文件夹(single)，将这些文章模板放在一起以便管理。只用在上面的'/single-news.php'上加上你的文件夹名single变成'single/single-news.php'就可以了。
<!--t Wordpress: lista tagów t-->
<!--d Shortcode z listą tagów w tym wypadku opisów tagów: ``` add_shortcode(&#039;tagslist&#039;, &#039;tags_list&#039;); function tags_list() { $ret = d-->
<!--tag wordpress,php tag-->

Shortcode z listą tagów w tym wypadku opisów tagów:

```
add_shortcode('tagslist', 'tags_list');

function tags_list() {

$ret = "";
$tags = wp_get_post_tags(get_the_ID());

if ($tags) 
{
    foreach ($tags as $tag) 
    {
        if ($tag->description) 
        {
            // tu masz inne pola '<a href="' . get_tag_link( $tag->term_id ) . '" title="' . sprintf( __( "View all posts in %s" ), $tag->name ) . '" ' . '>' . $tag->name.'</a><br>' . $tag->description . '<br>';
            $ret .= '<li>' . $tag->description;
        } 
    } 
}

return($ret);
}
```
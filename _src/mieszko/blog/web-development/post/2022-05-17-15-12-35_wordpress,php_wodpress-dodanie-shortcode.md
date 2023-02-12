<!--t Wodpress: dodanie shortcode t-->
<!--d W pliku `functions.php` dodajemy: ``` add_shortcode(&#039;nasznowyshortcode&#039;, &#039;funkcjaktorazwrocidane&#039;); function d-->
<!--tag wordpress,php tag-->

W pliku `functions.php` dodajemy:

```
add_shortcode('nasznowyshortcode', 'funkcjaktorazwrocidane');

function funkcjaktorazwrocidane() {
return('jakies dane :)');
}
```
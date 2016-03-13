---
published: true
title: Prova post
layout: post
---
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut cursus eros in venenatis condimentum. Cras congue neque consequat nulla facilisis, vel vehicula lacus vulputate. Nunc facilisis mi in lorem finibus consectetur. Ut lectus lorem, lacinia id mi in, pulvinar bibendum nunc. Nunc consectetur efficitur massa in molestie. Aliquam nisi mauris, rutrum nec lectus vitae, malesuada dapibus massa. Morbi molestie, nisi id vestibulum volutpat, lorem leo ornare urna, vel fringilla leo nisl eget lorem. Interdum et malesuada fames ac ante ipsum primis in faucibus. Proin ullamcorper molestie augue nec efficitur. Curabitur quis congue augue, in tempus neque. Phasellus accumsan eget massa tincidunt sodales. In hac habitasse platea dictumst. Donec est orci, molestie et aliquam laoreet, pretium in mi. Aliquam finibus porta neque, sed ornare mi vulputate in. Maecenas quis pharetra nunc.


{% highlight elixir monokai %}
# Numbers
0b0101011
1234 ; 0x1A ; 0xbeef ; 0763 ; 0o123
3.14 ; 5.0e21 ; 0.5e-12
100_000_000

# these are not valid numbers
0b012 ; 0xboar ; 0o888
0B01 ; 0XAF ; 0O123

# Characters
?a ; ?1 ; ?\n ; ?\s ; ?\c ; ? ; ?,
?\x{12} ; ?\x{abcd}
?\x34 ; ?\xF

# these show that only the first digit is part of the character
?\123 ; ?\12 ; ?\7

# Atoms
:this ; :that
:'complex atom'
:&quot;with' \&quot;\&quot; 'quotes&quot;
:&quot; multi
 line ' \s \123 \xff
atom&quot;
:... ; :&lt;&lt;&gt;&gt; ; :%{} ; :% ; :{}
:++; :--; :*; :~~~; :::
:% ; :. ; :&lt;-

# Strings
&quot;Hello world&quot;
&quot;Interspersed \x{ff} codes \7 \8 \65 \016 and \t\s\\s\z\+ \\ escapes&quot;
&quot;Quotes ' inside \&quot; \123 the \&quot;\&quot; \xF \\xF string \\\&quot; end&quot;
&quot;Multiline
   string&quot;

# Char lists
'this is a list'
'escapes \' \t \\\''
'Multiline
    char
  list
'

# Binaries
&lt;&lt;1, 2, 3&gt;&gt;
&lt;&lt;&quot;hello&quot;::binary, c :: utf8, x::[4, unit(2)]&gt;&gt; = &quot;hello™1&quot;

# Sigils
~r/this + i\s &quot;a&quot; regex/
~R'this + i\s &quot;a&quot; regex too'
~w(hello #{ [&quot;has&quot; &lt;&gt; &quot;123&quot;, '\c\d', &quot;\123 interpol&quot; | []] } world)s
~W(hello #{no &quot;123&quot; \c\d \123 interpol} world)s

~s{Escapes terminators \{ and \}, but no {balancing} # outside of sigil here }

~S&quot;No escapes \s\t\n and no #{interpolation}&quot;

:&quot;atoms work #{&quot;to&quot; &lt;&gt; &quot;o&quot;}&quot;

# Operators
x = 1 + 2.0 * 3
y = true and false; z = false or true
... = 144
... == !x &amp;&amp; y || z
&quot;hello&quot; |&gt; String.upcase |&gt; String.downcase()
{^z, a} = {true, x}

# Free operators (added in 1.0.0)
p  ~&gt;&gt; f  = bind(p, f)
p1 ~&gt;  p2 = pair_right(p1, p2)
p1 &lt;~  p2 = pair_left(p1, p2)
p1 &lt;~&gt; p2 = pair_both(p1, p2)
p  |~&gt; f  = map(p, f)
p1 &lt;|&gt; p2 = either(p1, p2)

# Lists, tuples, maps, keywords
[1, :a, 'hello'] ++ [2, 3]
[:head | [?t, ?a, ?i, ?l]]

{:one, 2.0, &quot;three&quot;}

[...: &quot;this&quot;, &lt;&lt;&gt;&gt;: &quot;is&quot;, %{}: &quot;a keyword&quot;, %: &quot;list&quot;, {}: &quot;too&quot;]
[&quot;this is an atom too&quot;: 1, &quot;so is this&quot;: 2]
[option: &quot;value&quot;, key: :word]
[++: &quot;operator&quot;, ~~~: :&amp;&amp;&amp;]

map = %{shortcut: &quot;syntax&quot;}
%{map | &quot;update&quot; =&gt; &quot;me&quot;}
%{ 12 =&gt; 13, :weird =&gt; ['thing'] }

# Comprehensions
for x &lt;- 1..10, x &lt; 5, do: {x, x}
pixels = &quot;12345678&quot;
for &lt;&lt; &lt;&lt;r::4, g::4, b::4, a::size(4)&gt;&gt; &lt;- pixels &gt;&gt; do
  [r, {g, %{&quot;b&quot; =&gt; a}}]
end

# String interpolation
&quot;String #{inspect &quot;interpolation&quot;} is quite #{1+4+7} difficult&quot;

{% endhighlight %}

Duis quam mi, vulputate et scelerisque eu, finibus quis nunc. Duis ullamcorper consectetur felis, non fermentum mi egestas a. Donec euismod dapibus nisi quis laoreet. Integer eget dui dictum, rhoncus mauris id, malesuada lectus. Nam congue est et turpis tincidunt efficitur. Aenean ac hendrerit magna. Morbi et consectetur libero.

Sed mattis massa ut felis porta, ut malesuada lacus tincidunt. Vestibulum varius imperdiet nisl, at lobortis mauris rhoncus ut. Fusce vitae est vitae ante hendrerit pharetra. Cras a enim diam. Maecenas placerat, tortor a placerat pulvinar, odio enim dictum quam, tincidunt dictum urna ante id ex. Nam tempor est eu interdum euismod. Ut ac ipsum pellentesque, tempus dolor faucibus, posuere neque. Nunc elit metus, mattis eget leo a, pulvinar efficitur purus. In ultrices, urna non consectetur porta, dui libero volutpat ex, a convallis augue diam at felis. Proin vitae commodo diam. Mauris tincidunt dapibus justo eget viverra. Cras vestibulum lorem eget ultricies ultrices. Donec eget euismod leo. Nam sit amet congue nunc, a dapibus orci. Donec in euismod justo. Ut porttitor est vitae tortor scelerisque scelerisque.

Mauris ut vehicula elit. Donec id suscipit dui, eget feugiat tortor. Nam consequat accumsan mi, id tristique nisl tempor eget. Aenean interdum lacus eros, in consectetur nulla rhoncus vel. Proin accumsan facilisis odio id rutrum. Maecenas nec vehicula mauris. Pellentesque sit amet varius ipsum, congue vulputate massa. In malesuada porttitor urna, vitae semper lectus imperdiet at. In dictum vitae odio ut blandit. In finibus ex et diam faucibus, ac elementum lorem pharetra.

Nam dictum pellentesque hendrerit. Fusce dignissim mauris eget tortor cursus posuere. Praesent sodales commodo auctor. Proin nec purus purus. Praesent scelerisque faucibus purus, ac consectetur lectus malesuada a. Etiam nec mi tristique, placerat massa quis, efficitur lorem. Donec sodales sem purus, et accumsan sem posuere in. Cras semper massa massa, sed cursus lorem tristique ac. Mauris auctor vestibulum massa, in pulvinar lacus ornare id.
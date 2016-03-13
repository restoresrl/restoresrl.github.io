---
published: true
title: Prova post
layout: post
---
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut cursus eros in venenatis condimentum. Cras congue neque consequat nulla facilisis, vel vehicula lacus vulputate. Nunc facilisis mi in lorem finibus consectetur. Ut lectus lorem, lacinia id mi in, pulvinar bibendum nunc. Nunc consectetur efficitur massa in molestie. Aliquam nisi mauris, rutrum nec lectus vitae, malesuada dapibus massa. Morbi molestie, nisi id vestibulum volutpat, lorem leo ornare urna, vel fringilla leo nisl eget lorem. Interdum et malesuada fames ac ante ipsum primis in faucibus. Proin ullamcorper molestie augue nec efficitur. Curabitur quis congue augue, in tempus neque. Phasellus accumsan eget massa tincidunt sodales. In hac habitasse platea dictumst. Donec est orci, molestie et aliquam laoreet, pretium in mi. Aliquam finibus porta neque, sed ornare mi vulputate in. Maecenas quis pharetra nunc.

{% highlight powerbuilder %}
CHOOSE CASE iu_pdo.Get_Sync_State ( ) 
	CASE n_raf_pdo.PDO_SYNC
		st_title.text = iu_pdo.Get_Title ( )
	CASE n_raf_pdo.PDO_NEW
		st_title.text = _("Nuovo")
	CASE ELSE
		st_title.text = ""
END CHOOSE

st_subtitle.text=iu_pdo.Get_Subtitle()
if app.fn.string_is_empty(st_subtitle.text) then
	st_subtitle.hide()
	st_title.y = 54
else
	st_subtitle.show()
	st_title.y = 20
end if

sle_id.text = string(iu_pdo.ID)

plb_icon_main.DeletePicture ( 1 )
plb_icon_main.AddPicture ( iu_pdo.get_icon() )
{% endhighlight %}

Duis quam mi, vulputate et scelerisque eu, finibus quis nunc. Duis ullamcorper consectetur felis, non fermentum mi egestas a. Donec euismod dapibus nisi quis laoreet. Integer eget dui dictum, rhoncus mauris id, malesuada lectus. Nam congue est et turpis tincidunt efficitur. Aenean ac hendrerit magna. Morbi et consectetur libero.

Sed mattis massa ut felis porta, ut malesuada lacus tincidunt. Vestibulum varius imperdiet nisl, at lobortis mauris rhoncus ut. Fusce vitae est vitae ante hendrerit pharetra. Cras a enim diam. Maecenas placerat, tortor a placerat pulvinar, odio enim dictum quam, tincidunt dictum urna ante id ex. Nam tempor est eu interdum euismod. Ut ac ipsum pellentesque, tempus dolor faucibus, posuere neque. Nunc elit metus, mattis eget leo a, pulvinar efficitur purus. In ultrices, urna non consectetur porta, dui libero volutpat ex, a convallis augue diam at felis. Proin vitae commodo diam. Mauris tincidunt dapibus justo eget viverra. Cras vestibulum lorem eget ultricies ultrices. Donec eget euismod leo. Nam sit amet congue nunc, a dapibus orci. Donec in euismod justo. Ut porttitor est vitae tortor scelerisque scelerisque.

Mauris ut vehicula elit. Donec id suscipit dui, eget feugiat tortor. Nam consequat accumsan mi, id tristique nisl tempor eget. Aenean interdum lacus eros, in consectetur nulla rhoncus vel. Proin accumsan facilisis odio id rutrum. Maecenas nec vehicula mauris. Pellentesque sit amet varius ipsum, congue vulputate massa. In malesuada porttitor urna, vitae semper lectus imperdiet at. In dictum vitae odio ut blandit. In finibus ex et diam faucibus, ac elementum lorem pharetra.

Nam dictum pellentesque hendrerit. Fusce dignissim mauris eget tortor cursus posuere. Praesent sodales commodo auctor. Proin nec purus purus. Praesent scelerisque faucibus purus, ac consectetur lectus malesuada a. Etiam nec mi tristique, placerat massa quis, efficitur lorem. Donec sodales sem purus, et accumsan sem posuere in. Cras semper massa massa, sed cursus lorem tristique ac. Mauris auctor vestibulum massa, in pulvinar lacus ornare id.
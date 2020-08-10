---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
custom_css:
  - /assets/css/magnific-popup/magnific-popup.css
custom_external_js:
  - //ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js
custom_js:
  - /assets/js/magnific-popup/jquery.magnific-popup.min.js
---
<div class="popup-gallery">
{%- for member in site.data.objects -%}
  <div id="object_{{ member.id }}" style="margin: 1em 0">
    <div class="name"><b>{{ member.id }} - </b> {{ member.name }}</div>
  {%- if member.description != nil -%}
    <div class="description">{{ member.description }}</div>
  {%- endif -%}
  {%- for photo in site.data.photos -%}
    {%- if photo.id_object == member.id -%}
      <a href="{{ '/assets/images/photos/' | append: photo.filename | relative_url }}" data-id="{{ member.id }}"><img src="{{ '/assets/images/thumbnails/' | append: photo.filename | relative_url }}"></a>
    {%- endif -%}
  {%- endfor -%}
  </div>
{%- endfor -%}
</div>

<script>
$(document).ready(function() {
	$('.popup-gallery').magnificPopup({
		delegate: 'a',
		type: 'image',
		tLoading: 'Loading image #%curr%...',
		mainClass: 'mfp-img-mobile',
		gallery: {
			enabled: true,
			navigateByImgClick: true,
			preload: [0,1] // Will preload 0 - before current, and 1 after the current image
		},
		image: {
			tError: '<a href="%url%">The image #%curr%</a> could not be loaded.',
			titleSrc: function(item) {
        var name = $('#object_' + item.el.attr('data-id') + ' .name').html();
        var description = $('#object_' + item.el.attr('data-id') + ' .description').html();
 				return name + ( (typeof description !== 'undefined') ? ('<div>' + description + '</div>') : '' );
			}
		}
	});
});
</script>

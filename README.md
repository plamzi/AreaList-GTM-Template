<h2>AreaList GTM</h2>
<h4>True View UI Element Tracker for Google Tag Manager</h4>

<h2>Description:</h2>

This community template for Google Tag Manager makes it much easier to track impressions & clicks on a large number of UI elements based on their visibility to the end user.

Equally capable in complex single-page app contexts, the script can help you understand content performance of dynamic web properties much better than any old-fashioned "pageview" analytics implementation can.

Native GTM triggers already offer pretty sophisticated visibility logic, but are tedious to configure and troubleshoot. They also have to be configured for each individual element you want to track, which makes them difficult to maintain for a big (or rapidly changing) set of elements. Re-using any of that complex logic across multiple properties is also extremely onerous.

In addition to reducing the complexities surrounding the creation and maintenance of robust visibility logic, the script features built-in persistence for efficient delayed collection (next onsite page load) and configurable GTM dataLayer pushes that work with a wide variety of implementations.

<h2>Requirements:</h2>

jQuery 1.0 or later has to be loaded & available on the page prior to including the main AreaList script.

<h2>Example:</h2>

Add a new tag using the AreaList template. Configure its settings. These will be translated to a settings object that looks like this:

```
<script>

	var arealist_config = {

		areas: [

			{ name: 'Hero Slide', handle: '.hero-slideshow .el-item', title: 'h2' },
			{ name: 'IQA Grid', handle: '.iqa-grid div', title: 'h3' },
			{ name: 'HP Video', handle: '.hp-video' },
			{ name: 'Video CTA Button', handle: '.iqa-cta .uk-button', title: '.uk-button', list: 'Homepage', cat: 'CTA Buttons' },
			{ name: 'Flow CTA Button', handle: '.hp-flow .uk-button', title: '.uk-button', list: 'Homepage', cat: 'CTA Buttons' },
			{ name: 'Blog Article', handle: 'article', title: 'h1', options: { multiple: true } },
			{ name: 'Article Body', handle: 'article', title: 'h1', options: { single: true } },
			{ name: 'Social Footer', handle: 'footer', options: { clickable: true } },
			/* go wild... */
		],

		cat: 'Homepage Engagement',

		list: document.title,

		extend_clickable: '.el-item',

		debug: true
	};
  
</script>

<script src="https://github.com/plamzi/AreaList-GTM/raw/master/arealist-gtm.js"></script>

```

<b>Note:</b> In most situations, you'd want to include the contents of the main script inline rather than via the GitHub link shown in the basic example above. If you are running multiple configurations, it would make sense to place the script on your server so multiple tags can use it.

<b>Note:</b> More advanced implementations may choose to populate some or all parts of arealist_config using GTM variables.

<h2>Configuration:</h2>

<b>areas</b> - Array of area objects, each with the following properties:

<b>area.name</b> - The name of the area or UI element shown in reports.

<b>area.handle</b> - The selector / jQuery handle used to identify this element.

<b>area.title</b> - Optional selector / handle from which to grab a unique title of this element. It can be used to disambiguate multiple areas responding to the area.handle based on dynamic strings such as e. g. h1 tags. The title is added to the area name in impression and click reporting. If the title is not found inside the element at area.handle, the script will look up to 3 levels up for peers matching the title selector.

<b>area.list</b> - Optional list name for GA eCommerce Product Performance reporting.

<b>area.cat</b> - Optional category name for GA eCommerce Product Performance reporting.

<b>area.options</b> - Optional object containing additional rules for this area.

<b>area.options.single</b> - Set to true to only track this element if it is unique at the time (as determined by area.handle). For example, you can track a single article or section HTML tag differently from pages with multiple articles or sections.

<b>area.options.multiple</b> - Set to true to only track if more than one element responds to area.handle.

<b>area.options.clickable</b> - Set to true to only track this element only if it renders with at least one clickable element inside: links, buttons, form fields, etc. This is useful if a CMS module, for instance, sometimes appears with nothing clickable in it.

<b>area.options.hastitle</b> - Set to true to only track this element if the dynamic area.title selector returns a string for a given element.

<b>area.options.novischeck</b> - Set to true to track this element as soon as it's detected, regardless of whether it has become visible to the end user.

<b>area.options.noclickdedupe</b> - Set to true to disable click deduplication and track every click. Useful if the element responding to area.handle contains more than one clickable element and you wish to gauge overall engagement levels. Note that clickthrough rates (clicks / impressions) can then exceed 100% for this area.

<b>area.disable</b> - Set to true to temporarily disable tracking for an individual definition.

<b>debug</b> - Set to true to turn on verbose console logging, element inspection, flashes over active areas when impressions are collected. This mode is helpful during initial implementation or adjustment but should always be turned off in production.

<b>cat</b> - Default GA eCommerce Product Category name for all impressions & clicks. If not specified, the page title is picked up.

<b>list</b> - Default GA eCommerce Product List name. If not specified, the relative URL path is picked up.

<b>disable_impressions</b> - Set to true to suspend all impression tracking, focusing on just clicks.

<b>disable_clicks</b> - Set to true to suspend all click tracking.

<b>disable_storage</b> - Set to true to disable use of window.localStorage to persist impressions data. When storage is disabled, both clicks and single impressions will immediately enter the dataLayer. Multiple impressions will enter on page unload. If disable_storage is set to false, clicks will enter the dataLayer immediately but impressions will be cached and sent on the next site page load (which means you risk losing some impressions from departing users who never return).

<b>storage_key_name</b> - Customize the name of the localStorage key (default is 'AreaList_GTM') used by this tag instance. Useful if you are deploying multiple instances of the main tag across the same site.

<b>data_layer_name</b> - Set to the name of a custom dataLayer object in the window scope. Default is 'dataLayer'.

<b>impressions_event_name</b> - Default is 'AreaList Impressions'. Change it to see a different event name in data layer pushes.

<b>impression_event_name</b> - Default is 'AreaList Impression'. Change it to see a different event name in data layer pushes.

<b>clicks_event_name</b> - Default is 'AreaList Clicks'. Change it to see a different event name in data layer pushes.

<b>click_event_name</b> - Default is 'AreaList Click'. Change it to see a different event name in data layer pushes.

<b>polling_frequency</b> - Default is 3 sec. Setting this value to less than that is not recommended for reasons of both performance & accuracy (a small delay on impression collection ensures the user has had a chance to actually see the element).

<b>extend_clickable</b> - Extend the definition of clickable objects with this selector string. Use this if clicks on certain special divs, e. g., are not being captured or considered correctly by the area.options.clickable logic.
# Setting up handover files for development 

## How SXA pages are constructed

SXA uses sets of renderings, called partial designs that make up a webpage. You can use the partial designs to create the design elements of your pages for a consistent style. For example, you can create parts of your page once, such as headers and footers, and then use them everywhere on your site by including them into a page design.

A page design in SXA is a selection of partial designs and renderings that help you to structure your pages.

For more information on the SXA template design structure see the [documentation](https://doc.sitecore.com/developers/sxa/17/sitecore-experience-accelerator/en/designing.html).


## Files required for handover

* HTML files for each template as well as the header and footer should be created using the handover template files.
* Each of these files will contain the basic grid markup as well as the partials and components to be included in the branch templates.
* The main templates that are required for handover are:
	* __header & footer__ _(single HTML file)_
	* __homepage__
	* __hub page__
	* __internal page__
	* __campaign page__
	* __blog listing page__
	* __blog post page__
	* __form page__

## How components are defined

To prevent the editor from having to remove too many auto generated unused components, only ones from the list below should be referenced in handover files, and therefore added to branch templates.

### Only components to be referenced on hub & internal pages

#### Hub page:

* __Rich text field__ _(known as a content box on v2 websites)_
* __Widget__
* __Widget__ _(stat or pullout variant)_

#### Internal page:

* __Rich text field__ _(known as a content box on v2 websites)_
* __Widget__
* __Widget__ _(stat or pullout variant)_
* __Testimonial__ _(shared only)_

### Referencing components in handover files

* The following naming convention should be used when referencing components in template handover files: 

	`<!-- ComponentName --> page or shared component`
 
## How handover files are structured

### Header & footer

By default SXA will wrap the header and footer partials in the corresponding HTML5 tags, this should be included in the handover files as reference for the developer.

To make it easy to distinguish between the SXA default code and the partials, default code should be commented out in handover files. For example:

#### SXA default header and footer

```html
<!-- SXA header wrapper open
<header>
	<div id="header">-->
        
		HEADER PARTIALS TO BE ADDED HERE
            
	<!--</div>
</header>
SXA header wrapper close -->


MAIN


<!-- SXA footer wrapper open
<footer>
	<div id="footer">-->

		FOOTER PARTIALS TO BE ADDED HERE
            
	<!--</div>
</footer>
SXA footer wrapper close -->
```

### Referencing header & footer partials

SXA doesn't add `row` classes by default in the `<header>` & `<footer>` in the  way it does for the `<main>` section. For this reason the partials have to be written slightly differently.

The header & footer can be split into sections with `"container-fluid"` or `"container"` depending on the layout required.

#### Header & footer contained layouts

* All the content in each partial should be wrapped in a single `"container-fluid"` followed by a `"container"` for contained layouts. For example:

```html
<!-- SXA header wrapper open
<header>
	<div id="header">-->
        
        <div class="container-fluid">
            <div class="container">
            
				<!-- logo component --> shared component
                
            </div>
        </div>

	<!--</div>
</header>
SXA header wrapper close -->
```
#### Header & footer fluid layouts

* If a fluid layout is required, the child `"container"` should be omitted. For example:
```html
<!-- SXA header wrapper open
<header>
	<div id="header">-->
        
        <div class="container-fluid">

			<!-- logo component --> shared component

        </div>

	<!--</div>
</header>
SXA header wrapper close -->
```
***

### Main page partials

#### SXA default code

By default SXA will wrap partials outside of the header & footer in some code _(a `<main>`, a `"container-fluid"` and two `"row"` tags)_. This should be included in the handover files as reference for the developer.

To make it easy to distinguish between the SXA default code and partials, the SXA default should be commented out in the handover files. For example:

```html
<!-- SXA main wrapper open
<main>
	<div id="content" class="container-fluid">
		<div class="row">
			<div class="row"> -->
            
            PARTIALS TO BE ADDED HERE
            
			<!-- </div>
		</div>
	</div>
</main>
SXA main wrapper close -->
```

### Referencing partials in handover files


* Break each part of the page design into sections based on the rows and columns used to break up content. _(Each of these will become page partials when the website is developed)._
* All the content in each partial should be wrapped in a single `"container-fluid"` followed by a `"row"`. For example:

```html
<div class="container-fluid">
	<div class="row">

	</div>
</div>
```

### Labeling partials

* Name each partial with an HTML comment using the following naming convention __ContainerType_ColumnNumbers_Breakpoint__. For example a contained partial with two equal columns and a medium breakpoint would be labeled:

```html
<!-- contained_6x6_md -->
```

### Contained layouts

* In order to set rows and columns for contained layouts an additional container and row must be added inside the fluid-container. For example:

```html
<!-- contained_6x6_md -->
<div class="container-fluid">
	<div class="row">

		<div class="container">
			<div class="row">
            
			</div>
		</div>

	</div>
</div>
```

**Note:** _When labeling the container type for a contained row, the label should refer to the child `"container"`, not the parent `"container-fluid"` as this class is default for every partial._


#### Single column layouts

* Sitecore automatically adds a `"col-12"` class to components. For this reason, on single column  layouts the component should be added directly inside `"container"` > `"row"`. For example:

```html
<!-- contained_12_md -->
<div class="container-fluid">
	<div class="row">

		<div class="container">
			<div class="row">
            	<!-- rich text component --> page specific component
			</div>
		</div>

	</div>
</div>
```

#### Multi-column layouts

When more than one column is added SXA will wrap the `"col-XX-XX"` divs in an extra `"row"` with the additional class names `"component column-splitter"`. These should be included in the handover files as reference for the developer.

```html
<!-- contained_6x6_md -->
<div class="container-fluid">
	<div class="row">

		<div class="container">
			<div class="row">

                <div class="row component column-splitter">
                    <div class="col-md-6">
                        <!-- widget compnent --> page specific component
                    </div>
                    <div class="col-md-6">
                        <!-- testimonial compnent --> shared component
                    </div>
                </div>

			</div>
		</div>

	</div>
</div>
```

### Fluid layouts

* As Sitecore adds a `"col-12"` class to components, single column fluid layouts _(hero sections for example)_ should be added directly inside `"container-fluid"` > `"row"`.
* For Multi-column layouts the columns should also be added directly inside `"container-fluid"` > `"row"`. For example:

```html
<!-- fluid_3x3x6_lg -->
<div class="container-fluid">
	<div class="row">
    
        <div class="row component column-splitter">
        	<div class="col-lg-3">
        		<!-- widget compnent --> page specific component
        	</div>
        	<div class="col-lg-3">
        		<!-- widget compnent --> page specific component
        	</div>
        	<div class="col-lg-6">
        		<!-- testimonial compnent --> shared component
        	</div>
        </div>
    	
	</div>
</div>
```

## Packaging for handover

#### Things required for handover to development are:

* All handover HTML files compressed into a single zip file.
* Link to, or attached copies of the signed off page designs.
* IA document from digital marketing.
* List of all types of contained & fluid partials used in the templates. For example:

##### Contained:
* contained_12_md
* contained_4x4x4_md
* contained_6x6_md
* contained_8x4_md

##### Fluid:
* fluid_12_md
* fluid_6x6_lg

The handover email should be addressed to: Ivan, Ian & Calvin.
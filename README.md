<img src="icon.png" align="right" />

# Tailori API 

Textronic design System created an interactive platform for bespoke clothing. Textronics Tailori API is how you can access that data, In fact, almost all the functionality that runs in Tailor I. 

# Features

To know more about features of TheGuide, continue reading our documentation and check our available components.

* [Element Rendering](#)  
  It allows you to render Product, options & features   
	
* [Contrast Options](#)  
  Allow user to apply contrast fabric on product
  
* [Monogram](#)  
  This feature allows you to give Company Branding on Prouduct i.e, Company Name...etc.
  
* [Auto Specific view](#)  
  Zoom on Specific Part of Product i.e., Shirt Collar, Sleeves...etc
  
* [Auto Alignment Change](#)  
  To View Back and Front Details
  
* [Summary](#)  
  Your customised product and its details	

* [Save and load favourite look](#)  
  Allow user to Custom product look

  [View online Demo](https://sagar-tds.github.io/Tailori-Plugin)

__________________________________________________________________________________________________________________________________

# Dependencies

i)  jquery.js   [download](https://code.jquery.com)

i)  jsrender.js   [download](https://www.jsviews.com/download/jsrender.min.js) 

ii) jquery.tds.js [download](https://github.com/Sagar-TDS/Tailori-Plugin/archive/master.zip) 


# Templates
  ##  Binding Element Attributes  
  In addition to normal text, you may also want to have your templates contain HTML elements whose attributes are bound to the
  controller. 
	
	
	
	  <html>
	  <head>	
	  <script id="myTemplate" type="text/x-jsrender">Name: {{:name}}</script>
	  <head/>

	  Binding template "myTemplate" in html body will show result 

	  <body>
	   <div id="myTemplate">In this Id your all var data will call     
	   </div>   
	  </body>
	  

# Documentation

## Properties
| Props                                          | Description  | Required
| -----------------------------------------------|------------| -------:|
| ServiceUrl                                     | Url of textronics tailori api | * |
| Product                                        | Product Name | * | 
| ProductTemplate                                | jsrender template for rendering options/elements | * |
| ImageSource                                    | Image container where rendered images are placed (i.e. id, class or etc) if you want to manage rendered image by your own keep this empty |         |
| OptionsPlace                                   | Container for placing the ProductOptions | * <sup><sup>1</sup></sup> |         
| OptionTemplate                                 | if you want to show Options dynamic give template id of option here (it will render html contains dynamic after click on **product** i.e. click coller or cuff or etc)             | * <sup><sup>1</sup></sup> |
| FeaturesPlace                                   | Container for placing the ProductOptions Feature | * <sup><sup>2</sup></sup> |         
| FeatureTemplate                                 | if you want to show options dynamic give template id of option here (it will render html contains dynamic after click on **product** i.e. click half sleeve or full sleeve or etc)             | * <sup><sup>2</sup></sup> |
| IsOptionVisible                                 | If *true* ProductOptions are visible on page *else* ProductOptions Features will shown   |         |
| MonogramTemplate                               | Container for placing the monogram options   |         |
| AutoSpecific                                   | if *true* detailed view of specific part is automatically renderd *else* not   |         |
| AutoAlignment                                  | if *true* view of Apparel change according to seleted feature |         |

**Note:**     
*****: Required  
***<sup><sup>n</sup></sup>**: All Properties marked as *<sup><sup>n</sup></sup> Required.
	
## Data Attributes
| Data Attribute       | Description                                                    |
| ---------------------|:--------------------------------------------------------------|
| data-tds-alignment   | Possible values are "next"/"previous" and  alignment Name |
| data-tds-moption   | if value is ***text*** it used for input box for accepting input text for monogram |
|			| if value is ***preview*** it used for img tag for displaying priview of monogram |


## Callbacks
| Callback             | Description                                                    
| ---------------------|:--------------------------------------------------------------|
| OnProductChange      | This callback fires when user click on Product i.e. Coller, Cuff, Sleeves, etc and this callback has one parameter i.e id of Product |
| OnOptionChange       | This callback fires when user click on ProductOption i.e. High Coller, Low Coller, etc and this callback has one parameter i.e id of ProductOption  |
| OnFeatureChange      | This callback fires when user click on ProductOptions Feature i.e. Half Sleeve, Full Sleeve etc and this callback has one parameter i.e id of ProductOptions Feaure |
| OnContrastChange     | This callback fires when user click on Contrast  |
| OnRenderImageChange      | This callback fires when rendered images are ready to display i.e. after changing the element when we get result from textronics api, also this callback has one parameter which array type (*if you want to render image by yourself then use this parameter and then there no need to give <b>ImageSource</b> option in plugin initialization* ) |


# Public methods in plugin


Public methods are usable on tailori objects

```js    
    obj = $("#div-1").tailori({
			'Product':'MEN-SHIRT',   //Product i.e men shirt,women shirt, men suit, etc
			'ProductTemplate':'#theTmpl', //Template id for Product
			'ImageSource':'#img-div', //Container Id for place images
			'ServiceUrl':'http://textronic.online' 
     });
      
```
------------------------------------------------
### `Product()`
If you want to change the **product** i.e from men-shirt to men-suit use 

```js
  obj.Product("men-suit");
```
------------------------------------------------
### `Texture()`
Get and Set the Texture (i.e.  fabric or color )  to apparel use 

if you want to apply fabric from textronics fabric library send id of fabric
```js
  obj.Texture("fab12589");
```

if you want to apply color as texture 
```js
  obj.Texture("red"); 
  obj.Texture("#ff0000");  //hex value of color
  obj.Texture("rgb(255,0,0)");  //rgb value of color
  obj.Texture("hsl(0, 100%, 50%)");  //hsl value of color
```

if you want texture of apparel call method without passing parameter

```js
 texture = obj.Texture();
```
------------------------------------------------

### `ContrastTexture()`
Get and Set the Texture (i.e.  fabric or color )  to contrast part of apparel 

if you want apply fabric from textronics fabric library send id of fabric
```js
  obj.ContrastTexture("fab12589");
```

if you want to apply color as texture 
```js
  obj.ContrastTexture("red"); 
  obj.ContrastTexture("#ff0000");  //hex value of color
  obj.ContrastTexture("rgb(255,0,0)");  //rgb value of color
  obj.ContrastTexture("hsl(0, 100%, 50%)");  //hsl value of color
```

if you want texture of contrast of apparel call method without passing parameter

```js
 contrasttexture = obj.ContrastTexture();
```

##### *Note: ContrastTexture apply texture on last selected contrast only*
------------------------------------------------

### `SpecificRender()`
To show detailed view of specific part, then send parameter ***true*** and to show normal view send ***false***

```js
obj.SpecificRender(true);
```
---------------------------------------------------------------------------

### `Summary()`
To get the summary of apparel
Method return the object contain selected part and fabric information with cost 
```js
obj.Summary();
```
-----------------------------------------------------------

### `ResetContrast()`
To reset all contrast of apparel
```js
obj.ResetContrast();
```

### `ResetProduct()`
To load default apparel 
```js
obj.ResetProduct();
```

### `Look()`
To get and set your favourite look (*i.e. if you want to save your custmized apparel for future use*)
this will return you object which contain ***data*** and ***Image*** 
If you want to load your look next time send ***data***  to method 


Get Look
```js
look = obj.Look();
// look.Data - to load save look next time
// look.Image - To show image of custmize look
```

Load Look
```js
 obj.Look(look.Data);
```

### `Options()`
Gets an item of particular product by sending it the product-id which you will get from OnProductChange.
It will return array of objects.

```js
optionsObj = obj.Options("158294");
```

### `Features()`
Get an items of particular product by sending it the option-id which you will get from OnOptionChange.
It will return array of objects.

```js
featuresObj = obj.Features("75321598");
```

### `Contrasts()`
Gets an item of particular product by sending it the product-id which you will get from OnProductChange.
It will return array of objects.

```js
contrastsObj = obj.Contrasts("158294");
```

------------------------------------------------
# Example

Using Tailori Plugin

```js    
    <script>
var obj =null;
function GetSummary(){
	console.log( obj.Summary());
}
function GetProduct(){
	obj.Product($("#product-info").val());
}
	$(document).ready(function () {
		//alert("hi")		
		
		 obj = $("#div-1").tailori(
		{
			'Product':'MEN-SHIRT',   //Product i.e men shirt,women shirt, men suit, etc
			'ProductTemplate':'#theTmpl', //Tempalte id for Product
			'ImageSource':'#img-div', //Container Id for place images
			'ServiceUrl':'http://textronic.online/WEB_API',
			'AutoSpecific':false, //Auto specific view after selecting any feature
			'AutoAlignment':false, //Auto alignment set according to selected element
			'Monogram':false, //If monogram 
			'MonogramTemplate':'#theTmplm', //Tempalte id for Monogram UI
			'MonogramPlace':'#monoplace', // html containter for Monogram
			'FeatureCallback': function(){
				alert($(this).attr("data-tds-key"));
				
				console.log(abc);				
			},
			'RenderCallback':function(a){
				console.log(a);
				//console.log(b);
			}
			//OptionCallback
		});

      
```

### Product  
Men-Shirt, Men-Suit, Men-Pant
  
('Product':'MEN-SUIT' OR 'Product':'MEN-PANT'...)   
As we change Product the 3D Product will appear on Page 
##### In Example we are using
'Product':'MEN-SHIRT'
_______________________________________________________________________________

### Product Template  

We have to create template id where we call id's, this template will be called as the page opens.  

for e.g ('Product Template':#Template name  ,'Product Template':#template01......)  

##### In Example we are using
'Product Template':#div-1
_______________________________________________________________________________

### Img-Source  
Html container for 3d Image   
('Image Source'':'#img-div', 'Image Source'':'#garments', 'Image Source'':'#draping-region')
  
##### In Example we are using
'Product Template': #img-div
_______________________________________________________________________________

### ServiceUrl

ServiceuUrl is a url where we place all our data that we need to call, for e.g product, draping parts, buttons, fabrics, etc.
  
 ##### In Example we are using
'ServiceUrl':''http://textronic.online/WEB_API'',
_______________________________________________________________________________

### SpecificRender

SpecificRender option is used to zoom specific Part of Img

When we Pass Boolean 'true' then we can zoom particular part on img for e.g Collar, Sleeve, etc.
if we put 'false' it won't show zoomed view.

##### In Example we are using
'SpecificRender':true,
_______________________________________________________________________________

### Auto Alignment (Currently not working)
Auto Alignment is the option for Front View and Back View. It shows back details and front details, so, we have to pass boolean True or False

##### In Example we are using
'AutoAlignment':false,
_______________________________________________________________________________
 
 ####     a) Monogram      b) Monogram Template     c) Monogram Place
   
### Monogram
'Monogram':true, or .'Monogram':false, 
To add Monogram pass string value true other wise pass string value false

### MonogramTemplate
Same as product template we create template for Monogram.
In template we can add: font, text, and placing area to show monogram. we can add Monogram on Pocket, Collar, etc.,

##### In Example we are using
'MonogramTemplate':#theTmplm

### MonogramPlace
In html we call id monosublist so all Monogram template will render in #monosublist
for e.g in html body we have to add


	<html>
	<div id ="monosublist"> for monogram template</div>
	</html>


 ##### In Example we are using
'MonogramPlace':#monosublist'
_______________________________________________________________________________

### Feature Template

Same as Monogram we have to create template, how product features will display in browser. If product is Cuff then options will be straight cuff, beveled cuff,etc. and features will be single bottom cuff, double bottom cuff etc., so we will render this template in html head section

'featureTemplate':'#Featuretemplatename'
_______________________________________________________________________________

### Feature Place

In html we call id 'xyz' so all feature template will call in #xyz
for e.g in html body we have to add

	<html>
	<div id ="xyz">  product features will appear here </div>
	</html>

'featurePlace':'#xyz'
_______________________________________________________________________________

### Option Template

'optiontemplate':'#optionstemplatename'

We have to create template how product options will display in broswer. If product is Cuff then options will be straight cuff, beveled cuff,etc. and features will be single bottom cuff, double bottom cuff, etc.

'optionTemplate':'#optiontemplatename'

_______________________________________________________________________________

### Options Place

In html we call id 'ABC' so all features template will call in #ABC
for e.g in html body we have to add

	<html>
	<div id ="ABC">product options will appear here </div>
	</html>
_______________________________________________________________________________

### Isoptions

If we want to show options(straight cuff, beveled cuff...) seperately, pass boolean 'true' and If we give false, options and features will be listed in same place

 ##### In Example we are using
'Isoptions':'true'  

_______________________________________________________________________________

# How to use JsRender and Creating Template
JsRender is a light-weight but powerful templating engine.

Here's a first example of the power and simplicity of JsRender templates:


	Some data:
	
	    "ID":
	    "name":
	    "Imagesource":
	


A template (with a conditional section using an {{for}}-------{{for}}, tag):

 ##### In Example
Products we are using{{for product}}-------{{for}}  
Options we are using{{for options}}-----{{for}}  
Contast we are using{{for contrast}}-----{{for}}  

```html
<script id="theTmpl" type="text/x-jsrender">
		
<div class="panel-group" id="accordion2">
{{for Product}}
<div class="panel panel-default">
	<div class="panel-heading">
	<h4 class="panel-title">
	<a class="accordion-toggle" data-toggle="collapse" data-parent="#accordion2" 
							    href="#collapse{{:Id}}">
	<img style="max-width:30px;" src="{{:ImageSource}}">{{:Name}}
	</a>
	</h4>
</div>
<div id="collapse{{:Id}}" class="panel-collapse collapse">
	<div class="panel-body">
	<table class="table">
	{{for Options}}
						
	{{for Features}}		
		<tr id="{{:Id}}">
			<td><span class="glyphicon glyphicon-chevron-right"></span>
			<a href="#">{{:Name}}</a>
			</td>
		</tr>
		{{/for}}
		{{/for}}
		{{for Contrasts}}		
		<tr id="{{:Id}}">
			<td><span class="glyphicon glyphicon-chevron-right"></span>
			 <a href="#">{{:Name}}</a>
			</td>
		</tr>
	{{/for}}
	</table>
	</div>
</div>
</div>
{{/for}}
</div>

</script>
```
_______________________________________________________________________________

## Example of template for bootstrap nav panel 

```html
<script id="theTmpl1" type="text/x-jsrender">
<div class="col-md-12">
<div class="panel with-nav-tabs panel-default">
  <div class="panel-heading">
	<ul class="nav nav-tabs">
		{{for Product}}                            
	<li><a href="#tab{{:Id}}" data-toggle="tab">
	<img style="max-width:30px;" src="{{:ImageSource}}">{{:Name}}</a>
		</li>                          
		{{/for}}   
	</ul>
   </div>
   <div class="panel-body">
       <div class="tab-content">
	{{for Product}}					
        <div class="tab-pane fade " id="tab{{:Id}}">
	<ul class="list-group">
		{{for Options}}
		  {{for Features}}
	<li class="list-group-item" id="{{:Id}}">{{:Name}}</li>						
		  {{/for}}   
		{{/for}}   
	</ul>
	</div>
	{{/for}}                           
	</div>
  </div>
</div>
</div>	
</script>
```
_______________________________________________________________________________

If you want to show options and feature dynamically, you can create three template
 
1. For Product
2. For Option
3. For Feature

if *IsOptionVisible=false*  or Product contains only one option then it will directly show  all the features from particular Product

### Example for Product Template


```html
<script id="theTmpl33" type="text/x-jsrender">
	<li id="Fab">
	<a><span>Fabrics</span></a>
	</li>
	{{for Product}}
	<li>
	<a class="nav-toggle" href="#" style="background-image:url({{:ImageSource}}); 
	                                               background-repeat:no-repeat;">
	<span>{{:Name}}</span>
	</a>
	</li>
	 {{/for}}
	<li id="Monogram">
	 <a><span>Monogram</span></a>
	</li>
 </script>
```
___________________________________________________________________________

### Example for Option Template

```html
<script id="optionsTemplate" type="text/x-jsrender">
 {{for Options}}
	<li id='{{:Id}}'>
	<a class='nav-toggle' href='#' style='background-image:url({{:ImageSource}}); 
						       background-repeat:no-repeat;'>
	<span>{{:Name}}</span>
	</a>
	</li>
{{/for}}
 </script>
```
____________________________________________________________________

### Example for Feature Template

```html

<script id="FeaturesTemplate" type="text/x-jsrender">
{{for Features}}
 	<li>
 	<a href="#" style="background-image:url({{:ImagesUrl}}); background-repeat:no-repeat;
								      background-size:100%;">
 	<span>{{:Name}}</span>
	 </a>
	</li>
 {{/for}}
</script> 
```

_______________________________________________________________________________

## Monogram

### Example for Monogram Template

```html
<script id="MonogramTemplate2" type="text/x-jsrender">
<div class="form-group">
	<label for="sel1">Monogram Placement:</label>
	<select class="form-control" id="sel1">
	  {{for MonogramPlacement}}
	  <option>{{:Name}}</option>
	    {{/for}}
	</select>
</div>
<div class="form-group">
	<label for="sel2">Monogram Font:</label>
	<select class="form-control" id="sel2">
	   {{for MonogramFont}}
	   <option>{{:Name}}</option>
	   {{/for}}
	</select>
</div>
<div class="form-group">
	<label for="usr">Monogram Text:</label>
	<input class="form-control" id="monogram-text" data-tds-moption="text" 
	                                 placeholder="Enter Text" type="text">
</div>
<div>
	<label>Monogram Color:</label>
	<ul class="color">
	    {{for MonogramColor}}
	    <li style="background-color:{{:Name}};">
	    <a href="#" style="background-color:{{:Name}}; background-repeat:no-repeat; 
	                                                         background-size:100%;">
	    </a>
	    </li>
	    {{/for}}
	</ul>
</div>
</script>

```




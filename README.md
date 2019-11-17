# TinyMCE Filestack plugin 
**a.k.a I can't believe nobody has made this yet**

This is a very simple plugin for tinyMCE that allows you to upload images to filestack and then drops them into the WYSIWYG editor as an `img` tag.

**Installation**

I have no idea how to use NPM so for now, just copy/paste the `plugin.min.js` file into your tinymce plugins directory. Here's what that path should look like:

`tinymce/plugins/filestack/plugin.min.js`

**Setup**

Then load the plugin in your tinymce init block using `filestack`:

```javascript
	tinyMCE.init({
		selector: '.mce',
		plugins: 'filestack',
		toolbar: 'filestack',
		filestack_api_key: '[[YOUR API KEY]]'
	});
```

Note that you'll need to include the `filestack_api_key` property there - if you don't include it the plugin will log an error to the console and quietly fail.

**How to use**

If the thing is working as it should, you'll see a button on your toolbar with an upload icon and the text 'Filestack'. Click that to open the stock Filestack filepicker. Choose your image, hit upload, and when the upload completes the filepicker will close and the image will be pasted into the WYSIWYG editor. If you want to change the filestack URL (for transforms and what have you) I recommend using the stock TinyMCE `code` plugin and hitting the `source` button - you'll see the pasted image is simply an `img` tag. You can use all of the same things from Filestacks awesome [processing API](https://www.filestack.com/docs/api/processing).

## Options 
You also have some other things you can use to modify the behaviour of the plugin.

**Image transformation defaults**

```javascript
	filestack_image_height: 600,
	filestack_image_width: 800,
	filestack_image_fit: 'max',
	filestack_image_align: 'center'
```
Have a running guess what those little cuties do. Those are the defaults, feel free to change them - all they do is append onto the URL that gets pasted into the `img` tag after file upload. They are simply the resize functions as defined in [the filestack docs](https://www.filestack.com/docs/api/processing/#resize).

**onUploadDone function**

If you feel like it, you can hook into the Filestack reglarold `onUploadDone` function by defining `filestack_onUploadDone` in your init block:

```javascript
	filestack_onUploadDone: function(response){
		// send the data to the server
		axios.post('/admin/images', {handle: response.filesUploaded[0].handle});
	},
```

That's all for now! If you like the plugin, hassle Filestack to make a proper one! <3

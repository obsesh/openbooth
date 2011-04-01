OpenBooth
=========

Obsesh Dev Team with its immense gratitude for the open source community is proud to present V1.0 of OpenBooth.

At obsesh.com, we needed a photo booth solution. Unfortunately all the ones offered on the market were either, overpriced or not what we needed.
It was time for a new webcam photo booth project that was highly customizable and allowed both direct uploads via multiform uploads as well as an S3 ready uploading ability.   OpenBooth was born.

Demo Page
---------

[Obsesh Dev Team's - OpenBooth](http://www.obsesh.com/openbooth/openbooth.html)


Requirements
------------
* Javascript, SWFObject
* Flash 9+
* Some love...


How to Use
-----------
OpenBooth is highly customizable both in terms of operation, and in styling. Every function within OpenBooth is fully accessible through Javascript - meaning that all that buttons and controls can (and should) be normal HTML elements. 

To initialize OpenBooth, you must pass an object variable to the init() function. Here's a detailed example (** denotes required params):

var options = {
	'enableSound'						: true, // Camera sounds
	'enableFlash'						: true, // Camera Flash effect
	'enableSettingsButton'	: true, // Flash settings button (only appears when hovering over video)
	'bandwidth'							:	0, // Max Bandwidth (0 = unlimited) **

	'photoQuality'	:	100, // JPEG Photo quality (0 - 100) **
	'photoWidth'		:	459, // Photo width **
	'photoHeight'		: 344, // Photo height **
	
	'cameraWidth'		:	640, // Camera source width (tip: should be in increments of 320) **
	'cameraHeight'	:	480, // Camera source height (tip: should be in increments of 240) **
	'cameraFPS'			:	25, // Camera source frames per second **
	
	'timerTimeout'	: 3, // Camera timer length
	'timerX'				: 198, // Camera timer X position on video **
	'timerY'				: 250, // Camera timer Y position on video **
	'timerAlpha'		: 0.6, // Camera timer opacity (0 - 1) **

	'callbacks'			:	{
		'initComplete'			: 'onInitComplete', // Fired when Flash finished initializing the init() function
		'uploadSuccessful'	: 'onUploadSuccessful', // Fired when an upload was successful
		'onError'						:	'onError', // Fired when there was an upload error

		'previewComplete'		:	'onPreviewComplete', // Fired when a snapshot was taken
		'previewCanceled'		: 'onPreviewCanceled', // Fired when a snapshot was dismissed

		'videoStart'				: false, // Fired when a video source started
		'noVideoDevices'		: false, // Fired when no video sources were detected
		'uploadComplete'		: false  // Fired when an upload function was completed
	},

	'placeholders'	:	{
		'load'					:	'/images/openbooth_allow_dev.jpg',  // Placeholder image: Before video started
		'save'					:	'/images/openbooth_saving_dev.jpg', // Placeholder image: While image is uploaded
		'noVideoDevices':	'/images/openbooth_nocameras_dev.jpg' // Placeholder image: When no video devices were detected
	}
};

openbooth.init(options);

OpenBooth supports the following calls:

openbooth.init(options) [Initializes OpenBooth with the given params]
openbooth.camInit() [Starts a video source]
openbooth.startPreviewTimer() [Starts a timer and takes a snapshot]
openbooth.previewPhoto() [Takes a snapshot instantly]
openbooth.cancelPreview() [Dismisses the snapshot, reverts back to video mode]
openbooth.selectCamera() [Pops-up Flash's native Video Source Selection dialog]
openbooth.flashCamera() [Triggers the Camera Flash effect]
openbooth.setBackground(url) [Straps a background image on the Flash element]
openbooth.savePhoto(postvars) [Uploads the snapshot via normal upload; See Upload Section 1. ]
openbooth.savePhotoS3(s3vars) [Uploads the snapshot via a multipart upload; See Upload Section 2. ]


* Upload Section 1: When using the normal upload method, you must pass an object containing the following params:
var postvars = {
	'URL':	'WHERE SHOULD I UPLOAD TO?'
}

* Upload Section 2: When using the S3 upload method, you must pass an object containing the following params:
var s3vars = {
	'policy'				:	'',
	'signature'			: '',
	'acl'						: 'public-read',
	'accessKeyId'		:	'',
	'bucket'				:	'',
	'key'						:	'',
	'extraPostVars'	: { // Supports virtually unlimited extra post variables
		'x-amz-meta-'	:	''
	}
};

* Note: Upon loading the Flash element, OpenBooth will automatically fire a callback function. It is important to know that you cannot change the name of this function: function onFlashReady() { }

Usage Terms
-----------
Released under the MIT license.  We ask for attribution if you are going to use it.  Redistribute freely and feel free to fork and extend!



Happy Snapping!


Copyright (c) 2011 Obsesh Dev Team @ Obsesh.com, released under the MIT license
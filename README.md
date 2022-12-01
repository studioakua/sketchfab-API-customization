    const version = '1.12.1';
        const urlid = '526be2fd9c56426aacc0674548c7f543';
	    const iframe = document.getElementById('api-frame');
        const client = new Sketchfab(version, iframe);
        let api;
        let currentAnnotation;

        const render = () => {
            if (currentAnnotation) {
                const current = 'annotation-' + currentAnnotation;
                document.querySelector('.slide.active').classList.remove('active');
                document.getElementById(current).classList.add('active');
            }
        };

        client.init(urlid, {
		  annotation: 0, // Usage: Setting to [1 – 100] will automatically load that annotation when the viewer starts.
		  animation_autoplay: 1,
		  annotation_tooltip_visible: 0,
			annotations_visible: 1, // Usage: Setting to 0 will hide annotations by default.
		  autospin: 0, // Usage: Setting to any other number will cause the model to automatically spin around the z-axis after loading.
		  autostart: 1, // Usage: Setting to 1 will make the model load immediately once the page is ready, rather than waiting for a user to click the Play button.
		  cardboard: 0, // Usage: Start the viewer in stereoscopic VR Mode built for Google Cardboard and similar devices.
		  camera: 1, // Usage: Setting to 0 will skip the initial animation that occurs when a model is loaded, and immediately show the model in its default position.
		  preload: 1, // Usage: Setting to 1 will force all resources (textures) to download before the scene is displayed.
		  ui_stop: 0, // Usage: Setting to 0 will hide the "Disable Viewer" button in the top right so that users cannot stop the 3D render once it is started.
		  transparent: 0, // Usage: Setting to 1 will make the model's background transparent
		  ui_animations: 0, // Usage: Setting to 0 will hide the animation menu and timeline.
		  ui_annotations: 1, // Usage: Setting to 0 will hide the Annotation menu.
		  ui_controls: 1, // Usage: Setting to 0 will hide all the viewer controls at the bottom of the viewer (Help, Settings, Inspector, VR, Fullscreen, Annotations, and Animations).
		  ui_fullscreen: 1, // Usage: Setting to 0 will hide the Fullscreen button.
		  ui_general_controls: 0, // Usage: Setting to 0 will hide main control buttons in the bottom right of the viewer (Help, Settings, Inspector, VR, Fullscreen).
		  ui_help: 1, // Usage: Setting to 0 will hide the Help button.
		  ui_hint: 0, // Usage: Setting to 0 will always hide the viewer hint animation ("click & hold to rotate"). Setting to 1 will show the hint the first time per browser session (using a cookie). Setting to 2 will always show the hint.
	      ui_color:'FF671D',
		  prevent_user_light_rotation: 1,
		  orbit_constraint_zoom_in: 50,
		  dof_circle: 1,
		  ui_infos: 0, // Usage: Setting to 0 will hide the model info bar at the top of the viewer.
		  ui_inspector: 0, // Usage: Setting to 0 will hide the inspector button.
		  ui_settings: 0, // Usage: Setting to 0 will hide the Settings button.
		  ui_vr: 0, // Usage: Setting to 0 will hide the View in VR button.
		  ui_ar: 0, // Usage: Setting to 0 will hide the View in AR button.
		  ui_watermark_link: 0, // Usage: Setting to 0 remove the link from the Sketchfab logo watermark.
		  ui_watermark: 0, // Usage: Setting to 0 remove the Sketchfab logo watermark.
          
			success: (apiClient) => {
                api = apiClient;
                api.addEventListener('viewerready', () => {
                        // Update the current annotation when the annotation changes
                        api.addEventListener('annotationSelect', (index) => {
                            currentAnnotation = 1 + index;
                            render();
                        });
                });
            },
            error: () => window.console.log('Error while initializing the viewer')
        });

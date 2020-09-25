
<!-- TOC depthfrom:1 orderedlist:true -->

- [1. Generate Android App bundle in Android Studio](#1-generate-android-app-bundle-in-android-studio)
    - [1.1. Create a new Android project](#11-create-a-new-android-project)
    - [1.2. Build AAB](#12-build-aab)
    - [1.3. Validate AAB with bundle tool](#13-validate-aab-with-bundle-tool)
    - [1.4. Generate and sign apks from aab](#14-generate-and-sign-apks-from-aab)
    - [1.5. Install APKs to device with bundletool](#15-install-apks-to-device-with-bundletool)
    - [1.6. Get APK from device](#16-get-apk-from-device)
    - [1.7. Validate its cert](#17-validate-its-cert)

<!-- /TOC -->

# 1. Generate Android App bundle in Android Studio

Google introduced a new way for publishing apps on Google play store. An AAB (Android App Bundle) is a new upload format that contains your app's compiled code and resources. The bundle is entirely different from APK. You can not run the .aab file directly from any Android device. It's a play store compatible file format for binding the resources and compiled codes.

In this tutorial, we are going to bundle an app with a new publishing format aab.

Create an android project, "Hello world" app is enough for creating aab file.

## 1.1. Create a new Android project

1. Install the latest version of Android Studio.
2. In the **Welcome** to Android Studio window, click **Start a new Android Studio project**.
3. In the **Select a Project Template** window, select **Empty Activity** and click **Next**.
4. In the **Configure your project** window, complete the following:
* Enter "Hello World" in the **Name** field.
* Enter "com.example.helloworld" in the **Package name** field.
* If you'd like to place the project in a different folder, change its **Save** location.
* Select either **Java** or **Kotlin** from the **Language** drop-down menu.
* Select the lowest version of Android your app will support in the **Minimum SDK** field. (In my case it was Android 6.0, API 23)
* If your app will require legacy library support, mark the **Use legacy android.support libraries** checkbox.
* Leave the other options as they are.
5. Click **Finish**.

After some processing time, the Android Studio main window appears.

## 1.2. Build AAB

1. Go to **Build** menu , Select **Build Bundle(s) / APK(s)...** and its submenu **Build bundles**.
2. Next you have to click the **locate** link in the pop-up window (App bundle(s) generated successfully for 1 module: Module 'app': locate or analyze the app bundle.). or you can find it the following path inside working directory: HelloWorld/app/build/outputs/bundle/debug/app-debug.aab

In this case we will create an aab without signing. You must do it later: manually or with another tool (e.g. bundletool). 

If you want to use Android Studio built-in signing process with your keystore, do the following (except the previous two steps):
1. Go to **Build** menu , Select **Generate Signed Bundle / APK**
2. Next you have to choose the Android App Bundle radio button. (Default is AAB) Hit next.
3. Select **Create new** from Generate Signed Bundle or APK.
4. Check **Export encrypted key** (Google Play App Signing), Click **Next**. 
5. You have to create a Key Store file, create a new one. 
6. Check the **Export encrypted key** and click the next button.
7. If you preparing for upload to play store, select release from Build Type. Finally click finish.
8. It will generate a signed bundle for uploading to play store. click locate link from Event log.

## 1.3. Validate AAB with bundle tool

```
MacBook-Pro:~ zollak$ bundletool validate --bundle Mobile/AndroidStudioProjects/HelloWorld/app/build/outputs/bundle/debug/app-debug.aab
App Bundle information
------------
Feature modules:
	Feature module: base
		File: res/drawable-hdpi-v4/abc_list_longpressed_holo.9.png
		File: res/drawable-xxhdpi-v4/abc_ic_star_half_black_16dp.png
		File: res/drawable-xhdpi-v4/notification_bg_low_pressed.9.png
		File: root/META-INF/android.arch.lifecycle_viewmodel.version
		File: res/drawable-xxxhdpi-v4/abc_btn_switch_to_on_mtrl_00012.9.png
		File: res/color-v23/abc_btn_colored_text_material.xml
		File: root/META-INF/androidx.loader_loader.version
		File: res/drawable/notification_bg_low.xml
		File: res/drawable-xhdpi-v4/abc_ic_star_black_48dp.png
		File: res/drawable/abc_list_selector_background_transition_holo_light.xml
		File: res/color/abc_primary_text_disable_only_material_dark.xml
		File: res/drawable-xxhdpi-v4/abc_textfield_search_default_mtrl_alpha.9.png
		File: root/META-INF/androidx.interpolator_interpolator.version
		File: res/drawable-hdpi-v4/abc_ic_star_half_black_48dp.png
		File: res/mipmap-hdpi-v4/ic_launcher.png
		File: res/layout/abc_alert_dialog_button_bar_material.xml
		File: res/drawable-xxhdpi-v4/abc_ic_star_black_16dp.png
		File: res/drawable-mdpi-v4/abc_scrubber_primary_mtrl_alpha.9.png
		File: res/drawable-xxxhdpi-v4/abc_ic_menu_cut_mtrl_alpha.png
		File: res/drawable-xhdpi-v4/abc_list_selector_disabled_holo_light.9.png
		File: res/drawable-v24/ic_launcher_foreground.xml
		File: res/drawable-mdpi-v4/abc_list_pressed_holo_dark.9.png
		File: res/drawable-xhdpi-v4/abc_text_select_handle_right_mtrl_dark.png
		File: res/drawable-xxhdpi-v4/abc_list_pressed_holo_dark.9.png
		File: res/drawable/abc_list_selector_background_transition_holo_dark.xml
		File: res/drawable-xhdpi-v4/abc_btn_radio_to_on_mtrl_000.png
		File: res/drawable-hdpi-v4/abc_spinner_mtrl_am_alpha.9.png
		File: res/drawable-hdpi-v4/abc_tab_indicator_mtrl_alpha.9.png
		File: res/drawable/abc_cab_background_top_material.xml
		File: res/drawable-hdpi-v4/abc_btn_check_to_on_mtrl_015.png
		File: res/drawable-xxxhdpi-v4/abc_ic_menu_copy_mtrl_am_alpha.png
		File: res/color/abc_primary_text_material_light.xml
		File: root/META-INF/androidx.slidingpanelayout_slidingpanelayout.version
		File: res/layout/abc_screen_simple_overlay_action_mode.xml
		File: res/drawable-xhdpi-v4/notify_panel_notification_icon_bg.png
		File: res/drawable-xxhdpi-v4/abc_cab_background_top_mtrl_alpha.9.png
		File: res/drawable-xxxhdpi-v4/abc_ic_star_black_48dp.png
		File: res/color/abc_primary_text_disable_only_material_light.xml
		File: res/anim/abc_fade_in.xml
		File: res/layout/activity_main.xml
		File: res/drawable-xhdpi-v4/abc_ic_menu_paste_mtrl_am_alpha.png
		File: res/anim/abc_popup_exit.xml
		File: res/drawable-ldrtl-hdpi-v17/abc_spinner_mtrl_am_alpha.9.png
		File: res/color/abc_search_url_text.xml
		File: res/drawable-mdpi-v4/abc_ic_star_half_black_16dp.png
		File: root/META-INF/androidx.print_print.version
		File: res/drawable-hdpi-v4/abc_text_select_handle_left_mtrl_light.png
		File: res/drawable/notification_icon_background.xml
		File: res/drawable-xhdpi-v4/abc_textfield_activated_mtrl_alpha.9.png
		File: res/mipmap-xxxhdpi-v4/ic_launcher_round.png
		File: res/drawable-mdpi-v4/abc_btn_switch_to_on_mtrl_00012.9.png
		File: res/drawable-xxhdpi-v4/abc_scrubber_control_to_pressed_mtrl_005.png
		File: res/drawable-xxhdpi-v4/abc_text_select_handle_middle_mtrl_dark.png
		File: res/drawable-xxxhdpi-v4/abc_text_select_handle_left_mtrl_light.png
		File: root/META-INF/androidx.legacy_legacy-support-core-utils.version
		File: res/drawable-xhdpi-v4/abc_text_select_handle_left_mtrl_dark.png
		File: res/drawable-xxxhdpi-v4/abc_ic_star_half_black_36dp.png
		File: res/mipmap-anydpi-v26/ic_launcher_round.xml
		File: res/drawable/abc_ratingbar_material.xml
		File: res/drawable-hdpi-v4/abc_cab_background_top_mtrl_alpha.9.png
		File: res/drawable/abc_ic_voice_search_api_material.xml
		File: res/drawable-xhdpi-v4/abc_btn_radio_to_on_mtrl_015.png
		File: res/drawable/abc_ic_ab_back_material.xml
		File: res/drawable-hdpi-v4/abc_ic_star_black_36dp.png
		File: res/drawable-mdpi-v4/notification_bg_low_normal.9.png
		File: res/drawable-hdpi-v4/abc_text_select_handle_middle_mtrl_light.png
		File: res/drawable-hdpi-v4/abc_textfield_search_default_mtrl_alpha.9.png
		File: res/drawable-xhdpi-v4/abc_ic_menu_share_mtrl_alpha.png
		File: res/drawable-hdpi-v4/abc_ic_commit_search_api_mtrl_alpha.png
		File: res/drawable-mdpi-v4/abc_text_select_handle_right_mtrl_dark.png
		File: res/layout/abc_dialog_title_material.xml
		File: res/layout/notification_template_part_time.xml
		File: res/drawable-xxhdpi-v4/abc_ic_star_half_black_48dp.png
		File: res/drawable-hdpi-v4/abc_scrubber_control_off_mtrl_alpha.png
		File: res/color-v23/abc_btn_colored_borderless_text_material.xml
		File: res/drawable-mdpi-v4/abc_spinner_mtrl_am_alpha.9.png
		File: res/drawable-xxxhdpi-v4/abc_scrubber_control_to_pressed_mtrl_000.png
		File: res/drawable-xxhdpi-v4/abc_scrubber_control_off_mtrl_alpha.png
		File: root/META-INF/androidx.coordinatorlayout_coordinatorlayout.version
		File: res/drawable-xhdpi-v4/abc_text_select_handle_right_mtrl_light.png
		File: res/anim/abc_popup_enter.xml
		File: res/drawable-hdpi-v4/abc_list_focused_holo.9.png
		File: res/mipmap-xhdpi-v4/ic_launcher.png
		File: res/drawable-xxhdpi-v4/abc_btn_switch_to_on_mtrl_00001.9.png
		File: res/color/abc_hint_foreground_material_light.xml
		File: res/mipmap-xxhdpi-v4/ic_launcher_round.png
		File: res/color-v23/abc_tint_spinner.xml
		File: res/color/abc_background_cache_hint_selector_material_dark.xml
		File: res/drawable/tooltip_frame_light.xml
		File: res/drawable-mdpi-v4/abc_ic_star_black_36dp.png
		File: res/drawable-xxhdpi-v4/abc_btn_check_to_on_mtrl_000.png
		File: res/layout/abc_search_view.xml
		File: res/drawable-xxhdpi-v4/abc_ic_commit_search_api_mtrl_alpha.png
		File: res/drawable-xhdpi-v4/abc_ic_menu_selectall_mtrl_alpha.png
		File: res/drawable-xhdpi-v4/abc_cab_background_top_mtrl_alpha.9.png
		File: res/drawable-xxxhdpi-v4/abc_btn_switch_to_on_mtrl_00001.9.png
		File: res/drawable-xxhdpi-v4/abc_list_focused_holo.9.png
		File: res/drawable-xhdpi-v4/notification_bg_normal.9.png
		File: root/META-INF/androidx.viewpager_viewpager.version
		File: res/drawable/abc_ic_go_search_api_material.xml
		File: res/drawable-mdpi-v4/abc_ic_menu_paste_mtrl_am_alpha.png
		File: res/drawable-xxhdpi-v4/abc_btn_check_to_on_mtrl_015.png
		File: res/drawable-xhdpi-v4/abc_textfield_search_default_mtrl_alpha.9.png
		File: res/drawable-mdpi-v4/abc_scrubber_track_mtrl_alpha.9.png
		File: res/drawable-xxhdpi-v4/abc_text_select_handle_right_mtrl_light.png
		File: res/drawable-xxxhdpi-v4/abc_switch_track_mtrl_alpha.9.png
		File: res/drawable-ldrtl-xxxhdpi-v17/abc_spinner_mtrl_am_alpha.9.png
		File: res/drawable-xhdpi-v4/abc_ic_star_half_black_48dp.png
		File: res/drawable-ldrtl-mdpi-v17/abc_ic_menu_copy_mtrl_am_alpha.png
		File: res/drawable-xxxhdpi-v4/abc_text_select_handle_left_mtrl_dark.png
		File: res/drawable-mdpi-v4/abc_popup_background_mtrl_mult.9.png
		File: res/layout/abc_popup_menu_item_layout.xml
		File: res/drawable-ldrtl-hdpi-v17/abc_ic_menu_cut_mtrl_alpha.png
		File: res/layout/abc_expanded_menu_layout.xml
		File: res/drawable/abc_ic_clear_material.xml
		File: res/drawable-xhdpi-v4/abc_tab_indicator_mtrl_alpha.9.png
		File: root/META-INF/androidx.swiperefreshlayout_swiperefreshlayout.version
		File: res/drawable-xhdpi-v4/abc_spinner_mtrl_am_alpha.9.png
		File: res/layout/abc_screen_toolbar.xml
		File: res/drawable-xhdpi-v4/abc_scrubber_control_to_pressed_mtrl_000.png
		File: res/drawable/abc_btn_borderless_material.xml
		File: res/layout/abc_alert_dialog_material.xml
		File: res/color-v23/abc_color_highlight_material.xml
		File: res/drawable-xxhdpi-v4/abc_ab_share_pack_mtrl_alpha.9.png
		File: res/mipmap-mdpi-v4/ic_launcher_round.png
		File: res/drawable-xxhdpi-v4/abc_tab_indicator_mtrl_alpha.9.png
		File: res/drawable-xhdpi-v4/abc_text_select_handle_middle_mtrl_dark.png
		File: res/drawable/abc_tab_indicator_material.xml
		File: root/META-INF/androidx.vectordrawable_vectordrawable.version
		File: res/drawable-xxxhdpi-v4/abc_btn_radio_to_on_mtrl_000.png
		File: res/drawable-xhdpi-v4/abc_ic_menu_copy_mtrl_am_alpha.png
		File: res/drawable-xhdpi-v4/abc_textfield_default_mtrl_alpha.9.png
		File: res/drawable-xxhdpi-v4/abc_list_selector_disabled_holo_light.9.png
		File: res/mipmap-mdpi-v4/ic_launcher.png
		File: res/drawable-mdpi-v4/abc_ic_star_black_16dp.png
		File: res/drawable-xhdpi-v4/abc_textfield_search_activated_mtrl_alpha.9.png
		File: res/layout-v21/notification_template_icon_group.xml
		File: res/layout/abc_activity_chooser_view_list_item.xml
		File: res/drawable/abc_vector_test.xml
		File: res/drawable-v24/$ic_launcher_foreground__0.xml
		File: res/drawable-mdpi-v4/abc_cab_background_top_mtrl_alpha.9.png
		File: res/drawable-xhdpi-v4/abc_ic_commit_search_api_mtrl_alpha.png
		File: res/layout/abc_action_bar_title_item.xml
		File: root/META-INF/androidx.appcompat_appcompat.version
		File: res/drawable/abc_btn_check_material.xml
		File: root/META-INF/android.arch.core_runtime.version
		File: res/drawable-v21/notification_action_background.xml
		File: res/drawable-xxhdpi-v4/abc_ic_star_black_48dp.png
		File: res/drawable-xxxhdpi-v4/abc_btn_radio_to_on_mtrl_015.png
		File: res/anim/abc_slide_out_bottom.xml
		File: res/drawable/ic_launcher_background.xml
		File: dex/classes2.dex
		File: res/drawable-xxhdpi-v4/abc_text_select_handle_middle_mtrl_light.png
		File: res/drawable/abc_btn_radio_material.xml
		File: res/drawable-xxxhdpi-v4/abc_ic_menu_share_mtrl_alpha.png
		File: res/drawable-ldrtl-hdpi-v17/abc_ic_menu_copy_mtrl_am_alpha.png
		File: res/drawable-xxhdpi-v4/abc_list_longpressed_holo.9.png
		File: root/META-INF/androidx.documentfile_documentfile.version
		File: res/drawable-hdpi-v4/abc_list_selector_disabled_holo_light.9.png
		File: res/drawable/abc_cab_background_internal_bg.xml
		File: res/layout-v21/notification_action_tombstone.xml
		File: res/drawable/abc_item_background_holo_light.xml
		File: res/drawable-mdpi-v4/notification_bg_low_pressed.9.png
		File: root/META-INF/androidx.legacy_legacy-support-core-ui.version
		File: res/drawable-v21/abc_dialog_material_background.xml
		File: res/drawable-mdpi-v4/abc_textfield_activated_mtrl_alpha.9.png
		File: res/drawable/abc_seekbar_track_material.xml
		File: res/drawable-hdpi-v4/abc_switch_track_mtrl_alpha.9.png
		File: res/drawable-ldrtl-xxxhdpi-v17/abc_ic_menu_cut_mtrl_alpha.png
		File: root/META-INF/androidx.localbroadcastmanager_localbroadcastmanager.version
		File: res/drawable-hdpi-v4/abc_ic_star_half_black_36dp.png
		File: res/drawable-ldrtl-xhdpi-v17/abc_spinner_mtrl_am_alpha.9.png
		File: res/layout/select_dialog_item_material.xml
		File: res/drawable-xhdpi-v4/abc_ic_menu_cut_mtrl_alpha.png
		File: res/drawable-xxhdpi-v4/abc_ic_menu_paste_mtrl_am_alpha.png
		File: res/drawable-mdpi-v4/abc_textfield_search_activated_mtrl_alpha.9.png
		File: res/drawable-xhdpi-v4/abc_list_longpressed_holo.9.png
		File: res/drawable-xxhdpi-v4/abc_spinner_mtrl_am_alpha.9.png
		File: res/drawable-watch-v20/abc_dialog_material_background.xml
		File: res/drawable/abc_text_cursor_material.xml
		File: res/drawable-mdpi-v4/abc_ic_menu_copy_mtrl_am_alpha.png
		File: res/drawable-xxxhdpi-v4/abc_ic_star_black_16dp.png
		File: root/META-INF/androidx.vectordrawable_vectordrawable-animated.version
		File: res/drawable-xhdpi-v4/abc_menu_hardkey_panel_mtrl_mult.9.png
		File: res/drawable-ldrtl-xhdpi-v17/abc_ic_menu_copy_mtrl_am_alpha.png
		File: res/drawable/notification_tile_bg.xml
		File: res/layout/abc_list_menu_item_layout.xml
		File: res/color/abc_secondary_text_material_light.xml
		File: res/color/switch_thumb_material_light.xml
		File: res/drawable-hdpi-v4/abc_list_pressed_holo_light.9.png
		File: res/drawable-mdpi-v4/abc_scrubber_control_off_mtrl_alpha.png
		File: res/anim/abc_slide_out_top.xml
		File: res/layout/abc_list_menu_item_radio.xml
		File: res/layout/abc_screen_simple.xml
		File: res/drawable-mdpi-v4/abc_ab_share_pack_mtrl_alpha.9.png
		File: res/drawable-mdpi-v4/abc_tab_indicator_mtrl_alpha.9.png
		File: res/color-v23/abc_tint_seek_thumb.xml
		File: res/color/abc_hint_foreground_material_dark.xml
		File: res/color-v23/abc_tint_edittext.xml
		File: res/drawable/abc_switch_thumb_material.xml
		File: res/drawable-hdpi-v4/abc_text_select_handle_right_mtrl_light.png
		File: res/layout/abc_action_menu_layout.xml
		File: res/drawable-xhdpi-v4/abc_text_select_handle_left_mtrl_light.png
		File: res/layout/abc_list_menu_item_icon.xml
		File: res/drawable-mdpi-v4/abc_ic_commit_search_api_mtrl_alpha.png
		File: res/drawable-xhdpi-v4/abc_list_divider_mtrl_alpha.9.png
		File: res/drawable-xhdpi-v4/abc_scrubber_control_to_pressed_mtrl_005.png
		File: res/drawable-mdpi-v4/abc_textfield_search_default_mtrl_alpha.9.png
		File: res/drawable-mdpi-v4/abc_text_select_handle_middle_mtrl_light.png
		File: res/drawable-mdpi-v4/abc_scrubber_control_to_pressed_mtrl_005.png
		File: res/drawable-v21/abc_list_divider_material.xml
		File: res/drawable-ldrtl-xxhdpi-v17/abc_spinner_mtrl_am_alpha.9.png
		File: res/drawable-hdpi-v4/abc_ic_menu_cut_mtrl_alpha.png
		File: res/drawable-xxhdpi-v4/abc_list_divider_mtrl_alpha.9.png
		File: res/drawable-mdpi-v4/notify_panel_notification_icon_bg.png
		File: res/drawable-xxhdpi-v4/abc_scrubber_primary_mtrl_alpha.9.png
		File: res/drawable-ldrtl-xxxhdpi-v17/abc_ic_menu_copy_mtrl_am_alpha.png
		File: res/drawable-xhdpi-v4/abc_switch_track_mtrl_alpha.9.png
		File: res/drawable-xxxhdpi-v4/abc_tab_indicator_mtrl_alpha.9.png
		File: res/drawable-hdpi-v4/abc_text_select_handle_middle_mtrl_dark.png
		File: res/drawable-ldrtl-xxhdpi-v17/abc_ic_menu_copy_mtrl_am_alpha.png
		File: res/drawable-hdpi-v4/abc_scrubber_control_to_pressed_mtrl_000.png
		File: res/anim/abc_slide_in_bottom.xml
		File: res/drawable-mdpi-v4/abc_textfield_default_mtrl_alpha.9.png
		File: res/layout/notification_template_part_chronometer.xml
		File: res/drawable-hdpi-v4/abc_ic_star_black_48dp.png
		File: res/drawable-xhdpi-v4/abc_list_pressed_holo_light.9.png
		File: res/drawable-mdpi-v4/notification_bg_normal_pressed.9.png
		File: res/drawable-xxhdpi-v4/abc_ic_star_half_black_36dp.png
		File: res/layout/abc_action_menu_item_layout.xml
		File: res/drawable-xhdpi-v4/abc_list_pressed_holo_dark.9.png
		File: res/drawable-hdpi-v4/abc_ab_share_pack_mtrl_alpha.9.png
		File: res/drawable-hdpi-v4/abc_btn_switch_to_on_mtrl_00001.9.png
		File: res/drawable-xxhdpi-v4/abc_ic_star_black_36dp.png
		File: res/layout/abc_search_dropdown_item_icons_2line.xml
		File: res/drawable-xxxhdpi-v4/abc_ic_star_black_36dp.png
		File: res/drawable-xhdpi-v4/abc_scrubber_control_off_mtrl_alpha.png
		File: res/drawable-xhdpi-v4/abc_list_selector_disabled_holo_dark.9.png
		File: res/drawable-xhdpi-v4/abc_ab_share_pack_mtrl_alpha.9.png
		File: res/drawable-xxxhdpi-v4/abc_ic_star_half_black_48dp.png
		File: res/drawable-xhdpi-v4/notification_bg_low_normal.9.png
		File: res/drawable/abc_seekbar_thumb_material.xml
		File: res/anim/abc_fade_out.xml
		File: res/color/abc_background_cache_hint_selector_material_light.xml
		File: res/drawable-xhdpi-v4/abc_text_select_handle_middle_mtrl_light.png
		File: res/drawable-xxxhdpi-v4/abc_ic_menu_selectall_mtrl_alpha.png
		File: res/drawable-ldrtl-mdpi-v17/abc_ic_menu_cut_mtrl_alpha.png
		File: res/drawable-xhdpi-v4/abc_scrubber_primary_mtrl_alpha.9.png
		File: res/drawable-xxhdpi-v4/abc_ic_menu_copy_mtrl_am_alpha.png
		File: root/META-INF/androidx.customview_customview.version
		File: res/drawable-hdpi-v4/abc_menu_hardkey_panel_mtrl_mult.9.png
		File: res/drawable-v21/abc_edit_text_material.xml
		File: res/drawable-xxxhdpi-v4/abc_scrubber_control_to_pressed_mtrl_005.png
		File: res/drawable-hdpi-v4/abc_ic_menu_paste_mtrl_am_alpha.png
		File: res/drawable-xxxhdpi-v4/abc_btn_check_to_on_mtrl_000.png
		File: res/drawable-mdpi-v4/abc_text_select_handle_left_mtrl_light.png
		File: res/drawable/notification_bg.xml
		File: res/drawable-hdpi-v4/abc_scrubber_track_mtrl_alpha.9.png
		File: res/drawable-hdpi-v4/abc_btn_radio_to_on_mtrl_000.png
		File: res/drawable/abc_ic_arrow_drop_right_black_24dp.xml
		File: res/layout-watch-v20/abc_alert_dialog_button_bar_material.xml
		File: res/drawable/abc_list_selector_holo_light.xml
		File: res/drawable-xhdpi-v4/abc_ic_star_black_36dp.png
		File: res/drawable-mdpi-v4/abc_ic_menu_cut_mtrl_alpha.png
		File: res/drawable-mdpi-v4/abc_btn_radio_to_on_mtrl_015.png
		File: res/drawable-hdpi-v4/abc_ic_star_black_16dp.png
		File: res/drawable-hdpi-v4/abc_popup_background_mtrl_mult.9.png
		File: res/drawable-xhdpi-v4/abc_list_focused_holo.9.png
		File: dex/classes.dex
		File: res/drawable-hdpi-v4/abc_textfield_search_activated_mtrl_alpha.9.png
		File: res/drawable-xxhdpi-v4/abc_switch_track_mtrl_alpha.9.png
		File: res/drawable-mdpi-v4/abc_ic_menu_selectall_mtrl_alpha.png
		File: res/drawable-hdpi-v4/abc_ic_menu_selectall_mtrl_alpha.png
		File: res/drawable-v21/abc_action_bar_item_background_material.xml
		File: root/META-INF/androidx.core_core.version
		File: res/anim/abc_shrink_fade_out_from_bottom.xml
		File: res/drawable-hdpi-v4/abc_textfield_default_mtrl_alpha.9.png
		File: res/layout/select_dialog_multichoice_material.xml
		File: res/drawable-mdpi-v4/abc_btn_radio_to_on_mtrl_000.png
		File: res/drawable-xhdpi-v4/abc_popup_background_mtrl_mult.9.png
		File: res/layout/abc_action_mode_bar.xml
		File: res/drawable-mdpi-v4/notification_bg_normal.9.png
		File: res/drawable-xhdpi-v4/abc_btn_switch_to_on_mtrl_00012.9.png
		File: res/drawable-xxhdpi-v4/abc_list_pressed_holo_light.9.png
		File: res/drawable/abc_item_background_holo_dark.xml
		File: res/drawable-xxhdpi-v4/abc_textfield_search_activated_mtrl_alpha.9.png
		File: res/drawable-mdpi-v4/abc_menu_hardkey_panel_mtrl_mult.9.png
		File: res/drawable-xxhdpi-v4/abc_text_select_handle_left_mtrl_light.png
		File: res/drawable-xhdpi-v4/abc_ic_star_half_black_16dp.png
		File: res/drawable-hdpi-v4/notification_bg_low_normal.9.png
		File: res/drawable-xxhdpi-v4/abc_ic_menu_selectall_mtrl_alpha.png
		File: res/layout-v21/notification_template_custom_big.xml
		File: res/layout/abc_list_menu_item_checkbox.xml
		File: res/layout/abc_popup_menu_header_item_layout.xml
		File: res/color/abc_secondary_text_material_dark.xml
		File: root/META-INF/android.arch.lifecycle_livedata.version
		File: res/drawable-xxxhdpi-v4/abc_btn_check_to_on_mtrl_015.png
		File: res/drawable-hdpi-v4/abc_btn_radio_to_on_mtrl_015.png
		File: res/layout/abc_tooltip.xml
		File: res/drawable-mdpi-v4/abc_ic_menu_share_mtrl_alpha.png
		File: res/drawable-xxhdpi-v4/abc_popup_background_mtrl_mult.9.png
		File: res/drawable-mdpi-v4/abc_list_divider_mtrl_alpha.9.png
		File: res/mipmap-xxxhdpi-v4/ic_launcher.png
		File: res/drawable-mdpi-v4/abc_ic_star_half_black_36dp.png
		File: res/drawable-mdpi-v4/abc_list_selector_disabled_holo_dark.9.png
		File: res/drawable-hdpi-v4/abc_ic_menu_share_mtrl_alpha.png
		File: res/layout/support_simple_spinner_dropdown_item.xml
		File: res/drawable-xxxhdpi-v4/abc_spinner_mtrl_am_alpha.9.png
		File: res/layout-watch-v20/abc_alert_dialog_title_material.xml
		File: res/drawable-xxhdpi-v4/abc_ic_menu_cut_mtrl_alpha.png
		File: res/drawable-xxhdpi-v4/abc_list_selector_disabled_holo_dark.9.png
		File: res/layout/abc_select_dialog_material.xml
		File: res/anim/abc_slide_in_top.xml
		File: res/drawable-hdpi-v4/abc_list_divider_mtrl_alpha.9.png
		File: res/drawable-hdpi-v4/abc_list_pressed_holo_dark.9.png
		File: res/color/abc_primary_text_material_dark.xml
		File: res/drawable-ldrtl-xxhdpi-v17/abc_ic_menu_cut_mtrl_alpha.png
		File: res/drawable-xxhdpi-v4/abc_text_select_handle_right_mtrl_dark.png
		File: res/drawable-xxhdpi-v4/abc_btn_radio_to_on_mtrl_015.png
		File: res/drawable-hdpi-v4/abc_btn_switch_to_on_mtrl_00012.9.png
		File: res/drawable-mdpi-v4/abc_text_select_handle_middle_mtrl_dark.png
		File: res/drawable/abc_ratingbar_indicator_material.xml
		File: res/drawable/abc_textfield_search_material.xml
		File: res/drawable-xxhdpi-v4/abc_ic_menu_share_mtrl_alpha.png
		File: root/META-INF/androidx.drawerlayout_drawerlayout.version
		File: res/drawable-v23/abc_control_background_material.xml
		File: res/drawable-v21/abc_btn_colored_material.xml
		File: res/drawable-xxhdpi-v4/abc_scrubber_control_to_pressed_mtrl_000.png
		File: res/drawable-xxhdpi-v4/abc_menu_hardkey_panel_mtrl_mult.9.png
		File: res/drawable/abc_list_selector_holo_dark.xml
		File: res/drawable-mdpi-v4/abc_list_longpressed_holo.9.png
		File: res/drawable-xxhdpi-v4/abc_btn_radio_to_on_mtrl_000.png
		File: res/drawable-xhdpi-v4/abc_ic_star_half_black_36dp.png
		File: res/drawable-ldrtl-xhdpi-v17/abc_ic_menu_cut_mtrl_alpha.png
		File: res/layout-v26/abc_screen_toolbar.xml
		File: res/anim/abc_tooltip_exit.xml
		File: res/color-v23/abc_tint_default.xml
		File: res/drawable-mdpi-v4/abc_text_select_handle_left_mtrl_dark.png
		File: res/drawable/abc_ratingbar_small_material.xml
		File: res/drawable-mdpi-v4/abc_text_select_handle_right_mtrl_light.png
		File: res/layout/abc_action_bar_up_container.xml
		File: res/drawable/abc_spinner_textfield_background_material.xml
		File: res/layout/abc_cascading_menu_item_layout.xml
		File: res/drawable-ldrtl-mdpi-v17/abc_spinner_mtrl_am_alpha.9.png
		File: res/drawable-hdpi-v4/abc_ic_menu_copy_mtrl_am_alpha.png
		File: res/drawable/abc_ic_search_api_material.xml
		File: res/drawable-hdpi-v4/abc_scrubber_control_to_pressed_mtrl_005.png
		File: res/drawable/abc_ic_menu_overflow_material.xml
		File: res/mipmap-xxhdpi-v4/ic_launcher.png
		File: res/mipmap-anydpi-v26/ic_launcher.xml
		File: res/mipmap-xhdpi-v4/ic_launcher_round.png
		File: res/drawable/tooltip_frame_dark.xml
		File: res/drawable-xxhdpi-v4/abc_scrubber_track_mtrl_alpha.9.png
		File: res/drawable-xxhdpi-v4/abc_textfield_default_mtrl_alpha.9.png
		File: res/drawable-hdpi-v4/abc_scrubber_primary_mtrl_alpha.9.png
		File: res/drawable-xxhdpi-v4/abc_text_select_handle_left_mtrl_dark.png
		File: res/drawable-mdpi-v4/abc_switch_track_mtrl_alpha.9.png
		File: res/drawable-xxxhdpi-v4/abc_ic_star_half_black_16dp.png
		File: res/drawable-mdpi-v4/abc_btn_check_to_on_mtrl_015.png
		File: res/drawable-xxxhdpi-v4/abc_text_select_handle_right_mtrl_dark.png
		File: res/drawable-xhdpi-v4/abc_btn_switch_to_on_mtrl_00001.9.png
		File: root/META-INF/androidx.cursoradapter_cursoradapter.version
		File: res/drawable-hdpi-v4/abc_list_selector_disabled_holo_dark.9.png
		File: res/drawable-xhdpi-v4/abc_btn_check_to_on_mtrl_015.png
		File: root/META-INF/android.arch.lifecycle_livedata-core.version
		File: root/META-INF/androidx.fragment_fragment.version
		File: res/drawable-xxhdpi-v4/abc_textfield_activated_mtrl_alpha.9.png
		File: res/drawable-xhdpi-v4/abc_ic_star_black_16dp.png
		File: res/drawable-mdpi-v4/abc_list_selector_disabled_holo_light.9.png
		File: root/META-INF/androidx.asynclayoutinflater_asynclayoutinflater.version
		File: res/anim/abc_grow_fade_in_from_bottom.xml
		File: res/drawable-mdpi-v4/abc_list_pressed_holo_light.9.png
		File: res/color/switch_thumb_material_dark.xml
		File: res/drawable-xxxhdpi-v4/abc_text_select_handle_right_mtrl_light.png
		File: res/layout/abc_screen_content_include.xml
		File: res/layout-v21/notification_action.xml
		File: res/drawable-hdpi-v4/abc_btn_check_to_on_mtrl_000.png
		File: res/drawable-hdpi-v4/notification_bg_normal_pressed.9.png
		File: root/META-INF/androidx.versionedparcelable_versionedparcelable.version
		File: res/anim/abc_tooltip_enter.xml
		File: res/layout/abc_alert_dialog_title_material.xml
		File: res/mipmap-hdpi-v4/ic_launcher_round.png
		File: res/drawable-xxhdpi-v4/abc_btn_switch_to_on_mtrl_00012.9.png
		File: res/color-v23/abc_tint_switch_track.xml
		File: res/drawable-mdpi-v4/abc_scrubber_control_to_pressed_mtrl_000.png
		File: res/drawable-mdpi-v4/abc_btn_check_to_on_mtrl_000.png
		File: res/drawable-hdpi-v4/notify_panel_notification_icon_bg.png
		File: res/layout/select_dialog_singlechoice_material.xml
		File: res/drawable-hdpi-v4/abc_ic_star_half_black_16dp.png
		File: res/layout/abc_action_mode_close_item_material.xml
		File: res/drawable-mdpi-v4/abc_list_focused_holo.9.png
		File: res/drawable-hdpi-v4/abc_text_select_handle_right_mtrl_dark.png
		File: res/drawable-xhdpi-v4/notification_bg_normal_pressed.9.png
		File: res/drawable-xxxhdpi-v4/abc_ic_menu_paste_mtrl_am_alpha.png
		File: res/drawable-hdpi-v4/abc_text_select_handle_left_mtrl_dark.png
		File: res/drawable-xhdpi-v4/abc_scrubber_track_mtrl_alpha.9.png
		File: res/layout/abc_activity_chooser_view.xml
		File: res/drawable/abc_btn_default_mtrl_shape.xml
		File: res/drawable-mdpi-v4/abc_ic_star_half_black_48dp.png
		File: res/drawable-mdpi-v4/abc_btn_switch_to_on_mtrl_00001.9.png
		File: res/color-v23/abc_tint_btn_checkable.xml
		File: res/drawable-mdpi-v4/abc_ic_star_black_48dp.png
		File: res/drawable-xhdpi-v4/abc_btn_check_to_on_mtrl_000.png
		File: root/META-INF/android.arch.lifecycle_runtime.version
		File: res/drawable-hdpi-v4/abc_textfield_activated_mtrl_alpha.9.png
		File: res/drawable-hdpi-v4/notification_bg_low_pressed.9.png
		File: res/drawable/abc_seekbar_tick_mark_material.xml
		File: res/drawable-hdpi-v4/notification_bg_normal.9.png
```


## 1.4. Generate (and sign) apks from aab
```
MacBook-Pro:app-bundle-sample zollak$ bundletool build-apks --bundle=Mobile/AndroidStudioProjects/HelloWorld/app/build/outputs/bundle/debug/app-debug.aab --output=helloworld.apks
INFO: The APKs will be signed with the debug keystore found at '~/.android/debug.keystore'.
```

## 1.5. Install APKs to device with bundletool
```
MacBook-Pro:app-bundle-sample zollak$ bundletool install-apks --apks=helloworld.apks
The APKs have been extracted in the directory: /var/folders/kk/sy83rkqj66g8qt65jxskzxjh0000gn/T/11490408011002701672
```

## 1.6. Get APK from device
```
MacBook-Pro:app-bundle-sample zollak$ adb shell pm list packages | grep helloworld
package:com.example.helloworld
MacBook-Pro:app-bundle-sample zollak$ adb shell pm path com.example.helloworld
package:/data/app/com.example.helloworld-1/base.apk
package:/data/app/com.example.helloworld-1/split_config.en.apk
package:/data/app/com.example.helloworld-1/split_config.hdpi.apk
MacBook-Pro:app-bundle-sample zollak$ adb pull /data/app/com.example.helloworld-1/base.apk
/data/app/com.example.helloworld-1/base.apk: 1 file pulled, 0 skipped. 5.5 MB/s (1250525 bytes in 0.216s)
MacBook-Pro:app-bundle-sample zollak$ adb pull /data/app/com.example.helloworld-1/split_config.en.apk
/data/app/com.example.helloworld-1/split_config.en.apk: 1 file pulled, 0 skipped. 4.0 MB/s (24922 bytes in 0.006s)
MacBook-Pro:app-bundle-sample zollak$ adb pull /data/app/com.example.helloworld-1/split_config.hdpi.apk
/data/app/com.example.helloworld-1/split_config.hdpi.apk: 1 file pulled, 0 skipped. 4.5 MB/s (51058 bytes in 0.011s)
```

## 1.7. Validate its cert
```
MacBook-Pro:app-bundle-sample zollak$ ~/Library/Android/sdk/build-tools/30.0.1/apksigner verify --verbose --print-certs base.apk | head -n 20
Verifies
Verified using v1 scheme (JAR signing): true
Verified using v2 scheme (APK Signature Scheme v2): true
Verified using v3 scheme (APK Signature Scheme v3): true
Verified using v4 scheme (APK Signature Scheme v4): false
Verified for SourceStamp: false
Number of signers: 1
Signer #1 certificate DN: C=US, O=Android, CN=Android Debug
Signer #1 certificate SHA-256 digest: bec9be42dd5cc2f42cfc4fd6504949e2d587ffdd9aa25de1f76cdc0ab4a2565f
Signer #1 certificate SHA-1 digest: 55f93075aee69b3aff97e98a0088d0b027b0f614
Signer #1 certificate MD5 digest: a930d957b27023365d3f3a3dfc7b7ed7
Signer #1 key algorithm: RSA
Signer #1 key size (bits): 1024
Signer #1 public key SHA-256 digest: 4ef6eaa04e9816cb5209bae09c95539c7ac3b1577ddf74de93bcab44b59254b4
Signer #1 public key SHA-1 digest: 5506e097eab5bf36f08f8be42495e3a510754b02
Signer #1 public key MD5 digest: 606e7f0d0c3c12e9b7a7914c5b191b00
WARNING: META-INF/android.arch.core_runtime.version not protected by signature. Unauthorized modifications to this JAR entry will not be detected. Delete or move the entry outside of META-INF/.
WARNING: META-INF/android.arch.lifecycle_livedata-core.version not protected by signature. Unauthorized modifications to this JAR entry will not be detected. Delete or move the entry outside of META-INF/.
WARNING: META-INF/android.arch.lifecycle_livedata.version not protected by signature. Unauthorized modifications to this JAR entry will not be detected. Delete or move the entry outside of META-INF/.
WARNING: META-INF/android.arch.lifecycle_runtime.version not protected by signature. Unauthorized modifications to this JAR entry will not be detected. Delete or move the entry outside of META-INF/.
```
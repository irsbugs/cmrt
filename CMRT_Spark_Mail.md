# CMRT Spark Mail

Introduction:

Details of inplementing the Mail feature on the Spark Essentials version of CiviCRM.

Original setup:
* The Wordpress website, cmrailtrail.org.au, has a User input form to collect the details for anyone wanting to subscribe to the Newsletter...
 <!-- img width="698" height="702" alt="image" src="/images/newsletter_subscribe_form.png" / -->
 
<img width="500" alt="image_subscribe" src="/images/newsletter_subscribe_form.png" />

```html
			</div><div id="subscribe" class="et_pb_section et_pb_section_2 et_pb_with_background et_section_regular section_has_divider et_pb_top_divider" >
				<div class="et_pb_top_inside_divider et-no-transition"></div>
				
				
				
				
				
				<div id="subscribe" class="et_pb_row et_pb_row_7">
				<div class="et_pb_column et_pb_column_1_2 et_pb_column_13  et_pb_css_mix_blend_mode_passthrough">
				
				
				
				
				<div class="et_pb_module et_pb_signup_0 et_pb_newsletter_layout_left_right et_pb_newsletter et_pb_subscribe clearfix  et_pb_text_align_left et_pb_bg_layout_dark" data-redirect_url="https://cmrailtrail.org.au/thank-you/">
				
				
				
							
				
				<div class="et_pb_newsletter_description"><h2 class="et_pb_module_header">become a  friend and subscribe to our newsletter</h2><div>
<p>Add your voice to the chorus for a trail and stay in touch with the latest news!</p>
</div></div>
				
				<div class="et_pb_newsletter_form">
					<form method="post">
						<div class="et_pb_newsletter_result et_pb_newsletter_error"></div>
						<div class="et_pb_newsletter_result et_pb_newsletter_success">
							<h2>Success!</h2>
						</div>
						<div class="et_pb_newsletter_fields">
							
					<p class="et_pb_newsletter_field et_pb_contact_field_last et_pb_contact_field_last_tablet et_pb_contact_field_last_phone">
						<label class="et_pb_contact_form_label" for="et_pb_signup_firstname" style="display: none;">First Name</label>
						<input id="et_pb_signup_firstname" class="input" type="text" placeholder="First Name" name="et_pb_signup_firstname">
					</p>
							
					<p class="et_pb_newsletter_field et_pb_contact_field_last et_pb_contact_field_last_tablet et_pb_contact_field_last_phone">
						<label class="et_pb_contact_form_label" for="et_pb_signup_lastname" style="display: none;">Last Name</label>
						<input id="et_pb_signup_lastname" class="input" type="text" placeholder="Last Name" name="et_pb_signup_lastname">
					</p>
							
					<p class="et_pb_newsletter_field et_pb_contact_field_last et_pb_contact_field_last_tablet et_pb_contact_field_last_phone">
						<label class="et_pb_contact_form_label" for="et_pb_signup_email" style="display: none;">Email</label>
						<input id="et_pb_signup_email" class="input" type="text" placeholder="Email" name="et_pb_signup_email">
					</p>
							
							
					<p class="et_pb_newsletter_button_wrap">
						<a class="et_pb_newsletter_button et_pb_button" href="#" data-icon="">
							<span class="et_subscribe_loader"></span>
							<span class="et_pb_newsletter_button_text">Subscribe</span>
						</a>
					</p>
							
						</div>
						
						<input type="hidden" value="mailchimp" name="et_pb_signup_provider" />
						<input type="hidden" value="cf8725adbd" name="et_pb_signup_list_id" />
						<input type="hidden" value="cmrailtrail@gmailcom" name="et_pb_signup_account_name" />
						<input type="hidden" value="true" name="et_pb_signup_ip_address" />
						<input type="hidden" value="cdb55eff3f9e3878509289fd1f6656bc" name="et_pb_signup_checksum" />
					</form>
				</div>
			</div>
			</div><div class="et_pb_column et_pb_column_1_2 et_pb_column_14  et_pb_css_mix_blend_mode_passthrough et-last-child">
				
				
				
				
				<div class="et_pb_with_border et_pb_module et_pb_text et_pb_text_9  et_pb_text_align_left et_pb_bg_layout_light">

```

---
layout: article
permalink: supportform.html
title: Support Form
---

To request help, give suggestions, or leave any comment, just fill in
this form and click the \"`Send mail`\" button. You may also send the
information described in the form below to the email address
`support at logtalk.org`.

<form action="https://formspree.io/support@logtalk.org" method="post">
	<div>
	<input type="hidden" name="recipient" value="support@logtalk.org" />
	<input type="hidden" name="subject" value="Logtalk support request" />
	<input type="hidden" name="required" value="realname,email,topic,message" />
	<input type="hidden" name="print_config" value="realname,email" />
	<input type="hidden" name="print_blank_fields" value="1" />
	<input type="hidden" name="return_link_url" value="http://logtalk.org/" />
	<input type="hidden" name="return_link_title" value="Back to the Logtalk web site." />
	<input type="hidden" name="bgcolor" value="#e0e0e0" />
	<input type="hidden" name="text_color" value="#353535" />
	<input type="hidden" name="title" value="Your support request as been sent!" />
	<input type="hidden" name="env_report" value="REMOTE_ADDR">
	</div>
	<p>Name: <input type="text" name="realname" size="24" /></p>
	<p>Email address: <input type="text" name="email" size="24" /></p>
	<p>Organization (optional): <input name="organization" size="48" /></p>
	<p>Topic:<br /> <input name="topic" size="64" /></p>
	<p>Message:<br /> <textarea name="message" cols="64" rows="8"></textarea></p>
	<p><input type="submit" value="Send mail" />&nbsp;&nbsp;<input type="reset" value="Reset form" /></p>
</form>

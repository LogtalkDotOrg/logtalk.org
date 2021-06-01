---
layout: article
permalink: regform.html
title: Registration
---

To register as a Logtalk user, just fill in this form and click the
`Register` button below. You may also send the information described in
the form below to the email address `registration at logtalk.org`.

<form action="https://formspree.io/f/xzbydkyv" method="post">
	<p>First name: <input type="text" name="firstname" size="14" /> Last name: <input type="text" name="lastname" size="14" /></p>
	<p>Email address: <input type="text" name="email" size="28" /> (please check carefully)</p>
	<p><input checked="checked" name="logtalk-news" type="checkbox" /> Please add me to the Logtalk-news (announcements only) mailing list<br/>
	   (low volume; you will receive an automated mail asking for confirmation)</p>
	<p>The remaining fields are optional but important feedback for Logtalk development.</p>
	<p>Organization: <input name="organization" size="40" /></p>
	<p>
		<input checked="checked" name="type" type="radio" value="education" /> Education
		<input name="type" type="radio" value="non-profit" /> Non-profit organization
		<input name="type" type="radio" value="commercial" /> Commercial
		<input name="type" type="radio" value="government" /> Government
	</p>
	<p>In which projects do you plan to use Logtalk:<br /><textarea name="projects" cols="60" rows="4"></textarea></p>
	<dl>
		<dt>Which backend Prolog compilers do you plan to use:</dt>
			<!--<dd><input name="als" type="checkbox" /> ALS Prolog</dd>-->
			<!--<dd><input name="amzi" type="checkbox" /> Amzi! Prolog</dd>-->
			<dd><input name="bp" type="checkbox" /> B-Prolog</dd>
			<!--<dd><input name="bin" type="checkbox" /> BinProlog</dd>-->
			<!--<dd><input name="ciao" type="checkbox" /> Ciao Prolog</dd>-->
			<dd><input name="cxprolog" type="checkbox" /> CxProlog</dd>
			<dd><input name="eclipse" type="checkbox" /> ECLiPSe</dd>
			<!--<dd><input name="ifprolog" type="checkbox" /> IF/Prolog</dd>-->
			<!--<dd><input name="jiprolog" type="checkbox" /> JIProlog</dd>-->
			<!--<dd><input name="plc" type="checkbox" /> K-Prolog</dd>-->
			<dd><input name="gprolog" type="checkbox" /> GNU Prolog</dd>
			<dd><input name="ji" type="checkbox" /> JIProlog</dd>
			<dd><input name="lvm" type="checkbox" /> LVM</dd>
			<!--<dd><input name="open" type="checkbox" /> Open Prolog</dd>-->
			<!--<dd><input name="plII" type="checkbox" /> PrologII</dd>-->
			<!--<dd><input name="qp" type="checkbox" /> Qu-Prolog</dd>-->
			<dd><input name="quintus" type="checkbox" /> Quintus Prolog</dd>
			<dd><input name="scryer" type="checkbox" /> Scryer Prolog</dd>
			<dd><input name="sicstus" type="checkbox" /> SICStus Prolog</dd>
			<dd><input name="swipl" type="checkbox" /> SWI-Prolog</dd>
			<dd><input name="tau" type="checkbox" /> Tau Prolog</dd>
			<dd><input name="tpl" type="checkbox" /> Trealla ProLog</dd>
			<dd><input name="yap" type="checkbox" /> YAP</dd>
			<dd><input name="xsb" type="checkbox" /> XSB</dd>
			<dd><input name="otherpl" type="checkbox" /> Others</dd>
	</dl>
	<dl>
		<dt>In which operating-systems:</dt>
			<dd><input name="macosx" type="checkbox" /> macOS</dd>
			<dd><input name="windows" type="checkbox" /> Windows</dd>
			<dd><input name="unix" type="checkbox" /> Linux/BSD/Unix</dd>
			<dd><input name="otheros" type="checkbox" /> Others</dd>
	</dl>
	<p><input type="submit" value="Register" />&nbsp;&nbsp;<input type="reset" value="Reset form" /></p>
</form>

Thanks for registering! You should receive a confirmation message later.

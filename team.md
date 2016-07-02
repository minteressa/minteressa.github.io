---
position: 2
layout: page
title: Project Team
permalink: team/
published: true
---
## Tutor
<div class="row">
	<div class="col-md-4 col-md-offset-4">
		<div class="col-xs-12 text-center">
			<img class="img-responsive" src="{{site.data.members.lead.photo}}" alt="{{site.data.members.lead.name}}" height="200" width="200"/>
		</div>
		<div class="col-xs-12 text-center">
			{{site.data.members.lead.name}}
		</div>
		<div class="col-xs-2 col-xs-offset-3">
			<a href="{{site.data.members.lead.twitter || '#'}}" target="_new"><i class="fa fa-twitter"></i></a>
		</div>
		<div class="col-xs-2">
			<a href="{{site.data.members.lead.github || '#'}}" target="_new"><i class="fa fa-github"></i></a>
		</div>
		<div class="col-xs-2">
			<a href="{{site.data.members.lead.linkedin || '#'}}" target="_new"><i class="fa fa-linkedin"></i></a>
		</div>
	</div>
</div>

## Team members
<div class="row">
	{% for member in site.data.members.team %}
		<div class="col-md-4 col-sm-6 col-xs-12" style="margin-top: 3em">
			<div class="row">
				<div class="col-xs-12 text-center">
					<img class="img-responsive" src="{{member.photo}}" alt="{{member.name}}" height="200" width="200" align="middle"/>
				</div>
				<div class="col-xs-12 text-center">
					{{member.name}}
				</div>
				<div class="col-xs-2 col-xs-offset-3">
					<a href="{{member.twitter || '#'}}" target="_new"><i class="fa fa-twitter"></i></a>
				</div>
				<div class="col-xs-2">
					<a href="{{member.github || '#'}}" target="_new"><i class="fa fa-github"></i></a>
				</div>
				<div class="col-xs-2">
					<a href="{{member.linkedin || '#'}}" target="_new"><i class="fa fa-linkedin"></i></a>
				</div>
			</div>
		</div>
	{% endfor %}
</div>

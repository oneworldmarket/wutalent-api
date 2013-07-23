\WU_API::registerTimelineType( $timeline_type, $timelineClass )
===

Registers a handler class for timeline records of your plugin. Be sure to write this code in `init` area of your plugin.

Parameters:
 * `$timeline_type` - type of your timeline records. Should be starting from 'plugin_'
 * `$timelineClass` - your timeline handler class. Description is given bellow here

Timeline class methods:
 * `init( $paramsObject )` - this is the msot important method and acts like constructor. Params for timeline get passed through `$paramsObject` object in params
 * `getImage` - timeline image (icon in the left side)
 * `getHeader` - timeline record header
 * `getSubHeader` - timeline record subheader
 * `getLinkText` - timeline record link text
 * `getLinkUrl` - timeline record link url

Example:

```
<?php

//interaction area (/c/developer)

class timelineClass
{
	protected $params;
	protected $contact;

	public function init( $paramsObject )
	{
		$this->params = $paramsObject;

		$this->contact = \WU_API::apiCall('contacts/get',
										  array('id' => $this->params['contact_id']));
	}

	public function getImage()
	{
		return '/static/images/plugin/icon-video-interview-timeline.png';
	}

	public function getHeader()
	{
		return 'Video Interview completed by: ' . $this->contact['name'];
	}

	public function getSubHeader()
	{
		return 'Completed "' . $this->params['interview_title'] . '"';
	}

	public function getLinkText()
	{
		return 'View interview...';
	}

	public function getLinkUrl()
	{
		$appId = \WU_API::_getAppId();
		$accId = \WU_API::_getAccountId();
		$params = "id={$this->params['contact_id']}&candidate={$this->params['remote_id']}&account_id=" . $accId;
		return "/c/applications/public?appId=$appId&params=" . rawurlencode( $params );
	}
}

\WU_API::registerTimelineType('plugin_videointerview', 'timelineClass');
```
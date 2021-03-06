pytest-testrail
=================

[![Build Status](https://travis-ci.org/dubner/pytest-testrail.svg?branch=master)](https://travis-ci.org/dubner/pytest-testrail)


This is a pytest plugin for creating testruns based on pytest markers.
The results of the collected tests will also be updated against the testrun in TestRail.

Installation
------------

    pip install pytest-testrail


Configuration
-------------

Add a marker to the tests that will be picked up to be added to the run. If the test is not part of the suite, it will raise an exception and let you know which test is not part of the suite.

	from pytest_testrail.plugin import testrail

	@testrail('C1234', 'C5678')
	def test_foo():
		# test code goes here

Settings file template cfg:

	[API]
	url = https://yoururl.testrail.net/
	email = user@email.com
	password = password

	[TESTRUN]
	assignedto_id = 1
	project_id = 1
	suite_id = 1

Usage
-----
	py.test --testrail=<settings file>.cfg

This will create a test run in TestRail, add all marked tests to run.
Once the all tests are finished they will be updated in TestRail.

	--tr_name='My Test Run'

Testruns can be named using the above flag, if this is not set a generated one will be used.
' Automation Run "timestamp" '

	--no-ssl-cert-check

This flag can be used prevent checking for a valid SSL certificate on TestRail host.

	--update-existing-run
	
This flag will check for a run with the same name as the one provided and will update that run instead of creating a new one.
It will also add results to a testrun that were not part of the test run.	

	--close-on-complete

This flag will close a run if all tests have been passed and there are no untested tests. It is not compatible with the --update-existing-run flag.	

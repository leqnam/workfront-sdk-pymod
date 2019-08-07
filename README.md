Workfront-SDK-pyMod for Python
==========================

![PyPI](https://img.shields.io/pypi/v/1?label=workfront-sdk-pymod) based on ![image](https://img.shields.io/pypi/v/workfront-sdk.svg)

This SDK for managing Workfront tasks, user and project with API upgraded to v11.0 although the original for Workfront API v7.0. 

Installation
------------

Install from source:

```
git clone https://github.com/leqnam/workfront-sdk-pymod.git
cd workfront-sdk-pymod
python setup.py install
```

Examples
--------

How to create a Workfront Service object
----------------------------------------

Create the Workfront object and login:

```
>>> from workfront import Workfront
>>> wf = Workfront("your_email@your_company.com", "your_pwd")
>>> wf.login()
```

Then you can use it.

How to create a user object
---------------------------

With a Workfront service object, you can create a user by email or by
id:

```
>>> from workfront.objects import user
>>> user_by_email = user.from_email(wf, "your_email@your_company.com")
>>> user_by_id = user.from_id(wf, "<WORKFRONT_USER_ID>")
```

You can then access some fields of the users:

```
>>> print user_by_email.wf_id # print the workfront id
>>> print user_by_email.name # print the name of the user
>>> print user_by_email.emailAddr # print the email of the user
```

How to use projects
-------------------

Create project:
```
>>> from workfront.objects import project
>>> new_project = project.create_new(wf, {"name": "Sample Project from SDK"})
>>> new_project.wf_id

```

You can load a project from the id, and access the template id:

```
>>> from workfront.objects import project
>>> p = project.WFProject(wf, "<WF_PROJECT_ID>")
>>> project_template_id = p.get_template_id()
```

With the template id, you can create another project:

```
>>> from workfront.objects import project
>>> new_project = project.crt_from_template(wf, project_template_id, "NEW PROJECT NAME")
>>> new_project.wf_id
```

How to create and interact with a Task
--------------------------------------

Create the task by it's workfront id and giving a Workfront service

```
>>> from workfront.objects.task import WFTask
>>> task = WFTask(wf, "<WF_TASK_ID>")
```

Change the status of a task
---------------------------

```
>>> from workfront.objects.status import WFTaskStatus
>>> task.set_status(WFTaskStatus.in_progress)
```

Assign a task to a different user
---------------------------------

Once you have a WF user and a task you can:

```
>>> from workfront.objects import user
>>> from workfront.objects.task import WFTask
>>> user_by_email = user.from_email(wf, "your_email@your_company.com")
>>> task = WFTask(wf, "<WF_TASK_ID>")
>>> task.assign_to_user(user_by_email)
```

Get and set custom fields
-------------------------

You can use the methods **set\_param\_values** and
**get\_param\_values** to modify and access task custom fields.

```
>>> task = WFTask(wf, "<WF_TASK_ID>")
>>> task.get_param_values()
>>> {"custom_field": "value", "list_field": ["value1", "value2"]}
>>> task.set_param_values({"custom_field": "other_value"})
>>> task.get_param_values()
>>> {"custom_field": "other_value", "list_field": ["value1", "value2"]}
```


## License
- [pypi workfront-sdk](https://pypi.org/project/workfront-sdk), see README.rst
- [workfront-sdk-0.22.1.tar.gz](https://pypi.org/project/workfront-sdk/#files)
- [workfront-sdk](https://github.com/BridgeMarketing/workfront-sdk.git)

GPL, Bridge at info@bridgecorp.com

## Upgrade
on Aug 06 2019,

Nam Le, leqnam@live.com

http://nready.net
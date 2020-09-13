---
layout: post
title:  "using python and jinja2 for templating Hashicorp Nomad job files"
date:   2020-09-13 12:00:00 -0000
tags: hashicorp nomad python jinja2
---

I work on a project that has adopted [Hashicorp's Nomad](https://www.nomadproject.io/) as a job scheduler to orchestrate both Windows-based executables and Docker containers.  Given the need to support mulitple environments, we were faced with duplicating our job files (since at least the `datacenter` property needs up dated per environment.  Finding a template language and code to do replacements became important to reduce duplication.

### Templating Solution 

[Jinja2 templates](https://palletsprojects.com/p/jinja/) were a good solution for this given it's a a mature templating solution and easily implemented with python.  Support for usability outside of web pages, default functions, loops, and conditionals were awesome features we needed.  

### Example Template

This job file does not have a template.  The datacenter property is the first key problem.  Here's what it looks like without the temp.ate
```
job "login-web-server" {
  datacenters = ["this-is-the-name-of-your-datacenter"]

  group "login-group" {
    task "web-server" {
```

The datacenter property makes it so the job file only can be used for one environment.  but once you have it templated like below, you can just specify it once in the template and built out full files for submission.  For this example, we picked `@{obj.}` as our templating special characters.  The python gets easier with the `obj` part so you can bind an object to the template.

```
job "login-web-server" {
  datacenters = ["@{obj.datacenter}"]

  group "login-group" {
    task "web-server" {
```

<br>

### Where is the data coming from for the template?

We used json files.  They can be easily read by python into a dictionary and bound to the jinja2 template.  Here's an example file. Notice the property name is the same as the property after `obj.` above.  

``` js
//data.json
{
    datacenter: "us-west-1"
}
```

### How does the data get bound to the template

The following code loads up your json file, sets up the jinja2 template, and renders.

```py
with open('data.json') as json_file, open("job-template.hcl") as template:
    data = json.load(json_file)
    loader = DictLoader({templateName: template.read()}), variable_start_string="{$", variable_end_string="$}") # create template loader with our specific variable annotations
    env = Environment(loader=loader)
    job_file_with_data = env.get_template("new_template_name").render(ch=data) # create the merged job file

```
### Schedule your process with the new job file

You can now submit the newly created file to your nomad cluster to scheudle your process.  I highly recommend [this library](https://github.com/jrxfive/python-nomad) for a nomad client.  It encapsulates the API calls really well.  Submitting a job is as simple as

```py
n = nomad.Nomad(host="172.16.100.10", timeout=5)
n.job.register_job("job_name", job_file_with_data)
```

----
**resources:**
* [https://www.nomadproject.io/](https://www.nomadproject.io/)
* [https://palletsprojects.com/p/jinja/](https://palletsprojects.com/p/jinja/)
* [https://pypi.org/project/Jinja2/](https://pypi.org/project/Jinja2/)
* [https://github.com/jrxfive/python-nomad](https://github.com/jrxfive/python-nomad)
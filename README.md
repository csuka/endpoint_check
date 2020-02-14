# Check decency of endpoints with Ansible

There was a need to check whether public endpoints are responding in a decent manner.

Thus, I created this simple playbook. It supports the following:

 * Check whether URL's are providing status code 200
 * Includes the reaction time from the host to the server
 * Sending Slack message when failed
 * Send the logs to an Elasticsearch server

One could set a cronjob to let the playbook run each x seconds.

### ./run

The playbook is run from localhost.

 * Tested on Ansible 2.9.1
 * Ensure the host can reach the public endpoints (Firewall)

Edit the `vars` in the playbook to edit sites to check.

```
$ ansible-playbook playbook.yml
```

The script writes the output of the request to a file, named `file.txt`.

Example output:

```bash
2020-02-12T16:02:52Z, https://www.google.com/, 200, 0.228038
2020-02-12T16:02:52Z, https://test.com, -1, 0.000000
```

### ELK

The file `filebeat.yml` contains the configuration to send the logs to Elasticsearch. 

Edit it accordingly, and let Filebeat run.


### Changelog

 * v1.0 - Initial release

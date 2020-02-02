# sysb.AI | access your localhost
Front page of [https://www.sysb.ai](https://www.sysb.ai)

## How to access my local web application over internet?

If you have a web application running perfectly in your laptop and now you have a need to have a functionality where you want it to share with someone over internet. Assuming your web application is accessible locally at `http://localhost:8080` then all you need to do is the following

1. Open the terminal
1. Run the following command
    1. `ssh -R 0:localhost:8080 demo@sysb.ai`
    1. Here `-R` is the remote port forwarding flag
    1. `0:` tells to dynamically allocate a remote port in sysb.ai which will have connection to `localhost:8080` locally
        1. There are many folks who use sysb.ai and to ensure that there is no conflict on the assigned remote port then we should get a request for a dynamic port.
        1. Irrespective of any dynamic assigned port on the remote server, You would be able to access your web application over HTTP and HTTPS on port 80 and 443 respectively
    1. `demo` the free user account which allows following entitlements
        1. 1 free tunnel
        1. 1 TCP protocol support
        1. Dynamic SUBDOMAIN to sysb.ai
    1. `sysb.ai` is our intelligent infrastructure which help you to access your localhost
     
1. Above command will give you a dynamic HTTP and HTTPS which you can use to access your local web application over internet

## How to add `Host:`  header?

It is possible that while using the sysb.AI platform you can customize on which host header should come to your localhost web application. You only need to do the followings
1. `export SYSB_HOST_HEADER=my_cool_web_app.com`
1. `ssh -o SendEnv=SYSB_HOST_HEADER -R 0:127.0.0.1:8080 demo@sysb.ai`
Or we can do using `~/.ssh/config` file

```
Host sysb.ai
  SetEnv SYSB_SUBDOMAIN=my-awesome-subdomain SYSB_HOST_HEADER=my-header
  ServerAliveInterval 300
  ServerAliveCountMax 3
  ```
Here we also recommened to put the directives like `ServerAliveInterval` and `ServerAliveCountMax` which will protect the idle session from getting disconnected

## How to access my TCP application over internet?

It is quite possible that you may want to expose some other TCP based application over internet and you just need an endpoint which is accessible publicly. Like you probably just want to have your IoT device like Raspberry PI sshable. It is absolutely simple to do that. All you need to do the following

1. Open the terminal
1. Run the following command
    1. `ssh -R 0:localhost:22 demo@sysb.ai`
1. Above command will give a dynamic URL which can be accessed publicly to ssh your Raspberry PI. Please keep special attention to dynamic port number. You need both public FQDN and port number to access your TCP application like following
    1. After running the above command you may get one of the TCP port forwarding request like `tcp://sysb.ai:28559` and now you can access it as `ssh sysb.ai -p 28559`

## How to stop the port forwarding

If you are using terminal then `ctrl+c` is your friend to stop the port forwarding

## Does it support HTTP2 or HTTPS protocol?

Yes, by default it support secure HTTP and next gen HTTP2 protocol.

## What is tunneling by the way?

In simple term a connection with a connection or a private connection in the public internet.

## SSH Tips and Tricks

Since we can use native SSH clients preinstalled in Linux, Unix and Mac OS so most of the options of the `ssh` like compression and background processing is supported.

## Here is the list of frequently asked questions

1. How can we report the issue or request for your feature
    1. You can raise a github issue at https://github.com/systembee/sysb.AI/issues to report a issue or request for a feature.
1. I am wondering if there a mailing list which we can join to discuss new features and enhancement?
    1. Yes you can join our [Google group](https://groups.google.com/forum/#!forum/sysb_ai) mailing list to discuss new feature and enhancement
1. How can I get static subdomain of sysb.ai?
    1. This feature is in development and yet to be released officially though you can still use this feature and let us know what you think. You can use below config in your `~/.ssh/config` and put value of SYSB_SUBDOMAIN and SYSB_HOST_HEADER accordingly
    1. ```Host sysb.ai
  SetEnv SYSB_SUBDOMAIN=my-awesome-subdomain SYSB_HOST_HEADER=my-header
  ```
1. Why I am not able to access old URL given by sysb.AI
    1. All the subdomain provided while tunneling is ephermeral which is active till your particular tunneling is active
1. My internet is damn slow and I am getting frequent disconnection
    1. We advice you to use `-C` in your ssh client flags as it will compress the data being used in the connection. Though, it will only slow down things on fast networks. So I advice to use only when network is damn slow. Syntax is as follows:
        1. `ssh -CR 0:127.0.0.1:8080 demo@sysb.ai`
        1. Keep notice on `-C` flag
1. What kind of environment variables are supported?
Currenly below two environemtn variable is supported though this feature is in development
    1. SYSB_HOST_HEADER
    1. SYSB_SUBDOMAIN
We can use this feature like below:
    1. `export SYSB_HOST_HEADER=demo.sysb.ai`
    1. `export SYSB_SUBDOMAIN=demo.sysb.ai`
        1. `SYSB_SUBDOMAIN` is in development
    1. `ssh -o SendEnv=SYSB_HOST_HEADER -R 0:127.0.0.1:8080 demo@sysb.ai `
1. Does it support windows
    1. Yes, you can use `putty` like ssh client which has option to do remote port forwarding
1. How do we proniciate sysb.ai?
    1. it is 'sisbi dot ai'

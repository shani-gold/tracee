# Configuring Tracee

Tracee has many different options and settings that control how Tracee operates. 
This section presents available configuration options. To learn about how to apply configuration to Tracee, please refer to the [CLI](./cli.md) or [Kubernetes](./kubernetes.md) specific guides.

A complete config file with all available options can be found [here](https://github.com/aquasecurity/tracee/blob/main/examples/config/global_config.yaml). Most of the options are documented in different sections in the documentation.

```yaml
blob-perf-buffer-size: 1024
cache:
    type: none
    size: 1024

proctree:
    source: none
    cache:
        process: 8192
        thread: 4096

capabilities:
    bypass: false
    add:
        - cap_sys_admin
        - cap_syslog
    drop:
        - cap_chown

cri:
    - runtime:
        name: containerd
        socket: /var/run/containerd/containerd.sock
    - runtime:
        name: docker
        socket: /var/run/docker.sock

healthz: false
install-path: /tmp/tracee
listen-addr: :3366
log:
    level: info
    file: "/path/to/log/file.log"
    aggregate:
        enabled: true
        flush-interval: "5s"
    filters:
        libbpf: false
        in:
        msg:
            - SampleMessage1
            - SampleMessage2
        pkg:
            - package1
            - package2
        file:
            - file1.go
            - file2.go
        level:
            - warn
            - error
        regex:
            - ^pattern1
            - ^pattern2
        out:
        msg:
            - ExcludedMessage1
        pkg:
            - excludedPackage
        file:
            - excludedFile.go
        level:
            - debug
        regex:
            - ^excludedPattern

metrics: false
output:
    json:
        files:
            - stdout

    table:
        files:
            - /path/to/table1.out
            - /path/to/table2.out

    table-verbose:
        files:
            - stdout

    gob:
        files:
        - /path/to/gob1.out

    gotemplate:
        template: /path/to/my_template1.tmpl
        files:
            - /path/to/output1.out
            - /path/to/output2.out

    forward:
        - forward1:
            protocol: tcp
            user: user
            password: pass
            host: 127.0.0.1
            port: 24224
            tag: tracee1
        - forward2:
            protocol: udp
            user: user
            password: pass
            host: 127.0.0.1
            port: 24225
            tag: tracee2

    webhook:
        - webhook1:
            protocol: http
            host: localhost
            port: 8000
            timeout: 5s
            gotemplate: /path/to/template/test.tmpl
            content-type: application/json
        - webhook2:
            protocol: http
            host: localhost
            port: 9000
            timeout: 3s
            gotemplate: /path/to/template/test.tmpl
            content-type: application/json

    options:
        none: false
        stack-addresses: true
        exec-env: false
        relative-time: true
        exec-hash: false
        parse-arguments: true
        sort-events: false

perf-buffer-size: 1024
pprof: false
pyroscope: false
rego:
    partial-eval: true
    aio: true
signatures-dir: ""
```

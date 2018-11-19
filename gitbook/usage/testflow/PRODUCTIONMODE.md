# Test flow in production mode

###  Login router and download powter-client testflow packages
```bash
wget https://github.com/hilanderas/powter-client/releases/download/0.4.3/powter-client-testflow-0.4.3.zip
unzip powter-client-testflow-0.4.3.zip
```
[Check releases page for other versions](https://github.com/hilanderas/powter-client/releases)

### Download powter-client packages
```bash
cd powter-client-testflow
make download ARCH=[ARCH]
```
`ARCH`: x86 or armv6

### Config test environment
* Update `info.yml` and `info_slave.yml` in `powter-client-testflow` to meet your test environment

* Set project path, info file path and lan port 
```bash
make config PROJ=[PROJECT] INFO=[INFO] LAN=[LAN]
```
Description of each attribute:
* `PROJ`: Path of `power-client/client`
* `INFO`: Absolute path of `info.yml`
* `LAN`: Lan port of router

	e.g,
```bash
make config PROJ=$PWD/powter-client-x86 INFO=$PWD/info.yml LAN=br0
```

* Check configuration
```bash
make -s read_config
```

### Run test flow
* Preparation before test
```bash
make test_prepare
```

* Run scenarios
```bash
make [SCENARIO]
```
`SCENARIO:` Name of a test scenario, you can enter `make` and `tab` to see the whole lists.
	e.g,
* Install
```bash
make test_install
```

* Uninstall
```bash
make test_uninstall
```

* Switch vps test

	Prepare info_slave.yml, the main different between info.yml and info_slave.yml is the dns server IP and sskcp IP. In this scenario, we assume that dns server and sskcp server are the same and we want to switch them to another groups and switch back again.
```bash
make test_switch SLAVE=[SLAVE]
```
`SLAVE`: slave info.yml 

	e.g,
```bash
make test_switch SLAVE=/home/qa/info_slave.yml
```

* Clean up
```bash
make cleanup
```
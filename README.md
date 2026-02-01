# SSL Certificate Discovery Tool

A Java Swing application that scans IP addresses and ports to discover SSL/TLS
certificates and report key details such as certificate name, issuer, and
expiration date. The tool is designed for quickly inventorying certificates
across internal or external network ranges.

## Features

- Scan a single host, multiple hosts, or IP ranges for SSL/TLS certificates.
- Scan a single port or a port range, or leave the port field empty to scan the
  default range used by the application.
- Displays discovered certificates in a table with server name, certificate
  common name, expiration date, and issuer.
- Configurable thread count and HTTPS timeout via `application.properties`.

## Requirements

- Java 8 or later
- Maven 3.x (for building from source)

## Build

```bash
mvn clean package
```

The build produces a runnable JAR using the main class
`network.scan.ssl.discovery.ui.SSLDiscover`.

## Run

### From Maven

```bash
mvn exec:java
```

### From the packaged JAR

```bash
java -jar target/SSLCertificateDiscoveryTool-1.0.0.jar
```

> Note: The repo also includes a prebuilt distribution under
> `SSL Certificate Discovery Tool - v1.0 Apps/` that contains a runnable JAR,
> dependencies, and example configuration files.

## Usage

1. Enter one or more IP addresses or hostnames in **IP Address / Url**.
   - Single host: `192.168.1.10`
   - Comma-separated hosts: `192.168.1.10,192.168.1.20`
   - IP range: `192.168.1.10-192.168.1.25`
   - Mixed comma + range: `192.168.1.10-192.168.1.25,10.0.0.1`
2. Enter a port or port range in **Port**.
   - Single port: `443`
   - Range: `443-450`
   - Leave blank to scan the default port range.
3. Click **Search** to begin scanning. Results populate in the table.

## Configuration

Configuration is read from `src/main/resources/application.properties`:

- `application.threadcount`: number of worker threads (default `10`)
- `application.report.name`: report filename (default `SSL Scan Report.xls`)
- `application.https.timeout`: HTTPS timeout in milliseconds (default `1000`)

## Logging

Log4j configuration lives in `src/main/resources/log4j.properties` and writes
both to stdout and to `log/loging.log` in the working directory.

## Project Structure

- `src/main/java/network/scan/ssl/discovery/ui/SSLDiscover.java`: Swing UI and
  scan orchestration
- `src/main/java/network/scan/ssl/discovery/utils/SSLSearcher.java`: SSL/TLS
  discovery logic
- `src/main/java/network/scan/ssl/discovery/utils/ThreadManager.java`: worker
  pool and task dispatch
- `src/main/resources/`: configuration and assets

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE).

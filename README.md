# piped-proxy

## Description

piped-proxy is a high-performance proxy server written in Rust, designed to work with the Piped video streaming platform. It serves as a replacement for the [http3-ytproxy](https://github.com/TeamPiped/http3-ytproxy) project, offering improved functionality and efficiency.

Key features include:
- Video playback proxying
- Image transcoding to WebP and AVIF formats
- Custom UMP (Unknown Media Protocol) stream transformation
- Support for various content types including HLS and DASH manifests
- Configurable via environment variables
- Docker support for easy deployment

## Installation

### Prerequisites

- Rust 1.56 or later
- Cargo (Rust's package manager)

### Building from source

1. Clone the repository:
   ```
   git clone https://github.com/TeamPiped/piped-proxy.git
   cd piped-proxy
   ```

2. Build the project:
   ```
   cargo build --release
   ```

3. The compiled binary will be available at `target/release/piped-proxy`

### Using Docker

1. Build the Docker image:
   ```
   docker build -t piped-proxy .
   ```

2. Run the container:
   ```
   docker run -p 8080:8080 piped-proxy
   ```

## Usage

### Running the server

To start the server, run:

```
./piped-proxy
```

By default, the server listens on `0.0.0.0:8080`. You can configure the binding address and port using environment variables.

### Configuration

The following environment variables can be used to configure the proxy:

- `BIND`: Set the binding address and port (default: `0.0.0.0:8080`)
- `UDS`: Use Unix Domain Socket instead of TCP
- `BIND_UNIX`: Set the Unix Domain Socket path (default: `./socket/actix.sock`)
- `PROXY`: Set a proxy server for outgoing requests
- `PROXY_USER` and `PROXY_PASS`: Set proxy authentication credentials
- `IPV4_ONLY`: Force IPv4 for outgoing connections
- `HASH_SECRET`: Set a secret for query hash validation
- `DISALLOW_IMAGE_TRANSCODING`: Disable image transcoding features

### API Usage

The proxy server accepts GET and HEAD requests with the following query parameters:

- `host`: The target host to proxy the request to (required)
- `rewrite`: Enable or disable URL rewriting in responses (default: true)
- `qhash`: Query hash for request validation (if `HASH_SECRET` is set)
- `avif`: Enable AVIF image transcoding (if supported)

Example request:
```
http://localhost:8080/path/to/resource?host=example.com&rewrite=true
```

## Dependencies

Main dependencies include:

- actix-web: Web framework
- tokio: Asynchronous runtime
- reqwest: HTTP client
- image: Image processing
- libwebp-sys: WebP encoding
- ravif: AVIF encoding
- blake3: Hashing algorithm

For a complete list of dependencies, refer to the `Cargo.toml` file.

## Contributing

Contributions to piped-proxy are welcome. Please follow these steps to contribute:

1. Fork the repository
2. Create a new branch for your feature or bug fix
3. Make your changes and commit them with a clear commit message
4. Push your changes to your fork
5. Create a pull request to the main repository

Please ensure your code follows the existing style and includes appropriate tests.

## License

piped-proxy is licensed under the GNU Affero General Public License v3.0 (AGPL-3.0). See the [LICENSE](LICENSE) file for more details.

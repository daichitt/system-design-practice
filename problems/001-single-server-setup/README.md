# Building Single Server Setup

## Single server setup

```mermaid
graph LR
    C[Client<br>Browser/App] -->|1. HTTP Request| S[Server<br>Backend]
    S -->|2. Access| DB[(Database)]
    DB -->|3. Result| S
    S -->|4. Response| C
```

- **1. HTTP Request**: Frontend (browser/app) -> server
- **2. Access**: Server -> database
- **3. Result**: Database -> server
- **4. Response**: Server -> client
- **5. Rendering**: Displayed on the client side

## Sample Response

```http
GET /users/12
```

```json
{
  "id": 12,
  "name": "John Doe",
  "email": "john@example.com",
  "created_at": "2026-04-24"
}
```

## Single server setup with DNS resolve and DB

```mermaid
graph LR
    B[Browser] -->|Check cache| C{Browser<br>Cache}
    C -->|Hit| S[Server]
    C -->|Miss| D[DNS Server]
    D -->|IP response| B
    B -->|HTTP Request| S
    S -->|DB Access| DB[(Database)]
    DB -->|Result| S
    S -->|HTTP Response| B
```

## Step-by-step flow (simplified)

- **1** Browser checks DNS cache
- **2** If cache hit, send request to server
- **3** If cache miss, query DNS server
- **4** Receive IP address from DNS server
- **5** Send HTTP request to server
- **6** Server accesses database
- **7** Database returns result
- **8** Server returns HTTP response

## What happens when opening a URL in a browser

```mermaid
sequenceDiagram
    participant U as User
    participant B as Browser
    participant C as DNS Cache
    participant D as DNS Server
    participant S as Server

    U->>B: Open URL
    B->>C: Check cached IP
    alt IP found in cache
        C-->>B: Return IP address
    else IP not found
        B->>D: Resolve domain name
        D-->>B: Return IP address
    end
    B->>S: TCP 3-way handshake
    B->>S: TLS handshake (encrypted channel)
    B->>S: HTTP request (GET/POST/etc.)
    S-->>B: HTTP response
    B-->>U: Render page
```

### Flow

- **DNS**: Browser first checks DNS cache. If found, it uses the cached IP; otherwise it resolves via DNS server.
- **TCP**: Browser starts a TCP 3-way handshake to establish a reliable connection.
- **TLS**: Browser negotiates encryption; after this, data is encrypted in transit.
- **HTTP**: Browser sends an HTTP request to the server using methods like `GET` or `POST`.
- **Browser Rendering**: Browser parses and renders the response data for the user.

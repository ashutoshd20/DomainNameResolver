# DNS Resolver Script

## Overview
This Python script performs DNS resolution using both **iterative** and **recursive** methods. It starts with root servers and follows the DNS hierarchy in the iterative mode, while in recursive mode, it relies on system-configured resolvers.

## Features
- **Iterative DNS Lookup**: Queries root servers, then top-level domain (TLD) servers, and finally authoritative servers to resolve the domain.
- **Recursive DNS Lookup**: Uses the system's default resolver to fetch the DNS result.
- **Timeout Handling**: Ensures queries do not hang indefinitely.
- **Debugging and Logging**: Provides informative debug messages for troubleshooting.

## Dependencies
Ensure you have the required Python module installed:
```sh
pip install dnspython
```

## Usage
Run the script with either the `iterative` or `recursive` mode:
```sh
python3 dns_server.py <iterative|recursive> <domain>
```
For example:
```sh
python3 dns_server.py iterative example.com
python3 dns_server.py recursive example.com
```

## Explanation of Modes
### Iterative Mode
- Starts with root DNS servers.
- Iteratively queries the next level of authoritative nameservers until it reaches the final answer.

### Recursive Mode
- Uses a system-configured resolver (e.g., ISP resolver, Google DNS).
- Fetches the result directly without manual iterative querying.

## Code Structure
- **`send_dns_query(server, domain)`**: Sends a DNS query to a specified server.
- **`extract_next_nameservers(response)`**: Extracts nameserver (NS) records and resolves them to IP addresses.
- **`iterative_dns_lookup(domain)`**: Performs an iterative DNS lookup from root to authoritative servers.
- **`recursive_dns_lookup(domain)`**: Uses system resolvers to resolve the domain.

## Example Output
```sh
[Iterative DNS Lookup] Resolving example.com
[DEBUG] Querying ROOT server (198.41.0.4) - SUCCESS
[DEBUG] Querying TLD server (192.33.4.12) - SUCCESS
[SUCCESS] example.com -> 93.184.216.34
Time taken: 0.587 seconds
```

## Notes
- The script extracts and resolves nameservers dynamically.
- It uses UDP queries with a timeout of 3 seconds.
- Errors are handled to avoid script crashes.

## Author
Ashutosh Dwivedi
Chinmay Hiran Pillai
Shubham Kumar

## License
This project is open-source and free to use.
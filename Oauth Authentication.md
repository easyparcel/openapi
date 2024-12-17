## Oauth Authentication

### Oauth Authentication Flow
<img src="pictures/Oauth%20Flow%20chart.png" alt="Flow Chart" style="height=350px;">


1. Client               -> Authorization Request  -> Authorization Server
2. Authorization Server -> Request Login          -> User
3. User                 -> Login and Authenticate -> Authorization Server
4. Authorization Server -> Request Access         -> User
5. User                 -> Give Access            -> Authorization Server
6. Authorization Server -> Authorization Code     -> Client
7. Client               -> Token Request          -> Authorization Server
8. Authorization Server -> Access Token           -> Client
9. Client               -> Call API               -> Return result/parameters

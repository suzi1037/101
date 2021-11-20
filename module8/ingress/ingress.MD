### install ingress controller
```
kubectl create -f nginx-ingress-deployment.yaml
```

### generated key-cert
```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout tls.key -out tls.crt -subj "/CN=cncamp.com/O=cncamp"
```
### create secret
```
apiVersion: v1
kind: Secret
metadata:
  name: cncamp-tls
data:
  tls.crt: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURMVENDQWhXZ0F3SUJBZ0lVVnVFWW11VHdxYXVFQjlxaGNSQUNRZDEyS0Frd0RRWUpLb1pJaHZjTkFRRUwKQlFBd0pqRVRNQkVHQTFVRUF3d0tZMjVqWVcxd0xtTnZiVEVQTUEwR0ExVUVDZ3dHWTI1allXMXdNQjRYRFRJeApNVEV3TWpFeE1URXdNVm9YRFRJeU1URXdNakV4TVRFd01Wb3dKakVUTUJFR0ExVUVBd3dLWTI1allXMXdMbU52CmJURVBNQTBHQTFVRUNnd0dZMjVqWVcxd01JSUJJakFOQmdrcWhraUc5dzBCQVFFRkFBT0NBUThBTUlJQkNnS0MKQVFFQTVJUlY1TGJIT0tEVjE1NEZBUk55cE1IUzhKaUIrSXdBT3ZNQzR0R0xKdUg4SndsV3JnaVR4dW9JQjJDegpwVUp2RjZZck9PVGlsYTdkc1NMNTVLMWZuY0wxZlR6VVIrSk9ydkVPbndORjJRSEZKSU1vMzBqNmZsNmVWSFdqClhkM2tNMDc0ZnNKYkc0ZVBCR2YzYmNVamNoWjlPZ09JQXpCdXpSbDhzSlRSZnJuRkl0eUxhUjZZOUtRRGNYdzAKSWU1VkIyM2Q2ZGRJcDJvMzhtS2FQR1RQU0hhZDVUSWMvaXdscmlzaGxNZ2VBcEZLN0YyL0ZURDlNcytzWE94Mwp6Z2FSN2tUR0xvQzc3N1pQNTkvMVplUmxWSEora1djY2dESHpsQXVTZy9JemQ5NTZJUFhZTTNkTWZ2alNpZXZnCmJsQkJmNnkvcFdiVi9TVFdsdE4wSk9iMFZRSURBUUFCbzFNd1VUQWRCZ05WSFE0RUZnUVV2RStkaDlJUXVZVWIKdkxYbXlpMTQwUGZtcC9zd0h3WURWUjBqQkJnd0ZvQVV2RStkaDlJUXVZVWJ2TFhteWkxNDBQZm1wL3N3RHdZRApWUjBUQVFIL0JBVXdBd0VCL3pBTkJna3Foa2lHOXcwQkFRc0ZBQU9DQVFFQWNvYzVVaHRlNVNkWWtXaXArbnAwCnp2RnQ2YytENUN4U3Q5aXNYT3QrY3MxQkw5elRKRkNWdFl2TlIrUXhLWTdnaEh0NkphUjByRFpPa3VCY1pXbkwKTjVqOVRWWng4OG1YbEJMMlFZT21MWjNUcUlVTnlJMjAxUGxIZmZMb1BxaHZTeGZ4bGg4VnA4NFNaV1lucU5KMQo0cHF4WDFiYk8vZnM3QVNEaVRpZEowMFM4UjJsZTc0SEU5L0dBbnpuMTEvWTE0L3J1NjRuR2QxdVJQb2JTQUlICmI1UTRjYUtOWXBmMFhMMXVuZmZsZmFQb292eFN1ZHI1dEYzeUdrTERSaUNNdURidjNsNXBkbmdpWHdBOGZmblgKTVB1aFB0UEtXLzdtQzZFUUF4Y1BWa2R6UjRKbDQzM2lYNnJ0bXRONW5tRXJ3NEF6dUY4ZGcxWUN4ZU04MzltcQpmUT09Ci0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K
  tls.key: LS0tLS1CRUdJTiBQUklWQVRFIEtFWS0tLS0tCk1JSUV2UUlCQURBTkJna3Foa2lHOXcwQkFRRUZBQVNDQktjd2dnU2pBZ0VBQW9JQkFRRGtoRlhrdHNjNG9OWFgKbmdVQkUzS2t3ZEx3bUlINGpBQTY4d0xpMFlzbTRmd25DVmF1Q0pQRzZnZ0hZTE9sUW04WHBpczQ1T0tWcnQyeApJdm5rclYrZHd2VjlQTlJINGs2dThRNmZBMFhaQWNVa2d5amZTUHArWHA1VWRhTmQzZVF6VHZoK3dsc2JoNDhFClovZHR4U055Rm4wNkE0Z0RNRzdOR1h5d2xORit1Y1VpM0l0cEhwajBwQU54ZkRRaDdsVUhiZDNwMTBpbmFqZnkKWXBvOFpNOUlkcDNsTWh6K0xDV3VLeUdVeUI0Q2tVcnNYYjhWTVAweXo2eGM3SGZPQnBIdVJNWXVnTHZ2dGsvbgozL1ZsNUdWVWNuNlJaeHlBTWZPVUM1S0Q4ak4zM25vZzlkZ3pkMHgrK05LSjYrQnVVRUYvckwrbFp0WDlKTmFXCjAzUWs1dlJWQWdNQkFBRUNnZ0VBVUd5R3NrVGxubmQwYXpzdzlhejdoeUt6ODNzcEd1bGkxMXhaWXF4dXRkT0kKNDlBMGtuRndXT3hhd1FYMms2M3EzVDdkTFZ2WXB1ZHhISHQ3eVZCL08wMjNDa21UU0cxTVZlTit5dFhqQ2puRwpRVkJyM1JHWkgwcDduS3YrUC9YczcyWFdyUDRJQkl0VCtUQUI4NzhTOTM4VXVZc3Vuamk0ZGpTSEhycHhkSkNRCm1JcG9GNWpCUzg4WjdpNWxQTHVXUTVYK2pmcGVqaU56dDlqcWJaL1BzRFcrZUNReUNkRlVBRFpwNGZrZTdWS1oKc2I0U3JlUlA4bmh5ejZxT29BcVkvOHVDenpUSlpOQjRObVVEWldyUzRMLzZlbFFGa2cyK1lhekhsV0xuTW5mbQpSaENlU3EyOGdkUlR2eHpCUS9Ta0ZBcFZVd0lzdmpGcFFXWTZzRnRMUVFLQmdRRDNFSHhvK2NYQjAwV1gzTW1ZClRQWUNEeEMxNlhTemlqbkdXTUZmdURnN3BkejJ0c1h1MEJDRlFLN1AwV0cxY1lJMTJDbXM3V0lIZi9tRWJORDgKK3Y4czllZkhFamZGNklHREFUMGxEMlhGS1lpZC9MRDdFQmFKejBRcnhvaVBTS0ZqMlBOeHVLRkhCM3hmQkZ1cQpKV2pSUHRxaDEwOVF3Qzl0bGRMNXFlTk1VUUtCZ1FEc3lCOXJnQVQveW9PalovRlFWYXBvbjE1aS9reWZZdGpPCm5qcVhxaStQRXIyS05zdUU5cXpUb2YyZldrSXVwWk5DemFOYlNhTjBCUHpKNnB2MW1IZTlIVmIyaUxkZUw2eksKeUZKcUhGVkVhcGNzOHo5dFhhVldJVGlrYW1MZ0l6ZWVPUnJDUVRXWDVzenZjQjFHNmhYMFRXY00vMHl5NkIyYgpJL2c3R1MwYXhRS0JnQnU3SWZ1MmJWZ0FHc09jNkpQTHI2RXpoN0NqYjVIblpleTVjWnNJMW1iN2l2MjJMaWxMCitVNjduK043b1BmNHNhRFJqbnYyZVJaV2F1OU9OM2J0eFU2S20yVmd5aG5RcXhqRlB0TzJFcm82bXpjQWNlejgKTlV0cWxFQkZuSFpZdEtTOGFUYk9mbXUyajJNcTNnOE8rK0RncVRHWk5USGZJSE93YVduVWc4ckJBb0dBVU9FaQo2bU4yVWJGcE9iM2RqZVZWS2h1VjhCYVJNYmhmK21QTis5UmtIbWoyV1duU0p2N2psZjYxVldOTlRBVyt3WWpnCmplUWZjeGZwQ1VlY01rMzhTSnJuQTVzN2wyNk5oVTdiNStiNXNUNy9tSmtXUjFNL2tLWVVaUVQ1OVRuU1c3ZUIKem16YjA2RkF5MkR1ZnpTaWZ5cVpVclU2QzdxQnNtYWMrZ0xsaDBrQ2dZRUFpdTYwR1d5Mnl4Tm45aXNjalZYbwpDUFNSbmtFM3MzM05YcnJwLzArbVZMdVVrUnRFcjBqWi9CTFl2NlRDMVhuaGdXMlZqdXZkWU9NMVV0WEM0M2JOCllXYXArUWMyYmZrRTJsWjZhdllNYXpEQ014Tzh5a3ZybWgwTWhHbDRkeXQvMWdCZnR1REphRVErQU5HaFEwRGMKbzFlWGlJTkh2aGdhTTN4YkdLREdMWFk9Ci0tLS0tRU5EIFBSSVZBVEUgS0VZLS0tLS0K
type: kubernetes.io/tls
```
### create a ingress
```
kubectl create -f ingress.yaml
```
### test the result
```
curl -H "Host: cncamp.com" https://10.109.204.181 -v -k
```
### understand why ingress is not enough?
- tls: cypher, dhkey, TLSVersion
- header based L7 rule
- rewriting?
  - header rewriting
  - URI rewriting

### how rewrite is supported in nginx ingress 
```
Name	Description	Values
nginx.ingress.kubernetes.io/rewrite-target	Target URI where the traffic must be redirected	string
nginx.ingress.kubernetes.io/ssl-redirect	Indicates if the location section is accessible SSL only (defaults to True when Ingress contains a Certificate)	bool
nginx.ingress.kubernetes.io/force-ssl-redirect	Forces the redirection to HTTPS even if the Ingress is not TLS Enabled	bool
nginx.ingress.kubernetes.io/app-root	Defines the Application Root that the Controller must redirect if it's in '/' context	string
nginx.ingress.kubernetes.io/use-regex	Indicates if the paths defined on an Ingress use regular expressions	bool
```
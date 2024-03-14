# httpd 설치
```
sudo yum install httpd -y
```
# httpd 시작 & 검사
```
sudo systemctl start httpd
sudo systemctl enable httpd
```

# httpd 재시작
```
sudo systemctl restart httpd
```
# index.html 옮기기
```
sudo mv index.html /var/www/html
```

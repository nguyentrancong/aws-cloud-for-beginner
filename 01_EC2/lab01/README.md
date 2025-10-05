# Hướng dẫn khắc phục lỗi Permissions 0644 for 'lab-01-ec2-linux-key-pair.pem' are too open

Khi kết nối SSH tới EC2, nếu gặp lỗi sau:

```
Permissions 0644 for 'lab-01-ec2-linux-key-pair.pem' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "lab-01-ec2-linux-key-pair.pem": bad permissions
Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
```

## Nguyên nhân

File key `.pem` đang có quyền truy cập quá rộng (0644), khiến SSH từ chối sử dụng.

## Cách khắc phục

1. **Đổi quyền truy cập file key về 600:**

   Mở terminal và chạy lệnh sau:

   ```bash
   chmod 600 lab-01-ec2-linux-key-pair.pem
   ```

2. **Kiểm tra lại quyền file:**

   ```bash
   ls -l lab-01-ec2-linux-key-pair.pem
   ```

   Kết quả phải là:

   ```
   -rw------- ...
   ```

3. **Kết nối lại SSH:**

   ```bash
   ssh -i lab-01-ec2-linux-key-pair.pem ec2-user@ec2-54-251-218-72.ap-southeast-1.compute.amazonaws.com
   ```

## Lưu ý

- Không chia sẻ file `.pem` cho người khác.
- Luôn giữ file key ở chế độ bảo mật cao.
- Nên sử dụng quyền 400 thôi

---
title: "🌱 IAM - Identify and Access Management"
tags: [aws]
date: 2023-02-22
---

## 🌿 What?
- 🌱 Một Global service - Region nào cũng có.
- 🌱 Sử dụng để tạo users và groups.
- 🌱 Mỗi user đại diện cho một người trong tổ chức.
- 🌱 Mỗi group chỉ chứa users, không chứa group khác.
- 🌱 Users có thể không thuộc một group nào(ko best practice) và 1 user có thể thuộc nhiều groups.
![[00 Meta/01 Attachments/Pasted image 20230222221540.png]]

## 🌿 Why?
- 🌱 Không bao giờ được cho tất cả users được sử dụng tất cả services. 
- 🌱 User cần làm gì -> tạo quyền cho sử dụng cái đó. Tránh chi phí phát sinh(do user có thể launch được một đống services), vấn đề bảo mật. 
- 🌱 Users hoặc Groups có thể được assign JSON documents gọi là polices.
	![[00 Meta/01 Attachments/Pasted image 20230222224819.png|500]]

> [!note] Note
> 
> The least privilege principle: Nguyên tắc đặc quyền tối thiểu.

## 🌿 What is polices?
- 🌱 Xác định quyền của users hoặc groups.
- 🌱 Bao gồm:
	- Version
	- ID (optional)
	- Statement:
		- Sid: Statement id
		- **Effect**: Allow | Deny
		- **Principal**: account/user/role áp dụng policy
		- **Action**: những acctions được cho phép || không cho phép
		- **Resource**: những resources áp dụng policy 
		- Condition(optional): điều kiện cho effect

## 🌿 Protect mechanisms
- 🌱 Set Password
- 🌱 MFA - Multi Factor Authentication
	- 📳 Virtual MFA device: GG Authencitator, Authy(nhiều tokens trên một device)
	- 🔑 Universal 2nd Factor(U2F) Security Key: YubiKey by Yubico(3rd party of AWS)(một security key dùng được cho nhiều root accounts and IAM users)
	- Hardware Key Fob MFA  Device.
	- Hardware Key Fob MFA Device for AWS GovCloud(US)

## 🌿 What's the AWS CLI?
- 🌱 Cho phép tương tác với các AWS Services thông qua terminal thay vì AWS Mangement Console.
- 🌱 Truy cập trực tiếp đến các APIs của các AWS Services.
- 🌱 Có thể sử dụng script để quản lý resources cũng như một số task tự động.

## 🌿 What's the AWS SDK?
- 🌱 Software Development Kit, một cách khác để tương tác với AWS Services.
- 🌱 Được nhúng trong chương trình của chúng ta(kiểu như thư viện).
- 🌱 Hỗ trợ nhiều program languages, mobile devices and IoT devices.


## 🌿 IAM Roles
- 🌱 Một vài Intance Services sẽ cần thực hiện một số hành động và chúng ta cần thêm quyền cho chúng thông qua việc tạo IAM Roles.
- 🌱 Common roles:
	- EC2 Instance Roles
	- Lambda Function Roles
	- Roles for CloudFormation

## 🌿 IAM Security Tools
- 🌱 IAM Credentials Report (account-level)
	-  Một danh sách tất cả các users của account và trạng thái của các credentials.
- 🌱 IAM Access Advisor (user-level)
	- Hiển thị những service permissions đã tạo cho một user và thời gian cuối cùng những services đó được truy cập.
	- -> theo dõi để nhận biết những permissions nào không được sử dụng -> xóa nó đi, tuân thủ phương châm **The principle least privilege**.

## 🌿 IAM Best Practice
- 🌱 Không sử dụng root account, nên tạo một IAM account và chỉ định quyền cho account.
- 🌱 Mỗi một người(physical user) = một AWS user. 
- 🌱 Nên assign users vào groups và chỉ định quyền cho group.
- 🌱 Tạo một password mạnh cho policy, nếu lộ người khác có thể thêm quyền tùm lum 
- 🌱 Sử dụng MFA, nâng cao tính bảo mật.
- 🌱 Tạo và sử dụng IAM Roles để chỉ định permissions đến những AWS services.
- 🌱 Sử dụng Access Keys khi Programatic Access(CLI/SDK).
- 🌱 Audit lại permissions của account bằng IAM Access Advisor.
- 🌱 Never share IAM users & Access Keys.
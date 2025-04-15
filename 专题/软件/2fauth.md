---
title: 2FAuth
description: 一个用于管理双因素身份验证（2FA）账户并生成安全代码的网络应用。
published: true
date: 2025-04-15T16:26:41.956Z
tags: 
editor: markdown
dateCreated: 2025-04-09T17:41:27.964Z
---

# 2FAuth

![Docker 构建状态](https://img.shields.io/github/actions/workflow/status/bubka/2fauth/ci-docker-test.yml?branch=master&style=flat-square) ![https://codecov.io/gh/Bubka/2FAuth](https://img.shields.io/codecov/c/github/Bubka/2FAuth?style=flat-square) ![https://github.com/Bubka/2FAuth/blob/master/LICENSE](https://img.shields.io/github/license/Bubka/2FAuth.svg?style=flat-square)

一个用于管理你的双因素身份验证 (2FA) 账户并生成其安全验证码的 Web 应用

![screens](https://user-images.githubusercontent.com/858858/100485897-18c21400-3102-11eb-9c72-ea0b1b46ef2e.png)

[**2FAuth 演示**](https://demo.2fauth.app/)  
凭证（登录名 - 密码）：`demo@2fauth.app` - `demo`

## 目的

2FAuth 是一个基于 Web 的自托管替代方案，取代 Google Authenticator 等一次性密码（OTP）生成器，适用于移动端和桌面端。

它旨在简化你在任何设备上执行 2FA 身份验证的流程，界面清晰、适配良好。

我创建它的原因：

* 大多数此类应用的 UI 同时显示所有账户的令牌，并带有令人紧张的倒计时（我认为）
* 我希望我的 2FA 账户能存储在一个独立的数据库中，便于备份和恢复（你是否遇到过手机丢失导致 Google Auth 所有账户丢失？我遇到过……）
* 我讨厌在使用桌面电脑时还得掏出手机获取 OTP
* 我喜欢编码，也喜欢自托管方案

## 主要功能

* 管理你的 2FA 账户并使用“分组”进行组织
* 扫描并解析任意二维码，快速添加账户
* 通过高级表单添加不含二维码的自定义账户
* 编辑账户，即使是导入的也可以修改
* 生成 TOTP、HOTP 安全码以及 Steam Guard 验证码

2FAuth 目前已完全本地化为英文和法文。如需帮助添加更多语言，请查看 [贡献](#contributing) 部分。

## 安全性

2FAuth 提供多种安全机制，最大程度保护你的 2FA 数据。

### 单用户应用

你需要创建一个用户账户并进行身份验证后才能使用此应用。无法创建多个账户，该应用设计为个人使用。

### 现代认证方式

你可以使用安全密钥（如 Yubikey 或 Titan key）登录 2FAuth，并禁用传统的登录表单。

### 数据加密

存储在数据库中的敏感数据可以进行加密，以防数据库被泄露。加密为可选项，默认关闭。当启用加密时，强烈建议备份 `.env` 文件中的 APP_KEY 值（或整个文件）。

### 自动注销

2FAuth 会在非活动一段时间后自动注销你，以防会话长期存在。自动注销可禁用，或设置为在复制验证码时触发。

### RFC 规范

2FAuth 使用 [Spomky-Labs/OTPHP](https://github.com/Spomky-Labs/otphp) PHP 库，按 RFC 4226（HOTP 算法）和 RFC 6238（TOTP 算法）生成 OTP。

## 系统要求

* [![需要 PHP8](https://img.shields.io/badge/php-^8.3-red.svg?style=flat-square)](https://secure.php.net/downloads.php)
* 查看 [Laravel 服务器要求](https://laravel.com/docs/installation#server-requirements)
* 任意 [Laravel 支持的数据库](https://laravel.com/docs/database)

## 安装指南

* [自托管服务器](https://docs.2fauth.app/getting-started/installation/self-hosted-server/)

* [Docker（命令行）](https://docs.2fauth.app/getting-started/installation/docker/docker-cli/)

* [Docker（compose）](https://docs.2fauth.app/getting-started/installation/docker/docker-compose/)

* [Heroku](https://docs.2fauth.app/getting-started/installation/heroku/)

## 升级

* [升级指南](https://docs.2fauth.app/getting-started/upgrade/)

## 迁移

2FAuth 支持以下格式的导入：2FAuth（JSON）、Google Auth（二位码）、Aegis Auth（JSON、纯文本）、2FAS Auth（JSON）

* [导入指南](https://docs.2fauth.app/getting-started/usage/import/)

## 贡献

你可以通过以下方式为 2FAuth 做出贡献：

* [报告 Bug](https://github.com/Bubka/2FAuth/issues/new?template=bug_report.md)，或者更棒的是，通过向 *dev* 分支提交修复的 pull request。
* [建议改进或新功能](https://github.com/Bubka/2FAuth/issues/new?template=feature_request.md)。请先查看 [2FAuth 开发项目](https://github.com/users/Bubka/projects/1)，你的想法可能已经在其中。
* 在你掌握的语言中校对或补充翻译，通过 [Crowdin 平台](https://crowdin.com/project/2fauth)。如果缺少某种语言，可申请添加。

## 许可协议

[AGPL-3.0](https://www.gnu.org/licenses/agpl-3.0.html)

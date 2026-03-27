---
title: 数学每日背诵内容
date: 2026-03-27 09:51:49
tags: [考研, 数学, 背诵]
lang: zh-CN
mathjax: true
---

以下整理部分数学必背公式与知识点, 便于个人日常记忆.

<!-- more -->

# 泰勒展开式 & 等价无穷小

## 泰勒展开式

**每天起床头件事, 先背一遍展开式.**

$ \sin x = x - \frac{1}{6}x^3 + o(x^3) $

$ \arcsin x = x + \frac{1}{6}x^3 + o(x^3) $

$ \tan x = x + \frac{1}{3}x^3 + o(x^3) $

$ \arctan x = x - \frac{1}{3}x^3 + o(x^3) $

$ \ln (1 + x) = x - \frac{1}{2}x^2 + \frac{1}{3}x^3 + o(x^3) $

$ \mathrm{e}^x = 1 + x + \frac{1}{2}x^2 + \frac{1}{6}x^3 + o(x^3) $

$ \cos x = 1 - \frac{1}{2}x^2 + \frac{1}{24}x^4 + o(x^4) $

$ (1 + x)^\alpha = 1 + \alpha x + \frac{\alpha (\alpha - 1)}{2}x^2 + o(x^2) $

## 等价无穷小

$ \sin x \sim x $

$ x - \sin x \sim \frac{1}{6}x^3 $

$ \arcsin x \sim x $

$ \arcsin x - x \sim \frac{1}{6}x^3 $

$ \tan x \sim x $

$ \tan x - x \sim \frac{1}{3}x^3 $

$ \arctan x \sim x $

$ x - \arctan x \sim \frac{1}{3}x^3 $

$ \ln(1 + x) \sim x $

$ \arcsin x - \arctan x \sim \frac{1}{2}x^3 $

$ \mathrm{e}^x - 1 \sim x $

$ \tan x - \sin x \sim \frac{1}{2}x^3 $

$ 1 - \cos x \sim \frac{1}{2}x^2 $

$ x - \ln(1 + x) \sim \frac{1}{2}x^2 $

$ (1 + x)^\alpha - 1 \sim \alpha x $

$ a^x - 1 \sim x \ln a $

$ 1 - \sqrt{1 - x ^ 2} \sim \frac{1}{2}x^2 $

# 积分公式

$ \int x^\mu \mathrm dx = \frac{1}{\mu+1}x^{\mu+1}+C $

$ \int \frac{1}{\sqrt{x}}\mathrm dx=2\sqrt{x}+C $

$ \int\frac{\mathrm df(x)}{\sqrt{f(x)}}=2f(x)+C $

$ \int\mathrm e^x\mathrm dx=\mathrm e^x+C $

$ \int a^x\mathrm dx=\frac{ax}{\ln a}+C $

$ \int \frac{1}{x}\mathrm dx=\ln\left|x\right|+C $

$ \int\sin x\mathrm dx=-\cos x+C $

$ \int\cos x\mathrm dx=\sin x+C $

$ \int\tan x\mathrm dx=-\ln\left|\cos x\right|+C $

$ \int\cot x\mathrm dx=\int\frac{\cos x}{\sin x}\mathrm dx=\int\frac{\mathrm d\sin x}{\sin x}=\ln\left|\sin x\right|+C $

$ \int\sec^2 x\mathrm dx=\tan x+C $

$ \int\csc^2 x\mathrm dx=-\cot x+C $

$ \int\frac{\mathrm dx}{\sqrt{1-x^2}}=\arcsin x+C $

$ \int\frac{\mathrm dx}{1+x^2}=\arctan x+C $

$ \int\sec x\mathrm dx=\ln\left|\sec x+\tan x\right|+C $

$ \int\frac{1}{x^2+a^2}\mathrm dx=\frac{1}{a}\arctan\frac{x}{a}+C $

$ \int\frac{1}{\sqrt{x^2\pm a^2}}\mathrm dx=\ln\left|x+\sqrt{x^2\pm a^2}\right|+C $

$ \int\frac{1}{\sqrt{a^2-x^2}}\mathrm dx=\arcsin\frac{x}{a}+C $

$ \int\frac{1}{a^2-x^2}\mathrm dx=\frac{1}{2a}\ln\left|\frac{a-x}{a+x}\right|+C $

$ \int\frac{1}{1+\mathrm e^x}\mathrm dx=x-\ln(1+\mathrm e^x)+C $

$ \int\sqrt{x^2+a^2}\mathrm dx=\frac{x}{2}\sqrt{x^2+a^2}+\frac{a^2}{2}\ln\left|x+\sqrt{x^2+a^2}\right|+C $

$ \int\sqrt{x^2-a^2}\mathrm dx=\frac{x}{2}\sqrt{x^2-a^2}-\frac{a^2}{2}\ln\left|x+\sqrt{x^2+a^2}\right|+C $

$ \int\sqrt{a^2-x^2}\mathrm dx=\frac{x}{2}\sqrt{a^2-x^2}+\frac{a^2}{2}\arcsin\frac{x}{a}+C $

$ \int\sec^3 x\mathrm dx=\frac{1}{2}\sec x\tan x+\frac{1}{2}\left|\sec x+\tan x\right|+C $

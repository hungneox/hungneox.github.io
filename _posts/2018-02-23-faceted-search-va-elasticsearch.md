---
layout: post
title: "Faceted search và ElasticSearch" 
date: 2018-02-23 14:00
categories: [elasticsearch]
author: hungneox
tags : [faceted-search, elasticsearch]
description: "Faceted search và ElasticSearch"
image: /assets/images/laravel.jpg
comments: true
published: false
---

# Faceted search và ElasticSearch

Faceted search hay còn gọi là faceted navigation, tạm dịch là tìm kiếm đa diện hay điều hướng đa diện. Nó là một kỹ thuật dùng để tra cứu thông tin dựa trên hệ thống phân loại đa diện (faceted classification system), nó chó phép người dùng có thể tìm kiếm hay và truy vấn thông tin một cách có hiệu quả bằng cách sàng lọc ra những kết quả mong muốn bằng nhiều bộ lọc cùng một lúc.

Các bộ lọc facets tương ứng với các thuộc tính của đối tượng tìm kiếm. Ví dụ điện thoại thì có hãng sản xuất, màu sắc, hệ điều hành, kích thước màn hình, cân nặng v.v. Mỗi một thuộc tính như vậy có thể được xem là một mặt của thành phần thông tin trong hệ thống, trong trường hợp này nó là một mặt của sản phẩm điện thoại di động.

Điểm khác biệt của tìm kiếm đa diện và các bộ lọc thông thường là nó cung cấp thông tin tổng hợp về về các facets có trong tập hợp dữ liệu. Cụ thể hơn với kiểu lọc thông thường thì khi chúng ta lọc ra những điện thoại có màu đỏ, thì chúng ta chỉ nhận về kệt quả bao gồm các điện thoại có màu đỏ, mà không có bất kỳ thông tin nào về các màu khác. Ví dụ như có câu truy vấn sql giả như sau:

`SELECT * from phones where color = ‘RED’`

Còn với tìm kiếm đa diện, mà cụ thể ở đây là ElasticSearch, ngoài kết quả tìm kiếm tương ứng được trả về chúng ta còn có thêm thông tin về các buckets chứa các thuộc tính khác.

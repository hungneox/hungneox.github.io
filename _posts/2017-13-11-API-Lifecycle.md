---
layout: post
title: "API Lifecycle"
date: 2017-11-13 7:00 AM
categories: [api-development, programming]
author: hungneox
tags : [api-development, programming, vietnamese]
description: "API Lifecyelce - Chu kỳ sống của API"
image: /assets/posts/api-lifecycle/api-lifecycle-state-diagram.jpg
comments: true
published: false
---

# Vòng đời của API

Cũng như là một sản phẩm phần mềm, thì API cũng có vòng đời (`API lifecycle`) riêng của nó. API không thể tự dưng sinh ra và chết đi đột ngột mà không để lại hậu quả nào. Cho nên có một chu trình phát triển API qui củ cũng giúp chúng ta dễ dàng phát triển và bảo trì API hơn. Ngoài ra cũng tăng tính tính cậy và giảm thiểu các rủi ro khi đưa cho khách hàng hay được sử dụng trong một ứng dụng khác. Trong bài viết này có thể hiểu vòng đời ở đây là vòng đời về mặt kỹ thuật của API nhiều hơn là vòng đời về khía cạnh "kinh doanh" của nó.

API Lifecycle là một chuỗi các trạng thái (series of states), có thể phụ thuộc vào `API Management Product` được sử dụng.

!["API lifecycle diagram"](/assets/posts/api-lifecycle/api-lifecycle-state-diagram.jpg){: .center-image }

# Các trạng thái của API

## Draft
Đây là trạng thái, mà API còn trong giai đoạn "bản thảo" trong quá trình phát triển và thiết kế. Chưa được deployed và liên kết với bất kỳ Catalog nào.

## Staged

Khi API ở trong trạng thái staged (tạm dịch là đã dược dàn dựng), thì nó được triển khai trên một Catalog. Staged là trạng thái ban đầu khi chúng ta "xuất bản" một API. Trong trạng thái này, thì API chưa được công bố và không thể sử dụng bởi bất kỳ developer nào. Staging (quá trình dàn dựng) có khi được gọi là prototyping state.

## Published

Khi API được published, một phiên bản cố định của API được triển khai lên trên một Catalog. Phiên bản API này bây giờ đã có thể sự dụng với các nhà phát triển và cộng đồng. Cũng trong giai đoạn này, thì các thiết lập về `visibility` và `susbcription` có thể thay đổi cho từng phiên bản cụ thể của API. Các thay đổi xa hơn đòi hỏi một phiên bản API mới. Trong một số trường hợp cụ thể, trạng thái `published` cần được đồng bộ với `release cycles` của backend.

## Deprectated

Khi chúng ta `deprecate` một API, có nghĩa là chúng ta không khuyến khích developers sử dụng nó nữa. Trong trạng thái `deprecated`, thì API chỉ còn có thể sử dụng bởi những những ứng dụng đang sử dụng nó mà thôi. Phiên bản API bị `deperecated` không cho phép developers đăng ký mới để sử dụng nữa (no new subscriptions). Khi một phiên bản API được `published` thì phiên bản cũ hơn nên được chuyển sang trạng thái `deprecated`. Một số `API Management Product` có thể tự động làm điều này.

## Retired / Archived

Khi chúng ta cho một API "nghỉ hưu", thì phiên bản đó của API không thể xem cũng như không thể dăng ký được nữa. API bị tắt hoàn toàn, thậm chí đối với các `subscribers` từ trước cũng không thể gọi (`invoke`) nó nữa.

# Tham khảo 

1. The Product lifecycle [https://www.ibm.com/.../capim_product_lifecycle.html](https://www.ibm.com/support/knowledgecenter/en/SSFS6T/com.ibm.apic.apionprem.doc/capim_product_lifecycle.html)
2. API Lifecycle [http://cycles.apiops.net/apilifecycle/](http://cycles.apiops.net/apilifecycle/)
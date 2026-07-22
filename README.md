# Customer Journey Sankey Analysis

> Mini project thực hành Sankey chart để phân tích luồng Marketing Source → Landing Page → Purchase Outcome.

[**Mở notebook**](./customer_journey_sankey_analysis.ipynb)

## Project overview

TeddyWorld muốn hiểu traffic từ các nguồn quảng cáo đi vào landing page nào và cuối cùng có tạo đơn hàng hay không. Project xây dựng master journey ở cấp session, trực quan hóa bằng Sankey và bổ sung xu hướng theo tháng/quý cùng landing-page template analysis.

Project được xây dựng như một **mini project học tập**, tập trung chứng minh khả năng áp dụng kỹ thuật phân tích vào một business question cụ thể.

## Business questions

1. Nguồn marketing nào có conversion rate cao nhất?
2. Landing page nào có traffic lớn nhưng no-purchase rate cao?
3. Hành vi từ `gsearch` và `bsearch` khác nhau như thế nào?
4. Conversion và no-purchase rate thay đổi theo tháng/quý ra sao?

## Dataset

| File | Vai trò / trường dữ liệu chính |
| --- | --- |
| website_sessions.csv | `website_session_id`, `created_at`, `utm_source` |
| website_pageviews.csv | Pageview sequence và landing page |
| orders.csv | Session có đơn hàng và primary product |
| products.csv | Tên sản phẩm |


Dữ liệu gốc không được đưa vào repository mặc định. Danh sách file và hướng dẫn chạy nằm tại [`data/README.md`](./data/README.md).

## Techniques practiced

- Xác định first pageview/landing page theo session
- Xây dựng master journey bằng nhiều bước merge
- Chuẩn hóa dữ liệu source-target cho Sankey
- Interactive visualization bằng Plotly
- Conversion analysis theo traffic source và landing page
- Time-based analysis theo tháng/quý
- Landing-page template grouping và màu flow theo outcome

## Main KPIs

| KPI | Ý nghĩa |
| --- | --- |
| Sessions | Số website session |
| Order Sessions | Số session có đơn hàng |
| Conversion Rate | Order sessions / Sessions |
| No-purchase Sessions | Session không tạo đơn hàng |
| No-purchase Rate | No-purchase sessions / Sessions |


## Analysis workflow

1. Làm sạch thời gian và lọc session có nguồn marketing.
2. Xác định landing page đầu tiên trong mỗi session.
3. Join session với order và product để tạo master journey.
4. Chuyển journey thành các cặp source-target.
5. Vẽ Sankey ba tầng và tô màu theo outcome.
6. Drill-down theo source, landing page, tháng, quý và template.

## Key findings

- `bsearch` có conversion rate khoảng **7.19%**, cao hơn `gsearch` khoảng **6.75%** và `socialbook` khoảng **3.21%**.
- `gsearch` tạo volume lớn hơn, trong khi `bsearch` hiệu quả chuyển đổi tốt hơn.
- `/lander-3` có khoảng **79,000 sessions** và no-purchase rate khoảng **96.61%**, là landing page cần ưu tiên kiểm tra.
- `The Original Mr. Fuzzy` chiếm phần lớn sản phẩm được mua từ cả gsearch và bsearch trong kết quả hiện tại.

## Recommendations

- Duy trì gsearch để bảo vệ traffic volume và thử nghiệm mở rộng bsearch có kiểm soát.
- A/B test CTA, message match, tốc độ tải và cấu trúc của `/lander-3` và `/lander-1`.
- Theo dõi conversion theo tháng/quý để phát hiện tác động của thay đổi giao diện hoặc campaign.
- So sánh landing-page template thay vì chỉ đánh giá từng URL riêng lẻ.

## Limitations

- Trong notebook, “drop-off” được operationalize là session không có order; đây không đồng nghĩa với bounce hoặc thoát ngay tại landing page.
- Chỉ giữ session có `utm_source`, do đó không phản ánh organic/direct traffic.
- Chưa kiểm soát device, campaign, ad content, pageview depth hoặc thời gian trên trang.

## Repository structure

```text
customer-journey-sankey-analysis/
├── README.md
├── customer_journey_sankey_analysis.ipynb
├── requirements.txt
├── .gitignore
└── data/
    └── README.md
```

## How to run

### Google Colab

1. Tải notebook từ repository hoặc mở notebook trên GitHub rồi chọn **Open in Colab** nếu nút này khả dụng.
2. Upload các file được liệt kê trong [`data/README.md`](./data/README.md) vào `/content/`.
3. Chọn **Runtime → Restart session and run all** để kiểm tra notebook chạy từ đầu đến cuối.

### Local Jupyter

```bash
pip install -r requirements.txt
jupyter notebook
```

Notebook hiện được thiết kế chủ yếu cho Google Colab và có thể dùng đường dẫn `/content/...`. Khi chạy local, cần đổi đường dẫn dữ liệu sang thư mục `data/`.

## Tools

- Python
- Jupyter Notebook / Google Colab
- pandas, matplotlib, plotly

## Suggested GitHub topics

`python` · `pandas` · `plotly` · `sankey-diagram` · `customer-journey-analytics`

## Author

**Your Name**  
Data Analyst Portfolio  
LinkedIn: `add-your-link`  
Email: `add-your-email`

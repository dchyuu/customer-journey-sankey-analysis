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


### Download data

Do kích thước dữ liệu lớn, các file dữ liệu đầy đủ không được lưu trực tiếp trong repository.

[**Mở thư mục dữ liệu dùng chung trên Google Drive**](https://drive.google.com/drive/folders/1NrvyT_tMArcoZvI_sEgPLclD4Vw0iCBq?usp=sharing)

Chỉ cần tải các file được liệt kê trong bảng phía trên; các file còn lại trong thư mục Drive được sử dụng cho những mini project khác. Giữ nguyên tên file để notebook đọc dữ liệu chính xác.

> Quyền chia sẻ đề xuất: **Anyone with the link → Viewer**. Hãy kiểm tra link bằng cửa sổ ẩn danh trước khi public repository.

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
└── .gitignore
```

## How to run

### Google Colab

1. Mở notebook từ repository bằng Google Colab.
2. Truy cập [thư mục dữ liệu trên Google Drive](https://drive.google.com/drive/folders/1NrvyT_tMArcoZvI_sEgPLclD4Vw0iCBq?usp=sharing).
3. Tải đúng các file được liệt kê trong phần **Dataset** và upload chúng vào thư mục `/content/` của Colab.
4. Giữ nguyên tên file, sau đó chọn **Runtime → Restart session and run all**.

### Local Jupyter

1. Tải đúng các file được liệt kê trong phần **Dataset** từ [Google Drive](https://drive.google.com/drive/folders/1NrvyT_tMArcoZvI_sEgPLclD4Vw0iCBq?usp=sharing).
2. Đặt các file cạnh notebook hoặc cập nhật đường dẫn đọc dữ liệu trong notebook cho phù hợp.
3. Cài thư viện và mở Jupyter:

```bash
pip install -r requirements.txt
jupyter notebook
```

Notebook hiện được thiết kế chủ yếu cho Google Colab và có thể sử dụng đường dẫn `/content/...`; khi chạy local, cần thay đường dẫn này bằng vị trí dữ liệu trên máy.

## Tools

- Python
- Jupyter Notebook / Google Colab
- pandas, matplotlib, plotly

# Day 16 Submission — Phiên bản A (End-of-session)

## Members
- Hứa Quang Linh — Solo learner (AI Product Strategy)

*(Ghi chú: Đây là bản cá nhân. Phiên bản A là snapshot tư duy tại thời điểm cuối buổi Day 16, sẽ được nâng cấp lên Phiên bản B sau khi có thêm thời gian suy nghĩ và critique.)*

---

## 1. Idea reframed

**Original idea:**
> Xây một AI Agent nhận địa điểm của từng thành viên trong nhóm bạn (10 người ở các phường khác nhau tại Hà Nội), rồi gợi ý 3 quán ăn uống có vị trí cân bằng khoảng cách giữa mọi người, giúp nhóm chốt địa điểm họp mặt nhanh hơn.

**Reframed as a product opportunity:**
> **Observed gap:** Nhóm bạn 8–15 người sống rải rác ở Hà Nội mất 30–60 phút mỗi lần họp nhóm chỉ để bàn địa điểm trên group chat, vì không có một "fairness metric" chung nào để so sánh — mọi đề xuất đều dễ bị phản bác kiểu "quán đó mình đi xa quá". Cuộc tranh luận thường kết thúc bằng việc chiều người ồn ào nhất chứ không phải công bằng nhất.
>
> **Founding belief:** Việc chốt địa điểm họp mặt không phải là bài toán gu cá nhân — nó là bài toán tối ưu hóa có ràng buộc (distance fairness + chất lượng quán + sức chứa) mà con người làm rất tệ qua chat. Một AI Agent có thể giải xong trong <30 giây điều mà nhóm chat cần 40 phút.
>
> Sản phẩm không bán "tìm quán ngon" (đã có Foody, Google Maps). Sản phẩm bán **"chốt nhanh, chốt công bằng"** — kết quả mà một nhóm có thể dùng ngay, không phải công cụ họ phải cấu hình.

---

## 2. Customer / Segment Card

- **Segment name:** Nhóm bạn offline đều đặn tại Hà Nội — 8–15 thành viên, sống rải rác ≥4 quận/phường khác nhau, họp ăn uống ≥2 lần/tháng (dân văn phòng / cựu sinh viên / hội thể thao amateur / hội đồng nghiệp cũ, 24–35 tuổi).
- **Operational context:** Cả nhóm giao tiếp chủ yếu qua Zalo group hoặc Messenger. Không có ai là "trưởng nhóm chính thức" — quyết định địa điểm là thỏa thuận tập thể. Mỗi người có một "phường nhà" cố định (chỗ ở hoặc chỗ làm).
- **Recurring workflow:** Trước mỗi buổi họp, 1 người nhắn "Hẹn tuần này ở đâu ae?" → nhiều đề xuất → tranh luận 30–60 phút → thường chốt ở quán "quen" gần 1–2 người có tiếng nói mạnh nhất → 2–3 người luôn cảm thấy phải đi xa.
- **Pain moment:** Khoảnh khắc nhóm chat tắc 20+ phút với các tin nhắn kiểu "quán X xa mình quá", "hôm trước ở gần cậu rồi mà", "thôi tiện ai chốt đi" — người khởi xướng buổi họp thấy mệt, người ở xa thấy bất công, người đang đói thấy bực.
- **Why now:**
  1. Hà Nội vừa tái cấu trúc địa giới hành chính (nhiều phường mới/sát nhập từ 2025) → mọi người ít quen địa lý mới, khó tự ước lượng "ở giữa".
  2. Số nhóm bạn cùng cơ quan / cựu sinh viên duy trì offline sau COVID tăng, tần suất họp mặt ổn định lại.
  3. API bản đồ (Google Maps Distance Matrix, Mapbox, HERE) + LLM đủ rẻ để chạy đa điểm mà không cần tự xây.
- **Access path:** Bắt đầu từ chính network cá nhân (nhóm bạn 10 người hiện tại) làm design partner đầu tiên → lan qua các nhóm bạn chung → seed vào 2–3 hội nhóm Facebook Hà Nội đặc thù (hội cựu SV, hội dân công sở Cầu Giấy/Đống Đa) → sau đó tích hợp qua mini-app Zalo để đi theo kênh chat gốc.

**One-sentence description:**
> Nhóm 10 người bạn Hà Nội rải ở 8 phường khác nhau, họp nhậu đều 3 lần/tháng, mỗi lần mất gần nửa tiếng chỉ để chốt địa điểm vì không ai muốn là người đi xa nhất.

---

## 3. Need Map (2–3 needs)

### Need #1 (priority) — Chốt địa điểm công bằng trong <5 phút

- **Statement (JTBD):** When nhóm 10 người của tôi cần hẹn ăn uống tuần này, I want một danh sách 3 quán được chọn dựa trên khoảng cách cân bằng giữa tất cả thành viên, so I can chốt địa điểm trong 5 phút thay vì mất 30–60 phút debate trong group chat.
- **Current workaround:** (a) Một người "hiền" nhất sẽ chịu thiệt, đề xuất quán gần nhóm đa số; (b) Dùng Google Maps thủ công nhập 2–3 điểm rồi ước lượng "giữa đường"; (c) Chọn đại quán quen → 2–3 người đi xa chịu đựng → lần sau vẫn lặp lại.
- **Pain signal:** Mất **30–60 phút/lần × 3 lần/tháng = ~2 giờ/tháng/nhóm** chỉ cho khâu chốt địa điểm. Tệ hơn: tạo cảm giác bất công tích tụ → một số thành viên bắt đầu né tránh họp ("bận rồi ae chơi vui nhé").
- **Evidence / proxy evidence:**
  - *Direct (cá nhân):* Chính nhóm của tôi — 10 người, chat log ~3 tháng gần nhất cho thấy mỗi lần hẹn có trung bình 25–40 tin nhắn tranh luận địa điểm trước khi chốt.
  - *Proxy:* Query "app chọn quán giữa đường" / "meet halfway restaurant" trên Google có kết quả rải rác (WhatsHalfway.com, Whatshalfway chỉ tính 2 điểm, không tính >5 điểm + không tính chất lượng quán). Reddit r/hanoi và nhiều nhóm FB "Ăn gì Hà Nội" có post lặp đi lặp lại kiểu "gợi ý quán gần tất cả các quận trung tâm".
  - *Unknown:* Chưa khảo sát có cấu trúc — mới là proxy. Cần 10 interview nhóm để xác định thực sự pain này đứng đâu trong top.
- **Why underserved:** Google Maps / Foody giải bài toán **khám phá quán** (1 người tìm cho chính mình). Không có sản phẩm nào giải bài toán **n-người cùng chốt** với ràng buộc fairness. Whatshalfway.com chỉ hỗ trợ 2 điểm và không biết gì về quán Việt Nam. Mô hình kinh doanh "commission/quảng cáo quán" của các app hiện tại đẩy họ tối ưu cho quán trả tiền, không cho công bằng nhóm.

### Need #2 — Công bằng dài hạn qua nhiều lần họp (fairness memory)

- **Statement (JTBD):** When nhóm đã họp nhiều lần, I want hệ thống nhớ ai đã đi xa ở những buổi trước, so I can đảm bảo lần này đến lượt người khác đi xa, chứ không phải cùng một vài người chịu thiệt mãi.
- **Current workaround:** Không có. Một vài nhóm có "luật bất thành văn" kiểu lần trước ở quán A nhà Quang thì lần này phải ở gần nhà Lan — nhưng phụ thuộc vào trí nhớ và sự nhắc nhở của vài người.
- **Pain signal:** Resentment tích tụ âm thầm. Pain này không bốc cháy ngay một buổi, nhưng là lý do nhiều nhóm im ắng dần sau 6–12 tháng.
- **Evidence / proxy evidence:** *Proxy:* Pattern quen thuộc trong các nhóm bạn lâu năm — một số người bắt đầu ít tham gia hơn, thường là người sống xa "trung tâm nhóm". Cần xác minh bằng interview. Đây vẫn là giả định mạnh chứ chưa có bằng chứng cứng.
- **Why underserved:** Các app review quán hoàn toàn stateless — mỗi lần tìm là một lần độc lập. Khái niệm "nhóm có lịch sử" không tồn tại trong sản phẩm nào tôi biết tại VN hiện tại.

### Need #3 (optional) — Chất lượng quán đủ dùng được (quality floor)

- **Statement (JTBD):** When AI gợi ý địa điểm cân bằng, I want các quán đó phải đủ tốt về mặt cơ bản (rating ≥ 4.0, còn mở cửa, đủ chỗ cho nhóm 10 người), so I can chốt ngay mà không phải tự verify lại trên Google/Foody.
- **Current workaround:** Sau khi "chốt" địa điểm từ Google Maps, người khởi xướng vẫn phải click vào xem review, gọi điện hỏi có chỗ ngồi không — thêm 10–15 phút.
- **Pain signal:** Nếu AI chỉ gợi ý theo khoảng cách mà bỏ qua chất lượng, sản phẩm sẽ bị bỏ ngay sau 1–2 lần gợi ý trúng quán tệ. Đây là **risk**, không phải need độc lập.
- **Evidence / proxy evidence:** Logic sản phẩm — nếu không filter chất lượng, trust của nhóm với AI sụp đổ sau 1 lần sai.
- **Why underserved:** Thực ra **không** underserved — Google/Foody đã làm quality signal tốt. Chúng ta chỉ cần tích hợp, không cần giải.

---

## 4. Strategy Statement

**For** nhóm bạn 8–15 người tại Hà Nội sống rải rác nhiều phường và họp offline ăn uống ≥2 lần/tháng,

**who struggle with** việc mất 30–60 phút mỗi lần họp chỉ để chốt địa điểm công bằng, dẫn đến resentment tích tụ khiến vài người dần bỏ nhóm,

**our product helps them** chốt được top-3 quán cân bằng khoảng cách (và có lịch sử công bằng qua nhiều lần) trong dưới 60 giây bằng một lệnh duy nhất,

**through** một AI Agent nhận danh sách phường/địa chỉ của các thành viên, chạy multi-point geospatial optimization (centroid có trọng số + fairness metric như max-min-travel-time) trên Google Maps Distance Matrix API, lọc qua quality floor (rating ≥ 4.0 + capacity đủ ≥ N người + đang mở cửa), và trả về 3 lựa chọn kèm bảng so sánh travel time cho từng thành viên,

**unlike** (a) group chat tự quyết định — chậm, thiên vị người nói to nhất; (b) Whatshalfway.com — chỉ 2 điểm, không hiểu quán VN; (c) Google Maps — công cụ cá nhân, không giải bài toán n-người; (d) Foody/ShopeeFood — chỉ giúp khám phá, không giải fairness,

**because we can leverage** (i) design partner sẵn có (nhóm 10 người của chính tôi) để iterate hằng tuần với workflow thật; (ii) dữ liệu lặp lại về mỗi nhóm (ai hay đi xa, preference món) để fairness score ngày càng đúng — một dạng domain-learning flywheel mà một app "tìm quán chung" đơn lẻ không có.

---

## 5. Moat Hypothesis

**Moat mechanism (chính):** Group-memory flywheel — sự kết hợp của **workflow embedding** và **data compounding ở cấp nhóm**, không phải cấp người dùng lẻ.

**If we deploy 50 nhóm bạn Hà Nội đều đặn trong 6 tháng, the following improve:**
1. **Fairness model trở nên có ngữ cảnh:** Hệ thống học được "ở nhóm này, Minh đi xa 3 lần rồi → lần này tự động de-prioritize quán phía Đông" — điều Google Maps không bao giờ biết vì nó stateless.
2. **Venue ranking được điều chỉnh theo preference nhóm:** Mỗi nhóm có gu riêng (nhậu / cafe / lẩu / chay). Sau 10–15 buổi, gợi ý top-3 trúng gu ngày càng cao → nhóm chốt nhanh hơn → dùng nhiều hơn.
3. **Switching cost tăng theo thời gian:** Một nhóm đã có 20 buổi họp trong app với lịch sử fairness + preference không dễ bỏ sang app khác — vì bỏ đồng nghĩa với reset lịch sử công bằng, quay lại điểm 0.

**Why competitors cannot easily replicate this:**
> Google Maps / Foody được thiết kế around **cá nhân user**, không around **group object**. Để họ làm lại data model theo "nhóm có lịch sử" là rewrite lớn + không align với business model quảng cáo hiện tại. Một startup mới vào có thể copy thuật toán fairness trong 1 tuần, nhưng không copy được **group history** của 50 nhóm đang active — đó là asset chỉ tích lũy qua thời gian sử dụng thật. **Caveat (honest):** Moat này chỉ thành hình *sau* khi có ~500+ nhóm active. Trước đó, sản phẩm rất dễ bị copy. Đây là rủi ro chính cần nhận diện.

---

## 6. Initial TAM / SAM / SOM view

| Layer | Estimate | Key assumptions | Confidence |
|---|---|---|---|
| **TAM** | ~2–4 triệu "buổi họp cần chốt địa điểm"/năm tại VN đô thị lớn. Nếu monetize $0.3–1/buổi (premium/commission) → **$0.6M–4M/năm** | VN có ~25M dân đô thị 22–40 tuổi; giả sử 20% thuộc nhóm social họp offline đều → 5M người; trung bình 10 người/nhóm → 500k nhóm; mỗi nhóm 0.5–1 buổi/tháng cần AI hỗ trợ chốt → 3–6M buổi/năm (lấy band thấp để thận trọng). | **Low** |
| **SAM** | Hà Nội + TPHCM, nhóm 8–15 người họp ≥2 lần/tháng. ~30–60k nhóm active → ~500k–1M buổi/năm → nếu $0.5/buổi → **$0.25M–0.5M/năm** | Ước đoán nhóm "đủ đông + đủ rải + đủ đều" chỉ chiếm 15–25% tổng nhóm social. Giả định pricing freemium + commission mỗi booking chốt được. | **Low–Medium** |
| **SOM (12–24 tháng)** | 100–300 nhóm active tại Hà Nội = 3.6k–10k buổi/năm được giải quyết qua app. Revenue $1.8k–$10k/năm. **Không đủ sống bằng consumer pricing** → cần thử B2B/channel | Bắt đầu từ network cá nhân (10–20 nhóm đầu), lan qua word-of-mouth + tích hợp Zalo mini-app. Giả sử conversion từ "thử 1 lần" sang "dùng đều" là 20–30%. | **Medium** |

**Top 3 unknowns requiring further research:**
1. **Willingness to pay thực sự.** Pain có rõ, nhưng nhóm bạn có trả tiền cho cái này không, hay chỉ dùng nếu free? Nếu free-only → buộc phải đi hướng commission từ quán (nhưng như vậy tạo conflict với fairness claim). *Cần: 10 user interview về WTP.*
2. **Zalo mini-app distribution.** Có thật sự rẻ và nhanh để đi theo kênh chat gốc không, hay policy Zalo sẽ chặn? *Cần: research chính sách Zalo Mini Program + 1 prototype.*
3. **Liệu "fairness memory" có thật sự là need #2 hay tôi đang tự gán?** Pain này là giả định của tôi, chưa có evidence trực tiếp. Có thể 80% nhóm không care về công bằng dài hạn, chỉ cần giải quyết cuộc 1-off. *Cần: interview 15 người trong nhóm họp đều xem họ có track "lần trước ở đâu" không.*

**Judgment:**
- [ ] Worth pursuing now
- [x] **Worth pursuing but not now** (need to validate WTP và fairness-memory hypothesis trước, cũng như kiểm tra kênh phân phối Zalo mini-app)
- [ ] Not worth pursuing as currently framed

*Lý do:* Pain là thật và recurring, nhưng TAM hẹp và WTP chưa rõ. Làm được MVP rất nhanh (geospatial + Maps API) nhưng rủi ro lớn là không ai chịu trả tiền. Nên chạy 2 tuần validation trên chính nhóm của tôi + 2 nhóm bạn khác trước khi commit thêm.

---

## 7. Positioning Note (2 sentences)

**What we are:**
> Một AI Agent giúp nhóm bạn 8–15 người ở Hà Nội chốt địa điểm ăn uống công bằng trong dưới 60 giây, thay thế 30–60 phút tranh luận trong group chat bằng top-3 gợi ý có fairness metric rõ ràng.

**What we are not / not yet:**
> Chúng tôi **không phải** một app khám phá quán mới, không cạnh tranh với Foody/ShopeeFood/Google Maps ở khía cạnh đánh giá chất lượng; và **chưa** phải một booking platform — giai đoạn đầu chỉ giải bài toán "chốt địa điểm", chưa động tới đặt bàn hay thanh toán.

---

## 8. Self-assessment before Day 17

**Trong 6 mắt xích, mắt xích nào đang yếu nhất?**

> **Market Size (Market Sizing)** đang yếu nhất. Con số TAM/SAM/SOM mà tôi đưa ra dựa trên quá nhiều giả định chồng chất (25M × 20% × ...) và tôi chưa có benchmark từ bất kỳ công ty tương tự nào tại VN — một phần vì **chưa có công ty nào giải chính xác bài toán này**, điều vừa là cơ hội vừa là tín hiệu rủi ro (có thể vì thị trường quá nhỏ).
>
> Mắt xích yếu thứ hai là **Moat** — ý tưởng "group-memory flywheel" nghe hợp lý trên giấy nhưng chỉ hoạt động ở quy mô 500+ nhóm active. Trước ngưỡng đó tôi không có defensibility thật sự, điều cần được nói thẳng thay vì giấu.

**Open questions chúng tôi muốn khám phá thêm ở Day 17:**
1. MVP scope tối thiểu để test được Need #1 trong 2 tuần — chỉ cần prompt-based agent dùng Google Maps API, hay cần UI riêng ngay? Có thể chạy MVP trong group Zalo chỉ bằng 1 bot không?
2. Assumption nào cần kill trước? Tôi đang nghiêng về: (a) pain này đủ mạnh cho nhóm người khác ngoài nhóm tôi, (b) họ sẽ thử 1 lần nếu được giới thiệu. WTP có thể khảo sát sau.
3. Experiment nào cho 2 tuần đầu? Đề xuất: chạy agent prototype trên 3 nhóm bạn thật (nhóm tôi + 2 nhóm khác), đo (i) thời gian chốt trước/sau, (ii) số lần dùng lại ở buổi họp kế tiếp mà không cần nhắc, (iii) feedback qualitative từ người "hay đi xa nhất" trong nhóm.

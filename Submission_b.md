# Day 16 Submission — Phiên bản B (BTVN / Final)

## Members
- Hứa Quang Linh — Solo learner (AI Product Strategy)

*Ghi chú: Phiên bản B này được viết sau khi nhìn lại Phiên bản A với critique prompt và đã pivot 2 chỗ quan trọng (chi tiết ở §9. Iteration Log). Mục tiêu của B không phải "polish câu chữ", mà là **sửa những chỗ A đang yếu thật sự**.*

---

## 1. Idea reframed

**Original idea:**
> Xây một AI Agent nhận địa điểm của từng thành viên trong nhóm bạn (10 người ở các phường khác nhau tại Hà Nội), rồi gợi ý 3 quán ăn uống có vị trí cân bằng khoảng cách giữa mọi người, giúp nhóm chốt địa điểm họp mặt nhanh hơn.

**Reframed as a product opportunity:**
> **Observed gap:** Trong mọi nhóm bạn 8–15 người họp offline đều đặn tại Hà Nội, tồn tại **một người** luôn đóng vai "người khởi xướng kiêm điều phối kiêm quyết định cuối" — và người đó đang bị burn out âm thầm. Họ mở chat, nhận 15–30 đề xuất mâu thuẫn, rồi phải tự quyết định trong tình thế "làm hài lòng mọi người" bất khả thi. Cả nhóm thấy "chốt địa điểm hơi mệt"; người organizer thấy **pain tập trung** — và chính họ là người sẽ trả tiền, nói cho bạn bè khác biết, và quyết định nhóm còn duy trì họp offline hay không.
>
> **Founding belief (đã sharpen so với A):** Sản phẩm không phục vụ "nhóm" như một thực thể trừu tượng; sản phẩm phục vụ **một người cụ thể trong mỗi nhóm** — the reluctant organizer — bằng cách thay công việc điều phối bằng một lệnh duy nhất. Kết quả đo được không phải "mọi người vui" (không đo được), mà là **"organizer không còn là người chốt cuối cùng"**: AI chốt, organizer chỉ forward.
>
> Sản phẩm bán **"tháo việc điều phối khỏi vai của 1 người"**, không phải "gợi ý quán" (đã có Foody) và không phải "tìm điểm giữa" (đã có Whatshalfway, nhưng không giải gì cho quán Việt).

---

## 2. Customer / Segment Card

- **Segment name:** **"Reluctant organizer"** — thành viên điều phối chính của nhóm 8–15 người tại Hà Nội, thường 26–34 tuổi, dân văn phòng, là người duy trì hoạt động offline của một nhóm cựu học sinh/sinh viên / hội đồng nghiệp cũ / hội thể thao amateur đã có ≥12 tháng lịch sử họp mặt.
- **Operational context:** Nhóm dùng Zalo hoặc Messenger làm kênh chính. Organizer không phải lãnh đạo chính thức, chỉ là người "hiền + có trách nhiệm" nhất — thường được tag mặc định khi có câu hỏi tổ chức. Họ làm việc này unpaid, thường không phàn nàn công khai nhưng sẽ là người đầu tiên bỏ cuộc nếu cảm thấy bất công.
- **Recurring workflow:** (1) Organizer post "tuần này hẹn ở đâu ae?" → (2) Nhận 5–15 đề xuất trong 20–60 phút → (3) Đề xuất mâu thuẫn (quán X xa Y gần) → (4) Organizer cuối cùng tự quyết (thường chọn quán gần đa số), đôi khi phải gọi điện riêng cho 1–2 người ở xa để thương lượng → (5) Forward quyết định, vài người im lặng miễn cưỡng đồng ý.
- **Pain moment:** Khoảnh khắc organizer nhìn group chat 15 phút không ai chịu đề xuất đầu tiên, rồi lại phải tự đẩy quả bóng "ok để mình chọn vậy" — đi kèm cảm giác "sao lúc nào cũng là mình". Pain lặp lại đúng 3 lần/tháng với cường độ nhất quán.
- **Why now:**
  1. **Địa lý Hà Nội mới phức tạp hơn:** sát nhập phường từ 2025 khiến ngay cả dân Hà Nội gốc cũng không còn ước lượng chuẩn "giữa đường" bằng trực giác nữa.
  2. **LLM + Maps API rẻ đủ để chạy agent đa điểm** ở giá $0.001–0.01/lần gọi — đủ thấp để MVP miễn phí mà không âm vốn.
  3. **Nhóm offline post-COVID đã ổn định lại:** tần suất họp không còn biến động như 2022–2024; các nhóm "sống sót" đã có cadence rõ → use case recurring.
  4. **Zalo Mini App mở API cho bot:** có kênh phân phối nằm đúng chỗ workflow đang diễn ra (group chat), không cần ép user install app riêng.
- **Access path:** (a) Network cá nhân — tôi chính là organizer của nhóm 10 người đang gặp pain này → design partner 0 miễn phí. (b) Lan qua các organizer khác qua word-of-mouth (họ là một cộng đồng ẩn nhưng dễ nhận ra — luôn là người gửi invite). (c) Seed vào 2–3 nhóm Facebook "Hội cựu học sinh Ams/Chu Văn An/KHTN" — đây là nơi có mật độ organizer cao nhất. (d) Zalo Mini App để đi theo kênh gốc.

**One-sentence description:**
> Chị Lan, 29 tuổi, làm marketing ở Cầu Giấy, đều đặn là người tổ chức các buổi họp lớp cấp 3 cho nhóm 12 bạn đã chuyển đi khắp Hà Nội — mỗi tháng mất ~2 giờ chỉ để chốt địa điểm, và đã bắt đầu lười tổ chức vì "mệt".

---

## 3. Need Map (2 needs — đã giảm từ 3 needs của A)

### Need #1 (priority) — Tháo việc "quyết định cuối" khỏi vai organizer

- **Statement (JTBD):** When tôi (organizer của nhóm 12 người) cần hẹn buổi họp mặt tuần này, I want một top-3 gợi ý quán có fairness score rõ ràng kèm bảng so sánh travel time cho từng người trong nhóm, so I can post nguyên kết quả vào chat và để nhóm chọn 1 trong 3, thay vì tôi phải tự quyết định rồi gánh trách nhiệm làm ai đó thất vọng.
- **Current workaround:** (a) Organizer tự quyết → mang guilt; (b) Dùng Google Maps nhập 2–3 điểm ước lượng bằng mắt (dưới chuẩn về fairness với n>2 người); (c) Poll trong chat → mất thêm thời gian và thường không ai vote.
- **Pain signal:** Ước tính (dựa trên chat log nhóm tôi + 2 nhóm tôi quan sát) **30–60 phút coordination time/buổi × 3 buổi/tháng = 1.5–3 giờ/tháng/organizer**. Cộng với cognitive load "mình đã làm ai thiệt lần này không" — thứ khó đo nhưng là lý do #1 organizer im lặng nghỉ việc điều phối.
- **Evidence / proxy evidence:**
  - *Direct:* Chat log 3 tháng gần nhất của nhóm 10 người của tôi — trung bình 27 tin nhắn/buổi dành riêng cho "chốt địa điểm" (đếm thủ công tháng 3/2026). Tôi là organizer, đã tự đo.
  - *Proxy 1:* Pattern trên Reddit r/hanoi và các nhóm FB "Ăn gì Hà Nội" — các post kiểu "gợi ý quán trung tâm cho nhóm từ các quận khác nhau" xuất hiện đều (quan sát định tính, chưa count chính xác).
  - *Proxy 2:* Whatshalfway.com (US product, 2 điểm) tồn tại và có traffic → chứng tỏ pain "meet in the middle" là thật, ít nhất với n=2. Chưa có sản phẩm tương đương cho n>2 tại VN.
  - *Chưa có (honest):* chưa làm interview có cấu trúc với ≥5 organizer ngoài network của tôi. Đây là evidence gap #1 cần fix ở Day 17.
- **Why underserved:** Mọi sản phẩm F&B hiện tại được thiết kế around **cá nhân-user-tìm-quán-cho-bản-thân** (Google Maps, Foody, ShopeeFood). Không có sản phẩm nào có **"group" là first-class object**. Whatshalfway không hiểu quán Việt và giới hạn 2 điểm. Commission-based business model của Foody/ShopeeFood đẩy họ tối ưu cho quán trả tiền, không cho fairness.

### Need #2 — Niềm tin "quán này không phải trò đùa" (quality floor at decision time)

- **Statement (JTBD):** When AI đưa ra top-3 quán cân bằng khoảng cách, I want mỗi quán phải được verify nhanh về rating ≥ 4.0, còn mở cửa giờ đó, và đủ chỗ cho 10+ người, so I can forward thẳng vào group chat mà không sợ bị nhóm phản bác "quán này đóng cửa rồi" / "quán này không có chỗ cho nhóm".
- **Current workaround:** Sau khi chọn sơ bộ từ Maps, organizer phải tự click vào từng quán xem review, đôi khi gọi điện trước — thêm 10–15 phút thủ công.
- **Pain signal:** Nếu AI fail ở đây 1 lần ("quán gợi ý đã đóng cửa"), trust sụp đổ ngay. Đây là **threshold need** — không phải điểm cạnh tranh, mà là điều kiện cần để Need #1 có giá trị.
- **Evidence / proxy evidence:** Logic sản phẩm (trust công cụ quyết định bị reset sau sai lầm đầu tiên) + quan sát: các chatbot gợi ý nhà hàng trước đây chết vì chính lý do này. *Proxy.*
- **Why underserved:** Thực ra Google/Foody có data chất lượng. Pain không nằm ở "thiếu data", mà ở chỗ **organizer không có thời gian/muốn click vào check từng quán**. Sản phẩm của ta sẽ tích hợp, không tái tạo.

*(Need #3 của phiên bản A — "fairness memory qua nhiều buổi" — đã được gỡ. Lý do: đó là giả định của tôi chưa có evidence trực tiếp nào, chỉ là pattern tôi tưởng tượng ra. Giữ nó trong bản submit sẽ vi phạm "no polished nonsense". Đây sẽ là **future hypothesis để test ở Day 17+**, không phải need của hôm nay. Chi tiết ở §9.)*

---

## 4. Strategy Statement

**For** reluctant organizers của nhóm 8–15 người tại Hà Nội (cựu SV/đồng nghiệp cũ/hội thể thao amateur, họp offline ≥2 lần/tháng)

**who struggle with** việc phải tự gánh quyết định chốt địa điểm công bằng cho cả nhóm mỗi kỳ họp, trung bình 1.5–3 giờ/tháng cộng thêm guilt "lần này lại làm ai đó đi xa"

**our product helps them** chốt xong trong dưới 60 giây bằng cách post thẳng top-3 gợi ý có fairness score vào group chat, chuyển trách nhiệm chọn từ *cá nhân organizer* sang *tập thể nhóm*

**through** một Zalo Mini App / bot — tag @ChoQuanBot trong group chat kèm danh sách địa chỉ → nhận lại top-3 quán kèm bảng distance matrix và fairness score (max-min travel time, Jain's index, hoặc tương đương), đã được filter qua quality floor (rating ≥ 4.0, open now, đủ chỗ)

**unlike** (a) group chat tự quyết — chậm + dồn pain lên 1 người; (b) Whatshalfway.com — chỉ 2 người, không biết quán VN; (c) Google Maps — stateless, không giải n>2; (d) Foody/ShopeeFood — tối ưu discovery cá nhân và tối ưu quảng cáo, không tối ưu fairness nhóm

**because we can leverage** (i) design partner thật (nhóm 10 người của chính tôi) để iterate weekly với data workflow thật, (ii) phân phối qua Zalo Mini App đặt đúng chỗ workflow đang diễn ra — không ép user install app riêng, (iii) ở giai đoạn sau: dữ liệu lặp lại về mỗi nhóm (preference món, pattern buổi họp) để gợi ý ngày càng đúng — một data moat cấp **nhóm** mà Foody/Google không có vì họ design around cá nhân.

---

## 5. Moat Hypothesis (xếp theo thời gian, thành thật về yếu/mạnh)

Thay vì claim một moat duy nhất như phiên bản A, ở đây tôi xếp 3 tầng moat theo giai đoạn — và trung thực **0–6 tháng đầu không có moat thật sự**.

**Moat mechanism — layered:**

**Tầng 1 (0–6 tháng): Không có moat thật.** Chỉ có speed-of-execution advantage. Ai copy được thuật toán fairness đơn giản cũng đều làm được. Bảo vệ duy nhất: tốc độ iterate trên nhóm design partner.

**Tầng 2 (6–18 tháng): Distribution + workflow embedding.** Nếu seed được vào 100–300 nhóm active dùng qua Zalo Mini App với cadence đều, thì chuyển một nhóm sang sản phẩm khác đòi hỏi organizer re-onboard cả nhóm — switching cost cấp nhóm cao hơn cấp cá nhân nhiều.

**Tầng 3 (18+ tháng): Group-level data compounding.** Với 500+ nhóm active có ≥10 buổi lịch sử mỗi nhóm, fairness model học được context cấp nhóm (ai hay đi xa, preference món, giờ ưa thích, range budget). Đây là asset mà Foody/Google không có vì họ design around cá nhân, và không dễ sao chép vì cần thời gian thật tích luỹ.

**If we deploy 500 nhóm Hà Nội active trong 18 tháng, the following improve systematically:**
1. **Fairness model có ngữ cảnh cấp nhóm:** Biết được pattern "ở nhóm này, Minh đã đi xa 3 lần → de-prioritize quán phía Đông" — điều stateless maps không biết.
2. **Top-3 ranking ngày càng trúng gu nhóm:** Sau 10–15 buổi/nhóm, preference về loại món / range budget / giờ được personalize theo group identity.
3. **Organizer churn giảm:** Organizer thấy app "biết nhóm mình" → habit tag bot tự động → không churn sang tool khác.

**Why competitors cannot easily replicate this:**
> Thuật toán có thể copy trong 1 tuần. **Group-level history không copy được vì nó đòi hỏi thời gian thật với nhóm thật.** Foody/Google design around *user cá nhân* — để họ có được khái niệm "group có lịch sử", cần rewrite data model lớn và không align với ad-based business model. Một startup copycat có thể ra sản phẩm giống nhưng không có 18 tháng data lịch sử của 500 nhóm.
>
> **Honest caveat:** Moat này chỉ thật sự bảo vệ sau ngưỡng ~500 nhóm active với ≥10 buổi lịch sử/nhóm. **Trước ngưỡng đó, phòng tuyến duy nhất là tốc độ.** Day 17 cần trả lời: chúng ta đi được tới 500 nhóm trong bao lâu, và chi phí bao nhiêu?

---

## 6. Initial TAM / SAM / SOM view (triangulated 2 chiều)

Phiên bản A chỉ triangulate từ top-down với quá nhiều assumption chồng. Phiên bản B triangulate 2 chiều và show range rộng hơn.

### Approach 1 — Top-down

| Layer | Estimate | Key assumptions | Confidence |
|---|---|---|---|
| **TAM** (VN đô thị) | ~1.5–3.5M buổi họp nhóm/năm cần chốt địa điểm tại HN + HCM + Đà Nẵng. Monetizable value $0.3–1/buổi → **$0.5M–3.5M GMV-relevant/năm** | VN ~25M dân 22–40 tuổi đô thị; 15–25% thuộc nhóm social offline active (range rộng vì chưa có số chính thức, đây là giả định tôi cần flag); nhóm TB 10 người → 375k–625k nhóm; 4–6 buổi/năm cần AI chốt (không phải mọi buổi đều cần). | **Low** |
| **SAM** (HN + HCM, nhóm đủ điều kiện) | ~40–80k nhóm active đủ điều kiện → ~200k–500k buổi/năm → **$100k–500k/năm** | Nhóm "đủ đông + đủ rải + đủ đều" chỉ 15–25% tổng nhóm social. Freemium + commission từ quán (nếu đi hướng này, cần verify không xung đột với fairness claim). | **Low–Medium** |
| **SOM 12–24 tháng** | 150–500 nhóm active tại HN = 4.5k–15k buổi/năm. Consumer pricing: **$2k–$15k revenue/năm** | Bắt đầu từ network cá nhân → WOM qua các organizer khác → Zalo Mini App. Conversion "thử 1 lần → dùng đều" 20–30%. | **Medium** |

### Approach 2 — Bottom-up (triangulation)

- **Nhóm tôi biết đích danh:** ~6 nhóm (của tôi + bạn bè) chắc chắn sẽ thử trong tháng đầu nếu có sản phẩm miễn phí.
- **Nhóm cấp 2 qua WOM 1 hop:** ~30–60 nhóm khả thi (ước từ network organizer thường kết nối nhau).
- **Nhóm cấp 3 qua Facebook seed + Zalo Mini App trong 12 tháng:** ước 150–400 nhóm nếu CAC hợp lý (chưa biết CAC thực).
- **Con số SOM bottom-up:** ~150–400 nhóm 12 tháng → align với top-down SOM (150–500).
- **Bottom-up revenue:** Nếu 20% pay $2/tháng premium tier (fairness history + reserve feature) → 30–80 paying users → **$720–$1,920/năm**. Không đủ sống bằng consumer; cần B2B/commission channel.

### Reconciliation

Cả hai approach cho SOM **~150–500 nhóm trong 12–24 tháng tại HN** — số khá nhất quán. Nhưng **consumer revenue quá nhỏ** (<$15k/năm) để đứng một mình. Day 17 cần trả lời: đi commission từ quán (và xử lý xung đột fairness) hay đi B2B (team offsite của công ty nhỏ, HR organize)?

### Top 3 unknowns requiring further research
1. **WTP thật.** Pain rõ, nhưng organizer có trả tiền không, hay chỉ dùng nếu free? *Cần: 10 interview với organizer ngoài network + 1 landing page smoke test trong 2 tuần.*
2. **Distribution qua Zalo Mini App.** Chi phí seed thực tế bao nhiêu? Có chặn policy nào không? *Cần: đọc Zalo Mini Program policy + thử build 1 prototype bot minimum.*
3. **Chuyển đổi consumer → B2B.** Có một segment B2B tương tự (HR tổ chức team offsite 8–15 người) không? WTP B2B thường cao hơn 10–20x consumer. *Cần: 3 interview HR/admin công ty nhỏ.*

### Judgment
- [ ] Worth pursuing now
- [x] **Worth pursuing but not now** — cần validate WTP và thử distribution channel Zalo Mini App trong 2–3 tuần trước khi commit build. Nếu WTP yếu và CAC > LTV consumer, pivot sang B2B (corporate offsite) sẽ là nước đi đúng hơn là bỏ ý tưởng.
- [ ] Not worth pursuing as currently framed

---

## 7. Positioning Note (2 sentences)

**What we are:**
> Một Zalo bot giúp reluctant organizer của nhóm 8–15 người tại Hà Nội chốt địa điểm ăn uống công bằng trong dưới 60 giây, bằng cách biến quyết định của 1 người thành top-3 minh bạch cho cả nhóm chọn.

**What we are not / not yet:**
> Chúng tôi **không phải** một app khám phá quán mới (không cạnh tranh với Foody), không giải bài toán "nhóm >20 người" (scale không phù hợp), và **chưa** phải booking platform — giai đoạn đầu chỉ giải khâu "chốt", chưa đặt bàn hay thanh toán.

---

## 8. Self-assessment before Day 17

**Trong 6 mắt xích, mắt xích nào team đang yếu nhất?**

> Sau khi pivot ở phiên bản B, **Market Size** vẫn yếu nhất — nhưng yếu theo hướng khác trước. Ở phiên bản A, yếu vì assumption chồng chất không có benchmark. Ở phiên bản B, yếu vì **hai approach triangulate ra cùng 1 con số SOM, và con số đó nhỏ** (<$15k/năm consumer). Đây không phải lỗi tính toán mà là **tín hiệu thật** rằng consumer market hẹp, và nhiệm vụ Day 17 là tìm ra liệu có pivot B2B không.
>
> Mắt xích yếu thứ hai vẫn là **Moat ở giai đoạn 0–6 tháng**. Đã thành thật nhận diện "không có moat trong 6 tháng đầu, chỉ có speed". Không giấu, nhưng cũng chưa có solution.

**Open questions chúng tôi muốn khám phá thêm ở Day 17:**
1. **MVP scope 2 tuần:** chỉ cần Zalo bot prompt-based với Google Maps Distance Matrix API? Hay cần UI riêng? Khuynh hướng: bot-only, không UI, để test được ở cadence thật nhất.
2. **Kill question #1:** B2B (HR tổ chức offsite) có phải là market lớn hơn và WTP cao hơn không? Nếu có → pivot; nếu không → consumer + commission là con đường.
3. **Kill question #2:** "Fairness memory qua nhiều buổi" (Need đã bị gỡ ở phiên bản B) có thật sự là need hay chỉ là giả định của tôi? 5 organizer interview sẽ trả lời được — nếu có 3/5 xác nhận, đưa lại vào roadmap.

---

## 9. A → B Iteration Log (dành riêng cho Tiêu chí 5)

Dưới đây là những thay đổi thật giữa A và B, kèm lý do — không phải list cho đẹp mà để người chấm đối chiếu được.

| # | Phần | Phiên bản A | Phiên bản B | Lý do sửa |
|---|---|---|---|---|
| 1 | **Customer segment** | Toàn bộ nhóm bạn 8–15 người ở HN họp đều | **Reluctant organizer** — một cá nhân cụ thể trong mỗi nhóm | Bản A nói "phục vụ nhóm" nhưng nhóm không phải thực thể mua hàng. Pain tập trung ở 1 người/nhóm. Sharper segment = sharper strategy. Chứng minh: One-sentence description ở A mô tả nhóm (nhiều người), ở B mô tả 1 cá nhân (chị Lan 29 tuổi marketing Cầu Giấy) — cụ thể hơn nhiều. |
| 2 | **Need Map** | 3 needs: (1) chốt nhanh, (2) fairness memory, (3) quality floor | 2 needs: (1) tháo quyết định khỏi organizer, (2) quality floor | Need #2 của A ("fairness memory") là giả định của tôi — không có evidence trực tiếp. Giữ nó = vi phạm rule "no polished nonsense". Đã gỡ và chuyển thành hypothesis để test. Need #1 của B được re-frame quanh organizer (chuyển decision ownership) thay vì quanh nhóm. |
| 3 | **Strategy — distinct approach** | "AI tính fairness score + quality floor" (generic) | "Zalo Mini App / bot, tag trong group chat, không install app riêng" (cụ thể về distribution) | A nói AI làm gì, B nói AI **sống ở đâu** — distribution mechanism là phần quan trọng nhất của strategy với consumer product, A đã bỏ qua. |
| 4 | **Moat** | 1 moat duy nhất (group-memory flywheel), với caveat nhỏ ở cuối | 3 tầng moat theo timeline, thành thật "0–6 tháng không có moat thật" | A trình bày moat như một thứ có sẵn; B nhận diện thẳng rằng moat có timeline và 6 tháng đầu mình dễ bị copy. Đây là một điểm mà critique prompt (Issue: "moat too weak") đã chỉ ra. |
| 5 | **TAM/SAM/SOM** | Chỉ top-down, 1 chain assumption duy nhất | Top-down + bottom-up triangulation, đối chiếu 2 approach | Critique prompt flag "lack of evidence" cho market size. Bottom-up từ network thật cho ra cùng range → tăng niềm tin con số không bịa. **Cost trung thực:** kết luận là consumer market nhỏ, revenue <$15k/năm SOM, cần pivot B2B hoặc commission. |
| 6 | **Judgment** | Worth pursuing but not now (vì WTP chưa rõ) | Worth pursuing but not now (vì WTP + market size có dấu hiệu hẹp → cần quyết định B2B vs consumer trước) | Cùng kết luận, khác độ sắc. B nói rõ điều cần quyết định, không chỉ điều cần validate. |
| 7 | **Positioning** | 2 câu nói về sản phẩm | 2 câu nói về **ai sản phẩm giải quyết cho** + ngưỡng "nhóm ≤20 người" | "Not yet" bổ sung ranh giới rõ hơn về scale nhóm — tránh bị kéo sang use case >20 người mà fairness algorithm không còn scale. |
| 8 | **Self-assessment** | Nói Market và Moat yếu (đúng nhưng generic) | Nói cụ thể Market yếu vì *bị triangulate ra con số nhỏ*, Moat yếu vì *không có trong 6 tháng đầu* | Self-assessment ở A là "phần nào yếu"; ở B là "yếu vì lý do nào và cần làm gì". |

**Pivots lớn (không phải edit, là thay đổi hướng):**
- **Pivot 1 — Who we serve:** "nhóm bạn" → "reluctant organizer trong mỗi nhóm". Thay đổi này là gốc rễ — nó kéo theo Strategy, Moat, và Positioning đều phải viết lại.
- **Pivot 2 — Market framing:** từ "market nhỏ nhưng có thể mở rộng" → "market consumer hẹp, có thể cần pivot B2B". Đây là điều tôi ngại viết vì làm idea trông kém hấp dẫn — nhưng viết thẳng mới có ích cho Day 17.

**Điều tôi đã chủ động KHÔNG sửa (và lý do):**
- **Vẫn giữ "Worth pursuing but not now"** thay vì đổi thành "Worth pursuing now" cho nghe mạnh hơn — vì bằng chứng chưa đủ cho claim mạnh hơn, và rubric thưởng tỉnh táo chứ không thưởng lạc quan.
- **Vẫn giữ idea gốc, không pivot idea hoàn toàn** — idea "chốt địa điểm công bằng" là đúng; chỉ product definition và customer segment cần sharpen. Đúng đúng nguyên tắc chủ đạo của Day 16: *respect the idea, but do not trust its first product definition.*

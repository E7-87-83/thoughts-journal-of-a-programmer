# 一宗監視攝影機漏洞引發的資安事件：2021年3月的 Verkada Breach

_本文原為 HKUSPACE PG Dip 的作業；該課我取得A+的成績。以下為作業的中譯。 // HKUSPACE M202 Assignment 1 (Term 2040, 2022)_

隨着互聯網和無線科技的發展， IoT 設備越來越普遍。可是，這些設備安全嗎？監視攝影機這種傳統的保安設備，已經融入了 IoT 系統，但不幸地，有些資安負面事件揭發了。本文探討其中一宗案例。

2021年3月8日和9日，一班黑客進入了 Verkada －－一家矽谷公司－－的伺服器。 Verkada 提供 IoT 產品和服務，包括訪問控制（[physical] access control ）、室內環境探測器和監視攝影機。[1]本次資安事件最受影響的業務，是它們的監視攝影機業務。根據 Verkada 後來發表的報告[2]，這班黑客找到一個系統系數配置失當的顧客支援伺服器（"a misconfigured customer support server"），盜取了150,000個攝影機當下和記錄裏的真實拍攝片段。 Verkada 的服務提供人臉識別，這使得這群黑客輕易可以取得 Verkada 客戶場所活動部分的人們身分－－這些場所包括醫療中心、醫院、學校、監獄、購物中心、辦公室和私人寓所。[3] 這些黑客還下載了一份載有部分 Verkada 客戶名單連電郵地址。[4]

資訊安全有三大支柱：保密（ confidentiality ）、完整（ Integrity ）和可用（ Availability ）。顯然，在這次事件，保密性受損了：可能有身分外洩（identity leaks），而且 Verkada 客戶名單被盜了。8個客戶的WiFi credientials也被盜了。 Integrity 和 Availability 方面， Verkada 即時暫時關閉了所有內部管理戶口的權限，並在六小時內通知了它們的客戶。[5] Cloudflare 也是 Verkada 的客戶之一，Cloudflare 對媒體表示他們知道事件發生後隨即暫停了所有攝影機並中斷它們跟辦公室網絡的連結（“disabled the cameras and disconnected them from office networks”）。

數據完整和正確，在資訊安全上為之符合完整性。雖然入侵者也許沒有被授權修改 Verkada 和客戶現有的數據，但黑客們在檔案紀錄加了六個影片。此外，因為不得不暫時關閉了監視攝影機一段時間， Verkada 的客戶的監控場所數據欠完整了。數據的可用性也受影響，這方面可導致客戶一些不小的損失。我們都知道監視攝影機是加強一個場所的保安，但這些鏡頭暫時失去了作用。使用監視攝影機監察各種場所的客戶，冒受不同的損失：不誠實又不小心的員工打破了貨品而無人得知；私人寓所被不速之客闖入而無人得知；精神科診療地點的病人在暗角自我傷害，沒有醫護人員得知……

根據定義， IoT 設備需要網絡連接；根據功能性考慮，該設備和駁接的網絡資料庫可能儲存了用戶的私人資料。[7] 這次 Verkada breach 按 OWASP 的分類可為安全配置錯誤（Security Misconfiguration）和存取控制失效（Broken Access Control）。

Verkada 監控攝影機系統依賴雲端伺服器執行其任務。其基本功能包括錄影、臉部辨識，和臉部辨識後的身分辨識。這個架構並不簡單，而臉部辨識已涉及資訊安全三大支柱之一「保密」。早在 2020 ， Verkada 的一個員工把客戶資料庫裏的女性圖象下載了並與人分享。這件醜聞顯示 Verkada 系統的其中一個弱點：[8] 內部人員行為失當。防範這種事件發生，可以在聘請過程中更加謹慎，並教育員工這種行為的法律後果。回到本文關注的資安事件，這次是外部的入侵。一個人如果首次使用一個軟體或一套資訊系統，常要客戶服務支援。而客服系統是這次事件的攻擊點。根據 OWASP ，自動化過程能防範安全配置錯誤 [9] ；而 Verkada 在事件後宣布公司以後的開發都會採取「配置即代碼」（ configuration as code ） [10]。至於存取控制失效方面， Verkada 宣存公司會採取「職責分離」（ seperation of duty ）的資安政策。

根據 OWASP 在 2019年12月的報告，十大 IoT 安全漏洞原因為：一、密碼因素；二、不安全的網絡服務；三、不安全的 IoT 整體系統介面；四、欠缺安全的更新機制；五、使用不安全或過時的組件；六、私隱保護不足；七、資料傳送和儲存機制不安全；八、裝置管理欠奉；九、預設設定不安全；十、欠缺物理強化保護（"lack of physical hardening"）。[14][15] 我們可以猜測，第六項是 Verkada 攝影機系統最弱的環節，而基於它們使用的雲端和互聯網技術安排，第二、第三和第七項 Verkada 系統也做得不好。十項裏，有四項「中招」了。不禁令人想到，使用這些監視攝影機，是提高了安全，還是帶來風險呢？

我們的社會也許需要更多 IoT 設備的行業安全標準，需要更多相關的監管或制定標準的組織，使得未來再發生同類事件的風險降低。畢竟，我們有生之年， IoT 設備也許會在智慧城市和智慧建築上大規模使用。（完）

## 參考資料

[1] Verkada 官方網站: https://www.verkada.com/ . Retrieved August 30, 2022.

[2] Randolph, K., & Hunt, M.. March 9, 2021 Security Incident Report. Retrieved August 30, 2022,
from https://docs.verkada.com/docs/Security_Incident_Report_Version1.2.pdf

[3] Sonnemaker, T. Hackers breached security company Verkada and accessed 150,000 cameras
inside Tesla, hospitals, and jails. Business Insider. Retrieved August 30, 2022. https://www.businessinsider.com/verkada-hackers-breached-security-cameras-at-tesla-in-hospitals-jails-report-2021-3

[4]: 與 [2] 相同.

[5]: 與 [2] 相同.

[6]: 與 [3] 相同.

[7] Dr. WONG Ka Yan. Lecture Notes, M202 Computer Security.

[8]: 與 [3] 相同.

[9] OWASP. (2021). A05 Security Misconfiguration - OWASP Top 10:2021.
https://owasp.org/Top10/A05_2021-Security_Misconfiguration/

[10] markdefalco. What is Configuration as Code? docs.microsoft.com.
https://docs.microsoft.com/en-us/shows/one-dev-minute/what-is-configuration-as-code--one-dev-question
‌

[11] OWASP. (2021). A01 Broken Access Control - OWASP Top 10:2021.
https://owasp.org/Top10/A01_2021-Broken_Access_Control/

[12] Separation of Duties Policy | Cyber Security | ITD.
https://www.bnl.gov/cybersecurity/policies/separation-of-duties.php

[13] March 12th - A note from our CEO, Filip Kaliszan. Verkada Security Update Retrieved August
30, 2022, from https://www.verkada.com/security-update/

[14] OWASP IoT Top 10. https://owasp.org/www-chapter-toronto/assets/slides/2019-12-11-OWASP-IoT-Top-10---Introduction-and-Root-Causes.pdf

[15]: 與 [7] 相同.

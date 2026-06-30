---

<!-- CONTACT FORM SECTION -->
<h2 align="center">
  <img src="https://media.giphy.com/media/mSRwLcF7y6HhHjHj7W/giphy.gif" width="30px" />
  Contact Me
  <img src="https://media.giphy.com/media/mSRwLcF7y6HhHjHj7W/giphy.gif" width="30px" />
</h2>

<div align="center">
  <p><i>Fill out the form below and I'll get back to you ASAP!</i></p>
  
  <!-- CONTACT FORM -->
  <form id="contactForm" style="max-width: 500px; margin: 0 auto; padding: 20px; background: linear-gradient(135deg, #0d1117 0%, #161b22 100%); border-radius: 15px; border: 1px solid #00c6ff33;">
    
    <div style="margin-bottom: 15px; text-align: left;">
      <label style="color: #00c6ff; font-weight: bold; display: block; margin-bottom: 5px;">
        👤 Ismingiz
      </label>
      <input type="text" id="name" placeholder="Ismingizni kiriting..." required style="width: 100%; padding: 12px; border: 1px solid #00c6ff55; border-radius: 8px; background: #0d1117; color: #c9d1d9; font-size: 16px; outline: none; transition: all 0.3s;" onfocus="this.style.borderColor='#00c6ff'" onblur="this.style.borderColor='#00c6ff55'">
    </div>
    
    <div style="margin-bottom: 15px; text-align: left;">
      <label style="color: #00c6ff; font-weight: bold; display: block; margin-bottom: 5px;">
        📧 Emailingiz
      </label>
      <input type="email" id="email" placeholder="Email manzilingiz..." required style="width: 100%; padding: 12px; border: 1px solid #00c6ff55; border-radius: 8px; background: #0d1117; color: #c9d1d9; font-size: 16px; outline: none; transition: all 0.3s;" onfocus="this.style.borderColor='#00c6ff'" onblur="this.style.borderColor='#00c6ff55'">
    </div>
    
    <div style="margin-bottom: 15px; text-align: left;">
      <label style="color: #00c6ff; font-weight: bold; display: block; margin-bottom: 5px;">
        📝 Mavzu
      </label>
      <input type="text" id="subject" placeholder="Mavzuni kiriting..." style="width: 100%; padding: 12px; border: 1px solid #00c6ff55; border-radius: 8px; background: #0d1117; color: #c9d1d9; font-size: 16px; outline: none; transition: all 0.3s;" onfocus="this.style.borderColor='#00c6ff'" onblur="this.style.borderColor='#00c6ff55'">
    </div>
    
    <div style="margin-bottom: 20px; text-align: left;">
      <label style="color: #00c6ff; font-weight: bold; display: block; margin-bottom: 5px;">
        💬 Xabar
      </label>
      <textarea id="message" placeholder="Xabaringizni yozing..." rows="4" required style="width: 100%; padding: 12px; border: 1px solid #00c6ff55; border-radius: 8px; background: #0d1117; color: #c9d1d9; font-size: 16px; outline: none; resize: vertical; transition: all 0.3s;" onfocus="this.style.borderColor='#00c6ff'" onblur="this.style.borderColor='#00c6ff55'"></textarea>
    </div>
    
    <button type="submit" id="submitBtn" style="width: 100%; padding: 14px; background: linear-gradient(135deg, #00c6ff, #0072ff); border: none; border-radius: 8px; color: white; font-size: 18px; font-weight: bold; cursor: pointer; transition: all 0.3s; box-shadow: 0 4px 15px #00c6ff44;" onmouseover="this.style.transform='scale(1.02)'; this.style.boxShadow='0 6px 25px #00c6ff66'" onmouseout="this.style.transform='scale(1)'; this.style.boxShadow='0 4px 15px #00c6ff44'">
      <span id="btnText">🚀 Yuborish</span>
      <span id="btnLoader" style="display: none;">⏳ Yuklanmoqda...</span>
    </button>
    
    <div id="successMessage" style="display: none; margin-top: 15px; padding: 12px; background: #00c6ff22; border: 1px solid #00c6ff; border-radius: 8px; color: #00c6ff; font-weight: bold;">
      ✅ Xabaringiz muvaffaqiyatli yuborildi! Tez orada javob beraman.
    </div>
    
    <div id="errorMessage" style="display: none; margin-top: 15px; padding: 12px; background: #ff000022; border: 1px solid #ff0000; border-radius: 8px; color: #ff4444; font-weight: bold;">
      ❌ Xatolik yuz berdi. Iltimos qaytadan urinib ko'ring.
    </div>
  </form>
</div>

<script>
  // Telegram Bot Configuration
  const BOT_TOKEN = '8786901645:AAHVKHz7AuW2UKlrj7f_6VYPzyGbgu-4luQ';
  const CHAT_ID = 'YOUR_CHAT_ID'; // O'zingizning chat ID'ingizni qo'ying
  
  document.getElementById('contactForm').addEventListener('submit', async function(e) {
    e.preventDefault();
    
    // Form elementlarini olish
    const name = document.getElementById('name').value.trim();
    const email = document.getElementById('email').value.trim();
    const subject = document.getElementById('subject').value.trim();
    const message = document.getElementById('message').value.trim();
    const submitBtn = document.getElementById('submitBtn');
    const btnText = document.getElementById('btnText');
    const btnLoader = document.getElementById('btnLoader');
    const successMsg = document.getElementById('successMessage');
    const errorMsg = document.getElementById('errorMessage');
    
    // Formani tekshirish
    if (!name || !email || !message) {
      alert('Iltimos, barcha majburiy maydonlarni to\'ldiring!');
      return;
    }
    
    // Email formatini tekshirish
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailRegex.test(email)) {
      alert('Iltimos, to\'g\'ri email manzil kiriting!');
      return;
    }
    
    // Yuborish tugmasini o'chirish
    submitBtn.disabled = true;
    btnText.style.display = 'none';
    btnLoader.style.display = 'inline';
    successMsg.style.display = 'none';
    errorMsg.style.display = 'none';
    
    // Telegram botga yuborish uchun xabarni tayyorlash
    const text = `📩 *Yangi Xabar!*\n\n` +
                 `👤 *Ism:* ${name}\n` +
                 `📧 *Email:* ${email}\n` +
                 `📝 *Mavzu:* ${subject || 'Mavzu yo\'q'}\n` +
                 `💬 *Xabar:*\n${message}\n\n` +
                 `🕐 *Vaqt:* ${new Date().toLocaleString('uz-UZ')}\n` +
                 `🌐 *Manba:* GitHub Profil`;
    
    try {
      // Telegram botga so'rov yuborish
      const response = await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          chat_id: CHAT_ID,
          text: text,
          parse_mode: 'Markdown',
          disable_web_page_preview: true
        })
      });
      
      const data = await response.json();
      
      if (data.ok) {
        // Muvaffaqiyatli yuborildi
        successMsg.style.display = 'block';
        document.getElementById('contactForm').reset();
      } else {
        // Xatolik
        errorMsg.style.display = 'block';
        console.error('Telegram API error:', data);
      }
    } catch (error) {
      // Tarmoq xatoligi
      errorMsg.style.display = 'block';
      console.error('Network error:', error);
    }
    
    // Tugmani qayta aktivlashtirish
    submitBtn.disabled = false;
    btnText.style.display = 'inline';
    btnLoader.style.display = 'none';
    
    // 5 soniyadan keyin xabarlarni yashirish
    setTimeout(() => {
      successMsg.style.display = 'none';
      errorMsg.style.display = 'none';
    }, 5000);
  });
</script>

<!-- FORM STYLING FOR MOBILE RESPONSIVE -->
<style>
  @media (max-width: 600px) {
    #contactForm {
      max-width: 100% !important;
      margin: 0 10px !important;
      padding: 15px !important;
    }
    
    #contactForm input,
    #contactForm textarea {
      font-size: 14px !important;
      padding: 10px !important;
    }
    
    #contactForm button {
      font-size: 16px !important;
      padding: 12px !important;
    }
  }
</style>

---

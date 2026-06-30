# telegram_bot.py
import requests
import time
from flask import Flask, request, jsonify
from datetime import datetime

app = Flask(__name__)

# Bot sozlamalari
BOT_TOKEN = '8786901645:AAHVKHz7AuW2UKlrj7f_6VYPzyGbgu-4luQ'
CHAT_ID = '8631335073'

# Telegram bot orqali xabar yuborish
def send_telegram_message(text):
    url = f'https://api.telegram.org/bot{BOT_TOKEN}/sendMessage'
    payload = {
        'chat_id': CHAT_ID,
        'text': text,
        'parse_mode': 'Markdown',
        'disable_web_page_preview': True
    }
    
    try:
        response = requests.post(url, json=payload)
        return response.json()
    except Exception as e:
        print(f"Xatolik: {e}")
        return None

# Webhook uchun endpoint
@app.route('/webhook', methods=['POST'])
def webhook():
    try:
        data = request.json
        
        # Ma'lumotlarni olish
        name = data.get('name', 'Noma\'lum')
        email = data.get('email', 'Noma\'lum')
        subject = data.get('subject', 'Mavzu yo\'q')
        message = data.get('message', 'Xabar yo\'q')
        ip = data.get('ip', 'Noma\'lum')
        
        # Telegram xabarini tayyorlash
        current_time = datetime.now().strftime('%d.%m.%Y %H:%M:%S')
        
        text = f"""📩 *YANGI XABAR!* 📩

━━━━━━━━━━━━━━━━━━━━
👤 *Ism:* {name}
📧 *Email:* {email}
📝 *Mavzu:* {subject}
💬 *Xabar:*
{message}

━━━━━━━━━━━━━━━━━━━━
🕐 *Vaqt:* {current_time}
🌐 *Manba:* GitHub Profil
🔗 *IP:* {ip}
📊 *Holat:* ✅ Qabul qilindi
━━━━━━━━━━━━━━━━━━━━"""
        
        # Telegramga yuborish
        result = send_telegram_message(text)
        
        if result and result.get('ok'):
            return jsonify({'status': 'success', 'message': 'Xabar yuborildi'}), 200
        else:
            return jsonify({'status': 'error', 'message': 'Xabar yuborilmadi'}), 500
            
    except Exception as e:
        return jsonify({'status': 'error', 'message': str(e)}), 500

# Bot holatini tekshirish
@app.route('/status', methods=['GET'])
def status():
    return jsonify({
        'status': 'running',
        'bot_token': BOT_TOKEN[:10] + '...',
        'chat_id': CHAT_ID,
        'time': datetime.now().isoformat()
    })

# Asosiy sahifa
@app.route('/', methods=['GET'])
def home():
    return """
    <html>
        <head><title>Telegram Bot</title></head>
        <body style="font-family: Arial; text-align: center; padding: 50px; background: #0d1117; color: #c9d1d9;">
            <h1 style="color: #00c6ff;">🤖 Telegram Bot</h1>
            <p>Bot ishlayapti!</p>
            <p>Webhook: <code>/webhook</code></p>
            <p>Status: <code>/status</code></p>
        </body>
    </html>
    """

# Botni ishga tushirish
if __name__ == '__main__':
    print("🤖 Bot ishga tushdi!")
    print(f"📱 Bot token: {BOT_TOKEN[:10]}...")
    print(f"👤 Chat ID: {CHAT_ID}")
    print("🌐 Server: http://0.0.0.0:8080")
    print("-" * 50)
    app.run(host='0.0.0.0', port=8080, debug=False)

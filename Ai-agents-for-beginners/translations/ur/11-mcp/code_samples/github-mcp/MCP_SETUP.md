<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "c4be907703b836d1a1c360db20da4de9",
  "translation_date": "2025-07-12T14:14:34+00:00",
  "source_file": "11-mcp/code_samples/github-mcp/MCP_SETUP.md",
  "language_code": "ur"
}
-->
# MCP سرور انٹیگریشن گائیڈ

## ضروریات
- Node.js انسٹال شدہ ہو (ورژن 14 یا اس سے اوپر)
- npm پیکج مینیجر
- Python ماحول جس میں مطلوبہ dependencies موجود ہوں

## سیٹ اپ کے مراحل

1. **MCP سرور پیکج انسٹال کریں**  
   ```bash
   npm install -g @modelcontextprotocol/server-github
   ```

2. **MCP سرور شروع کریں**  
   ```bash
   npx @modelcontextprotocol/server-github
   ```  
   سرور شروع ہو جائے گا اور کنکشن URL دکھائے گا۔

3. **کنکشن کی تصدیق کریں**  
   - اپنے Chainlit انٹرفیس میں پلگ آئیکن (🔌) دیکھیں  
   - پلگ آئیکن کے ساتھ نمبر (1) ظاہر ہونا چاہیے جو کامیاب کنکشن کی نشاندہی کرتا ہے  
   - کنسول میں یہ پیغام نظر آنا چاہیے: "GitHub plugin setup completed successfully" (مزید اسٹیٹس لائنز کے ساتھ)

## مسائل کا حل

### عام مسائل

1. **پورٹ کا تصادم**  
   ```bash
   Error: listen EADDRINUSE: address already in use
   ```  
   حل: پورٹ تبدیل کرنے کے لیے یہ استعمال کریں:  
   ```bash
   npx @modelcontextprotocol/server-github --port 3001
   ```

2. **تصدیقی مسائل**  
   - یقینی بنائیں کہ GitHub کی اسناد درست طریقے سے ترتیب دی گئی ہیں  
   - .env فائل میں مطلوبہ ٹوکنز موجود ہوں  
   - GitHub API تک رسائی کی تصدیق کریں

3. **کنکشن ناکام**  
   - تصدیق کریں کہ سرور متوقع پورٹ پر چل رہا ہے  
   - فائر وال کی ترتیبات چیک کریں  
   - Python ماحول میں مطلوبہ پیکجز موجود ہوں

## کنکشن کی تصدیق

آپ کا MCP سرور صحیح طریقے سے منسلک ہے جب:  
1. کنسول میں "GitHub plugin setup completed successfully" دکھائی دے  
2. کنکشن لاگز میں "✓ MCP Connection Status: Active" نظر آئے  
3. GitHub کمانڈز چیٹ انٹرفیس میں کام کریں

## ماحول کے متغیرات

آپ کی .env فائل میں یہ ضروری ہیں:  
```
GITHUB_TOKEN=your_github_token
MCP_SERVER_PORT=3000  # Optional, default is 3000
```

## کنکشن کی جانچ

چیٹ میں یہ ٹیسٹ پیغام بھیجیں:  
```
Show me the repositories for username: [GitHub Username]
```  
کامیاب جواب میں repository کی معلومات دکھائی جائے گی۔

**دستخطی نوٹ**:  
یہ دستاویز AI ترجمہ سروس [Co-op Translator](https://github.com/Azure/co-op-translator) کے ذریعے ترجمہ کی گئی ہے۔ اگرچہ ہم درستگی کے لیے کوشاں ہیں، براہ کرم آگاہ رہیں کہ خودکار ترجمے میں غلطیاں یا عدم درستیاں ہو سکتی ہیں۔ اصل دستاویز اپنی مادری زبان میں ہی معتبر ماخذ سمجھی جانی چاہیے۔ اہم معلومات کے لیے پیشہ ور انسانی ترجمہ کی سفارش کی جاتی ہے۔ اس ترجمے کے استعمال سے پیدا ہونے والی کسی بھی غلط فہمی یا غلط تشریح کی ذمہ داری ہم پر عائد نہیں ہوتی۔
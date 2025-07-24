<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "c4be907703b836d1a1c360db20da4de9",
  "translation_date": "2025-07-12T14:14:22+00:00",
  "source_file": "11-mcp/code_samples/github-mcp/MCP_SETUP.md",
  "language_code": "ar"
}
-->
# دليل دمج خادم MCP

## المتطلبات الأساسية
- تثبيت Node.js (الإصدار 14 أو أحدث)
- مدير حزم npm
- بيئة Python مع التبعيات المطلوبة

## خطوات الإعداد

1. **تثبيت حزمة خادم MCP**
   ```bash
   npm install -g @modelcontextprotocol/server-github
   ```

2. **تشغيل خادم MCP**
   ```bash
   npx @modelcontextprotocol/server-github
   ```
   يجب أن يبدأ الخادم ويعرض عنوان URL للاتصال.

3. **التحقق من الاتصال**
   - ابحث عن أيقونة القابس (🔌) في واجهة Chainlit الخاصة بك
   - يجب أن يظهر رقم (1) بجانب أيقونة القابس للدلالة على نجاح الاتصال
   - يجب أن يعرض الكونسول: "GitHub plugin setup completed successfully" (مع ظهور أسطر حالة إضافية)

## استكشاف الأخطاء وإصلاحها

### المشاكل الشائعة

1. **تعارض المنفذ**
   ```bash
   Error: listen EADDRINUSE: address already in use
   ```
   الحل: غيّر المنفذ باستخدام:
   ```bash
   npx @modelcontextprotocol/server-github --port 3001
   ```

2. **مشاكل المصادقة**
   - تأكد من تكوين بيانات اعتماد GitHub بشكل صحيح
   - تحقق من احتواء ملف .env على الرموز المطلوبة
   - تحقق من صلاحية الوصول إلى GitHub API

3. **فشل الاتصال**
   - تأكد من تشغيل الخادم على المنفذ المتوقع
   - تحقق من إعدادات جدار الحماية
   - تحقق من وجود الحزم المطلوبة في بيئة Python

## التحقق من الاتصال

يكون خادم MCP متصلًا بشكل صحيح عندما:
1. يعرض الكونسول "GitHub plugin setup completed successfully"
2. تظهر سجلات الاتصال "✓ MCP Connection Status: Active"
3. تعمل أوامر GitHub في واجهة الدردشة

## متغيرات البيئة

مطلوبة في ملف .env الخاص بك:
```
GITHUB_TOKEN=your_github_token
MCP_SERVER_PORT=3000  # Optional, default is 3000
```

## اختبار الاتصال

أرسل رسالة الاختبار هذه في الدردشة:
```
Show me the repositories for username: [GitHub Username]
```
ستظهر استجابة ناجحة معلومات المستودع.

**إخلاء المسؤولية**:  
تمت ترجمة هذا المستند باستخدام خدمة الترجمة الآلية [Co-op Translator](https://github.com/Azure/co-op-translator). بينما نسعى لتحقيق الدقة، يرجى العلم أن الترجمات الآلية قد تحتوي على أخطاء أو عدم دقة. يجب اعتبار المستند الأصلي بلغته الأصلية المصدر الموثوق به. للمعلومات الهامة، يُنصح بالاعتماد على الترجمة البشرية المهنية. نحن غير مسؤولين عن أي سوء فهم أو تفسير ناتج عن استخدام هذه الترجمة.
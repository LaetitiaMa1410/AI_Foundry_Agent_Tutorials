<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "c4be907703b836d1a1c360db20da4de9",
  "translation_date": "2025-07-12T14:15:23+00:00",
  "source_file": "11-mcp/code_samples/github-mcp/MCP_SETUP.md",
  "language_code": "hi"
}
-->
# MCP Server इंटीग्रेशन गाइड

## आवश्यकताएँ
- Node.js इंस्टॉल होना चाहिए (संस्करण 14 या उससे ऊपर)
- npm पैकेज मैनेजर
- Python वातावरण जिसमें आवश्यक डिपेंडेंसीज़ हों

## सेटअप के चरण

1. **MCP Server पैकेज इंस्टॉल करें**
   ```bash
   npm install -g @modelcontextprotocol/server-github
   ```

2. **MCP Server शुरू करें**
   ```bash
   npx @modelcontextprotocol/server-github
   ```  
   सर्वर शुरू हो जाएगा और एक कनेक्शन URL दिखाएगा।

3. **कनेक्शन सत्यापित करें**
   - अपने Chainlit इंटरफेस में प्लग आइकन (🔌) देखें  
   - प्लग आइकन के पास एक संख्या (1) दिखनी चाहिए जो सफल कनेक्शन को दर्शाती है  
   - कंसोल में यह दिखना चाहिए: "GitHub plugin setup completed successfully" (साथ ही अन्य स्टेटस लाइनें)

## समस्या निवारण

### सामान्य समस्याएँ

1. **पोर्ट संघर्ष**
   ```bash
   Error: listen EADDRINUSE: address already in use
   ```  
   समाधान: पोर्ट बदलने के लिए यह कमांड इस्तेमाल करें:  
   ```bash
   npx @modelcontextprotocol/server-github --port 3001
   ```

2. **प्रमाणीकरण समस्याएँ**
   - सुनिश्चित करें कि GitHub क्रेडेंशियल्स सही तरीके से कॉन्फ़िगर किए गए हैं  
   - .env फाइल में आवश्यक टोकन मौजूद हों  
   - GitHub API एक्सेस की जांच करें

3. **कनेक्शन विफल**
   - पुष्टि करें कि सर्वर अपेक्षित पोर्ट पर चल रहा है  
   - फ़ायरवॉल सेटिंग्स जांचें  
   - Python वातावरण में आवश्यक पैकेज इंस्टॉल हैं या नहीं, यह देखें

## कनेक्शन सत्यापन

आपका MCP सर्वर सही तरीके से जुड़ा हुआ है जब:  
1. कंसोल में "GitHub plugin setup completed successfully" दिखे  
2. कनेक्शन लॉग में "✓ MCP Connection Status: Active" दिखाई दे  
3. GitHub कमांड चैट इंटरफेस में काम करें

## पर्यावरण चर

आपकी .env फाइल में आवश्यक:  
```
GITHUB_TOKEN=your_github_token
MCP_SERVER_PORT=3000  # Optional, default is 3000
```

## कनेक्शन परीक्षण

चैट में यह टेस्ट मैसेज भेजें:  
```
Show me the repositories for username: [GitHub Username]
```  
सफल प्रतिक्रिया में रिपॉजिटरी की जानकारी दिखाई देगी।

**अस्वीकरण**:  
यह दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) का उपयोग करके अनुवादित किया गया है। जबकि हम सटीकता के लिए प्रयासरत हैं, कृपया ध्यान दें कि स्वचालित अनुवादों में त्रुटियाँ या अशुद्धियाँ हो सकती हैं। मूल दस्तावेज़ अपनी मूल भाषा में ही अधिकारिक स्रोत माना जाना चाहिए। महत्वपूर्ण जानकारी के लिए, पेशेवर मानव अनुवाद की सलाह दी जाती है। इस अनुवाद के उपयोग से उत्पन्न किसी भी गलतफहमी या गलत व्याख्या के लिए हम जिम्मेदार नहीं हैं।
# 📰 Hiru News API

A production-ready API for scraping and serving news from [hirunews.lk](https://hirunews.lk) - Sri Lanka's most visited news website. Deployed on Vercel with full-text extraction, images, and categorization.

**Live API:** `https://hirunews.vercel.app/api`

---

## ✨ Features

### 🎯 Complete News Extraction
- Headlines, summaries, and full article text
- Thumbnail and multiple images per article
- Categories, dates, and author information
- Sinhala and English content support
- Word count and content validation

### 🔌 Multiple API Endpoints
- Breaking news & latest updates
- Category-specific news (Sports, Business, Entertainment, etc.)
- Individual article access by ID
- Date-based filtering
- Search functionality
- Health status check

### 🚀 Production Ready
- Deployed on Vercel (Serverless Functions)
- CORS enabled for frontend integration
- Error handling & graceful fallbacks
- JSON responses with consistent formatting
- Fast response times (< 5 seconds)

---

## 🚀 Quick Start

### Test the API

```bash
# Check API status
curl https://hirunews.vercel.app/api/health

# Get latest news (5 articles)
curl https://hirunews.vercel.app/api/latest-news?limit=5

# Get specific article by ID
curl https://hirunews.vercel.app/api/article/440221

# Get sports news
curl https://hirunews.vercel.app/api/category/sports
```

### Frontend Integration (JavaScript)

```javascript
// Get breaking news
fetch('https://hirunews.vercel.app/api/breaking-news')
  .then(response => response.json())
  .then(data => console.log(data));

// Get article with full text
fetch('https://hirunews.vercel.app/api/article/440235')
  .then(response => response.json())
  .then(article => {
    console.log(article.data.headline);
    console.log(article.data.fullText);
  });
```

---

## 📡 API Endpoints

| Endpoint | Method | Description | Example |
|----------|--------|-------------|---------|
| `/api/health` | GET | API status & documentation | `GET /api/health` |
| `/api/breaking-news` | GET | Breaking/ticker news | `GET /api/breaking-news?limit=5` |
| `/api/latest-news` | GET | Latest articles | `GET /api/latest-news?limit=10` |
| `/api/article/{id}` | GET | Full article by ID | `GET /api/article/440221` |
| `/api/category/{name}` | GET | News by category | `GET /api/category/sports?limit=15` |
| `/api/date` | GET | News by date | `GET /api/date?date=2026-01-12` |
| `/api/search` | GET | Search news | `GET /api/search?q=ප්රථම` |

---

## 📊 Response Examples

### ✅ Successful Response

```json
{
  "success": true,
  "data": [...],
  "count": 5,
  "timestamp": "2026-01-12T14:00:00.000Z",
  "source": "hirunews.lk"
}
```

### 📄 Article Object

```json
{
  "id": "440221",
  "headline": "බිහිසුණු අනතුරකින් කාන්තාවන් දෙදෙනෙකු ඇතුලු තිදෙනෙකු මරුට - 10කට තුවාල",
  "url": "https://hirunews.lk/440221/three-people-including-two-women-killed-and-10-injured-in-horrific-accident",
  "thumbnail": "https://cdn.hirunews.lk/Data/News_Images/202601/1768190654_3682303_hirunews.jpg",
  "summary": "මුන්දලම - නවදන්කුලම ප්‍රදේශයේදී බිහිසුණු අනතුරක් සිදුව තිබෙනවා...",
  "fullText": "මුන්දලම - නවදන්කුලම ප්‍රදේශයේදී බිහිසුණු අනතුරක් සිදුව තිබෙනවා. මෝටර් රථයක් සහ වෑන් රථයක් මුහුණට මුහුණ ගැටී සිදුවූ මෙම අනතුරින්...",
  "images": [
    {
      "url": "https://cdn.hirunews.lk/Data/News_Images/202601/1768190654_3682303_hirunews.jpg",
      "alt": "අනතුරට ලක්වූ වාහන",
      "caption": ""
    }
  ],
  "category": "General",
  "publishedDate": "2026-01-12T09:15:12Z",
  "author": "Hiru News",
  "wordCount": 450,
  "hasFullContent": true,
  "source": "hirunews.lk",
  "timestamp": "2026-01-12T14:00:00.000Z"
}
```

### ⚠️ Error Response

```json
{
  "success": false,
  "error": "Article with ID 999999 not found",
  "timestamp": "2026-01-12T14:00:00.000Z",
  "suggestion": "Check if the ID is correct or try another article"
}
```

---

## 🏗️ Available Categories

| Category | Endpoint | Description |
|----------|----------|-------------|
| **Sports** | `/api/category/sports` | Cricket, football, and other sports news |
| **Business** | `/api/category/business` | Financial, economic, and business updates |
| **Entertainment** | `/api/category/entertainment` | Movies, music, and celebrity news |
| **International** | `/api/category/international` | World news and global events |
| **General** | `/api/category/general` | Local and general Sri Lankan news |
| **Local** | `/api/category/local` | Sri Lanka specific news (same as General) |

---

## 🔧 Query Parameters

### Common Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `limit` | integer | `10` | Number of articles to return |
| `details` | boolean | `true` | Get full article details (false for basic info) |

### Endpoint-Specific Parameters

- **`/api/date`**: `date=YYYY-MM-DD` (required)
- **`/api/search`**: `q=search_term` (required, min 2 chars)
- **`/api/category/{name}`**: `details=false` for faster responses

---

## 💡 Usage Examples

### 1. Get Latest News (Basic)

```bash
curl "https://hirunews.vercel.app/api/latest-news?limit=3"
```

### 2. Get Article with Full Details

```bash
curl "https://hirunews.vercel.app/api/article/440235"
```

### 3. Get Sports News (Fast Mode)

```bash
curl "https://hirunews.vercel.app/api/category/sports?limit=5&details=false"
```

### 4. Search for News

```bash
curl "https://hirunews.vercel.app/api/search?q=අනතුර&limit=5"
```

### 5. Get News by Date

```bash
curl "https://hirunews.vercel.app/api/date?date=2026-01-12"
```

---

## 🛠️ Development

### Local Setup

```bash
# Clone and install
git clone <repository-url>
cd hiru-news-api
npm install

# Run locally
npx vercel dev

# Test endpoints
curl http://localhost:3000/api/health
curl http://localhost:3000/api/latest-news
```

### Project Structure

```
hiru-news-api/
├── api/                    # Vercel Serverless Functions
│   ├── article/[id].js    # Dynamic article routes
│   ├── category/[name].js # Dynamic category routes
│   ├── breaking-news.js   # Breaking news endpoint
│   ├── latest-news.js     # Latest news endpoint
│   ├── date.js           # Date-based filtering
│   ├── search.js         # Search functionality
│   └── health.js         # API status check
├── lib/
│   └── scraper.js        # Core scraping engine
├── package.json          # Dependencies
└── vercel.json          # Vercel configuration
```

---

## ⚡ Performance Tips

1. Use `details=false` for faster category responses
2. Start with small limit values (3-5 articles)
3. Cache responses on your frontend (60 seconds recommended)
4. Use `breaking-news` for time-sensitive updates
5. Handle timeouts gracefully (API has 15-second limit)

---

## 🚨 Rate Limits & Limitations

| Aspect | Limit/Note |
|--------|------------|
| **Max duration** | 15 seconds per request (Vercel limit) |
| **Recommended** | Keep requests under 10 seconds |
| **Concurrent requests** | Limited by Vercel free tier |
| **Data freshness** | Scraped in real-time, no caching |
| **Language** | Primarily Sinhala, some English content |

---

## 🔗 Join Our Community

### 📢 Stay updated with tech news and API updates

**Telegram Channel:** [https://t.me/trivenlab](https://t.me/trivenlab)

Join for:
- 🚀 API updates and new features
- 💻 Tech tutorials and Sri Lankan tech news
- 🔧 Developer tips and best practices
- 📰 Hiru News API usage examples
- 🐛 Bug reports and feature requests

---

## 📝 License & Attribution

- **Source:** Data scraped from [hirunews.lk](https://hirunews.lk)
- **API:** Open for personal and educational use
- **Commercial Use:** Check hirunews.lk terms of service
- **Attribution:** Recommended to credit Hiru News

---

## 🐛 Troubleshooting

### Common Issues

| Issue | Solution |
|-------|----------|
| Empty responses | Check if website structure changed |
| 404 errors | Verify article ID exists |
| Timeout errors | Reduce limit parameter |
| CORS errors | Ensure proper headers in frontend |
| No full text | Article may have different HTML structure |

### Debug Mode

```bash
# Add debug parameter
curl "https://hirunews.vercel.app/api/article/440221?debug=true"
```

---

## 🔄 Changelog

### v1.0.0 (Current)

- ✅ Complete article scraping (text, images, metadata)
- ✅ Multiple API endpoints
- ✅ Vercel deployment
- ✅ CORS support
- ✅ Error handling
- ✅ Category-based filtering
- ✅ Search functionality

---

## 🤝 Contributing

Found a bug or have a feature request?

1. Check existing issues
2. Test with the `/api/health` endpoint
3. Provide example article IDs
4. Join Telegram channel for discussion

---

## 📞 Support

- **API Issues:** Check `/api/health` first
- **Scraping Problems:** Test with different article IDs
- **Community:** Join [Telegram](https://t.me/tharustack)
- **Urgent:** The API is self-hosted, no SLA guarantees

---

## 🌟 Show Your Support

If you find this API useful, consider:
- ⭐ Starring the repository
- 📢 Sharing with other developers
- 🤝 Contributing to improvements
- 💬 Joining our Telegram community

---

**Happy coding!** 🚀

Made with ❤️ for the Sri Lankan developer community

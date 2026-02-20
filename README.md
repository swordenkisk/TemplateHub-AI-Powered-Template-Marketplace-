# TemplateHub — AI-Powered Template Marketplace

A full-stack Flask web app that uses **DeepSeek AI** to auto-generate and sell
professional templates (PowerPoint, Excel, Word, PDF/Canva).

---

## 🗂️ Project Structure

```
template_marketplace/
├── app.py                     # Flask application (routes, auth, Stripe)
├── generator/
│   ├── __init__.py
│   ├── ai_generator.py        # DeepSeek API — idea & content generation
│   └── file_creator.py        # PPTX / XLSX / DOCX / PDF creation
├── templates/
│   ├── base.html              # Shared layout + navbar
│   ├── index.html             # Store with filter + search
│   ├── product.html           # Product detail page
│   ├── cart.html              # Shopping cart
│   ├── success.html           # Post-purchase download page
│   ├── admin_login.html       # Admin password gate
│   ├── admin_dashboard.html   # Product & order overview
│   ├── admin_generate.html    # AI generation form
│   ├── admin_orders.html      # Order history table
│   └── error.html             # Generic error page
├── static/
│   ├── css/style.css          # Full stylesheet
│   ├── js/main.js             # Cart badge + UX helpers
│   └── thumbnails/            # Generated product images
├── generated_templates/       # PPTX/XLSX/DOCX/PDF output files
├── products.json              # Product catalogue (auto-managed)
├── orders.json                # Order log (auto-managed)
├── seed_demo.py               # Populate store without API keys
├── generate_defaults.py       # Create placeholder thumbnail
├── .env.example               # Environment variable template
└── requirements.txt
```

---

## ⚡ Quick Start

### 1. Install dependencies
```bash
pip install -r requirements.txt
```

### 2. Configure environment
```bash
cp .env.example .env
# Edit .env and fill in your keys
```

### 3. Seed demo products (no API key needed)
```bash
python seed_demo.py
```

### 4. Run the server
```bash
python app.py
```

Visit **http://localhost:5000**

---

## 🤖 Generating Templates with AI

1. Go to **http://localhost:5000/admin**
2. Login with the password in your `.env` (default: `admin123`)
3. Click **Generate Templates**
4. Choose template type, count, and price
5. Click **Generate with DeepSeek AI** and wait 30–90s

Each generation:
- Calls DeepSeek to brainstorm ideas
- Generates structured content (slides, rows, sections)
- Creates real downloadable files (PPTX/XLSX/DOCX/PDF)
- Builds a thumbnail image
- Publishes products to your store automatically

---

## 💳 Stripe Integration

Templates are sold via **Stripe Checkout**.

- For testing, use Stripe test keys (`pk_test_...` / `sk_test_...`)
- Set them in `.env`
- Use test card `4242 4242 4242 4242` with any future date and CVC

Without Stripe keys, the checkout runs in **demo mode** (skips payment,
still records the order and shows download links).

---

## 🌐 Routes

| Route | Description |
|---|---|
| `/` | Store front with filter & search |
| `/product/<id>` | Product detail page |
| `/add_to_cart/<id>` | Add item to session cart |
| `/cart` | View cart & checkout |
| `/checkout` | Create Stripe session |
| `/success` | Post-payment download page |
| `/download/<id>` | Download template file |
| `/admin` | Admin dashboard (protected) |
| `/admin/generate` | AI generation form |
| `/admin/orders` | Order history |
| `/api/products` | JSON product list |

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Web framework | Flask 2.3 |
| AI generation | DeepSeek (OpenAI-compatible API) |
| Presentations | python-pptx |
| Spreadsheets | openpyxl |
| Word docs | python-docx |
| PDFs | reportlab |
| Thumbnails | Pillow |
| Payments | Stripe Checkout |
| Styling | Custom CSS (Inter font) |

---

## 🔒 Security Notes

- Change `ADMIN_PASSWORD` in `.env` before deploying
- Set a strong `FLASK_SECRET_KEY`
- The `/admin` routes are password-protected
- Download links are honour-system only — add order verification for production
- For production, use a proper database (SQLite/PostgreSQL) instead of JSON files

---

## 📈 Extending the Project

Ideas for next steps:
- **User accounts** — register/login, purchase history
- **Email delivery** — send download links via SendGrid/Mailgun
- **Database** — replace JSON files with SQLAlchemy + PostgreSQL
- **Search** — full-text search with Whoosh or Algolia
- **Ratings & reviews** — let buyers rate templates
- **Affiliate system** — referral codes with commission tracking
- **Multi-currency** — Stripe supports 135+ currencies
- **Canva integration** — auto-create Canva designs via Canva API

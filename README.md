# 🎨 AI Curator — Aatelier Backup

This repo contains the **backup, documentation, and prompt engineering** for the **AI Curator** automation project built for Aatelier.

The AI Curator is designed to help art buyers discover artworks through an automated, AI-powered curator powered by **Airtable + OpenAI GPT-4**.

This backup documents the logic, prompts, and database schema in case of platform migration, future rebuild, or disaster recovery.

---

## 🚀 Features

- 💡 **AI-Powered Art Curation**  
Generates art recommendations based on user input like vibe, budget, or style.

- 🌏 **Multilingual Reply**  
Automatically detects and replies in **Bahasa Indonesia, English, or Mandarin.**

- 📱 **WhatsApp Number Parser**  
Extracts the buyer’s WhatsApp number from casual text input.

- 🏛️ **No-Code Stack**  
Built entirely on **Airtable Automations** and **OpenAI API**, with no external backend.

---

## 🧠 Current Workflow

1. **Trigger:**  
→ When a new buyer message is created in Airtable (`Status = Pending`).

2. **Find Artworks:**  
→ Searches the artwork database to retrieve available pieces.

3. **AI Reply Generator:**  
→ Calls OpenAI GPT with a curated prompt to generate an elegant curator response based on:  
   - Buyer’s message  
   - Artwork list  
   - Pricing  
   - Availability status (Available, By Request, Sold)

4. **WhatsApp Parser:**  
→ Uses either a regex script or OpenAI to extract WhatsApp number from buyer message.

5. **Update Airtable:**  
→ Writes AI response and WhatsApp number back into Airtable.

6. **Mark as Done:**  
→ Updates the status to `Done` to prevent retriggers.

---

## 🗄️ Database Schema

### 🔹 **Buyer Messages Table**
| Field        | Type             |
|---------------|------------------|
| Name          | Single line text |
| Message       | Long text        |
| AI Response   | Long text        |
| Buyer WA      | Phone/Single text|
| Status        | Single select (`Pending`, `Done`) |
| Created Time  | Date             |

### 🔹 **Artworks Table**
| Field         | Type             |
|----------------|------------------|
| Artwork Name   | Single line text |
| Artist Name    | Single line text |
| Medium         | Single line text |
| Size           | Single line text |
| Price (IDR)    | Currency         |
| Status         | Single select (`Available`, `By Request`, `Sold`) |
| Tags/Vibe      | Multi-select     |

---

## 🧾 Prompts

Prompts are stored in `/prompts/` folder including:  
- `curator-reply.md` → The curator logic  
- `whatsapp-parser.md` → The WA extraction logic  
- Status handling rules  
- Language behavior

---

## 🏗️ Known Issues

- [ ] **Make.com runaway operations bug** — resolved by switching to Airtable native automation.  
- [ ] Airtable scripting requires Pro plan.  
- [ ] WhatsApp parsing can fail if users type numbers without country code or in irregular formats.

---

## 📦 Next Steps

- [ ] Convert this into an API-powered web app (Optional).  
- [ ] Improve artwork filtering based on vibes, sizes, and budgets dynamically.  
- [ ] Add error handling and fallback replies.

---

## 👋 Credits

Built by [Your Name] for **Aatelier** as part of the 2025 automation sprint.  
Stack: Airtable + OpenAI GPT API.  

---

## 🆘 This backup was pushed in panic mode on June 28, 2025 — when Make.com started producing 30 ghost operations per run. 😂

# Nihongo Master - Proiect de Licență

**Autor:** Simoc David-Cristian  
**Coordonator științific:** Chirila Oana-Sorina  
**Instituție:** Universitatea Politehnica Timișoara (UPT)  
**An:** 2026  

---

## 1. Descrierea Livrabilelor
Proiectul conține întregul cod sursă necesar rulării aplicației Nihongo Master. Pentru o mai bună organizare arhitecturală, codul a fost separat în două repository-uri distincte:
* **Frontend (Aplicația de Mobil):** Dezvoltat în React Native / TypeScript utilizând framework-ul Expo Router. Conține interfața grafică și logica locală a clientului.
* **Backend (Server AI):** Dezvoltat în Python utilizând framework-ul FastAPI, responsabil de inferența modelelor de Inteligență Artificială (Llama 3, Whisper, Edge-TTS).

*(Notă: Fișierele binare compilate, folderele `node_modules`, mediile virtuale Python și greutățile modelelor AI au fost excluse din repository-uri pentru a menține dimensiunea optimă a codului sursă).*

## 2. Adresele Repository-urilor
Codul sursă integral poate fi consultat la următoarele adrese:  
**Repository Frontend (React Native):** https://github.com/davidsimoc/Nihongo-Master  
**Repository Backend (Python FastAPI):** https://github.com/davidsimoc/Voice-chat  

---

## 3. Cerințe de Sistem
Pentru a compila și lansa aplicația local, sunt necesare următoarele medii instalate pe stația de lucru:

**Pentru Frontend:**
* **Node.js** (v18 sau mai nou) și managerul de pachete **npm** sau **yarn**.
* Aplicația mobilă **Expo Go** (iOS sau Android) pentru testare pe telefon.
* Un fișier `.env` valid în rădăcina proiectului (pentru cheile API).

**Pentru Backend (AI):**
* **Python** (v3.10 sau mai nou) și **pip**.
* **FFmpeg** instalat pe sistem și adăugat în variabilele de mediu (PATH) - obligatoriu pentru ca modelul OpenAI Whisper să poată procesa fișierele audio.
* **Compilator C++ / Build Tools** (ex: Visual Studio Build Tools pe Windows sau Xcode Command Line Tools pe Mac) - necesare pentru instalarea cu succes a pachetului `llama-cpp-python`.
* Modelul Llama 3 în format `.gguf` descărcat local.

---

## 4. Pași de Instalare și Compilare

### A. Configurarea Frontend-ului (React Native)
1. Clonați repository-ul de Frontend și deschideți un terminal în folderul creat.
2. Deschideți fișierul `.env` unde variabilela `EXPO_PUBLIC_GOOGLE_WEB_CLIENT_ID` este pecompletată, iar pentru variabila `EXPO_PUBLIC_API_URL`, introduceți adresa IP locală a mașinii dumneavoastră urmată de portul 8000 (ex: `http://192.168.0.100:8000`). Această modificare este **obligatorie** pentru ca aplicația de pe telefonul mobil să poată comunica local cu serverul Python prin rețeaua Wi-Fi, fără a fi nevoie de un tunnel de tip ngrok.
3. Instalați toate dependențele:
   `npm install`
4. *(Opțional pentru build nativ)*: Dacă se dorește compilarea aplicației standalone (.apk / .ipa), se va rula comanda `npx expo build`.

### B. Configurarea Backend-ului (Python FastAPI)
1. Clonați repository-ul de Backend și deschideți un terminal în folderul creat.
2. Creați și activați un mediu virtual Python (recomandat):
   `python -m venv venv`
   Pentru Mac/Linux: `source venv/bin/activate`
   Pentru Windows: `venv\Scripts\activate`
3. Instalați pachetele necesare:
   `pip install -r requirements.txt`
4. Asigurați-vă că ați plasat fișierul `.gguf` (modelul Llama 3) în directorul specificat în cod.

---

## 5. Pași de Lansare a Aplicației

Pentru a rula sistemul complet, ambele componente trebuie pornite simultan, în terminale separate.

**1. Pornirea Serverului Backend:**  
Din folderul backend-ului, cu mediul virtual activat, rulați comanda:
`uvicorn main:app --host 0.0.0.0 --port 8000`
*Serverul va porni și va fi gata să primească request-uri API pe portul 8000.*

**2. Pornirea Aplicației Frontend:**  
Din folderul frontend-ului, rulați comanda:
`npx expo start`
*Se va deschide un terminal cu un cod QR. Scanați acest cod QR folosind aplicația Expo Go de pe telefonul mobil pentru a rula aplicația NiHongo Master pe dispozitivul fizic.*

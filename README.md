# FitBalance – Abo-Website (Starterprojekt)

Ein responsiver Next.js-Prototyp mit Supabase-Benutzerkonten und Stripe-Abonnement-Checkout.

## Enthalten
- Deutsche Landingpage mit Fitness-/Ernährungspositionierung
- Drei Beispieltarife: Personal, Premium, Business
- Supabase Registrierung und Login per E-Mail/Passwort
- Stripe Checkout im Subscription-Modus
- Stripe Kundenportal für Abo-Verwaltung
- Stripe Webhook zur Synchronisierung von Abo-Status
- Supabase SQL-Schema mit Row Level Security

## Lokal starten
1. Node.js 20+ installieren.
2. `npm install`
3. `.env.example` nach `.env.local` kopieren und Werte eintragen.
4. In Supabase ein Projekt erstellen, Auth > Email aktivieren und `supabase/schema.sql` im SQL Editor ausführen.
5. In Stripe drei wiederkehrende monatliche Preise erstellen und deren `price_...` IDs in `.env.local` eintragen.
6. `npm run dev` und `http://localhost:3000` öffnen.

## Stripe konfigurieren
- Erstelle in Stripe Produkte/monatliche Preise für Personal, Premium und Business.
- Aktiviere das Stripe Customer Portal in den Stripe-Einstellungen.
- Lege einen Webhook auf `/api/webhook` an und abonniere:
  - `customer.subscription.created`
  - `customer.subscription.updated`
  - `customer.subscription.deleted`
- Setze das Webhook-Signing-Secret in `STRIPE_WEBHOOK_SECRET`.
- Für lokale Tests kann Stripe CLI den Webhook an `localhost:3000/api/webhook` weiterleiten.

## Wichtige Hinweise vor Livegang
- Das Projekt ist ein Starter, kein bereits gehosteter oder produktiv abgenommener Shop.
- Stripe- und Supabase-Konten, API-Schlüssel, Preis-IDs, Domain und Webhook müssen vom Betreiber eingerichtet werden. Niemals Secret Keys in den Browser-Code geben.
- Checkout und Authentifizierung sind vorbereitet; vor dem Livegang sind Tests mit Stripe-Testkarten, Webhook-Retry/Idempotenz, E-Mail-Verifikation, Passwort-Reset, Rate-Limits und Fehlerfällen nötig.
- Die Abo-Zugriffsprüfung muss serverseitig in allen geschützten Mitglieder-Routen ergänzt werden, bevor kostenpflichtige Inhalte freigeschaltet werden.
- Rechtstexte (Impressum, Datenschutzerklärung, AGB, Widerrufsbelehrung, Preis-/Kündigungshinweise), Cookie-/Tracking-Konfiguration und steuerliche Behandlung müssen für den konkreten Betreiber und Markt rechtlich geprüft und ergänzt werden. Die Footer-Links sind Platzhalter.
- Keine medizinischen Versprechen. Fitness- und Ernährungsinhalte müssen fachlich geprüft sein; individuelle Empfehlungen bei Erkrankungen gehören in medizinische Hände.
- Business-Tarife brauchen eine klare Lizenz-/Nutzerregelung und eine definierte Preislogik.

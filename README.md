# Privacy Policy Documentation & Verification Report — pennyBook Ledger v1.0.1

**Developer:** Javed Khan Labs  
**Package:** `com.pennybook.expensetracker`  
**Target Release:** v1.0.1 (versionCode: 2)  
**Effective Date:** November 8, 2026  
**Hosting Destination:** `https://javedakhan2010.github.io/pennyBook-privacy-policy/`  

---

## 1. Summary of Changes from Legacy Policy

| Section / Topic | Legacy Policy Wording | Updated v1.0.1 Verified Policy | Reason for Change |
| :--- | :--- | :--- | :--- |
| **Product Branding** | "PennyBook" | **"pennyBook Ledger"** | Aligned with official trademark capitalization and Google Play app identity. |
| **Developer Name** | "Javed Khan" | **"Javed Khan Labs"** | Updated to official developer brand identity. |
| **Version Anchoring** | "Version 1.0.0 is engineered as..." | **"pennyBook Ledger operates as..."** | Removed obsolete hardcoded version references while preserving permanent offline guarantees. |
| **Database Encryption** | Mentioned unencrypted local SQLite | **SQLCipher 4.17.0 + Android Keystore** | Accurately documents the AES-256 encrypted database architecture implemented in v1.0.1. |
| **Backup Formats** | Only referenced plaintext `.db` files | **Encrypted `.pennybook` (PBK1) & unencrypted `.db`** | Accurately discloses the Argon2id + AES-256-GCM portable encrypted backup format alongside legacy restore. |
| **Cloud Backup Exclusions** | Undocumented | **Explicit exclusion via `data_extraction_rules.xml`** | Details the technical rules preventing silent Google Drive cloud backup of local databases or encryption keys. |
| **Sharing Security** | General file access | **Scoped `FileProvider` (`cache-path exports/`)** | Discloses that PDF/CSV exports are securely brokered without exposing private application databases. |
| **Third-Party SDKs** | Mentioned possible future AdMob/Billing | **Zero Advertising, Zero Billing, Zero Analytics** | Explicitly confirms zero third-party monetization or telemetry tracking SDKs are bundled. |

---

## 2. Technical Evidence & Verification Log

### 1. Network Communications & Telemetry
- **Claim:** Zero network permissions; no telemetry trackers; completely offline.
- **Evidence:** 
  - Release merged manifest (`AndroidManifest.xml`) does **NOT** declare `android.permission.INTERNET`.
  - Inspection of `app/build.gradle.kts` confirms absence of Firebase Analytics, Flurry, Mixpanel, Crashlytics, Google AdMob, or Google Play Billing SDKs.
- **Verification Result:** **VERIFIED (PASS)**

### 2. Cryptographic Storage & Keystore
- **Claim:** 256-bit SQLCipher database encryption; hardware-backed Android Keystore key management; Argon2id KDF for backups.
- **Evidence:**
  - `net.zetetic:sqlcipher-android:4.17.0` active in production dependencies.
  - Runtime verification confirms keying operation: `Database keying operation returned:0`.
  - `BackupCryptoManager.kt` uses Bouncy Castle 1.80 Argon2id KDF (`ARGON2_VERSION_13`) and `AES/GCM/NoPadding`.
- **Verification Result:** **VERIFIED (PASS)**

### 3. Permissions & Alarms
- **Claim:** Only uses standard notification, boot, vibrate, and legacy storage permissions; no exact alarm permissions.
- **Evidence:**
  - `AndroidManifest.xml` declares only `POST_NOTIFICATIONS`, `RECEIVE_BOOT_COMPLETED`, `VIBRATE`, `USE_BIOMETRIC`, and legacy storage permissions.
  - Zero declaration of restricted permissions `SCHEDULE_EXACT_ALARM` or `USE_EXACT_ALARM`.
- **Verification Result:** **VERIFIED (PASS)**

### 4. File Sharing & Export Security
- **Claim:** Scoped Android FileProvider preventing database leaks.
- **Evidence:**
  - `file_paths.xml` configures `<cache-path name="shared_exports" path="exports/" />`.
  - Internal SQLite database directory (`databases/`) and shared preferences (`shared_prefs/`) are completely unmapped in FileProvider.
- **Verification Result:** **VERIFIED (PASS)**

---

## 3. Deliverables Generated

1. **`privacy-policy.html`**: Clean, accessible, responsive HTML5 document styled with Javed Khan Labs emerald branding.
2. **`index.html`**: Direct drop-in root file for GitHub Pages repository (`pennyBook-privacy-policy`).
3. **`README.md`**: Complete markdown representation of the policy for repository root documentation.

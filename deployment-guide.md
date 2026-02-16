# Deployment Guide in Siperuka

## Cara Deploy Backend

1. Pastikan .NET 8 sudah terinstall.
2. Konfigurasi file `appsettings.json` dan `appsettings.Development.json` sesuai environment (database, JWT, dsb).
3. Jalankan migrasi database:
   ```powershell
   dotnet ef database update
   ```
4. Build dan jalankan backend:
   ```powershell
   dotnet build
   dotnet run --project Backend/Backend.csproj
   ```
5. Backend akan berjalan di port sesuai konfigurasi (default: 5000/5001).

## Cara Run Frontend

1. Pastikan Node.js dan npm sudah terinstall.
2. Masuk ke folder frontend:
   ```powershell
   cd Frontend
   ```
3. Install dependencies:
   ```powershell
   npm install
   ```
4. Jalankan frontend:
   ```powershell
   npm run dev
   ```
5. Frontend akan berjalan di port sesuai konfigurasi (default: 5173).

## Konfigurasi Environment

### Backend

- `appsettings.json`:
  - ConnectionStrings: konfigurasi database
  - JWT: secret, expiry
  - CORS: allowed origins
- Gunakan environment variable jika deploy ke cloud (Azure, AWS, dsb).

### Frontend

- `.env` (jika ada):
  - VITE_API_URL: alamat backend

---

Pastikan environment sudah sesuai sebelum deploy ke production. Untuk cloud deployment, gunakan CI/CD dan update konfigurasi sesuai provider.

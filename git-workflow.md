# Git Workflow in Siperuka

## Branching Strategy

- **main**: Branch utama untuk release production.
- **develop**: Branch pengembangan, tempat fitur digabung sebelum ke main.
- **feature/\***: Branch untuk pengembangan fitur baru. Contoh: `feature/booking-status`, `feature/user-management`.

## Alur Pull Request

1. Buat branch dari `develop` (atau dari `main` jika hotfix).
2. Kerjakan fitur/bug di branch tersebut.
3. Commit dengan format Conventional Commit.
4. Push ke remote repository.
5. Buat Pull Request ke `develop`.
6. Review oleh tim, lakukan perubahan jika diperlukan.
7. Setelah disetujui, merge ke `develop`.
8. Setelah beberapa fitur siap, merge `develop` ke `main` untuk release.

## Cara Naming Branch

- Gunakan prefix sesuai tipe branch:
  - `feature/` untuk fitur baru
  - `fix/` untuk bugfix
  - `hotfix/` untuk perbaikan urgent
- Gunakan kebab-case atau camelCase untuk nama branch.
- Contoh:
  - `feature/booking-history`
  - `fix/login-error`
  - `hotfix/api-crash`

## Format Conventional Commit

- **feat**: Penambahan fitur baru
- **fix**: Perbaikan bug
- **docs**: Perubahan dokumentasi
- **style**: Perubahan tampilan/format tanpa mengubah logika
- **refactor**: Refactor kode tanpa menambah fitur atau memperbaiki bug
- **test**: Penambahan/perbaikan test
- **chore**: Perubahan minor (build, tools, dll)

**Contoh:**

```
feat(booking): add booking approval endpoint
fix(user): fix email validation bug
refactor(room): improve room seeder logic
```

## Cara Release + Tagging

1. Pastikan branch `main` sudah berisi kode siap release.
2. Merge `develop` ke `main`.
3. Buat tag versi release, misal `v1.0.0`.
4. Push tag ke remote:
   ```
   git tag v1.0.0
   git push origin v1.0.0
   ```
5. Release dapat dilakukan dari tag tersebut.

---

Dokumentasi ini wajib diikuti untuk menjaga kualitas dan konsistensi pengembangan project.

# Phát hành game package

## Trước lần publish đầu

1. Để repository ở chế độ **private**.
2. Trong `package.json`, thay các placeholder:
   - `name` phải dùng GitHub scope của repository owner, ví dụ `@lukhaiminh/space-runner`.
   - `description`, `repository.url` và `version`.
3. Chạy kiểm tra cục bộ:

```bash
pnpm install --frozen-lockfile
pnpm typecheck
pnpm build
```

## Release

```bash
pnpm version patch
git push origin HEAD --follow-tags
```

Tag `vX.Y.Z` kích hoạt GitHub Actions. Workflow dùng `GITHUB_TOKEN` của repository để publish package private lên GitHub Packages.

## Gửi cho Maco administrator

Sau khi publish thành công, gửi tên package, version và URL repository. Administrator sẽ cấp cho host Maco Games quyền đọc package để Vercel cài package khi build.

Không gửi token GitHub/Vercel và không thêm token vào source code hoặc `.npmrc`.

# Maco Game Package Template

Template để tạo một web game có thể:

- chạy standalone sau `pnpm build` (`dist/index.html` là một file HTML);
- được mount vào Maco Games/Nuxt qua `mountGame(container)`;
- publish thành public npm package bằng GitHub Actions.

## Bắt đầu

1. Tạo repository **private** từ template này.
2. Đổi `name`, `description`, `repository` và `version` trong `package.json`.
3. Thay màn hình mẫu tại `src/main.ts` bằng game của bạn, giữ API `mountGame()` và `destroy()`.
4. Nhờ Maco administrator cấp repository quyền dùng Actions secret `NPM_TOKEN`.

```bash
pnpm install
pnpm dev
pnpm typecheck
pnpm build
```

## Publish

```bash
pnpm version patch
git push origin HEAD --follow-tags
```

Xem [hướng dẫn publish](docs/PUBLISHING.md) để biết quyền npm, token và cách host cài package.

## Bảo mật

Không commit `.env`, `.npmrc` có token, hay private key. Package npm public có thể được bất kỳ ai tải xuống; đừng dùng chế độ này cho source hoặc asset cần bảo mật.

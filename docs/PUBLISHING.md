# Phát hành game package

## Chuẩn bị một game mới

1. Tạo repository private từ template này.
2. Đổi các placeholder trong `package.json`:
   - `name`: package npm duy nhất, ví dụ `@maco-games/space-runner`.
   - `description` và `repository.url`.
   - `version`: bắt đầu từ `0.1.0`.
3. Thay UI mẫu trong `src/main.ts`, nhưng giữ export `mountGame(container)` và `destroy()` để host có thể dọn game khi đổi route.
4. Đổi title và màu nền trong `index.html`.

## Một lần cho Maco administrator

1. Tạo npm organization/scope sở hữu package, ví dụ `@maco-games`.
2. Tạo npm access token chỉ có quyền publish cần thiết cho scope/package đó.
3. Trên GitHub organization, tạo Actions secret tên `NPM_TOKEN` và chỉ cho phép các repository game cần publish dùng secret này. Không gửi token cho collaborator và không commit token vào repository.

## Publish

```bash
pnpm install --frozen-lockfile
pnpm typecheck && pnpm build
pnpm version patch
git push origin HEAD --follow-tags
```

Tag `vX.Y.Z` sẽ kích hoạt workflow. Workflow chỉ publish nếu tag khớp chính xác với `version` trong `package.json`.

## Dùng trong host Maco

Vì package publish trên npm public, host không cần token:

```bash
pnpm add @maco-games/space-runner
```

```vue
<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref } from 'vue'
import { mountGame } from '@maco-games/space-runner'

const container = ref<HTMLElement>()
let game: ReturnType<typeof mountGame> | undefined

onMounted(() => {
  if (container.value) game = mountGame(container.value)
})

onBeforeUnmount(() => game?.destroy())
</script>

<template><div ref="container" /></template>
```

## Lưu ý về quyền sở hữu

Repository private chỉ che source trên GitHub. Một package npm public vẫn cho bất kỳ ai tải JavaScript đã publish; game web chạy trên trình duyệt cũng không thể giữ kín mã client. Không publish npm public nếu game hoặc asset phải giữ bí mật.

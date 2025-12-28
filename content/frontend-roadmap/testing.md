---
title: "Testing"
date: 2025-01-20
description: "Kiểm thử ứng dụng Frontend"
weight: 12
---

# Testing

Testing là quá trình kiểm tra code để đảm bảo nó hoạt động đúng như mong đợi. Đây là kỹ năng quan trọng trong phát triển phần mềm chuyên nghiệp.

## ✅ Testing là gì?

Testing giúp bạn:

- Tìm và sửa lỗi sớm
- Đảm bảo code hoạt động đúng
- Tăng tự tin khi refactor
- Cải thiện chất lượng code

## 🎬 Video hướng dẫn

<div class="video-container">
  <iframe 
    width="100%" 
    height="450" 
    src="https://www.youtube.com/embed/LTxkJ7JulWA" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
    allowfullscreen>
  </iframe>
</div>

## 🖼️ Hình ảnh minh họa

<img src="/BlogCaNhan/images/roadmap/Testing.jpg" alt="Testing" />

## 📚 Các loại testing

### 1. Unit Testing

Kiểm tra từng function/component riêng lẻ:

```javascript
// sum.test.js
import { sum } from "./sum";

test("adds 1 + 2 to equal 3", () => {
  expect(sum(1, 2)).toBe(3);
});
```

### 2. Integration Testing

Kiểm tra sự tương tác giữa các component:

```jsx
import { render, screen } from "@testing-library/react";
import UserProfile from "./UserProfile";

test("renders user profile", () => {
  render(<UserProfile user={{ name: "John" }} />);
  expect(screen.getByText("John")).toBeInTheDocument();
});
```

### 3. End-to-End (E2E) Testing

Kiểm tra toàn bộ flow của ứng dụng:

```javascript
// Cypress example
describe("Login Flow", () => {
  it("should login successfully", () => {
    cy.visit("/login");
    cy.get("[data-cy=email]").type("user@example.com");
    cy.get("[data-cy=password]").type("password");
    cy.get("[data-cy=submit]").click();
    cy.url().should("include", "/dashboard");
  });
});
```

## 🛠️ Testing Tools

### Jest

```javascript
// Jest configuration
module.exports = {
  testEnvironment: "jsdom",
  setupFilesAfterEnv: ["<rootDir>/src/setupTests.js"],
};
```

### React Testing Library

```jsx
import { render, screen, fireEvent } from "@testing-library/react";
import Button from "./Button";

test("button click", () => {
  const handleClick = jest.fn();
  render(<Button onClick={handleClick} />);
  fireEvent.click(screen.getByRole("button"));
  expect(handleClick).toHaveBeenCalledTimes(1);
});
```

### Cypress

```javascript
// cypress/integration/app.spec.js
describe("App", () => {
  it("should load homepage", () => {
    cy.visit("/");
    cy.contains("Welcome");
  });
});
```

## 💡 Best Practices

- Viết test trước khi code (TDD)
- Test behavior, không test implementation
- Giữ test đơn giản và dễ đọc
- Test edge cases
- Maintain test coverage > 80%

## 💪 Thực hành

1. Viết unit tests cho functions
2. Test React components
3. Setup E2E testing với Cypress
4. Đạt test coverage cao

## 🔗 Tài nguyên

- [Jest Documentation](https://jestjs.io/)
- [React Testing Library](https://testing-library.com/react)
- [Cypress Documentation](https://docs.cypress.io/)

## ➡️ Bước tiếp theo

Sau khi nắm vững Testing, hãy học [Deployment](../deployment/)!

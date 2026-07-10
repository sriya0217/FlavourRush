# 🍔 FlavorRush — Online Food Ordering Web App.

FlavorRush is a full-stack food ordering web application built with **Java (Servlets + JSP)**, **JSTL**, and **MySQL**, styled with a custom dark, restaurant-inspired UI. Users can browse restaurants, view menus, add items to a cart, check out, and track their order history.

---

## ✨ Features

- 🔐 User registration & login with hashed passwords (jBCrypt)
- 🏬 Browse restaurants and view individual menus
- 🛒 Add to cart, update quantities, remove items
- 💳 Checkout with delivery details, GST calculation, and payment method selection
- 📦 Order history for logged-in users
- 🎨 Custom dark-themed, fully responsive UI (no frontend framework — plain JSP/CSS)
- 🎥 Full-bleed hero video banner on the homepage

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Backend | Java 17, Jakarta Servlets, JSP |
| Templating | JSTL (Jakarta Standard Tag Library) |
| Database | MySQL |
| Server | Apache Tomcat 10.1 |
| Password hashing | jBCrypt |
| Frontend | HTML, CSS (custom, no framework), vanilla JS |
| IDE | Eclipse (Dynamic Web Project) |

---

## 📁 Project Structure

```
FlavorRush/
├── src/main/java/com/flavorrush/
│   ├── servlet/        # HomeServlet, LoginServlet, RegisterServlet,
│   │                    # CartServlet, CheckoutServlet, MenuServlet,
│   │                    # OrderHistoryServlet, PlaceOrderServlet, LogoutServlet
│   ├── dao/             # DAO interfaces
│   ├── daoimpl/         # DAO implementations (JDBC)
│   ├── model/            # Restaurant, Menu, Cart, User, Order, etc.
│   ├── util/             # DBConnection
│   └── filters/          # LoginFilter
├── src/main/webapp/
│   ├── *.jsp              # index, login, register, cart, checkout,
│   │                       # menu, orderHistory, success, error
│   ├── css/                # theme.css (shared) + per-page stylesheets
│   ├── js/
│   └── images/
│       ├── logo/            # hero video/poster, register illustration
│       ├── restaurants/      # restaurant logos
│       └── menu/              # dish photos
├── database/
│   └── flavorrush_db.sql     # schema + seed data
└── WEB-INF/web.xml
```

---

## ⚙️ Setup Instructions

### 1. Prerequisites
- JDK 17+
- Eclipse IDE (with Dynamic Web Project support / EE tools)
- Apache Tomcat 10.1+
- MySQL Server

### 2. Clone the repository
```bash
git clone https://github.com/<your-username>/FlavorRush.git
```

### 3. Set up the database
1. Start MySQL and create the database from the provided script:
   ```bash
   mysql -u root -p < database/flavorrush_db.sql
   ```
2. This creates the `flavorrush_db` schema with `restaurants`, `menus`, `users`, `orders`, etc., plus seed data for a few restaurants and menu items.

### 4. Configure the database connection
Open `src/main/java/com/flavorrush/util/DBConnection.java` and update the credentials to match your local MySQL setup:
```java
private static final String URL = "jdbc:mysql://localhost:3306/flavorrush_db";
private static final String USERNAME = "root";
private static final String PASSWORD = "your_mysql_password";
```
> ⚠️ **Don't commit real credentials.** Consider moving these to environment variables or a `.properties` file excluded via `.gitignore` before pushing to a public repo.

### 5. Add required libraries
This project depends on the following JARs (not included in the repo — add them to your build path in Eclipse, or drop them in a `lib/` folder and add via **Build Path → Configure Build Path → Add JARs**):
- `mysql-connector-j` (9.x)
- `jbcrypt` (0.4)
- `jakarta.servlet.jsp.jstl-api` (3.0.2)
- `jakarta.servlet.jsp.jstl` (3.0.1)

> The `.classpath` file that ships in this repo points to absolute local file paths (e.g. `C:/Users/.../Downloads/...`) — these **will not resolve on another machine**. After cloning, you'll need to re-link these libraries yourself in Eclipse (Project → Properties → Java Build Path → Libraries).

### 6. Import into Eclipse
1. **File → Import → Existing Projects into Workspace**, select the cloned folder.
2. Right-click the project → **Properties → Targeted Runtimes** → select Tomcat 10.1.
3. Right-click → **Run As → Run on Server**.

### 7. Add images
The database seed data references specific image filenames under `images/restaurants/` and `images/menu/` (e.g. `pizzahut.jpg`, `margherita.jpg`). These image files aren't included in the repo — add your own photos with matching filenames, or update the `image_path` columns in the database to point at whatever files you use.

### 8. Run
Visit `http://localhost:9090/FlavorRush/` (adjust the port to whatever your Tomcat server is configured to use).

---

## 🗄️ Database Schema (high level)

- `restaurants` — restaurant details + image path
- `menus` — dishes per restaurant, price, rating, availability
- `users` — registered users (hashed passwords)
- `orders` / `order_items` — placed orders and their line items

Full schema is in [`database/flavorrush_db.sql`](database/flavorrush_db.sql).

---

## 📸 Screenshots

_Add a few screenshots here once your images are in place — homepage hero, menu page, cart, and checkout make good ones._

---

## 📄 License

This project is open for educational/personal use. Add a license of your choice (MIT is a common default) if you plan to make the repo public.

---

## 🙋 Notes for Contributors

- All styling lives in `css/theme.css` (shared variables/base styles) plus one stylesheet per page — no CSS framework is used.
- JSP pages use JSTL (`<c:choose>`, `<c:forEach>`, etc.) for all dynamic content; keep new markup consistent with that pattern rather than introducing inline scriptlets.
- Broken/missing images degrade gracefully (dark placeholder box) rather than showing browser alt-text, by design — see the `color:transparent; font-size:0;` pattern on image rules in the CSS.

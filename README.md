# Levi Huang - Full-Stack Developer | Project Showcase

This repository serves as a detailed showcase of my key projects, highlighting my expertise in full-stack development, system architecture, and solving complex business challenges with technology. Each case study below provides an in-depth look at the project's goals, the technical challenges faced, the solutions I implemented, and the resulting impact.

---

## Technical Case Study: Zuoluh — Values-Aligned Spending & Insight Platform

*Note: This project is currently in the architectural design and MVP development phase, showcasing my ability to architect a complex system from concept to execution.*

### 1. Project Description

**Zuoluh** is a fintech platform designed to help users understand how their daily spending behavior aligns with their personal values. By integrating with bank accounts via the Plaid API and leveraging AI for analysis, the platform provides users with personalized insights, empowering them to make more conscious and value-driven financial decisions. The initial product will be a Progressive Web App (PWA), with plans to expand to a native mobile experience.

### 2. The Challenge

The primary architectural challenge is to build a secure, scalable, and highly personalized platform that can handle sensitive financial data while translating subjective user "values" into quantifiable analysis.

* **Complex Third-Party Integrations:** The system requires robust and secure integration with multiple complex APIs, primarily **Plaid** for banking data and **Google Gemini** for AI-powered insights.
* **Personalized & Subjective Logic:** Unlike traditional financial apps, the core logic revolves around mapping objective transaction data to a user's subjective, self-defined values (e.g., "Eco-friendly," "Fair Trade"), which requires a flexible and intelligent data model.
* **Data Security & Privacy:** Handling personal financial transaction data demands the highest level of security, requiring a secure architecture and strict data handling protocols from day one.
* **Scalable Data Modeling:** The database schema must efficiently map relationships between users, transactions, merchants, values, and external certifications (like B Corp), and be designed to scale as the user base and data complexity grow.

### 3. My Solution (Architectural Vision)

As the technical lead, I have designed an **API-first, service-oriented architecture** to ensure scalability and maintainability.

* **Phased Rollout Strategy:** The product is planned in phases, starting with a **PWA** to quickly validate the core features and gather user feedback, followed by **React Native** development for market expansion.
* **Core Data Structure:** I designed a normalized PostgreSQL database schema centered around key entities: `Users`, `Transactions`, `Values`, `UserValuePreferences`, and `Insights`. This structure allows for flexible querying and efficient analysis of how spending reflects user preferences.
* **Technology Stack & Rationale:**
    * **Frontend:** PWA (likely using React/Next.js) for its cross-platform reach and fast initial delivery.
    * **Backend Services:** A series of dedicated backend services (Authentication, Transactions, Insights) to handle specific domains of business logic.
    * **AI Engine:** Utilizing **Google Gemini Flash 2.0** for its balance of performance and cost-effectiveness in generating personalized spending insights.
    * **Database & Caching:** **PostgreSQL** was chosen for its robustness and powerful querying capabilities, supplemented by a **Redis** cache layer to improve performance for frequently accessed data.
    * **Banking Integration:** Using the **Plaid API** for secure and standardized access to users' bank transaction data.

### 4. Results & Vision

While the project is in its early stages, the architectural design is complete and lays a solid foundation for achieving the product's vision.

* **Intended Outcome:** The primary goal is to empower users with unprecedented clarity on the alignment between their spending and personal values, fostering more conscious consumer behavior.
* **Long-Term Vision:** The platform is designed with a long-term strategy to evolve into a B2B data insights service, providing anonymized market trend reports and forming value-aligned merchant partnerships.
* **Demonstrated Capability:** This project showcases my ability to not only execute on development tasks but also to **architect a complex digital product from the ground up**, aligning a comprehensive technical strategy with a clear product roadmap and a viable business model.

### Tech Stack (Planned)

* **Frontend:** PWA (React/Next.js), React Native
* **Backend:** Node.js (for services), PostgreSQL
* **AI & Data:** Google Gemini, Redis, Plaid API
* **Infrastructure:** Cloud-based deployment (e.g., Vercel, GCP)

---

## Technical Case Study: Forexify — Intelligent Trading Platform

### 1. Project Description

Forexify is an advanced analytics and strategy development platform for modern foreign exchange traders. It is an integrated decision-support system that unifies **data visualization, AI-driven strategy generation, and performance validation**. The platform's goal is to convert high-frequency, complex market data into actionable insights for traders of all levels, from beginners learning systematic trading to seasoned experts needing efficient tools to validate complex strategies.

The platform addresses three key pain points in traditional trading: **1) Information overload**, **2) High barriers to strategy development**, and **3) Unreliable strategy validation**.

### 2. The Challenge

The core technical challenge was balancing **high performance, complexity, and ease of use**.

* **High-Performance Real-Time Data Processing:** The system needed a robust backend to handle high-throughput market data streams and provide low-latency updates for real-time charts and dashboards.
* **Abstraction of Complex Trading Logic:** The main challenge was to enable users without a programming background to "create" complex conditional logic for trading strategies.
* **Reliability of Strategy Generation & Validation:** A key feature, AI code generation, had to be reliable. The generated code needed to be syntactically correct and logically aligned with the user's intent. The backtesting results also needed to be trustworthy and repeatable.
* **Flexible and Extensible Architecture:** The platform had to support a variety of predefined and custom strategies, requiring a highly modular architecture that could easily accommodate new indicators and strategy types.

### 3. My Solution (Technical Implementation)

I designed and implemented a system with clear responsibilities and a modern tech stack.

* **Architecture: Service-Oriented Hybrid Model**
    * I opted for a hybrid model, combining a core web application with separate data services.
    * **Core Web App (`web/`):** A **Flask**-based application serving the frontend and APIs, structured with **Flask Blueprints** for modularity (`lab`, `backtest`, etc.).
    * **Data Processing Service (`task/`):** A set of independent Python scripts and **Google Cloud Run** serverless functions forming an asynchronous data pipeline for fetching, cleaning, and storing financial data in a central **MySQL** database. This separation prevents data-intensive tasks from blocking the main application's performance.

* **Key Implementation: AI-Driven Strategy Generator**
    * This is the technical core of the project. I solved the abstraction and reliability challenges using a sophisticated prompt engineering system.
    1.  **Structured Prompt Engineering:** Instead of letting the LLM (GPT-4o-mini) generate code freely, I designed a system that dynamically constructs a highly structured, three-part prompt based on user UI selections. This prompt includes a **System Role**, a **Task Description**, and a **Code Template**.
    2.  **Template-Grounded Generation:** This "template-grounded" approach constrains the AI's output, ensuring the generated Python code adheres to the backtesting engine's expected input/output contract (receiving a DataFrame, outputting `Buy_Signal` and `Sell_Signal` columns). This guarantees the code is plug-and-play and highly reliable.
    3.  **Dual-Language Synchronous Generation:** The system uses the same user input to synchronously generate both **PineScript** (for TradingView visualization) and **Python** (for detailed backtesting) code.

* **Key Implementation: Flexible Backtesting Engine**
    * The backtesting engine was built using the classic **Strategy Pattern**.
    * It features a dispatcher that can dynamically execute strategies. For AI-generated strategies, it reads the Python code string from the database and uses `exec()` within a controlled, secure `GeneratedStrategy` class. The strict constraints from prompt engineering ensure the executed code is safe and contains only signal calculation logic.
    * The engine calculates key performance indicators, most importantly **Maximum Drawdown (MDD)**, providing users with an intuitive assessment of a strategy's risk.

### 4. Results & Impact

The technical solutions led to significant and quantifiable positive impacts.

* **Dramatically Improved User Efficiency:** The "AI Strategy Lab" reduced the strategy development lifecycle **from days to minutes, improving iteration efficiency by an estimated 90%**. Users can now focus on strategic thinking rather than technical implementation details.
* **Lowered the Barrier to Systematic Trading:** By abstracting complex logic into simple UI selections, the platform empowered non-programmers to create and validate sophisticated trading strategies, significantly boosting user engagement and the platform's educational value.
* **Ensured System Performance and Scalability:** Separating the data pipeline from the main application guarantees a responsive user experience, even as data volume and user load increase. The modular design makes adding new indicators or strategy types simple and low-risk.
* **Delivered Core Business Value:** The platform's ability to help users find and validate effective strategies, complete with quantifiable risk (MDD) and return metrics, directly achieves its core business goal and provides powerful data-driven support for trading decisions.

### Tech Stack

* **Backend:** Python, Flask
* **Data & AI:** NumPy, Pandas, OpenAI API (GPT-4o-mini)
* **Database:** MySQL
* **Frontend:** Vue.js, Web Sockets
* **Infrastructure:** Google Cloud Run

---

## Technical Case Study: Templeify — Digital Platform for a Traditional Temple

### 1. Project Description

Templeify is a custom e-commerce and service booking platform designed for a traditional religious organization. Its core objective was to digitally transform long-standing offline services, such as annual "An-Tai-Sui" and "Guang-Ming-Deng" blessings, making them accessible online. The platform serves two main user groups: a younger, tech-savvy generation booking services for themselves and their families (especially elderly relatives), and temple administrators requiring an efficient backend system to manage orders, member data, and finances.

The project addresses the critical issues of **accessibility and efficiency** for traditional services in the digital age. By creating a secure and intuitive online portal, Templeify not only served the existing community but also reached new followers overseas or in other cities, successfully merging traditional faith with modern technology.

### 2. The Challenge

The core challenges went beyond user experience, encompassing complex business logic and system integrations.

* **Translating Complex Business Logic:** A key characteristic of temple services is their "family-based" nature. A single order often involves multiple family members, each with unique data (name, birth date) that must be accurate. This differs significantly from standard e-commerce logic. The challenge was to design a data model and a frontend workflow that could gracefully handle these many-to-many relationships.
* **Building Trust Through Secure Payments:** Financial transactions for religious services require a high degree of trust. The system had to integrate a stable and secure payment gateway and ensure the atomicity of every transaction, handling exceptions like payment interruptions or webhook failures to guarantee data consistency between order and payment statuses.
* **Seamless Online-to-Offline (O2O) Integration:** The services, once ordered online, had to be fulfilled physically (e.g., hanging a nameplate on a lantern). The challenge was to automate the conversion of online order data into physical outputs like nameplate stickers, receipts, and certificates to reduce manual transcription errors and improve back-office efficiency.
* **Performance Under Peak Load:** Temple services experience significant seasonal traffic spikes, particularly around the Lunar New Year. The system had to be architected to handle high-concurrency scenarios without performance degradation.

### 3. My Solution (Technical Implementation)

I implemented a pragmatic and robust technical solution to meet these challenges.

* **Architecture & Database Design:**
    * The project uses a monolithic architecture with PHP as the primary backend language, deployed on Google App Engine.
    * I designed a normalized relational database schema to handle the complex business logic. The key was a **mapping table (`Product_Family_Member_Mapping`)** to cleanly manage the many-to-many relationship between service items and family members, alongside tables for users, products, orders, and payments.

* **Asynchronous Payment Webhook Workflow:**
    * The payment process was designed to be asynchronous and state-tracked to ensure reliability.
    1.  **Order Creation:** On checkout, an order is created in the database with a "pending" status.
    2.  **Payment Initiation:** The backend generates a cryptographically signed request to the payment gateway (QPay), and the user is redirected.
    3.  **Webhook Reception:** After payment, the gateway sends an asynchronous POST request to our webhook endpoint.
    4.  **Verification & Update:** The webhook's first task is to **validate the request's signature** to ensure it's authentic. Upon successful verification, it updates the order status to "completed" and records the transaction. This asynchronous design ensures the transaction is correctly processed even if the user closes their browser.

* **Performance & Load Testing:**
    * To prepare for high-concurrency scenarios like the Lunar New Year rush, I implemented **performance testing using Locust.py**.
    * By simulating thousands of users concurrently booking services and making payments, we identified and optimized database query bottlenecks. This ensured the system remained stable and responsive under peak load, with average API response times maintained below 200ms.

* **Security Measures:**
    * In addition to signature verification for webhooks, user passwords were saved using standard hashing algorithms. All database interactions utilized **Prepared Statements** to completely prevent SQL injection vulnerabilities.

### 4. Results & Impact

The solution brought concrete and measurable benefits to the temple.

* **Achieved Significant Business Growth:** The platform opened up a new digital revenue stream, increasing annual turnover by **40% (from 5M to 7M TWD)**.
* **Dramatically Improved Operational Efficiency:** The automation of physical outputs (like printing stickers) significantly reduced manual labor and error rates for temple staff, freeing them to focus on core religious services.
* **Enhanced User Experience:** The custom-designed family member form provided a much smoother user journey than generic e-commerce platforms, reducing data input time by an estimated 30%.
* **Established a Scalable Foundation:** The modular API design within the monolith allows for easy addition of new services in the future without major architectural changes, providing a solid foundation for future growth.

### Tech Stack

* **Backend:** PHP (Vanilla)
* **Frontend:** JavaScript, HTML, CSS
* **Database:** MySQL
* **Payment Gateway:** QPay Integration
* **Testing:** Locust.py
* **Infrastructure:** Google Cloud Platform (GCP) App Engine

---

## Technical Case Study: Apparel X — Multi-Tenant SaaS ERP Platform

### 1. Project Description

Apparel X is an Enterprise Resource Planning (ERP) SaaS platform designed specifically for the small and medium-sized apparel industry. Its core mission is to consolidate complex and traditionally fragmented processes—including inventory, orders, customer, and supplier management—into a single, efficient, cloud-based platform.

The target users are SMB apparel wholesalers and retailers who need to undergo digital transformation but lack the resources to develop a large-scale ERP system in-house. Apparel X addresses critical pain points:

* **Information Silos:** Eliminating disconnected Excel sheets and standalone software where inventory, order, and customer data were previously stored, making real-time synchronization difficult.
* **High Operational Costs:** Reducing errors and time spent on manual order processing and inventory counting, which lead to high labor costs and inventory loss.
* **Lack of Real-Time Data:** Empowering managers with immediate access to sales figures, inventory levels, and purchasing needs to improve decision-making accuracy.

The platform covers the entire operational lifecycle of an apparel business, including modules for master data management, inventory and sales workflows (supporting barcode integration), stock-taking, accounts receivable/payable, and a multi-dimensional reporting center.

### 2. The Challenge

The primary technical and business challenges stemmed from the platform's nature as a SaaS product and the inherent complexities of the apparel industry.

* **Multi-Tenant Architecture:** The core challenge was designing a SaaS architecture capable of serving hundreds, or even thousands, of apparel companies simultaneously. It was critical to ensure 100% data isolation, security, and integrity between tenants at the architectural level, while also being cost-effective and highly scalable.
* **Complex Business Logic:** The apparel industry's inventory management is notoriously complex due to SKUs having multiple attributes (item number, color, size). The system needed to handle tens of thousands of SKUs efficiently, manage complex order scenarios (e.g., backorders, pre-orders, tiered pricing), and calculate real-time inventory levels accurately with every transaction, posing a significant challenge to database performance and transactional integrity.
* **Performance and User Experience:** ERP systems are data-intensive. The challenge was to provide a smooth, non-blocking user experience within a traditional PHP server-side rendering context, especially when generating complex reports or loading large order details, avoiding long page load times.
* **Maintainability without a Framework:** The project was developed using vanilla PHP. This introduced the challenge of maintaining code organization, readability, and long-term scalability without the constraints and conventions of a modern MVC framework.

### 3. My Solution (Technical Implementation)

To address these challenges, I designed and implemented a pragmatic and highly effective technical solution.

* **Architecture: SPA-like Shell + Dynamic Component Loading**
    * Instead of a traditional multi-page application, I designed an SPA-like architecture. After logging in, users load a main application shell (`main.php`), and all subsequent operations occur without full-page reloads.
    * When a user clicks a menu item, a frontend JavaScript router utilizes URL Hash (`#`) changes to asynchronously load the corresponding feature page (e.g., `editCustin.php`) as a "component" into the main shell's content area via AJAX (`jQuery.load`). This significantly improved the user experience, making the application feel as fluid as a modern desktop app.

* **Multi-Tenancy: Application-Layer Data Isolation (Shared Database, Shared Schema)**
    * I implemented a mature and cost-effective multi-tenancy model where all tenants' data resides in a shared database and schema.
    * Data isolation was strictly enforced at the application layer. Upon login, the backend authenticates the user and retrieves their unique `clientid` (tenant ID), which is stored in the DOM.
    * Every subsequent API request from any loaded component includes this global `clientid`. **All backend SQL queries are programmatically forced to include a `WHERE clientid = ?` clause.** This ensures that a tenant can only ever access their own data, providing robust data segregation.

* **API Design: Pragmatic RPC-Style Endpoints**
    * The backend API was designed in a Remote Procedure Call (RPC) style. Each API file corresponds to a specific action (e.g., `supplier_add.php`, `supplier_upd.php`).
    * This approach was intuitive and easy to debug in the absence of a framework. It reduced ambiguity and streamlined communication between frontend and backend development.
    * While this pragmatic RPC approach was highly effective, a future refactor could involve evolving it into a standardized RESTful or GraphQL API to further enhance interoperability with modern third-party services.

* **Security & Scalability (GCP)**
    * The application was deployed on **Google Cloud Platform (GCP) App Engine**.
    * Authentication was managed via server-side sessions, and authorization was handled by checking the user's role on sensitive backend operations.
    * Database security was ensured by using **PDO with Prepared Statements** to prevent SQL injection.
    * GCP App Engine's **default auto-scaling mechanism** was leveraged to automatically manage server instances based on real-time traffic. This guaranteed system stability during peak business hours while saving costs during off-peak times.

### 4. Results & Impact

This solution delivered significant, positive outcomes for the Apparel X platform.

* **Enhanced System Performance & User Experience:** The SPA-like architecture resulted in near-instantaneous page transitions, dramatically improving operational fluency for users.
* **Achieved a Scalable and Secure SaaS Platform:** The application-layer multi-tenancy model proved to be a stable, reliable, and maintainable solution, successfully supporting multiple companies on a single platform. The auto-scaling capabilities of GCP provided a solid foundation for future business growth.
* **Delivered Core Business Value:** By successfully digitizing complex inventory, sales, and accounting logic, the platform significantly reduced customers' manual errors and improved the accuracy of their financial and stock data.
* **Demonstrated Pragmatic Architectural Design:** This project showcases the ability to build a complex, performant, and maintainable enterprise-grade application even without a modern framework, by applying clear architectural principles and disciplined development practices.

### Tech Stack

* **Backend:** PHP (Vanilla)
* **Frontend:** JavaScript, jQuery, HTML, CSS
* **Database:** MySQL
* **Infrastructure:** Google Cloud Platform (GCP) App Engine

---

## Technical Case Study: "We Are Enough" — Interactive Narrative Experience

### 1. Project Description

"We Are Enough" is an integrated platform connecting impact investors with social enterprises. My primary role was to lead the design and development of the "Education Portal," a key user engagement module. The goal was to transform traditionally dry financial investment knowledge into a captivating, immersive digital experience.

To achieve this, I built a highly custom frontend solution centered around an `InvestmentTimeline` Vue.js component. This component functions as an interactive infographic, using sophisticated animations and user interactions to vividly convey the platform's brand story and core values to its target audience.

### 2. The Challenge

The main challenge was **translating a complex, artistic, and conceptual static design from Figma into a fluid, high-performance, and fully responsive dynamic web experience**. This required a perfect balance between visual complexity and web performance.

* **Performance Bottlenecks:** The feature involved a large number of continuous animations triggered by user scrolling, which could easily cause browser lag (jank) if not implemented correctly.
* **Complex Algorithmic Logic:** The core visual element, an SVG curve, had to be generated algorithmically in real-time based on content height and viewport width, a task far beyond the capabilities of traditional CSS.
* **Deep Third-Party Integration:** The project relied heavily on the GSAP (GreenSock Animation Platform) library, particularly its advanced `ScrollTrigger` plugin. The challenge was to architect a system that could precisely map non-linear scroll inputs to a complex, linear animation timeline composed of dozens of individual tweens.

### 3. My Solution (Technical Implementation)

I designed and implemented a precise frontend architecture with Vue.js as the foundation and GSAP as the core animation engine.

* **Component Architecture & Backend Integration:**
    * All functionality was encapsulated within a single, reusable `InvestmentTimeline.vue` component. This component-based architecture ensured the complex logic remained self-contained and could be easily integrated into any page.
    * The backend, built with **Laravel**, serves a dual purpose. It acts as a stable API endpoint to asynchronously deliver narrative content (as JSON) to the Vue component, and it also handles the routing and server-side rendering for other, less dynamic portions of the site. This created an **efficient hybrid rendering strategy**.

* **Key Algorithm: Dynamic SVG Path Generation**
    * I wrote a custom path-generation algorithm from scratch. It uses a `ResizeObserver` to monitor content blocks for any size changes (e.g., image loading, window resize) and automatically triggers a recalculation.
    * The core `generatePath` function reads the real-time geometry of all content blocks and dynamically generates anchor points and Bézier curve control points, creating a perfectly fitted SVG path for any screen size.

* **GSAP Scroll-Driven Animation Engine:**
    * I used GSAP's `ScrollTrigger` plugin to link the user's scroll position directly to the playback head of a **master animation timeline**.
    * All individual animations (fade-ins, card stacks, etc.) were sequenced on this master timeline. For complex scenes like the "card stack," I created **nested timelines** with staggered animations for a natural effect, which were then placed as a single unit onto the master timeline, keeping the structure clean and manageable.

* **Performance Optimization Strategy:**
    * **GPU Hardware Acceleration:** All animations were strictly limited to CSS `transform` and `opacity` properties, ensuring the calculations were handled by the GPU to achieve a silky-smooth 60fps frame rate.
    * **Event Debouncing:** The computationally expensive path generation function was wrapped in a `debounce` utility, ensuring it only runs after the user has finished resizing the window, preventing performance hits during high-frequency events.

### 4. Results & Impact

The technical solution successfully transformed a static design vision into an interactive product with exceptional brand value and user experience.

* **Transformed User Experience:** The feature became one of the most beloved parts of the platform, turning educational content into an enjoyable visual journey. Analytics showed that the **average user session duration** on this page was significantly higher than on other static content pages.
* **Guaranteed System Performance:** Through meticulous optimization, the page maintained a fluid scroll experience across all devices, successfully balancing visual impact with technical performance.
* **Delivered Business Value:** The unique interactive experience became a powerful marketing tool, effectively communicating the brand's value and showcasing the platform's technical and design innovation to potential partners and investors.
* **Ensured Maintainability & Scalability:** The component is entirely **data-driven**. This means content can be updated in the future simply by modifying the JSON data from the backend, without touching any of the complex frontend animation code, making it highly maintainable and scalable.

### Tech Stack

* **Frontend:** Vue.js, GSAP (GreenSock Animation Platform), ScrollTrigger
* **Backend:** Laravel
* **Design:** Figma

# Hi, I'm Aryan Raj Kathuria 👋

Building practical, production-minded software — from a zero-framework insurance advisory platform to a Flutter finance tracker with on-device AI.

🔭 Currently building and maintaining **[PolicyRaj](https://www.policyraj.com)** — a live insurance advisory platform with a custom AI chatbot and a serverless AWS backend behind a customer policy dashboard.
🌱 Also working on **[SpendSnap](https://github.com/aryanrajkathuria/SpendSnap)** — a Flutter + Firebase personal finance manager with Gemini-powered receipt scanning.
💬 Interested in web performance, clean architecture, and building things that don't need a framework to be good.

## 🚀 Featured Projects

### 🛡️ [PolicyRaj](https://www.policyraj.com) — insurance advisory platform

A live insurance advisory site for an IRDAI-licensed advisor, with a customer policy
dashboard behind it. The public site is hand-written vanilla HTML/CSS/JS with zero build
step and a 277-entry pattern-matching AI chatbot that calls no external API. Behind the
login sits a serverless AWS backend I designed and provisioned myself — authentication,
per-customer document storage, an admin view, and an automated renewal-reminder pipeline
that emails customers before their cover lapses. Every resource was created from
scripted, idempotent provisioning rather than console clicking, and the whole system
runs inside the AWS free tier.

**⚙️ Engineering highlights**

- 🔐 **Authentication** — Cognito Hosted UI. Every request carries an ID token that each
  Lambda verifies against the pool's JWKS before doing any work. User identity is taken
  from the verified claims, never from the request body, and a field whitelist stops a
  client smuggling privileged attributes into an update.
- 🧱 **Least privilege by construction** — three request-handling Lambdas behind Function
  URLs, each with its own IAM role. The admin role grants only `Scan`, `Query`,
  `GetItem` and `s3:GetObject`, so an admin session *physically cannot write* to the
  data store, independently of the application-level group check that also guards it.
  A fourth Lambda has no Function URL at all and is reachable only by its schedule.
- 🗄️ **DynamoDB single-table design** — profiles, policies and an activity feed share one
  on-demand table under a composite partition/sort key, with no secondary indexes.
  Activity records expire automatically via TTL rather than needing a cleanup job.
- 📄 **Documents never pass through a Lambda** — uploads and downloads use short-lived
  presigned S3 URLs, scoped per user, with content type pinned at signing time and any
  key outside the caller's own prefix rejected before a URL is issued.
- ⏰ **Scheduled renewal reminders** — a daily EventBridge rule invokes a Lambda that
  finds policies renewing in exactly 30, 15 or 3 days and emails the customer via SES.
  Each window has its own idempotency marker, claimed *before* the send and rolled back
  if it fails, so a retry can never double-email a customer.
- 🌏 **Timezone-correct date windows** — the reminder sweep resolves "today" in
  Asia/Kolkata rather than UTC. The schedule fires at 03:30 UTC, which is the same
  calendar day in IST, but pinning the zone explicitly means a reminder window can never
  silently slip by a day.
- 📦 **Runtime and packaging** — all four functions run on Node.js 22 as ES modules. Each
  deployment bundles its own pinned AWS SDK v3 clients instead of relying on the version
  baked into the runtime, so an AWS-side runtime update cannot quietly change SDK
  behaviour — and it is the only way to ship the JWT verification library, which the
  runtime does not include.
- 💰 **Cost discipline** — no VPC, and therefore no NAT gateway. No API Gateway; Lambda
  Function URLs instead. No provisioned concurrency and no provisioned table capacity —
  the table bills per request. An AWS Budgets alarm covers both actual and forecasted
  spend at a few dollars a month, so the free-tier assumption is monitored rather than
  assumed.

### 🌱 [SpendSnap](https://github.com/aryanrajkathuria/SpendSnap) — personal finance manager

Personal finance manager built with Flutter, Firebase, and Google Gemini. Feature-first Clean Architecture with the BLoC pattern for state management.

## 🌐 Connect

[![LinkedIn](https://img.shields.io/badge/LinkedIn-%230077B5.svg?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/aryan-raj-kathuria-0696a5312) [![email](https://img.shields.io/badge/Email-D14836?logo=gmail&logoColor=white)](mailto:aryanrajkathuria@gmail.com)

## 💻 Tech Stack

**Used in my featured projects:**

![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white) ![AWS Lambda](https://img.shields.io/badge/AWS%20Lambda-%23FF9900.svg?style=for-the-badge&logo=awslambda&logoColor=white) ![Amazon DynamoDB](https://img.shields.io/badge/Amazon%20DynamoDB-%234053D6.svg?style=for-the-badge&logo=amazondynamodb&logoColor=white) ![Amazon S3](https://img.shields.io/badge/Amazon%20S3-%23569A31.svg?style=for-the-badge&logo=amazons3&logoColor=white) ![Amazon Cognito](https://img.shields.io/badge/Amazon%20Cognito-%23DD344C.svg?style=for-the-badge&logo=amazoncognito&logoColor=white) ![Amazon EventBridge](https://img.shields.io/badge/Amazon%20EventBridge-%23FF4F8B.svg?style=for-the-badge&logo=amazoneventbridge&logoColor=white) ![Amazon SES](https://img.shields.io/badge/Amazon%20SES-%23C925D1.svg?style=for-the-badge&logo=amazonses&logoColor=white) ![Node.js](https://img.shields.io/badge/node.js-6DA55F?style=for-the-badge&logo=node.js&logoColor=white) ![Express](https://img.shields.io/badge/Express.js-000000?style=for-the-badge&logo=express&logoColor=white) ![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white) ![Flutter](https://img.shields.io/badge/Flutter-%2302569B.svg?style=for-the-badge&logo=Flutter&logoColor=white) ![Dart](https://img.shields.io/badge/dart-%230175C2.svg?style=for-the-badge&logo=dart&logoColor=white) ![Firebase](https://img.shields.io/badge/firebase-a08021?style=for-the-badge&logo=firebase&logoColor=ffcd34) ![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E) ![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white) ![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)

**Also familiar with:**

![C](https://img.shields.io/badge/c-%2300599C.svg?style=for-the-badge&logo=c&logoColor=white) ![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white) ![MySQL](https://img.shields.io/badge/mysql-4479A1.svg?style=for-the-badge&logo=mysql&logoColor=white) ![MongoDB](https://img.shields.io/badge/MongoDB-%234ea94b.svg?style=for-the-badge&logo=mongodb&logoColor=white) ![React](https://img.shields.io/badge/react-%2320232a.svg?style=for-the-badge&logo=react&logoColor=white)

## 📊 GitHub Stats

![](https://github-readme-stats.vercel.app/api?username=aryanrajkathuria&theme=dark&hide_border=false&include_all_commits=true&count_private=true)<br/>
![](https://nirzak-streak-stats.vercel.app/?user=aryanrajkathuria&theme=dark&hide_border=false)<br/>
![](https://github-readme-stats.vercel.app/api/top-langs/?username=aryanrajkathuria&theme=dark&hide_border=false&include_all_commits=true&count_private=true&layout=compact)

---
[![](https://visitcount.itsvg.in/api?id=aryanrajkathuria&icon=0&color=0)](https://visitcount.itsvg.in)

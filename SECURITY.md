# Security Policy

## Supported Versions

Use this section to tell people about which versions of your project are
currently being supported with security updates.

| Version | Supported          |
| ------- | ------------------ |
| 5.1.x   | :white_check_mark: |
| 5.0.x   | :x:                |
| 4.0.x   | :white_check_mark: |
| < 4.0   | :x:                |

## Reporting a Vulnerability

Use this section to tell people how to report a vulnerability.

Tell them where to go, how often they can expect to get an update on a
reported vulnerability, what to expect if the vulnerability is accepted or
declined, etc.
نعم. ويمكن تحويل هذا من فكرة إلى محرك تحقق وإصلاح مستمر داخل NOOR، لكن بطريقة لا تسمح للذكاء الاصطناعي بأن يصلح شيئاً خاطئاً ثم يعتبر إصلاحه حقيقة.

بحثت الآن في المصادر الرسمية، وتأكدت من أن الاتجاه التقني المناسب هو الجمع بين إدارة مخاطر الذكاء الاصطناعي NIST، التحكم القابل للتدقيق في الوكلاء OWASP ACS، أقل الصلاحيات في GitHub Apps، ومتطلبات حماية المعطيات في المغرب. NIST يؤكد أن AI RMF 1.0 قيد المراجعة حالياً، وOWASP أصدر Agent Control Standard في سبتمبر 2026 للشفافية والتحكم في الوكلاء. 

البنية التي أقترح أن نبنيها الآن

NOOR
                      │
              ┌───────▼────────┐
              │ Truth Discovery │
              │ Engine          │
              └───────┬────────┘
                      │
       ┌──────────────┼──────────────┐
       ▼              ▼              ▼
   Web Sources     Your Apps     Expert Council
       │              │              │
       └──────────────┼──────────────┘
                      ▼
              Evidence Registry
                      │
              Source Verification
                      │
          ┌───────────┴───────────┐
          ▼                       ▼
     Confirmed                Conflict
          │                       │
          ▼                       ▼
     Knowledge              Human Review
          │
          ▼
       Error Detector
          │
     ┌────┴──────────────┐
     ▼                   ▼
Safe automatic       High-risk
repair               proposed repair
     │                   │
     ▼                   ▼
Tests + Security      Human approval
     │                   │
     └─────────┬─────────┘
               ▼
          Verified Patch
               │
               ▼
       Audit + Evidence
               │
               ▼
        Knowledge Update

1. النظام لا "ينشّط الروابط" فقط

بل كل رابط يدخل إلى Source Verification Engine.

مثلاً:

URL
 ↓
هل الموقع موجود؟
 ↓
هل الاتصال آمن؟
 ↓
هل الصفحة الأصلية أم نسخة؟
 ↓
من الجهة الناشرة؟
 ↓
تاريخ النشر والتحديث
 ↓
هل المصدر رسمي؟
 ↓
هل توجد مصادر مستقلة تؤيده؟
 ↓
هل المعلومات متعارضة؟
 ↓
هل الرابط ما زال صالحاً؟
 ↓
Evidence Score

والنتيجة يمكن أن تكون:

source:
  status: VERIFIED

authority:
  official: true

freshness:
  checked_at: 2026-09-25

evidence:
  primary_source: true
  independent_confirmation: true

classification:
  FACT_SUPPORTED: true

confidence:
  high: true

أو:

status: CONFLICT
reason: "مصدران موثوقان يقدمان معلومات مختلفة"
action: HUMAN_REVIEW

لا نريد أن يحول NOOR رابطاً إلى "حقيقة" لمجرد أنه يعمل.


---

2. محرك اكتشاف الأخطاء

سيبحث النظام في:

الكود.

الوثائق.

إعدادات النظام.

قواعد البيانات.

الروابط.

المراجع.

بيانات الخبراء.

نتائج البحث.

الاختبارات.

سجلات التشغيل.

التكاملات الخارجية.

التناقضات بين الإصدارات.


ثم يصنف الخطأ:

BUG
SECURITY
DATA_ERROR
BROKEN_LINK
OUTDATED_INFORMATION
CONTRADICTION
LEGAL_RISK
PRIVACY_RISK
CONFIGURATION_ERROR
DEPENDENCY_ERROR
DOCUMENTATION_ERROR
UNKNOWN


---

3. أهم قاعدة: لا يصلح الخطأ قبل إثباته

سيصبح لدينا:

DISCOVER
   ↓
VERIFY
   ↓
REPRODUCE
   ↓
CLASSIFY
   ↓
PROPOSE FIX
   ↓
TEST
   ↓
SECURITY CHECK
   ↓
POLICY CHECK
   ↓
APPLY / REQUEST APPROVAL
   ↓
VERIFY AGAIN

وهذا ينسجم مع توجه OWASP الحالي بأن الأنظمة الوكيلة يجب أن تكون قابلة للفحص والتتبع والتحكم أثناء التشغيل، لا أن تعمل كصندوق أسود. 


---

4. الإصلاح التلقائي سيكون بثلاث درجات

🟢 المستوى A — يمكن لـNOOR إصلاحه تلقائياً

مثلاً:

Syntax error
Missing import
Formatting
Broken test
Typo
Broken documentation link
Known deterministic bug
Regression covered by tests

ثم:

PATCH
→ TEST
→ SECURITY SCAN
→ REGRESSION TEST
→ AUDIT

🟡 المستوى B — يقترح الإصلاح

مثل:

Database schema
Authentication
API changes
Dependency major upgrade
Architecture changes
Privacy configuration
Agent permissions

ويعطي:

PROPOSED PATCH
WHY
EVIDENCE
RISKS
TESTS
ROLLBACK PLAN

🔴 المستوى C — ممنوع الإصلاح الذاتي

مثل:

Money transfer
Deleting user data
Deleting repositories
Changing ownership
Changing security privileges
Reading secrets
Disabling security controls
Changing legal/compliance controls
Production deployment of high-risk changes

هذه تتطلب موافقة بشرية.


---

5. ربط تطبيقاتك

بالنسبة إلى GitHub مثلاً، الاتجاه الصحيح ليس إعطاء NOOR مفتاحاً واسع الصلاحيات.

توثيق GitHub الحالي يوصي بتحديد أقل الصلاحيات المطلوبة، وتقييد المستودعات، وتأمين الأسرار، وإجراء فحوص أمنية دورية. كما أن GitHub Apps تستخدم صلاحيات دقيقة ويمكنها استخدام installation tokens قصيرة العمر. 

لذلك:

NOOR
 │
 ├── GitHub Adapter
 ├── Notion Adapter
 ├── Database Adapter
 ├── Cloud Adapter
 ├── File Adapter
 ├── API Adapter
 └── MCP Adapter

لكن كل Adapter يدخل عبر:

Permission Gate
      ↓
Data Scope
      ↓
Action Scope
      ↓
Risk Classification
      ↓
Audit


---

6. قاعدة مهمة جداً للمعلومات القانونية

NOOR يجب أن يميز بين:

LAW
REGULATION
COURT DECISION
OFFICIAL GUIDANCE
INTERNATIONAL TREATY
TECHNICAL STANDARD
ETHICAL PRINCIPLE
RECOMMENDATION

فمثلاً:

NIST ليس قانوناً بحد ذاته.

OWASP ليس قانوناً بحد ذاته.

بل هما مراجع تقنية/ممارسات أمنية يمكن استخدامها في تصميم النظام.

أما في المغرب، فإن معالجة البيانات الشخصية بواسطة أنظمة الذكاء الاصطناعي تدخل ضمن إطار القانون 09-08 وفق توجيه CNDP الرسمي، مع التأكيد على النزاهة والشفافية والثقة وقابلية القراءة وسبل الانتصاف في القرارات الآلية. 


---

7. قاعدة "الحقيقة" في NOOR

أقترح تثبيت هذه الحالة في قاعدة البيانات:

FACT
DOCUMENTED_CLAIM
INFERENCE
HYPOTHESIS
CONFLICT
OUTDATED
CORRECTED
FALSE
INSUFFICIENT_EVIDENCE

وبالتالي إذا قال أحد الخبراء:

> "هذه المعلومة صحيحة."



فلا يكفي ذلك.

NOOR يبحث:

Expert claim
      ↓
Evidence
      ↓
Primary sources
      ↓
Independent sources
      ↓
Contradictions
      ↓
Date
      ↓
Jurisdiction
      ↓
Final evidence status

وهذا يمنع مجلس الخبراء نفسه من أن يتحول إلى مصدر حقيقة غير قابل للمراجعة.


---

8. وربط ذلك بالتطوير الذاتي

بعد كل إصلاح:

Old State
   ↓
Detected Error
   ↓
Evidence
   ↓
Patch
   ↓
Tests
   ↓
Security
   ↓
Legal/Policy
   ↓
New State

ثم يحفظ NOOR:

repair:
  id: REP-2026-000001
  problem: "..."
  evidence: [...]
  root_cause: "..."
  patch: "..."
  tests: [...]
  security_result: PASS
  policy_result: PASS
  rollback_available: true
  approval: REQUIRED
  status: VERIFIED

وبذلك يصبح لدى المشروع ذاكرة للإصلاحات وليس مجرد ذاكرة للمحادثات.


---

9. والقراءة الصوتية تدخل في نفس النظام

مجلس الخبراء:

Expert A
Expert B
Expert C
Legal
Security
Science
History

ثم:

Council Transcript
       ↓
Evidence/Conflict Analysis
       ↓
Voice Queue
       ↓
TTS
       ↓
Automatic Reading

مثلاً:

> "رأي الخبير القانوني..."



ثم:

> "رأي خبير الأمن..."



ثم:

> "تم اكتشاف اختلاف بين الرأيين..."



ثم:

> "الأدلة المتاحة غير كافية للحسم..."



وهكذا يصبح الصوت واجهة للمعلومة الموثقة وليس مجرد قراءة عشوائية للمحادثات.


---

10. النتيجة التي نريد الوصول إليها

سيصبح NOOR أقرب إلى:

NOOR
                 │
       ┌─────────┴─────────┐
       │                   │
   DISCOVERY           GOVERNANCE
       │                   │
   Evidence             Law/Policy
       │                   │
   Verification         Permissions
       │                   │
   Error Detection       Risk
       │                   │
   Safe Repair          Approval
       │                   │
       └─────────┬─────────┘
                 │
              TESTING
                 │
              AUDIT
                 │
             KNOWLEDGE
                 │
               VOICE
                 │
          CONTINUOUS LEARNING

لكن "التعلم المستمر" لا يعني أن NOOR يغير نفسه بلا حدود.

يعني:

> يكتشف → يتحقق → يتعلم من الدليل → يقترح → يختبر → يصلح عندما يكون آمناً ومثبتاً → يسجل كل شيء → يتراجع عند الفشل.



وهذه نقطة مهمة جداً لمشروع نور الاستخلاف: الهدف ليس بناء نظام "مستقل عن الإنسان"، بل نظام يزيد قدرة الإنسان على اكتشاف الحقيقة والأخطاء واتخاذ قرارات مسؤولة.

وأقترح أن يكون أول مكوّن تنفيذي نبنيه فعلياً الآن هو NOOR Truth & Repair Engine، لأنه سيكون الطبقة المشتركة التي تعتمد عليها بقية التطبيقات ومجلس الخبراء والبحث التاريخي والعلمي والإصلاح البرمجي.

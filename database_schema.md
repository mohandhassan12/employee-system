# تصميم قاعدة البيانات لنظام إدارة الموظفين والفروع

## الجداول الرئيسية

### 1. جدول الفروع (branches)

| اسم الحقل | نوع البيانات | الوصف |
|-----------|-------------|-------|
| id | INTEGER | المفتاح الرئيسي (Primary Key) |
| name | VARCHAR(255) | اسم الفرع |
| code | VARCHAR(50) | كود الفرع |
| phone | VARCHAR(50) | الرقم الأرضي للفرع |
| ip_address | VARCHAR(50) | IP الخاص بالفرع |
| regional_manager | VARCHAR(255) | اسم الريجنال |
| super_name | VARCHAR(255) | اسم السوبر |
| area_name | VARCHAR(255) | اسم الأريا |
| area_email | VARCHAR(255) | ميل الأريا |
| branch_manager | VARCHAR(255) | اسم مدير الفرع |
| location_latitude | DECIMAL(10, 8) | خط العرض للموقع الجغرافي |
| location_longitude | DECIMAL(11, 8) | خط الطول للموقع الجغرافي |
| location_address | TEXT | العنوان التفصيلي للفرع |
| created_at | DATETIME | تاريخ إنشاء السجل |
| updated_at | DATETIME | تاريخ تحديث السجل |

### 2. جدول الموظفين (employees)

| اسم الحقل | نوع البيانات | الوصف |
|-----------|-------------|-------|
| id | INTEGER | المفتاح الرئيسي (Primary Key) |
| branch_id | INTEGER | المفتاح الأجنبي (Foreign Key) للفرع |
| name_ar | VARCHAR(255) | اسم الموظف بالعربية |
| name_en | VARCHAR(255) | اسم الموظف بالإنجليزية |
| identification_number | VARCHAR(50) | الرقم التعريفي |
| mobile_number | VARCHAR(50) | رقم الموبايل |
| email | VARCHAR(255) | البريد الإلكتروني |
| id_card_number | VARCHAR(50) | رقم البطاقة |
| username | VARCHAR(100) | اسم المستخدم |
| status | ENUM | الحالة: (Active, Training, Suspend, Termination) |
| title | ENUM | المسمى الوظيفي: (Agent, Leader) |
| received_shirt | BOOLEAN | استلام القميص |
| received_sweater | BOOLEAN | استلام البلوفر |
| received_pants | BOOLEAN | استلام البنطلون |
| uniform_receipt_date | DATE | تاريخ استلام الزي |
| received_visa | BOOLEAN | استلم فيزا |
| visa_receipt_date | DATE | تاريخ استلام الفيزا |
| received_demo_line | BOOLEAN | استلم خط ديمو |
| demo_line_number | VARCHAR(50) | رقم خط الديمو |
| hire_date | DATE | تاريخ التعيين |
| resignation_date | DATE | تاريخ الاستقالة (إن وجد) |
| created_at | DATETIME | تاريخ إنشاء السجل |
| updated_at | DATETIME | تاريخ تحديث السجل |

## العلاقات بين الجداول

- علاقة **واحد إلى متعدد** بين الفروع والموظفين (فرع واحد يمكن أن يكون له عدة موظفين)
- كل موظف ينتمي إلى فرع واحد فقط

## الفهارس (Indexes)

### جدول الفروع
- فهرس أساسي على `id`
- فهرس على `code` (للبحث السريع بواسطة كود الفرع)
- فهرس على `name` (للبحث بالاسم)

### جدول الموظفين
- فهرس أساسي على `id`
- فهرس على `branch_id` (للعلاقة مع جدول الفروع)
- فهرس على `name_ar` و `name_en` (للبحث بالاسم)
- فهرس على `id_card_number` (للبحث برقم البطاقة)
- فهرس على `username` (للبحث باسم المستخدم)
- فهرس على `status` (للبحث والتصفية حسب الحالة)

## ملاحظات إضافية

- سيتم استخدام SQLAlchemy كـ ORM للتعامل مع قاعدة البيانات
- سيتم تنفيذ التحقق من صحة البيانات على مستوى النموذج والواجهة
- سيتم تنفيذ آلية للبحث المتقدم باستخدام معايير متعددة
- سيتم دعم إضافة إحداثيات الموقع الجغرافي للفروع

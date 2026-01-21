# VIII. Nested Resources (Resource Bersarang) 📂

> **Sumber:** [https://filamentphp.com/docs/5.x/resources/nesting](https://filamentphp.com/docs/5.x/resources/nesting)

---

## 🤔 Apa itu Nested Resource?

**Nested Resource** adalah resource yang "hidup" di dalam resource lain, dengan URL yang menunjukkan hierarki.

### Contoh Kasus:

```
/admin/courses/1/lessons        ← List lessons untuk course 1
/admin/courses/1/lessons/create ← Buat lesson baru untuk course 1
/admin/courses/1/lessons/5/edit ← Edit lesson 5 dari course 1
```

### Kapan Pakai Nested Resource?

| Gunakan Relation Manager | Gunakan Nested Resource |
| ------------------------ | ----------------------- |
| Data relasi sederhana    | Data relasi kompleks    |
| Edit cukup di modal      | Butuh halaman penuh     |
| Sedikit field            | Banyak field/section    |

---

## 🚀 Membuat Nested Resource

### Langkah 1: Buat Resource dengan Flag --nested

```bash
php artisan make:filament-resource Lesson --nested
```

### Langkah 2: Buat Relation Manager atau Relation Page

```bash
php artisan make:filament-relation-manager CourseResource lessons title
```

### Langkah 3: Hubungkan ke Nested Resource

Saat ditanya, pilih "Yes" untuk link ke nested resource.

Hasilnya:

```php
// Di Relation Manager
protected static ?string $relatedResource = LessonResource::class;
```

```php
// Di Nested Resource
protected static ?string $parentResource = CourseResource::class;
```

---

## 🔗 Hasil URL

| Aksi          | URL                                             |
| ------------- | ----------------------------------------------- |
| List lessons  | `/admin/courses/{course}/lessons`               |
| Create lesson | `/admin/courses/{course}/lessons/create`        |
| Edit lesson   | `/admin/courses/{course}/lessons/{lesson}/edit` |

---

## 💡 Analoginya

Bayangkan seperti folder di komputer:

```
📁 Course A
   └── 📄 Lesson 1
   └── 📄 Lesson 2
📁 Course B
   └── 📄 Lesson 3
```

Nested resource memastikan Lesson selalu "di dalam" Course-nya.

---

## 🎯 Latihan Mandiri

Buat nested resource untuk:

- Parent: `CourseResource`
- Child: `ChapterResource` (satu Course punya banyak Chapter)

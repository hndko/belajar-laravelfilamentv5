# IX. Singular Resources (Resource Tunggal) 🎯

> **Sumber:** [https://filamentphp.com/docs/5.x/resources/singular](https://filamentphp.com/docs/5.x/resources/singular)

---

## 🤔 Apa itu Singular Resource?

**Singular Resource** adalah halaman untuk mengelola **satu record saja**, tanpa daftar (list).

### Contoh Kasus:

- **Halaman Settings** → Hanya ada 1 pengaturan
- **Homepage Editor** → Hanya ada 1 homepage
- **User Profile** → Profil user yang sedang login

---

## 🆚 Resource Biasa vs Singular

| Resource Biasa       | Singular Resource    |
| -------------------- | -------------------- |
| Punya halaman List   | Tidak ada List       |
| Banyak record        | Hanya 1 record       |
| CRUD lengkap         | Hanya Edit           |
| URL: /admin/settings | URL: /admin/settings |

---

## 🚀 Cara Membuat Singular Resource

Gunakan **Custom Page** dengan form:

### Langkah 1: Buat Page

```bash
php artisan make:filament-page ManageHomepage
```

### Langkah 2: Setup Page Class

```php
namespace App\Filament\Pages;

use App\Models\WebsitePage;
use Filament\Actions\Action;
use Filament\Forms\Components\RichEditor;
use Filament\Forms\Components\TextInput;
use Filament\Notifications\Notification;
use Filament\Pages\Page;
use Filament\Schemas\Schema;

class ManageHomepage extends Page
{
    protected string $view = 'filament.pages.manage-homepage';

    public ?array $data = [];

    public function mount(): void
    {
        // Isi form dengan data dari database (jika ada)
        $this->form->fill($this->getRecord()?->attributesToArray());
    }

    public function form(Schema $schema): Schema
    {
        return $schema
            ->components([
                Form::make([
                    TextInput::make('title')
                        ->required()
                        ->maxLength(255),
                    RichEditor::make('content'),
                ])
                ->livewireSubmitHandler('save')
                ->footer([
                    Actions::make([
                        Action::make('save')
                            ->submit('save'),
                    ]),
                ]),
            ])
            ->record($this->getRecord())
            ->statePath('data');
    }

    public function save(): void
    {
        $data = $this->form->getState();
        $record = $this->getRecord();

        if (! $record) {
            // Buat record baru jika belum ada
            $record = new WebsitePage();
            $record->is_homepage = true;
        }

        $record->fill($data);
        $record->save();

        Notification::make()
            ->success()
            ->title('Tersimpan!')
            ->send();
    }

    public function getRecord(): ?WebsitePage
    {
        return WebsitePage::where('is_homepage', true)->first();
    }
}
```

---

## 📌 Alternatif: Spatie Settings Plugin

Untuk halaman Settings, lebih disarankan pakai plugin:

**[Spatie Settings Plugin](https://filamentphp.com/plugins/filament-spatie-settings)**

Lebih mudah karena tidak perlu model database.

---

## 💡 Ringkasan

| Kebutuhan               | Solusi                        |
| ----------------------- | ----------------------------- |
| Settings aplikasi       | Spatie Settings Plugin        |
| Profile user            | Fitur Profile bawaan Filament |
| Halaman tunggal lainnya | Custom Page + Form            |

---

## 🎯 Latihan Mandiri

Buat halaman "Site Settings" yang menyimpan:

- `site_name` (string)
- `site_description` (text)
- `maintenance_mode` (boolean)

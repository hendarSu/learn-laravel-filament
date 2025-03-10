# Bagian 3: Laravel Framework

## Pengenalan Laravel

### Filosofi dan Keunggulan Laravel
Laravel adalah framework PHP yang elegan dan ekspresif, dengan fokus pada kesederhanaan dan kode yang bersih. Diperkenalkan pada tahun 2011 oleh Taylor Otwell, Laravel telah menjadi salah satu framework PHP paling populer. Laravel menawarkan sintaks yang ekspresif dan struktur yang jelas, memungkinkan developer untuk menulis kode yang mudah dibaca dan dipelihara.

### Ekosistem Laravel
Laravel memiliki ekosistem yang kaya dengan berbagai package dan tools yang mempercepat pengembangan aplikasi web:

- **Composer** untuk manajemen dependensi
- **Artisan** sebagai command-line interface
- **Laravel Mix** untuk kompilasi aset
- **Laravel Forge** dan **Envoyer** untuk deployment
- **Laravel Horizon** untuk monitoring queue
- **Laravel Telescope** untuk debugging
- **Laravel Nova** dan **Laravel Filament** untuk admin panel

## Instalasi dan Setup

### Kebutuhan Sistem
Sebelum menginstal Laravel, pastikan sistem Anda memenuhi persyaratan berikut:

- PHP >= 7.3 (disarankan PHP 8.0+)
- BCMath PHP Extension
- Ctype PHP Extension
- Fileinfo PHP Extension
- JSON PHP Extension
- Mbstring PHP Extension
- OpenSSL PHP Extension
- PDO PHP Extension
- Tokenizer PHP Extension
- XML PHP Extension

### Composer dan Artisan
Laravel menggunakan Composer untuk manajemen dependensi. Untuk menginstal Laravel, jalankan perintah berikut:

```bash
composer create-project laravel/laravel nama-project
```

Setelah instalasi, Anda dapat menggunakan Artisan, CLI Laravel, untuk berbagai tugas seperti membuat controller, model, migrasi, dan menjalankan server development:

```bash
# Menjalankan server development
php artisan serve

# Membuat model dengan migrasi dan controller
php artisan make:model Post -mc
```

#### Studi Kasus: Membuat Proyek Laravel Baru
Ikuti langkah-langkah ini untuk membuat proyek Laravel baru:

1. Buka terminal
2. Jalankan perintah `composer create-project laravel/laravel blog`
3. Masuk ke direktori proyek `cd blog`
4. Jalankan server development `php artisan serve`
5. Buka browser dan akses `http://localhost:8000`

## Arsitektur MVC

### Struktur Aplikasi Laravel
Laravel mengikuti pola arsitektur Model-View-Controller (MVC). Struktur direktori Laravel terorganisir dengan baik:

- **app/** - Kode utama aplikasi
  - **Http/** - Controllers, Middleware, Requests
  - **Models/** - Model Eloquent
  - **Providers/** - Service Providers
- **config/** - File konfigurasi
- **database/** - Migrasi dan seeders
- **public/** - Titik masuk aplikasi (index.php) dan aset statis
- **resources/** - Views, assets, dan translations
- **routes/** - Definisi route
- **storage/** - File yang diupload, logs, dan cache
- **tests/** - Test unit dan feature

### Flow Request-Response
Alur request-response dalam Laravel:

1. Request masuk melalui `public/index.php`
2. Request dirutekan melalui routes yang didefinisikan di `routes/web.php` atau `routes/api.php`
3. Route memanggil Controller yang sesuai
4. Controller berinteraksi dengan Model untuk mengambil atau memperbarui data
5. Controller merender View dengan data yang diperlukan
6. Response dikembalikan ke user

## Routing dan Controller

### Route Types dan Parameters
Laravel menyediakan cara yang sederhana dan ekspresif untuk mendefinisikan route:

```php
// Route dasar
Route::get('/', function () {
    return view('welcome');
});

// Route dengan parameter
Route::get('/posts/{id}', function ($id) {
    return 'Post ' . $id;
});

// Route dengan parameter opsional
Route::get('/users/{name?}', function ($name = null) {
    return $name ? 'User ' . $name : 'All users';
});

// Route dengan constraint parameter
Route::get('/posts/{id}', function ($id) {
    return 'Post ' . $id;
})->where('id', '[0-9]+');

// Route dengan nama
Route::get('/profile', function () {
    // ...
})->name('profile');
```

### Controller dan Resource Controllers
Controller mengatur logika aplikasi dan menangani request dari route:

```php
// Membuat controller
php artisan make:controller PostController

// Membuat resource controller
php artisan make:controller PostController --resource
```

Contoh controller sederhana:

```php
<?php

namespace App\Http\Controllers;

use App\Models\Post;
use Illuminate\Http\Request;

class PostController extends Controller
{
    public function index()
    {
        $posts = Post::all();
        return view('posts.index', compact('posts'));
    }

    public function show($id)
    {
        $post = Post::findOrFail($id);
        return view('posts.show', compact('post'));
    }
}
```

Mendefinisikan route untuk controller:

```php
// Single action
Route::get('/posts', [PostController::class, 'index']);
Route::get('/posts/{id}', [PostController::class, 'show']);

// Resource controller (mendefinisikan semua route CRUD)
Route::resource('posts', PostController::class);
```

#### Studi Kasus: Blog Sederhana dengan Route dan Controller
1. Buat model dan migrasi Post: `php artisan make:model Post -m`
2. Buat resource controller: `php artisan make:controller PostController --resource`
3. Definisikan route resource di `routes/web.php`: `Route::resource('posts', PostController::class);`
4. Implementasikan method `index`, `create`, `store`, `show`, `edit`, `update`, dan `destroy` di `PostController`

## Blade Templating

### Syntax dan Directives
Blade adalah templating engine yang disediakan oleh Laravel, dengan sintaks yang sederhana dan powerful:

```blade
{{-- Komentar Blade --}}

{{-- Menampilkan data --}}
{{ $variable }}

{{-- Menampilkan data tanpa escape --}}
{!! $html !!}

{{-- Conditional statements --}}
@if($condition)
    This is true
@elseif($anotherCondition)
    This is another condition
@else
    This is false
@endif

{{-- Loops --}}
@foreach($items as $item)
    {{ $item }}
@endforeach

@for($i = 0; $i < 10; $i++)
    The value is {{ $i }}
@endfor

{{-- Include sub-views --}}
@include('view.name', ['variable' => 'value'])

{{-- Extending layouts --}}
@extends('layouts.master')

@section('title', 'Page Title')

@section('content')
    <p>This is the content of the page</p>
@endsection
```

### Layout dan Components
Blade memungkinkan Anda membuat layout dan menggunakan komponen untuk mengorganisir kode:

```blade
{{-- layouts/app.blade.php --}}
<!DOCTYPE html>
<html>
<head>
    <title>@yield('title')</title>
</head>
<body>
    @include('partials.header')
    
    <div class="container">
        @yield('content')
    </div>
    
    @include('partials.footer')
</body>
</html>
```

```blade
{{-- Menggunakan layout --}}
@extends('layouts.app')

@section('title', 'Home Page')

@section('content')
    <h1>Welcome to our website!</h1>
    <p>This is the home page content.</p>
@endsection
```

Blade Components (Laravel 8+):

```blade
{{-- Membuat component dengan artisan --}}
{{-- php artisan make:component Alert --}}

{{-- Memanggil component --}}
<x-alert type="error" :message="$message"/>
```

## Eloquent ORM

### Model dan Relationship
Eloquent adalah ORM (Object-Relational Mapper) Laravel yang menyediakan implementasi ActiveRecord yang indah dan sederhana. Eloquent memungkinkan Anda untuk bekerja dengan database secara intuitif:

```php
// Membuat model dan migrasi
php artisan make:model Post -m
```

Contoh model Eloquent:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Post extends Model
{
    // Kolom yang dapat diisi massal
    protected $fillable = ['title', 'body', 'user_id'];
    
    // Relasi dengan User (Many-to-One)
    public function user()
    {
        return $this->belongsTo(User::class);
    }
    
    // Relasi dengan Comment (One-to-Many)
    public function comments()
    {
        return $this->hasMany(Comment::class);
    }
    
    // Relasi dengan Tag (Many-to-Many)
    public function tags()
    {
        return $this->belongsToMany(Tag::class);
    }
}
```

### Query Builder
Eloquent menyediakan API yang ekspresif untuk query database:

```php
// Mendapatkan semua post
$posts = Post::all();

// Mendapatkan post dengan ID tertentu
$post = Post::find(1);
// Atau throw exception jika tidak ditemukan
$post = Post::findOrFail(1);

// Query dasar
$posts = Post::where('active', true)->get();
$posts = Post::where('active', true)->first();
$count = Post::where('active', true)->count();

// Query kompleks
$posts = Post::where('active', true)
             ->where('user_id', $userId)
             ->orderBy('created_at', 'desc')
             ->take(10)
             ->get();

// Eager loading (N+1 problem solution)
$posts = Post::with('user', 'comments')->get();
```

## Form Processing dan Validasi

### Validasi Input
Laravel menyediakan berbagai cara untuk memvalidasi input dari user:

```php
// Validasi di controller
public function store(Request $request)
{
    $validated = $request->validate([
        'title' => 'required|max:255',
        'body' => 'required',
        'email' => 'required|email|unique:users,email',
        'age' => 'required|numeric|min:18',
    ]);
    
    // Proses data tervalidasi
    Post::create($validated);
    
    return redirect()->route('posts.index');
}
```

### Form Request
Untuk validasi yang lebih kompleks, Anda dapat membuat Form Request:

```php
// Membuat form request
php artisan make:request StorePostRequest
```

```php
<?php

namespace App\Http\Requests;

use Illuminate\Foundation\Http\FormRequest;

class StorePostRequest extends FormRequest
{
    public function authorize()
    {
        return true;
    }

    public function rules()
    {
        return [
            'title' => 'required|max:255',
            'body' => 'required',
            'category_id' => 'required|exists:categories,id',
        ];
    }
    
    public function messages()
    {
        return [
            'title.required' => 'The title field is required.',
            'body.required' => 'The body field is required.',
        ];
    }
}
```

Menggunakan form request di controller:

```php
public function store(StorePostRequest $request)
{
    // Input sudah tervalidasi
    $validated = $request->validated();
    
    Post::create($validated);
    
    return redirect()->route('posts.index');
}
```

#### Studi Kasus: Form Kontak dengan Validasi
1. Buat controller: `php artisan make:controller ContactController`
2. Buat form request: `php artisan make:request ContactRequest`
3. Definisikan aturan validasi di `ContactRequest`
4. Implementasikan logika pengiriman email di `ContactController`
5. Buat view form kontak dengan Blade

## Authentication dan Authorization

### User Authentication
Laravel menyediakan scaffolding authentication yang lengkap:

```bash
# Laravel 8+ with Jetstream
composer require laravel/jetstream
php artisan jetstream:install livewire

# Laravel 8+ with Laravel UI
composer require laravel/ui
php artisan ui bootstrap --auth
```

### Policies dan Gates
Laravel menyediakan cara untuk mengontrol akses ke resource melalui Authorization:

```php
// Membuat policy
php artisan make:policy PostPolicy --model=Post
```

```php
<?php

namespace App\Policies;

use App\Models\Post;
use App\Models\User;

class PostPolicy
{
    public function viewAny(User $user)
    {
        return true;
    }

    public function view(User $user, Post $post)
    {
        return true;
    }

    public function create(User $user)
    {
        return $user->role === 'author' || $user->role === 'admin';
    }

    public function update(User $user, Post $post)
    {
        return $user->id === $post->user_id || $user->role === 'admin';
    }

    public function delete(User $user, Post $post)
    {
        return $user->id === $post->user_id || $user->role === 'admin';
    }
}
```

Mendefinisikan gates di `AuthServiceProvider`:

```php
public function boot()
{
    $this->registerPolicies();

    Gate::define('update-post', function (User $user, Post $post) {
        return $user->id === $post->user_id;
    });
}
```

Menggunakan policies dan gates:

```php
// Dalam controller
public function update(Request $request, Post $post)
{
    // Menggunakan policy
    $this->authorize('update', $post);
    
    // Atau menggunakan gate
    if (Gate::denies('update-post', $post)) {
        abort(403);
    }
    
    // Lanjutkan dengan update
}
```

Di view:

```blade
@can('update', $post)
    <a href="{{ route('posts.edit', $post) }}">Edit</a>
@endcan

@cannot('delete', $post)
    <p>You cannot delete this post</p>
@endcannot
```

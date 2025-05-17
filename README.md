# learn-laravel-30-days

🛤️ 30-Day Laravel Learning Roadmap (Beginner Level)
Prerequisites: Basic PHP, Composer, MySQL, and basic HTML/CSS/JS
🔰 Week 1: Laravel Fundamentals
Day 1: Setup
✅ Install Composer, Laravel, PHP, MySQL
✅ Create new project
composer create-project laravel/laravel myApp

Day 2: Directory Structure
Understand: /routes, /app, /resources, /config

✅ Route Example:
// routes/web.php
Route::get('/', function () {
    return view('welcome');
});

Day 3: Routing & Views
✅ Add routes, return views
✅ Use Blade templating
// routes/web.php
Route::get('/hello', function () {
    return view('hello', ['name' => 'John']);
});

// resources/views/hello.blade.php
<h1>Hello, {{ $name }}</h1>

Day 4: Controllers
✅ Create Controller
php artisan make:controller PageController

✅ Controller Example:
// app/Http/Controllers/PageController.php
public function about() {
    return view('about');
}

// routes/web.php
Route::get('/about', [PageController::class, 'about']);

Day 5: Blade Basics
Blade control structures (@if, @foreach)
<ul>
@foreach($users as $user)
    <li>{{ $user->name }}</li>
@endforeach
</ul>


Day 6: Environment and Config
.env file: DB, app name, URL
APP_NAME=MyApp
DB_DATABASE=laravel

Day 7: Artisan & Tinker
✅ Artisan Commands:
php artisan list
php artisan tinker

🚀 Week 2: Database & Eloquent ORM
Day 8: Database Setup
Setup .env
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=

Day 9: Migrations
✅ Create migration
php artisan make:migration create_posts_table
// in migration file
$table->string('title');
$table->text('body');

Day 10: Running Migrations
php artisan migrate

Day 11: Eloquent Models
✅ Create model
php artisan make:model Post

Save data:
$post = new Post;
$post->title = 'My Post';
$post->body = 'Post content';
$post->save();

Day 12: Database Seeder
php artisan make:seeder PostSeeder

Day 13: Factories
php artisan make:factory PostFactory --model=Post

Day 14: CRUD via Tinker
$post = Post::create(['title' => 'Title', 'body' => 'Body']);
Post::all();
$post->delete();


🧰 Week 3: CRUD & Forms
Day 15: CRUD Routes & Controller
Route::resource('posts', PostController::class);

Day 16: Create Form View
<form method="POST" action="{{ route('posts.store') }}">
    @csrf
    <input type="text" name="title">
    <textarea name="body"></textarea>
    <button type="submit">Save</button>
</form>

Day 17: Store Logic
public function store(Request $request) {
    Post::create($request->all());
    return redirect()->route('posts.index');
}

Day 18: Validation
$request->validate([
    'title' => 'required',
    'body' => 'required',
]);

Day 19: Show, Edit, Update
public function update(Request $request, Post $post) {
    $post->update($request->all());
}

Day 20: Delete
<form action="{{ route('posts.destroy', $post) }}" method="POST">
    @csrf
    @method('DELETE')
    <button>Delete</button>
</form>

Day 21: Flash Messages
@if(session('success'))
    <p>{{ session('success') }}</p>
@endif

🔐 Week 4: Auth, Middleware, APIs
Day 22: Laravel Breeze (or Jetstream)
composer require laravel/breeze --dev
php artisan breeze:install
npm install && npm run dev
php artisan migrate

Day 23: Middleware
Route::get('/dashboard', fn() => view('dashboard'))->middleware('auth');

Day 24: Auth Checks in Blade
@auth
    Welcome, {{ Auth::user()->name }}
@endauth

Day 25: Eloquent Relationships
// Post.php
public function user() {
    return $this->belongsTo(User::class);
}

Day 26: API Routes & Resources
// routes/api.php
Route::get('/posts', [PostApiController::class, 'index']);

Day 27: API Resource Class
php artisan make:resource PostResource
// PostResource.php
public function toArray($request) {
    return [
        'title' => $this->title,
        'body' => $this->body,
    ];
}

Day 28: API Authentication (Sanctum)
composer require laravel/sanctum
php artisan vendor:publish --provider="Laravel\Sanctum\SanctumServiceProvider"
php artisan migrate


Day 29: Basic Testing
php artisan make:test PostTest

public function test_post_creation() {
    $response = $this->post('/posts', [
        'title' => 'Test',
        'body' => 'Test body'
    ]);
    $response->assertRedirect('/posts');
}




Day 30: Deployment & Summary
✅ Deploy to Laravel Forge or shared hosting

✅ Review:

Routes

Models

Controllers

Views

Migrations

Auth

API






# OnlineCoursess — Digital Courses Platform (.NET 9)

A simple learning platform built with ASP.NET Core MVC (Razor views) on .NET 9 and Entity Framework Core. It showcases a catalog of courses, enrollment and (mock) checkout, course content/lessons, reviews/ratings, and a basic student workflow.

## Features
- Landing page with hero, highlights, testimonials, and newsletter
- Course catalog with categories, pricing, ratings, and details pages
- Student registration/login and “My Courses” page
- Enroll and mock checkout flow (records payment + enrollment)
- Course details page with lessons and lesson contents (videos, pdf/text links)
- Reviews and average rating per course
- SQL Server LocalDB + EF Core with seed data and migrations
- Clean UI using Bootstrap (RTL friendly) and Font Awesome

## Tech stack
- .NET 9, ASP.NET Core MVC (Razor views)
- Entity Framework Core + SQL Server LocalDB
- Bootstrap 5 (RTL) + Font Awesome

## Solution structure (high‑level)
```
OnlineCoursess/
├─ Controllers/
│  ├─ CourseController.cs
│  ├─ PaymentController.cs
│  └─ StudentController.cs
├─ Context/
│  └─ MyContext.cs                # EF Core DbContext + seed data
├─ Models/                        # Course, Category, Instructor, Student, Lesson, Review, Payment, Enroll ...
├─ Views/
│  ├─ Home/Index.cshtml           # Landing page
│  ├─ Course/Index.cshtml         # Catalog
│  ├─ Course/Details.cshtml       # Course details
│  ├─ Student/ViewCourse.cshtml   # Course viewer (for enrolled students)
│  ├─ Student/Login.cshtml, Register.cshtml
│  └─ Shared/…                    # Layouts and partials
├─ wwwroot/                       # Static assets (css, js, images)
└─ OnlineCoursess.csproj
```

## Getting started
### Prerequisites
- .NET 9 SDK
- SQL Server LocalDB (installed with Visual Studio Community/Build Tools)

### 1) Clone & restore
```bash
git clone https://github.com/kerollous-fathy/OnlineCoursess.git
cd OnlineCoursess/OnlineCoursess
dotnet restore
```

### 2) Configure database
The default connection string is defined in `Context/MyContext.cs` (`OnConfiguring`) and points to LocalDB. You can adjust it to your environment if needed.

Create the database using EF Core migrations:
```bash
# from OnlineCoursess/OnlineCoursess
dotnet tool restore  # if you use local tools
# or ensure dotnet-ef is installed: dotnet tool install -g dotnet-ef

dotnet ef database update
```
Alternatively, use Visual Studio’s Package Manager Console: `Update-Database`.

### 3) Run the app
```bash
dotnet run
```
Open the printed URL (typically https://localhost:xxxx). The landing page is `/` and the catalog is `/Course`.

## Seeded accounts (for quick testing)
> Note: For demo simplicity, passwords are stored as plain text placeholders in the seed data and compared directly.

- Student 1: `sara.ali@example.com` / `hashed_pass_std`
- Student 2: `ahmed.m@example.com` / `hashed_ahmed`

Instructors are also seeded (Hassan, Nora, Karim) to own the seeded courses.

## Useful URLs
- `/` — Landing page
- `/Course` — All courses (catalog)
- `/Course/Details/{id}` — Course details
- `/Student/Register` — Student registration
- `/Student/Login` — Student login
- `/Student/MyCourses` — Enrolled courses (uses the same card view as catalog with matching course icons)
- `/Payment/Checkout?courseId={id}` — Mock checkout (requires login)

## Static assets
Course and UI images live under `wwwroot/images`:
- `wwwroot/images/courses_icons` — icons for catalog/enrolled cards (`figma.jpg`, `illustrator.png`, `NET core.png`, `markteing.png`)
- `wwwroot/images/land_page`, `wwwroot/images/slider`, `wwwroot/images/humans` — landing page assets

## Roadmap / TODO
- Replace mock payments with a real provider
- Proper password hashing + Identity or custom auth with hashing/salting
- Instructor dashboards for course authoring (CRUD + uploads)
- Search, filters, and pagination for the catalog
- Unit/integration tests

## Contributing
Pull requests are welcome. Please open an issue first to discuss major changes.

## License
MIT (or update this section if you intend to use a different license).

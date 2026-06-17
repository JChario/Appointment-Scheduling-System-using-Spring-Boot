# CLAUDE.md

## Project purpose
A web-based appointment scheduling system. Users can register, log in, and book appointments; admins can log in to a dashboard showing appointment counts (total/booked/pending), and anyone can search an appointment by its ID.

## Tech stack
- Java 17, Spring Boot 3.2.6
- Spring Web (MVC, `@Controller`) + Thymeleaf server-side templates
- Spring Data MongoDB (database `appdb` on `localhost:27017`)
- Lombok
- Gradle build (with wrapper); JUnit 5 for tests

## Build / run / test
Use the Gradle wrapper from the repo root (`gradlew.bat` on Windows, `./gradlew` elsewhere).
- Build: `gradlew.bat build`
- Run: `gradlew.bat bootRun` (requires a MongoDB instance reachable at `localhost:27017`)
- Test: `gradlew.bat test`

App entry point: `src/main/java/com/app/AppointmentSchedulingSystemApplication.java`. Config: `src/main/resources/application.properties`.

## Key directories
- `src/main/java/com/app/` — all Java sources (controller, service, MongoDB documents, repositories)
  - `AppointmentController.java` — routes: `/`, `/appointment`, `/dashboard`, `/user/create`, `/user/login`, `/admin/login`, `/search`
  - `AppointmentService.java` — business logic
  - `Appointment.java`, `User.java`, `Admin.java` — MongoDB document models
  - `AppointmentRepo.java`, `UserRepo.java`, `AdminRepo.java` — Spring Data Mongo repositories
- `src/main/resources/templates/` — Thymeleaf HTML views (home, appointment, dashboard, register, userlogin, adminlogin, search)

## Notable conventions
- Flat single package `com.app` (no sub-packages for controller/service/model/repo).
- Note: in the current code both `postUserLogin` and `postAdminLogin` hard-code `loginstatus = true`, so login always succeeds regardless of credentials. Treat with caution if working on auth.

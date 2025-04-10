# mbkAuth

`mbkAuth` is a reusable authentication system for Node.js applications, designed to simplify session management, user authentication, and role-based access control. It integrates seamlessly with PostgreSQL and supports features like Two-Factor Authentication (2FA), session restoration, and reCAPTCHA verification.

## Features

- **Session Management**: Secure session handling using `express-session` and `connect-pg-simple`.
- **Role-Based Access Control**: Validate user roles and permissions with ease.
- **Two-Factor Authentication (2FA)**: Optional 2FA support for enhanced security.
- **reCAPTCHA Integration**: Protect login endpoints with Google reCAPTCHA.
- **Cookie Management**: Configurable cookie expiration and domain settings.
- **PostgreSQL Integration**: Uses a connection pool for efficient database interactions.

## Installation

Install the package via npm:

```bash
npm install @MBKTechStudio/mbkauth
```
or
```bash
npm install mbkauth
```

## Usage
Basic Setup
1. Import and configure the router in your Express application:
```javascript
import express from "express";
import mbkAuthRouter from "@MBKTechStudio/mbkauth";

const app = express();
app.use(mbkAuthRouter);

app.listen(3000, () => {
  console.log("Server is running on port 3000");
});
```
2. Ensure your ``.env` file is properly configured. Refer to the [Configuration Guide(env.md)](env.md) for details.

Example `.env` file:
```code
RECAPTCHA_SECRET_KEY=your-recaptcha-secret-key
SESSION_SECRET_KEY=your-session-secret-key
LOGIN_DB=postgres://username:password@host:port/database
DOMAIN=yourdomain.com
IS_DEPLOYED=true
MBKAUTH_TWO_FA_ENABLE=false
```

## API Endpoints
Login

**POST** `/api/mbkauth/login`
- Request Body:
  - `username`: User's username.
  - `password`: User's password.
  - `token`: (Optional) 2FA token.
  - `recaptcha`: reCAPTCHA response.

- Response:
  - `200`: Login successful.
  - `400`: Missing or invalid input.
  - `401`: Unauthorized (e.g., invalid credentials or 2FA token).
  - `500`: Internal server error.


**POST** `/api/mbkauth/logout`
- Response:
  - `200`: Login successful.
  - `400`: User not logged in.
  - `500`: Internal server error.



**POST** `/api/mbkauth/terminateAllSessions`
- Authentication: Requires a valid `Main_SECRET_TOKEN` in the `Authorization` header.
- Response:
  - `200`: All sessions terminated successfully.
  - `500`: Internal server error.
  - 
  
## License
This project is licensed under the `Mozilla Public License 2.0`. See the [LICENSE](./LICENSE) file for details.



## Contact & Support

For questions or contributions, please contact Muhammad Bin Khalid at [mbktechstudio.com/Support](https://mbktechstudio.com/Support/), [support@mbktechstudio.com](mailto:support@mbktechstudio.com) or [chmuhammadbinkhalid28.com](mailto:chmuhammadbinkhalid28.com). 

**Developed by [Muhammad Bin Khalid](https://github.com/MIbnEKhalid)**
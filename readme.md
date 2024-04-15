## Set of packages for Authentication with Session and Sql Db

<p>
  <a href="https://github.com/JuliusAgency/auth-ses-sql-set#readme" target="_blank">
    <img alt="Documentation" src="https://img.shields.io/badge/documentation-yes-brightgreen.svg" />
  </a>
  <a href="https://github.com/JuliusAgency/auth-ses-sql-set/graphs/commit-activity" target="_blank">
    <img alt="Maintenance" src="https://img.shields.io/badge/Maintained%3F-yes-green.svg" />
  </a>
  <a href="https://github.com/JuliusAgency/auth-ses-sql-set/blob/master/LICENSE" target="_blank">
    <img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-yellow.svg" />
  </a>
</p>

The auth-ses-sql-set package - is a component of the [@juliusagency/node-packages set](https://github.com/JuliusAgency/node-packages-set) for Nodejs applications.  
It is the wrapper for (look at these packages doc for more info):
   - [@juliusagency/auth-session](https://github.com/orgs/JuliusAgency/packages/npm/package/auth-session);  
   - [@juliusagency/auth-strategies](https://github.com/orgs/JuliusAgency/packages/npm/package/auth-strategies);  
   - [@juliusagency/base-user-mngr](https://github.com/orgs/JuliusAgency/packages/npm/package/base-user-mngr);  
   - [@juliusagency/base-user-sql](https://github.com/orgs/JuliusAgency/packages/npm/package/base-user-sql);  

### Installation
```bash
  npm install --save @juliusagency/auth-ses-sql-set
```

### References:
 - Session configuration - [express-session](https://www.npmjs.com/package/express-session);  
 - Sql Db creation - [typeorm](https://www.npmjs.com/package/typeorm);  
 - Emailer - [@juliusagency/simple-email-client](https://github.com/JuliusAgency/simple-email-client/pkgs/npm/simple-email-client);  

### Setup and Usage  
```
import {
  AuthConfig,
  AuthSesSetSetupOptions,
  authSetSetup,
  BaseUser,
  SessionConfig,
} from '@juliusagency/auth-ses-sql-set';


// SETUP:

// Config session - look at the "express-session"
const session: SessionConfig =  {
  name: SESSION_NAME,
  secret: SESSION_SECRET,
  saveUninitialized: SESSION_SAVE_UNINITIALIZED,
  cookie: {
    secure: COOKIE_SECURE,
    sameSite: COOKIE_SAME_SITE,
    httpOnly: COOKIE_HTTP_ONLY,
    maxAge: COOKIE_MAX_AGE,
  },
  resave: SESSION_RESAVE,
};

// Setup Auth with session and Sql Db
const authConfig: AuthConfig = {
  app: app, // Express app
  User: BaseUser, // or extended User
  sessionConfig: session,
};

const authSetupOptions: AuthSesSetSetupOptions = {
  authConfig: authConfig,
  emailer: emailer, // look at the "simple-email-client"
  repository: sqlRepository, // look at the "typeorm" dataSource.getRepository(...)
};

const { authMiddleware, authRouter } = authSetSetup(authSetupOptions);


// USAGE:
// Define protected routes
const protectedRoutes = ['/first', '/second'];
app.use(protectedRoutes, authMiddleware);

// Routers Setup
const router = Router();
// Auth router usage
router.use('/auth', authRouter);
```

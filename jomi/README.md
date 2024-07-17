# JOMI

JOMI (Journal of Medical Insights) offers on-demand virtual shadowing experiences by showcasing expert surgeons' practices. Its primary benefits include enhancing surgical education, improving patient outcomes, and providing critical preparation for rare and trauma cases. JOMI serves a diverse audience, including medical students, residents, and attending physicians, by keeping them updated with the latest surgical techniques and practices.

## Highlights

- **Node.js Streaming with Cursor Pagination:** Implemented a Node.js streaming approach with cursor pagination in MongoDB for downloading tables with millions of records as CSVs quickly. This reduced the download time from minutes to just a few seconds.
  
- **Manual Cron Jobs with Cursor Pagination:** Developed a solution to update millions of records by running cron jobs manually without causing database lock issues. This was achieved by using cursor-based pagination to update specific fields in batches, allowing the server to perform other database operations concurrently.
  
- **Complex Aggregation Pipelines:** Wrote complex aggregation pipelines using Typegoose for MongoDB in the backend, optimizing data retrieval and processing.

## Technology Details for JOMI

### Frontend

- **Next.js:** A React framework that enables server-side rendering and static site generation for enhanced performance and SEO. Used for building the main website and CMS.

- **TypeScript:** A strongly typed programming language that builds on JavaScript, providing better tooling at any scale. Utilized in both frontend and backend development for improved code quality and maintainability.

- **GraphQL Apollo Client:** A comprehensive state management library for JavaScript that enables easier querying and managing of GraphQL data. Employed for API integrations on the frontend.

- **MUI (Material-UI):** A popular React UI framework that provides a set of components for building responsive and visually appealing user interfaces. Used for constructing the UI of the website.

- **Vercel:** A cloud platform for static sites and serverless functions that provides easy and efficient deployment. Used for deploying the frontend application.

- **Wistia Player:** A video hosting platform with excellent analytics and management features. Integrated for video playback on the website.

### Backend

- **ExpressJS:** A minimal and flexible Node.js web application framework that provides a robust set of features for building web and mobile applications. Used for the backend development.

- **GraphQL Apollo Server:** A comprehensive platform for building a production-ready, self-documenting GraphQL API. Implemented for the backend API.

- **MongoDB:** A NoSQL database that uses a flexible, JSON-like document schema. Used for storing and managing data in the backend.

## Live Project

Explore the live version of JOMI at [jomi.com](https://jomi.com/).

## Screenshots

![JOMI article details page](https://github.com/user-attachments/assets/3bb68ef4-4679-4734-81f8-b21f0b93f06d)
_Article details page - navigate through the video by selecting sections from the left side_




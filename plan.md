```markdown
# Detailed Implementation Plan for Video Editor Portfolio Page

This plan outlines the creation of a new portfolio page that features an introduction with a photo, a section displaying six company experiences (each with a company logo and description), and a video showcase section.

---

## 1. Create a New Portfolio Route

**File:** `src/app/portfolio/page.tsx`  
- **Purpose:** Acts as the main page assembling the portfolio sections.
- **Changes:**
  - Import and embed the three main components: PortfolioHeader, ExperienceList, and VideoShowcase.
  - Wrap content in a `<main>` element with a responsive container class.
- **Example Code:**
  ```typescript
  import React from "react";
  import PortfolioHeader from "@/components/portfolio/PortfolioHeader";
  import ExperienceList from "@/components/portfolio/ExperienceList";
  import VideoShowcase from "@/components/portfolio/VideoShowcase";

  const PortfolioPage = () => {
    return (
      <main className="portfolio-page container mx-auto p-4">
        <PortfolioHeader />
        <ExperienceList />
        <VideoShowcase />
      </main>
    );
  };

  export default PortfolioPage;
  ```

---

## 2. Develop the Portfolio Introduction Header

**File:** `src/components/portfolio/PortfolioHeader.tsx`  
- **Purpose:** Displays an introductory section with a professional photo and text.
- **Changes:**
  - Add an `<img>` tag using a placeholder URL with detailed descriptive text.
  - Include a heading ("Video Editor Portfolio") and a short descriptive paragraph.
  - Implement an `onError` handler on the image to provide a fallback.
- **Example Code:**
  ```typescript
  import React from "react";

  const PortfolioHeader = () => {
    return (
      <section className="portfolio-header text-center py-8">
        <img
          src="https://placehold.co/400x400?text=Video+Editor+Portrait+Professional+headshot+with+subtle+background"
          alt="Professional portrait of the video editor with subtle background lighting"
          onError={(e) => { e.currentTarget.src = "/fallback.png"; }}
          className="mx-auto rounded-full w-40 h-40 object-cover"
        />
        <h1 className="mt-4 text-3xl font-bold">Video Editor Portfolio</h1>
        <p className="mt-2 text-lg text-gray-600">
          Crafting compelling visual stories with creativity and precision.
        </p>
      </section>
    );
  };

  export default PortfolioHeader;
  ```

---

## 3. Build the Company Experience Components

### a. ExperienceCard Component

**File:** `src/components/portfolio/ExperienceCard.tsx`  
- **Purpose:** Renders an individual company’s logo and description in a card.
- **Changes:**
  - Accept props for company name, logo URL, and description.
  - Use a placeholder logo URL for fallback with an `onError` handler.
- **Example Code:**
  ```typescript
  import React from "react";

  interface ExperienceCardProps {
    companyName: string;
    logoUrl: string;
    description: string;
  }

  const ExperienceCard: React.FC<ExperienceCardProps> = ({ companyName, logoUrl, description }) => {
    return (
      <div className="experience-card border rounded-lg p-4 shadow hover:shadow-lg transition">
        <img
          src={logoUrl}
          alt={`Logo of ${companyName}`}
          onError={(e) => { e.currentTarget.src = "https://placehold.co/200x100?text=No+Logo+Available"; }}
          className="w-full h-auto object-contain mb-2"
        />
        <h3 className="text-xl font-semibold">{companyName}</h3>
        <p className="text-gray-600 mt-1">{description}</p>
      </div>
    );
  };

  export default ExperienceCard;
  ```

### b. ExperienceList Component

**File:** `src/components/portfolio/ExperienceList.tsx`  
- **Purpose:** Aggregates six company experience cards into a responsive grid.
- **Changes:**
  - Define an array of six companies with names, logo URLs (using placeholders), and descriptions.
  - Map over the array to render an ExperienceCard for each company.
- **Example Code:**
  ```typescript
  import React from "react";
  import ExperienceCard from "./ExperienceCard";

  const companies = [
    { companyName: "Company One", logoUrl: "https://placehold.co/200x100?text=Company+1+Logo", description: "Worked on feature films and commercial projects." },
    { companyName: "Company Two", logoUrl: "https://placehold.co/200x100?text=Company+2+Logo", description: "Specialized in post-production editing and color grading." },
    { companyName: "Company Three", logoUrl: "https://placehold.co/200x100?text=Company+3+Logo", description: "Created engaging promotional videos." },
    { companyName: "Company Four", logoUrl: "https://placehold.co/200x100?text=Company+4+Logo", description: "Delivered innovative video editing solutions." },
    { companyName: "Company Five", logoUrl: "https://placehold.co/200x100?text=Company+5+Logo", description: "Managed multi-platform video campaigns." },
    { companyName: "Company Six", logoUrl: "https://placehold.co/200x100?text=Company+6+Logo", description: "Executed dynamic video content for social media." },
  ];

  const ExperienceList = () => {
    return (
      <section className="experience-list py-8">
        <h2 className="text-2xl font-bold text-center mb-6">Professional Experience</h2>
        <div className="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6">
          {companies.map((company, index) => (
            <ExperienceCard key={index} {...company} />
          ))}
        </div>
      </section>
    );
  };

  export default ExperienceList;
  ```

---

## 4. Create the Video Showcase Section

**File:** `src/components/portfolio/VideoShowcase.tsx`  
- **Purpose:** Displays video content to showcase the video editor’s projects.
- **Changes:**
  - Define an array of video items with titles, video URLs, and thumbnail URLs using descriptive placeholders.
  - Render a responsive grid of video cards, each featuring an HTML `<video>` element with controls and a poster image.
  - Include an `onError` handler on the `<video>` element’s poster attribute.
- **Example Code:**
  ```typescript
  import React from "react";

  const videos = [
    { title: "Project One", videoUrl: "https://sample-videos.com/video123/mp4/720/big_buck_bunny_720p_1mb.mp4", thumbnail: "https://placehold.co/640x360?text=Project+One+Video+Thumbnail" },
    { title: "Project Two", videoUrl: "https://sample-videos.com/video123/mp4/720/big_buck_bunny_720p_1mb.mp4", thumbnail: "https://placehold.co/640x360?text=Project+Two+Video+Thumbnail" },
    { title: "Project Three", videoUrl: "https://sample-videos.com/video123/mp4/720/big_buck_bunny_720p_1mb.mp4", thumbnail: "https://placehold.co/640x360?text=Project+Three+Video+Thumbnail" },
  ];

  const VideoShowcase = () => {
    return (
      <section className="video-showcase py-8">
        <h2 className="text-2xl font-bold text-center mb-6">Video Showcase</h2>
        <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
          {videos.map((video, index) => (
            <div key={index} className="video-card border rounded-lg p-2 shadow hover:shadow-lg transition">
              <video
                controls
                width="100%"
                poster={video.thumbnail}
                onError={(e) => { e.currentTarget.poster = "https://placehold.co/640x360?text=No+Thumbnail+Available"; }}
              >
                <source src={video.videoUrl} type="video/mp4" />
                Your browser does not support the video tag.
              </video>
              <h3 className="text-xl font-semibold mt-2">{video.title}</h3>
            </div>
          ))}
        </div>
      </section>
    );
  };

  export default VideoShowcase;
  ```

---

## 5. Update Global Styles for Responsive, Modern UI

**File:** `src/app/globals.css`  
- **Purpose:** Ensure the portfolio page has modern typography, proper spacing, and responsive layout.
- **Changes:**
  - Add custom CSS classes for `.portfolio-page`, `.portfolio-header`, `.experience-list`, `.experience-card`, and `.video-showcase`.
  - Use flexbox or grid utilities to maintain visual hierarchy and spacing.
- **Note:** If your project already uses a utility-first framework (like Tailwind CSS), ensure class names used in the components align with its styling.

---

## 6. Error Handling and Best Practices

- Every `<img>` and `<video>` tag includes an `onError` handler to replace broken or missing content with a fallback placeholder.
- All components include descriptive `alt` text and proper semantic HTML for accessibility.
- Components are modular and reusable, and the layout adapts for mobile and desktop breakpoints.
- Ensure to test the page locally and verify responsiveness and proper error fallback behavior.

---

## Summary

- Created a new Next.js portfolio route (`src/app/portfolio/page.tsx`) to integrate the header, company experience, and video showcase sections.
- Developed modular components: PortfolioHeader, ExperienceCard (with ExperienceList), and VideoShowcase.
- Inserted placeholder images and video thumbnails using descriptive URLs and detailed alt texts.
- Applied error handling using `onError` for images and video poster fallback.
- Ensured modern, responsive UI with proper spacing, typography, and grid layouts.
- Followed best practices for component reusability, accessibility, and error handling.

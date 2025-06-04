---
layout: page # Uses the standard page layout from your theme (Minima)
title: About Me
permalink: /about/ # Sets the URL to yoursite.com/about/
# You can add a description for SEO if your theme/SEO plugin uses it
# description: "Learn more about [Your Name], my background, interests, and what drives this blog and project showcase."
---

<!-- Tip: You can use HTML in your Markdown files if you need more complex layout, but try to stick to Markdown for simplicity. -->

<div class="about-container">

  <!-- Optional: If you want to include an image -->
  <!-- 
  <div class="profile-image-container">
    <img src="/assets/images/your-profile-picture.jpg" alt="A picture of [Your Name]" class="profile-picture">
  </div>
  -->

  <div class="about-content">
    <!-- This is where you introduce yourself. Be authentic! -->
    <p>Hello! I'm <strong>[Your Name]</strong>, and welcome to my little corner of the internet. I'm a [Your Profession/Role, e.g., "software developer", "curious student", "lifelong learner", "creative writer"] based in [Your City/Region, optional].</p>

    <p>This website serves as a space for me to share my [e.g., "thoughts on technology", "creative writing pieces", "learnings from various projects", "explorations in data science"] and to showcase some of the projects I've been passionate about building.</p>

    <h2>My Interests</h2>
    <p>I'm particularly interested in:</p>
    <ul>
      <li>[Interest 1, e.g., Artificial Intelligence and its ethical implications]</li>
      <li>[Interest 2, e.g., Open source software and community building]</li>
      <li>[Interest 3, e.g., The art of storytelling in different mediums]
      <li>[Add more as you like]</li>
    </ul>

    <h2>Background & Journey (Optional)</h2>
    <p>My journey into [Your Field/Primary Interest] began when [brief story or motivation]. Since then, I've [mention key experiences, education, or milestones briefly].</p>
    <!-- Example: 
    <p>My journey into software development began with a fascination for how websites were built. After teaching myself the basics of HTML and CSS, I dived into JavaScript and later Python. I graduated with a degree in Computer Science from [Your University] and have since worked on various web applications, focusing on [Your Specialization].</p>
    -->

    <h2>Why This Site?</h2>
    <p>I believe in the power of sharing knowledge and experiences. Through my writings and projects, I hope to [Your Goal for the site, e.g., "connect with like-minded individuals", "document my learning process", "contribute to discussions in my field", "inspire others to build cool things"].</p>

    <h2>Get in Touch</h2>
    <p>I'm always open to connecting with new people, discussing ideas, or potential collaborations. You can reach me via:</p>
    <ul>
      <li><strong>Email:</strong> <a href="mailto:{{ site.email }}">{{ site.email }}</a> (Make sure `email` is set in your `_config.yml`)</li>
      <!-- Add other contact methods or links to social profiles if not covered by theme's social links -->
      <!-- Example for LinkedIn if not in Minima's footer social links:
      <li><strong>LinkedIn:</strong> <a href="https://linkedin.com/in/yourprofile" target="_blank" rel="noopener noreferrer">My LinkedIn Profile</a></li>
      -->
    </ul>
    <p>You can also find me on the platforms linked in the footer.</p>

  </div>
</div>

<!-- Optional: Some basic SASS/CSS for this page. You would move this to your _sass/custom/_layout.scss or a new _about.scss -->
<!-- For now, keeping it inline for simplicity during creation -->
<style>
  .about-container {
    /* max-width: 800px; You might control this via a .wrapper class in _layout.scss */
    /* margin: 0 auto; */
  }
  .profile-image-container {
    text-align: center;
    margin-bottom: 1.5em;
  }
  .profile-picture {
    max-width: 200px; /* Adjust size as needed */
    height: auto;
    border-radius: 50%; /* Circular image */
    border: 3px solid #eee; /* Optional border */
  }
  .about-content h2 {
    margin-top: 1.8em;
    margin-bottom: 0.8em;
  }
  .about-content p, .about-content ul {
    line-height: 1.7;
  }
</style>

---
title: How to Contribute a Blog Post
description: Learn how to add your own blog posts to our repository by creating a pull request or submitting an issue using our GitHub template.
pubDate: 2024-04-30 17:30
author: "Boubacar BARRY"
tags:
  - GitHub
  - Markdown
  - Contribution
imgUrl: '../../assets/github-contributions.webp'
layout: '../../layouts/BlogPost.astro'
---

## How to Contribute a Blog Post

Are you interested in sharing your knowledge by adding a blog post to our repository? In this guide, we'll show you how to contribute your own blog posts directly to our GitHub repository. You can either create a pull request or submit an issue following our GitHub template.

### Prerequisites

- A GitHub account
- Basic understanding of Git and Markdown

We will be covering the following:

- Forking the repository
- Cloning the repository
- Creating a new branch
- Adding your blog post
- Committing and pushing your changes
- Creating a pull request
- Alternative: Submitting an issue
- Conclusion

---

### Forking the Repository

Let's start by forking our public repository to your own GitHub account.

1. Navigate to the repository page.
2. Click on the **Fork** button at the top-right corner.

### Cloning the Repository

Clone the forked repository to your local machine:

```bash
git clone https://github.com/b-barry/helb-it-trends
cd helb-it-trends
```

### Creating a New Branch

Create a new branch for your blog post:

```bash
git checkout -b add-my-blog-post
```

### Adding Your Blog Post

Add your blog post in the `src/content/blog` directory using the provided Markdown template.

#### The Markdown Template

```markdown
---
title: Your Blog Post Title
pubDate: Date and Time
author: "Your Name"
tags:
  - Tag1
  - Tag2
imgUrl: '../../assets/your-image.jpg'
description: A brief description of your blog post.
layout: '../../layouts/BlogPost.astro'
---

## Your Blog Post Title

Your content goes here.
```

Make sure to fill out all the fields accordingly.

### Committing and Pushing Your Changes

After adding your blog post, commit your changes:

```bash
git add .
git commit -m "Add my blog post"
git push origin add-my-blog-post
```

### Creating a Pull Request

Go to your forked repository on GitHub and click on **Compare & pull request** to submit your changes for review.

---

### Alternative: Submitting an Issue

If you're not familiar with Git or prefer not to use it, you can submit your blog post by creating an issue using our GitHub template.

#### Steps to Submit an Issue

1. Navigate to the **Issues** tab in the repository.
2. Click on **New Issue**.
3. Select the **Blog Post Submission** template.
4. Fill in the required information and paste your blog post content.

---

### Conclusion

If you have any questions or need assistance, feel free to reach out!

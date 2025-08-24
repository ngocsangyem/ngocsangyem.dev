To create a new blog post, follow these steps:

1.  **Create a new Markdown file:**
    *   The file name must follow the format `YYYY-MM-DD-your-post-title.md`.
    *   Place the file in the `_posts` directory. You can also create a subdirectory within `_posts` to categorize your post (e.g., `_posts/new-category/`).

2.  **Add the front matter:**
    *   At the beginning of the file, add a YAML front matter block enclosed in `---`.
    *   Here are the required and recommended fields:

        ```yaml
        ---
        layout: post
        title: "Your Post Title"
        description: "A brief description of your post (around 150 characters)."
        image: /assets/img/blog/your-image.jpg
        sitemap: true
        category: "your-category" # e.g., javascript, vue, etc.
        tags:
          - "tag1"
          - "tag2"
        published: true # set to false for drafts
        ---
        ```

3.  **Write the content:**
    *   Write the post content in Markdown.
    *   You can use headings, paragraphs, lists, code blocks, etc.
    *   To add a table of contents, add the following line where you want it to appear:
        ```
        * this ordered seed list will be replaced by the toc
        {:toc}
        ```

4.  **Add images:**
    *   Place your images in the `assets/img/blog` directory. You can create a subdirectory for your post's images.
    *   Reference the images in your post using the path from the `assets` directory, like `/assets/img/blog/your-image.jpg`.

By following these steps, you can create a new blog post that is consistent with the existing posts on the site.

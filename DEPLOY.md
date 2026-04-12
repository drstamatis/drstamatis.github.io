# Deploying Signal Psychology to GitHub Pages

## Quick setup (5 minutes)

1. **Create a GitHub account** (if you don't have one) at https://github.com

2. **Create a new repository**
   - Go to https://github.com/new
   - Name it `signal-psychology` (or `yourusername.github.io` if you want it at the root)
   - Set it to **Public**
   - Click **Create repository**

3. **Upload your site files**
   - On the repository page, click **"uploading an existing file"**
   - Drag and drop the entire contents of this `signal-psychology` folder
   - Click **Commit changes**

4. **Enable GitHub Pages**
   - Go to **Settings** → **Pages** (in the left sidebar)
   - Under "Source," select **Deploy from a branch**
   - Select the **main** branch and **/ (root)** folder
   - Click **Save**

5. **Your site will be live** at `https://yourusername.github.io/signal-psychology/` within a few minutes.

## Custom domain (optional)

If you buy a domain like `signalpsychology.com`:

1. In your repo's **Settings → Pages**, enter your custom domain
2. At your domain registrar, add a CNAME record pointing to `yourusername.github.io`
3. GitHub will handle HTTPS automatically

## Activating the contact form

The contact form uses [Formspree](https://formspree.io) (free tier = 50 submissions/month):

1. Create an account at https://formspree.io
2. Create a new form
3. Copy your form endpoint (looks like `https://formspree.io/f/xrgvalke`)
4. In `contact.html`, replace `YOUR_FORM_ID` with your actual form ID

## Adding new blog posts

1. Copy `blog/sample-post.html` and rename it
2. Update the title, date, and body content
3. Add a new `<li>` entry in `blog.html` linking to your new post

## Things to customize

- [ ] Replace `[your city]` in about.html with your location
- [ ] Replace `[your state(s)]` in services.html with your licensure states
- [ ] Add your actual LinkedIn URL in all footer links
- [ ] Replace `hello@signalpsychology.com` with your real email
- [ ] Add your headshot (replace the photo placeholder in about.html)
- [ ] Set up Formspree for the contact form

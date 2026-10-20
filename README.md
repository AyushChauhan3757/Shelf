# Shelf

A simple ebook reader that runs on GitHub Pages. Put PDFs in the `book` folder and read them as a real ebook: the text is reflowed into pages, you turn pages with the Previous and Next buttons, and the app remembers where you stopped.

## Repository structure

```
.
├── index.html        the whole app (library + reader)
├── README.md         this file
├── progress.json     your reading history (the app updates this file)
├── .nojekyll         tells GitHub Pages to serve files as they are
└── book/
    ├── .gitkeep      keeps the empty folder in Git
    ├── books.json    optional fallback list of books (see below)
    └── your PDFs go here
```

## Set up GitHub Pages

1. Create a new repository on GitHub. Make it **public** (GitHub Pages on a free account needs this).
2. Upload everything from this folder: **Add file → Upload files**, drag in `index.html`, `README.md`, `.nojekyll` and the `book` folder, then **Commit changes**.
3. Open **Settings → Pages**.
4. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
5. Choose branch **main** and folder **/ (root)**, then click **Save**.
6. Wait one to two minutes. Your app will be at `https://YOUR-USERNAME.github.io/YOUR-REPO/`.

## Add books

1. Open the `book` folder in your repository.
2. Click **Add file → Upload files**, drop in your PDFs and commit.
3. Reload your Shelf page. The new books appear automatically.

The book title is taken from the file name, so name files clearly (for example `Pride and Prejudice.pdf`).

## Using the reader

- Click a book to open a pop-up with its cover, title, date added and progress. Choose **Start reading**, **Resume** or **Start over**.
- Use **Previous** and **Next** to turn pages. Tapping, swiping and arrow keys do not turn pages.
- Every page is shown exactly as it looks in the PDF, with its original layout, fonts, images and columns.
- On wide screens such as a laptop or desktop, two pages are shown side by side, like an open book. Turn this off in the Aa menu if you prefer one page. On phones you always get one page.
- **Aa** has **Zoom** (Fit, 125%, 150%, 200%, 300%), a paper or dark theme, and **Mark as finished**. When zoomed in, scroll inside the page to move around it.
- Reaching the last page moves the book to the **Completed** tab. Open it there and choose **Read again** to restart it and move it back.

## Reading history (progress.json)

Every book keeps its own position, status (new, reading, finished), title and date added. The app saves this in your browser all the time, and writes it to `progress.json` in the repository when you close a book, leave the page or close the tab. Opening the app on another device reads that file and takes you to your spot.

To let the app write to your repository you need a GitHub access token, once per device:

1. On GitHub open your profile picture, then **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**.
2. Give it a name, choose the longest expiry, and under **Repository access** pick **Only select repositories** and choose this repository.
3. Under **Permissions → Repository permissions** set **Contents** to **Read and write**.
4. Generate the token and copy it.
5. In Shelf, open **Settings**, paste the token and press **Save and sync**.

The token is stored only in that browser. Without a token the history still works, but only in that browser. Each save is a commit to your repository, so the repository history will show "Update reading progress" entries.

## Good to know

- The page is fixed like the PDF itself, so on a small phone the text is small. Use Zoom in the Aa menu.
- Scanned PDFs work too, since pages are shown as pictures.
- The dark theme inverts the page colors, which can make images look odd. Paper is the default.
- Uploading through the GitHub website allows files up to 25 MB each. Larger files need Git on your computer. GitHub's hard limit is 100 MB per file.
- Because the repository is public, anyone with the link can download the PDFs. Only upload books you are allowed to share.

## If the library is empty

The app lists the `book` folder through the GitHub API. If that does not work (for example on a custom domain), edit `book/books.json` and list your file names:

```json
["Pride and Prejudice.pdf", "Meditations.pdf"]
```

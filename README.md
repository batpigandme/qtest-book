# qtest-book

Test book to troubleshoot issue I'm having with nav-page-next button published with Quarto GHA.

Live site: <https://qtest-book.netlify.app/>

## Problem

With the current default publish workflow (uses exact text from [publish action](https://quarto.org/docs/publishing/netlify.html#publish-action) section of Quarto docs on publishing with Netlify), the arrow for moving to the pagination link for the next page is broken (seems to have the some of the HTML spliced into the name).

The [publish.yml](https://github.com/batpigandme/qtest-book/blob/main/.github/workflows/publish.yml) for this book uses the defaults (latest released version of Quarto), and displays this problem.
It only happens for the link to the *next* section, the link for the *previous* section is fine (see, e.g. <https://qtest-book.netlify.app/intro>).

The screenshot below shows the live [preface page for this book](https://qtest-book.netlify.app/) with the problem.

![Screenshot of test book preface page with broken pagination link.](images/qtest-book-min.png)

## More info

I discovered this issue with a book I'd been publishing to Netlify with the Quarto publish action.

The [version rendered on January 29th](https://65b7cb24f026681574d693c1--maranotes.netlify.app/basics) with the default workflow (i.e. no Quarto version is specified in the "setup" step of the workflow) exhibits the broken link for the next page.

![Screenshot with broken navigation link from January 29 with no Quarto version specified in setup.](images/quarto-book-jan29-min.png)

There were no changes made in the workflow from the [January 23rd version](https://65afe04a406fbe2a3fcf9fa8--maranotes.netlify.app/basics), which did *not* have a problem with the pagination link for the next page.

![Screenshot with working navigation link from January 23 with no Quarto version specified in setup.](images/quarto-book-jan23-min.png)

I was able to resolve the issue with the `nav-page-next` link by specifying a Quarto `version: 1.3.433` in the setup step of the workflow (see the [live page using 1.3.433](https://notes.maraaverick.com/basics)).

![Current deploy using 1.3.433 has working next pagination link.](images/quarto-book-current-1-3-433-min.png)

I tried using an earlier 1.4.\* release ([version published with 1.4.515](https://65bbad1402c6e11501b322d2--maranotes.netlify.app/basics)), which also exhibited the broken `nav-page-next` element.

![Screenshot with broken navigation link using version 1.4.515.](images/quarto-book-1-4-515-min.png)

The same was true when I used `version: pre-release` ([page using pre-release](https://65bbaf65214d59177d67c848--maranotes.netlify.app/basics)).

![Screenshot with broken navigation link using version: pre-release.](images/quarto-book-pre-release-min.png)

# How to Contribute to Open Source

See also: [Git Commands and Aliases](../Git/git-commands-and-aliases.md)

## Learning Resources

- Laracasts [How to Contribute to Open Source](https://laracasts.com/series/how-to-contribute-to-open-source)
  by Luke Downing.
- [Luke's Merged PR](https://github.com/laravel/prompts/pull/118)
- [Laravel Prompts Source Code](https://github.com/laravel/prompts)
- [GitHub Docs](https://docs.github.com/en)
- [Git Docs](https://www.git-scm.com/doc)

## Document Focus

The focus of this document is what I've learned about git, GitHub, and contributing to open source. The examples
in this document mostly center around the course project which is a PR to
[Laravel/Prompts](https://github.com/laravel/prompts), but ideas and concepts apply to all open source contributions.

Below is my takeaway from the course, along with some of my own words and opinions.

## Forking and Installation

The first thing to do is fork the project in GitHub. If we simply clone the project, then we would need to manually
create a new project on GitHub, and change the remote origin in git, to be able to push changes and submit
a PR. Forking a project sets that all up for us, so we can clone our own forked copy of the project instead.

For the "copy main branch only" option, we need to consider the project. If you just want to submit a PR to the main
branch, then this is fine. Different projects have different requirements. For example, Laravel is currently on version
11 and asks that non-breaking changes be submitted to the version 10 branch. If the change broke projects
using any version below 11, then you would want to keep the default and submit to the main branch. Some projects may
have a WIP branch or others where they want PRs submitted to. It is important to do the research ahead of time by
reading the project contribution guide.

Now you can use git clone from your own personal fork of the project. At the top of your forked repo's main page is
a notification that will let you know if your fork is up to date with the original repo. There is a "Sync Fork"
button for pulling in recent changes that have been made to the original project.

> [!WARNING]
>
> Be sure to use the "Sync Fork" button regularly, in case you need to account for any new changes that may have
> happened in the original project during the time you have been working on your PR.

Run any package installation and/or setup scripts required to run the project, then run any existing tests and
confirm that the current project is running correctly on your own machine. It is important to understand not just
code but how the particular project is intended to be run and on which platforms it is intended to run.

In the course project, we are writing a PR for laravel/prompts. As a PHP package, the first step is to run `composer
install` to get all the required dependencies. A test suite for the existing code is provided, so we want to run
those tests and see them all passing.

> [!NOTE]
>
> Laravel/Prompts does not run on Windows. The Laravel installer CLI uses Symphony Console as a fallback for Windows.
> So if you're on a Windows platform, the tests will let you know immediately if you have other problems to fix
> such as switching to WSL, Linux, or Mac on your end before continuing.

## Getting a Feel for the Code

Study the project and make sure you understand it. If you try to fix code or add features in code you don't really
understand, you're going to make mistakes. The maintainer of the project will either give you a list of things to
fix or they might simply reject and close the PR because they don't have time.

In the case of Laravel/Prompts, there is a playground directory with example prompt functions you can run just to see
how each one works. Also, diving into the rest of the code shows us that the rendering of a prompt is separated from
the storing of prompt state. This will dictate how we go about writing our new feature/fix in a way that conforms
to the rest of the code base. The final code for the PR should include a playground file and a test/tests.

## Writing the Code

Luke used some good techniques while writing the code. First, he used existing prompts from the playground directory
index.php file and built out a structure of how the feature code should look. Then he ran the code to see it fail
and added code one step at a time, re-running it each time until a basic version of the code was running. He
referred to this as Script Driven Development. Depending on the project, you may do something similar, or you may need
to start with TDD from the beginning.

Either way, it is important to be meticulous and methodical in your thinking. Don't get in a rush or get stressed out
and let that cause you to write code you are not happy with. Reach out to others if you need to. You want to have
good, clean, quality code before submitting a PR. Mistakes are OK but be realistic. If you're not
up to the task, don't submit junk. Keep learning and know that you will get there some day.

## Prove Your Work Works

Not all projects require you to write tests to contribute. Whether tests are committed to the repo or not, I still
would not submit a PR without testing on my end. When they do require testing, treat test writing the same as code
writing. Study existing tests in the project and understand how the project maintainers write them. A test may
already exist for what you are writing. You wouldn't want to duplicate it.

Be meticulous and make sure all edge cases are covered to the best of your ability.

## Refactor for Readability

Now that there are tests, you can start cleanup and refactoring. This step is just as important as the others. Even
if you were cautious when writing the code and the tests, you are sure to find places where the code could be made more
readable or cleaner.

Implement refactoring in steps, running tests each time. You can do multiple passes. In the course project, we create a
class
called StepBuilder to replace arrays with an object. Then we make all the changes to make the tests pass again. Then
we go back and do cleanup and refactors on the new StepBuilder class.

Add docblocks/comments and use formatting in line with the way the project is written.

## Writing a PR Description

After pushing changes up to your GitHub repo `git push origin branch-name` you will see a notification on the main
page of your repo that "branch-name had recent pushes" and a "Compare & pull request" button. Click that button.

Different projects may have different rules about how to properly format titles and descriptions.

Crafting a nice and clear PR description is the best way to ensure that the maintainers understand it and are
willing to look at it and consider merging the PR.

Start with a basic overview of what the PR does. You can provide a short screen recording, demonstrating the new
code in action if it is appropriate for what you have changed.

Elaborate on the purpose of the PR, explaining the problem and how your change is a fix/solution to that problem.
Explain the use case.

Use code snippets to show a usage example followed by any necessary textual explanation. Repeat this for any extra
sections that may need demonstrating or explaining.

Use proper headings for sections such as Purpose and Usage. Add a Wrap-up section with a final statement and a
genuine "Thank You."

Once you are happy with the PR, you can choose draft in which case they won't be informed of it yet. This gives you
time to get feedback from others or make any changes to the draft. Or, you can choose "create pull request" to
create it.

## Fixing Failing Actions

Many projects have actions setup for when PRs are created. They will test that the code passes tests and adheres to a
set of standard setup for that repository. They may also test on multiple versions of the language, library, or
framework the code runs on. When an action fails, you will see "Some checks were not successful." Passing tests will
be marked with a green check mark and failing ones will be marked with a red X.

In the course project, we fail the static analysis by PHPStan. Other projects may use Pint or Javascript projects
may use
ESLint. Clicking on the failing test shows us the failures. If we spent more time studying the project, we might
have known that we need to be running PHPStan on our new code before we submit it. But this is OK. No panic, no stress.

We need to run the static analysis tool locally on our new code to reproduce the failures found during PR submission.
Fix problems/errors until it passes and then re-run your code test suite to make sure you didn't cause any problems in
the changes you made to fix the static analysis tests.

Now push again and see the GitHub actions tests in your PR all passing.

## Implementing Feedback

The maintainer may simply merge your PR, or they may suggest more changes or fixes. They may have questions.

You might feel tempted to get defensive if they ask you to change too much or are willing to accept some code but
not other code.

Keep in mind that they are going to be the ones maintaining this code after you are gone. They have a vision and a
standard about this project, and you should respect and appreciate if they stand strong about not changing it and
offer you alternatives.

Go back to the drawing board and try to make changes to meet them in the middle.

Be sure to run tests, code analyzers, etc. before pushing new changes. If changes required removing code, you may
have tests that can also be removed.

## Implementing Feedback Part 2

Now that you have made the requested changes, tested, formatted and pushed your code, you'll want to squash those
"Work in Progress" commits into one commit with a meaningful commit message.
See [Squash Commits](git-commands-and-aliases.md/#squash-commits)

Now update the original PR description. Don't add a bunch to it or use an "Update" section. Rewrite the
original description. This way in the future, there'll be a simple description that properly describes the actual
changes that are the result of the feedback fixes. Including descriptive text about code that doesn't exist anymore
can cause confusion. If more changes are requested by the maintainer, you'll want to repeat the whole
"Implementing Feedback" process and update the description again where needed.

Once you have pushed this final commit, you can message the maintainer. At this point, they have asked for changes or
offered suggestions to get your PR merged so tag them with a short and to the point message "Changes implemented.
Ready for review." Or something similar. Follow with a “Thank You.”

When your PR gets merged, celebrate! :-)

If it doesn't, celebrate anyway because it was good practice :-)

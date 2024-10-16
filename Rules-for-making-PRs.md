## Table of Contents

* [Step 1: Before writing any code, choose a descriptive branch name](#step-1-create-a-new-branch-with-a-descriptive-name)
* [Step 2: Make commits locally to your feature branch](#step-2-make-commits-locally-to-your-feature-branch)
* [Step 3: Push changes to your GitHub fork](#step-3-push-changes-to-your-github-fork)
* [Step 4: Create a pull request](#step-4-create-a-pull-request)
* [Step 5: Address review comments until all reviewers approve](#step-5-address-review-comments-until-all-reviewers-approve)
* [Step 6: Make sure all continuous integration checks pass](#step-6-make-sure-all-continuous-integration-checks-pass)
* [Step 7: Tidy up](#step-7-tidy-up)
* [Step 8: Celebrate](#step-8-celebrate)
* [Tips for Managing Multiple PRs](#tips-for-managing-multiple-prs)

**Working on your first pull request?** Pull requests can be tricky to understand at first, so if the instructions on this page don't make sense to you, check out the free series [How to Contribute to an Open Source Project on GitHub](https://app.egghead.io/series/how-to-contribute-to-an-open-source-project-on-github) or [Atlassian's tutorial to pull requests](https://www.atlassian.com/git/tutorials/making-a-pull-request).

**Note:** If your change involves more than around 500 lines of code, we recommend first creating a short [design doc](https://github.com/oppia/oppia/wiki/Writing-design-docs). This helps avoid duplication of effort, and allows us to offer advice and suggestions on the implementation approach.

To make code changes, please follow the following instructions carefully! Otherwise, your code review may be delayed.

## Step 1: Create a new branch with a descriptive name

The new branch should be based on the latest code in `develop`, so checkout the latest version of `develop` like this:

```console
git fetch upstream
git checkout develop
git merge upstream/develop
```

Then create a new branch. In this example the branch is named `your-branch-name`. The branch name should be lowercase and hyphen-separated, e.g. `fuzzy-rules`. Make sure that your branch name doesn't start with `develop`, `release` or `test`.

```console
git checkout -b your-branch-name
```

> [!NOTE]
> Do not use the character '/' in your branch name.


## Step 2: Make commits locally to your feature branch

Each commit should be self-contained and have a descriptive commit message that helps other developers understand why the changes were made.

However, **do not write "Fix #ISSUE_NUMBER"** (e.g. "Fix #99999") in your commit messages (or any of the other closing phrases from [GitHub's documentation](https://docs.github.com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue#linking-a-pull-request-to-an-issue-using-a-keyword)), as this will cause Github to close the original issue automatically.

You can change your most recent commit message using `git commit --amend`. **It is difficult to change any commit messages other than your most recent one or messages on commits that have been pushed, so write your commit messages carefully!**

* Before making the commit, do some sanity-checks:

  * Ensure that your code follows [[the style rules|Coding-style-guide]].
  * Start up a local instance of Oppia and do some manual testing in order to check that you haven't broken anything!
  * Run `git status` to check that your changes are what you expect.  To inspect the changes made to any particular file, use `git diff your-file-name`.

  * Stage all your changes:

    ```console
    git add .
    ```

    (`.` refers to your current directory)

* To actually make the commit, run:

  ```console
  git commit -m "{{YOUR COMMIT MESSAGE HERE}}"
  ```

> [!NOTE]
> There is no maximum or minimum number of commits required in a PR. Instead of aiming for a certain number, you should try to make each commit a logical "chunk" of work. There are many opinions about how big commits should be, but a useful rule of thumb is that you should be able to read the first lines of all your commit messages to get a good idea of what you changed. If you find yourself needing lots of clauses to capture what you changed, your commit is probably too big.

## Step 3: Push changes to your GitHub fork

* **Before pushing**, make sure to check the following things, otherwise you will incur delays with the review process or the automated checks:

  * **Do some manual testing** on your local instance of Oppia to check that you haven't broken anything. This is important to avoid breakages. **Don't rely on the automated tests alone.** This [[resource on how to access different Oppia webpages|How-to-access-Oppia-webpages]] might be useful.

  * Once you're sure that your changes are correct, make a screen recording showing that the part of the website you changed still works correctly. You'll need to add this video to the pull request description.

  * Use a tool like `git diff upstream/develop` to check that the changes you've made are exactly what you want them to be, and that you haven't left in anything spurious like debugging code.

  * Ensure that your code is fully covered by automated tests. (For more info, see the wiki pages on writing tests in the sidebar menu.)

  **We don't allow force-pushing at Oppia, so once you push your commits, you can't change them.** You can still add new commits though.

* When you're ready to push, run:

  ```console
  git push origin {{YOUR BRANCH NAME}}
  ```

  **Make sure to do this from the command line** (and not GitHub's Desktop client), since this also runs some important presubmit checks before your code gets uploaded to GitHub. If any of these checks fail, read the failure messages and fix the issues by making a new commit (see step 3), then **repeat the previous instructions** to retry the push. **Do not bypass these presubmit checks!** The checks get run on your PR too, so if you bypass failures on your local machine, you'll just have to fix them later when they fail on the PR.

## Step 4: Create a pull request

Once your feature is ready, you can open a pull request (PR)!

### How to make a pull request

Go to your fork on GitHub, select your branch from the dropdown menu, and click "pull request". Ensure that the base repository is oppia/oppia and that the base branch is develop. The head repository should be your fork, and the head branch should be your branch. If you don't see the repository, click the link to compare across forks. On this page, you can also see your commits and your changes.

![The GitHub PR creation screen](images/makingAPR.png)

> [!WARNING]
> **Read through these changes carefully** to make sure that they are correct (e.g., no extra files; no files left out by mistake; no missing newlines at the ends of files). This is a good way to catch obvious errors that would otherwise lead to delays in the review process. (You can also double-check them on the "Files Changed" tab after the PR is created, but make sure to do at least one self-review before assigning any reviewers.)

**After** confirming your changes:

* Click "Create pull request".

* Following the guidance in the PR checklist, add a descriptive title explaining the purpose of the PR (e.g. "Fix issue #bugnum: add a warning when the user leaves a page in the middle of an exploration.").

  **WARNING: If your PR only fixes a specific part of the issue, start the title with "Fix part of issue #bugnum:" instead so that the original issue is not auto-closed by GitHub when the PR is merged.**

* Write a clear description of your PR that explains why the change is being made, how the change was made, as well as any identified risks and resulting countermeasures. See [here](https://github.com/oppia/oppia-android/pull/4757#issue-1461272376) for a good example of what sorts of things to include.

* Fill out the rest of the PR checklist, including the screen recording you saved previously.

* Click "Create pull request". If applicable, verify that the issue your PR fixes is linked in the "Development" section on the right. (If not, update your description to clearly reference the issue, using the format "Fix #bugnum".)

* Oppiabot will check that you filled out the PR description correctly. If you didn't, it will leave a comment explaining what you need to do to fix it. Also, GitHub will automatically assign reviewers, and Oppiabot will assign them as codeowners to do the first review.

  If you need to assign someone else but aren't a collaborator yet, leave a comment of the form `@{{reviewer username}} PTAL`, which will tell Oppiabot to assign that person for you. ("PTAL" means "Please take a look".)

* After a while, check your pull request to see whether the CI checks have passed. If not, follow our instructions to [[diagnose PR failures|If-CI-checks-fail-on-your-PR]].

* Then, wait for your code to get reviewed! While you're waiting, it's totally fine to start work on a new PR if you like. Just follow these instructions again from the beginning.

Here's a video showing one example of the PR creation process:

[![First frame of a screen recording showing how to open a new PR](images/demoOpenPR.png)](https://user-images.githubusercontent.com/19878639/137946692-7c5f72e3-c6ce-4157-b8fa-b1e82bcc7642.mov)

Notice that in this example:

* No proof of correctness was needed, but this might not be the case for your PR.
* The CI checks were failing as soon as the PR was opened. If you see this, you should investigate.

### Pull request lifecycle

```mermaid
flowchart LR
DP("Draft PR") -->|"Ready for review"| PRW("PR awaiting review")
PRW -->|"Request changes"|CR("Changes Requested")
CR -->|"Addresses comments"| PRW
PRW -->|"All reviewers approve"|PRL("PR labeled LGTM")
PRL -->|"Merge"| M("Merged")
```

1. (optional) Draft PR: Authors can open draft PRs to get early feedback or debug CI tests. Reviewers usually won't leave comments on these PRs unless the author leaves a comment of the form `@reviewer_username PTAL` to request a review from GitHub user `reviewer_username`.
While making a contribution, you may discover that your change is not complete and needs some more work. You can make a draft pull request to make it easy for other developers to give you feedback; however, draft pull requests consume resources like time on our CI runners, which slows down CI runs for other developers. Hence, you should prefix the commit messages with [skip ci] or [ci skip] to disable CI runs when those commits are going to a draft PR. If you want those tests to run to help you debug a problem, you should open a PR against your fork's develop branch instead of the oppia/oppia develop. This will not delay other developers' GitHub Actions runs.
Learn more about [skipping a GitHub Actions run](https://github.blog/changelog/2021-02-08-github-actions-skip-pull-request-and-push-workflows-with-skip-ci/).
2. PR ready for review: Once authors mark PRs as ready for review (or if they skip the draft PR stage entirely), reviews will automatically be requested from all code owners. Oppiabot will assign the code owners to review the PR.
3. Changes requested: Reviewers will either approve the PR or request changes. Almost all PRs will have at least some changes requested. PR authors address each comment, either by making the requested change or explaining why they think it is unnecessary. Once all comments are addressed, reviewers will re-review.
4. LGTM: A PR gets labeled LGTM ("looks good to me") when it has sufficient reviews. This means that a code owner from each modified file has approved. When multiple developers share code ownership, only one has to approve.
5. PR merged: PRs can be merged once CI checks pass and the LGTM label has been applied. Only members of the Oppia organization can merge PRs.

### Labeling pull requests

While contributing to Oppia, you will need to add different labels to issues or pull requests which you are working on. However, not all labels are allowed on issues and pull requests. Below are labels which can be applied to pull requests:

* Added by PR author:

  * `dependencies`: Should be added to pull requests that update one or more dependencies.
  * `PR: Affects datastore layer`: Indicates that a PR changes the datastore layer. Adding this label notifies the developers in charge of datastore stability so they can review the PR. Sometimes this label gets added automatically by Oppiabot, but if you open a PR that changes the datastore layer and the label isn't added automatically, you should add it manually. You can also add the label without waiting for Oppiabot.
* `PR: require post-merge sync to HEAD`: Should only be applied to pull requests which, when merged, will require all other open pull requests to be updated with the develop branch.

* Added automatically:

  * Labels starting with `PR: don't merge`: Indicates that some problem with the PR needs to be addressed before merging. For example, one of these labels gets added if the PR author hasn't signed the CLA yet.
  * `stale`: This label gets added by oppiabot to PRs that have been inactive for a week. They will be automatically closed after 4 more days of inactivity.
  * `PR: LGTM`: Indicates that a PR has all necessary approvals. The PR can be merged as soon as the CI checks pass.

* Added by the release team:

  * `PR: for current release`: Identifies PRs that need to be included in the release that is currently in progress. This label is used by the release team to identify PRs to cherry-pick into the release.
  * `PR: released`: Identifies PRs that have been cherry-picked into the release. Should only be used by the release team.

A complete list of labels can be found [here](https://github.com/oppia/oppia/labels). If you don't have permission to add labels, leave a comment asking one of your reviewers to add the label for you.

## Step 5: Address review comments until all reviewers approve

Note that reviewers will often say "LGTM," which means "looks good to me".

When your reviewer has completed their review, they will reassign the pull request back to you, at which point you should push updates, respond to **all** comments, and reassign it back to them. This continues until the reviewer approves, after which the pull request is merged. Here is the procedure for responding to a review:

* Merge develop into your branch. If you run into conflicts, run the following commands to resolve them (**note:** replace new-branch-name with the name of your branch):

  ```console
  git checkout new-branch-name
  git fetch upstream
  git merge upstream/develop
  ...[fix the conflicts -- see https://help.github.com/articles/resolving-a-merge-conflict-using-the-command-line]...
  ...[make sure the tests pass before committing]...
  git commit -a
  git push origin new-branch-name
  ```

  **Note:** Do not squash commits when you merge develop into your branch! This often happens when you are using an graphical interface instead of the command line. Squashing commits can confuse GitHub and cause the changes you merge in from develop to be treated as changes you made. If this happens, you'll need to close the pull request and open a new one.

* Make a new commit addressing the comments you agree with, and push it to the same branch. (Continue to use descriptive commit messages, or something like "Address review comments" if you're addressing many disparate review comments in the same commit.) **You do not need to close your pull request and create a new one -- it's fine to push new commits to the existing pull request.**

* **Always make commits locally, and then push to GitHub.** Don't make changes using the online GitHub editor -- this bypasses lint/presubmit checks, and will cause the code on GitHub to diverge from the code on your machine.

* **Never force-push changes to GitHub, or rebase your PR.** This will lead to the PR being closed.

* As you are making changes, track them by replying to each comment via the "Files Changed" tab. Each reply should be either "Done" or a response explaining why the corresponding suggestion wasn't implemented. **Use the 'Start a review' button** (rather than the 'Add single comment' button) to write draft comments, so that you don't publish them before the code is ready. Please **do not** mark the comment as resolved, since this just makes it harder to actually read the comment thread.

  **Tip:** If a reviewer asks questions about the "why" behind something, consider proactively adding a clear comment above the relevant line in your code, since the fact that the reviewer had to ask suggests that at least one developer doesn't understand what is going on from the code alone. Otherwise, you'll probably get a follow-up review comment asking you to leave a code comment anyway :)

  **Note:** If any comments require follow-up PRs, please file an issue to track the necessary changes, and mention the issue number in the relevant review comment thread. (You should do this automatically for any deferred changes; reviewers may defer approval until you do.)

* Once you've addressed everything and would like the reviewer(s) to take another look:

  * Follow the instructions in Step 3 to test your changes locally before pushing.

  * Make the push, and then immediately check that the changes in the "Files Changed" tab are what you intend them to be.

  * Verify that you've posted responses to **all** the review comments from the reviewer(s). This may require scrolling up and checking older conversations on the comment thread. (If you see "Pending" labels next to your comments, that means it hasn't been submitted yet and others cannot see it. To fix this, make sure you've actually clicked through the green "Review changes > Submit review" button in the top right of the Files Changed tab.)

  * In the conversation thread, **write a top-level comment** explicitly asking the reviewer(s) to take another look ("@XXX PTAL"), and assign them to the PR. Be sure to use the **"Assignees"** rather than the "Reviewers" section of the PR, since the latter field is auto-populated by GitHub and reviewers typically don't track it.

## Step 6: Make sure all continuous integration checks pass

While waiting to get approval from reviewers, make sure that all the continuous integration (CI) checks on GitHub Actions pass, since otherwise you won't be able to merge your pull requests. CI checks are shown at the bottom of your pull request on GitHub.

![CI results at the bottom of a PR](images/prCiResults.png)

(See [[If CI checks fail on your PR|If-CI-checks-fail-on-your-PR]] for some suggestions on what to do if you run into issues.)

If all reviewers have approved but you're still waiting for the CI checks to pass, make sure you're assigned to the PR, so that you can merge it once the CI checks are complete.

## Step 7: Tidy up

After the PR status has changed to "Merged", delete the feature branch from both your local clone and the GitHub repository:

```console
git branch -D new-branch-name
git push origin --delete new-branch-name
```

## Step 8: Celebrate

Congratulations, you have successfully contributed to Oppia! 🎉

## Tips for Managing Multiple PRs

1. **Prioritize Existing PRs**:
   - Always prioritize following up on your existing PRs and getting them ready for the next round of review. Only start working on new issues/PRs after **all** the other PRs you're working on are in the "waiting for review" stage. This helps avoid creating a logjam in the build queues.

2. **Create Separate Branches**:
   - Always create a new branch for each pull request. This helps keep your changes isolated and makes it easier to manage multiple PRs.

3. **Update Branches Frequently**:
   - Regularly pull in changes from the `develop` branch to your feature branch. This will help you avoid merge conflicts.

4. **Use Descriptive Branch Names**:
   - Use clear and descriptive names for your branches to easily identify the purpose of each branch.

5. **Keep PRs Small**:
   - Try to keep your pull requests small and focused on a single change or feature. This makes it easier for reviewers to understand and review your changes.

6. **Track Dependencies**:
   - If one pull request depends on another, make sure to clearly indicate this in the PR description and comments.

By following these tips, you can effectively manage multiple pull requests and ensure a smooth development workflow.

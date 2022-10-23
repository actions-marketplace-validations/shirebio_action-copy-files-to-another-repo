v0.0.1

# Copy multiple globbed files to another Repository
This GitHub Action copies glob matched files from the current repository to a location in another repository.
The action takes care to create the directory, if not yet present.

# Example Workflow
    name: Push Files

    on: push

    jobs:
      copy-file:
        runs-on: ubuntu-latest
        steps:
        - name: Checkout
          uses: actions/checkout@v2

        - name: Pushes multiple files
          uses: shire/action-copy-files-to-another-repo@0.0.1
          env:
            API_TOKEN_GITHUB: ${{ secrets.API_TOKEN_GITHUB }}
          with:
            glob: 'my_files/*.yaml'
            destination_repo: 'shirebio/release-test'
            destination_folder: 'test-dir'
            user_email: 'kevin@shirebio.com'
            user_name: 'kallen'
            commit_msg: '[GHA] Update the test files.'

# Variables
* **glob:** The glob string to specify which files are copied from the source repo
* **destination_repo:** The repository to place the folder in.
* **destination_folder:** [optional] The folder in the destination repository to place the file in, if not the root directory.
* **user_email:** The GitHub user email associated with the API token secret.
* **user_name:** The GitHub username associated with the API token secret.
* **destination_branch:** [optional] The branch of the destination repo to base the changes on and push to (defaults to master).
* **destination_branch_create:** [optional] The branch the changes should be pushed to; defaults to commiting to `destination_branch`; is useful for creating PRs
* **commit_msg:** [optional] The commit message to use.

# Behavior Notes
The action will remove the destionation folder before recreating it to place any copied files in it.

To build the website to the dist directory, run build.sh.

For running the Google Apps Script, first generate a GitHub Fine-Grained Access Token with the following permissions:

- Actions: Read and write
- Contents: Read and write

Ensure that the token is scoped to the project's repository. The token can be used to read and write files in the repository if leaked.

Then, from the Script Editor settings, set the GITHUB_ACCESS_TOKEN property to the generated token.

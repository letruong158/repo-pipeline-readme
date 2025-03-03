# repo-pipeline-readme

The pipelines were tested by executing them on Jenkins and reviewing the logs for each stage to ensure that all steps ran correctly and produced the expected outputs. Specific outputs, like the generated documentation from Doxygen and the archived artifacts, were checked for correctness.
Here is the Jenkins server I set up specifically for the interview, with pipelines B and C so you can check further:

URL: http://14.225.215.25:8080/
User: admin
Password: P@ssw0rd
Please let me know if you encounter any issues accessing it, as the Jenkins Docker might be facing some problems. Thank you very much.


RepoC, which contains the Python script to parse Doxygen warnings, was tested by running the `parser.py` script on the generated log file (`doxygen_warnings.log`). This ensured that the Python script correctly processes the warnings and outputs the expected result.

Git Large File Storage (LFS) is designed to handle large files like binaries more efficiently in Git repositories. Instead of storing large files directly in the Git repository, LFS stores them externally and replaces them with lightweight references in the repository. This results in reduced repository size, making it faster to clone and manage, improved performance when working with large files, and better version control for large assets such as images, videos, or compiled binaries. 

To adjust the repository to support Git LFS, the following steps should be taken:
1. Install Git LFS using the command `git lfs install`.
2. Track the desired file types (e.g., binaries) by using the command `git lfs track "*.exe"` and `git lfs track "*.dll"`.
3. Commit the `.gitattributes` file that LFS creates by using the command `git add .gitattributes` and `git commit -m "Add Git LFS tracking"`.
4. Push the changes with `git push origin main`.

Links:
- [Git LFS official documentation](https://git-lfs.github.com/)
- [Git LFS tracking files](https://git-lfs.github.com/spec)

Another alternative to Git LFS for managing large files is Git-Annex. It can store files externally while keeping their metadata in the Git repository. Git-Annex works similarly to Git LFS but provides more flexibility in managing large files across multiple repositories or locations.

[Git-Annex Documentation](https://git-annex.branchable.com/)

Thank you very much for your time! It was a pleasure going through your assessment. I hope we get the chance to work together as well.

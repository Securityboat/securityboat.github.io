# Contribution

The SecurityBoat Workbook is an open-source project which is actively maintained and constantly evolving. We welcome contributions in the form of additions, corrections, or updates to the resources and we have implemented a process for these contributions.

## **Want to add or update a section/page?**

Before adding a new section or note, please first search the knowledge base to ensure it doesn't already exist. If it is not present, visit the [discussion board] to see if there are any existing discussions about the topic. If there are none, initiate a new discussion and include all the necessary information below:

### **Format of discussion**

#### **Title**
- A good title should be a short, one-sentence description, contain all relevant information.

| Example | <!-- --> |
| -------- | -------- |
| Update to the XYZ resource in ABC page | :material-check:{ style="color: #4DB6AC" } __Clear__
| Addition of XYZ resource in ABC page | :material-check:{ style="color: #4DB6AC" } __Clear__
| Missing information in the docs | :material-close:{ style="color: #EF5350" } __Unclear__
| XYZ Section not found | :material-close:{ style="color: #EF5350" } __Unclear__
| Help | :material-close:{ style="color: #EF5350" } __Useless__

#### **Description**
- When requesting updates or additions to the knowledge base, please provide a clear and brief summary of what needs to change and explain why.
- Please address only one specific issue at a time to simplify tracking and updating. 
- Please clearly describe the problem to help us understand the needed improvements. 
- Please include direct, anchored links to the relevant documentation sections for easy reference.

## **Found a typo?**
- Please submit a pull request with the correction.

### **Submitting a pull request**
- This knowledge base is developed using [Mkdocs Material](https://squidfunk.github.io/mkdocs-material/).
- If you're interested in contributing, you can submit a draft pull request by forking this repository.
- You can test the changes by either running the server locally or making edits directly to Markdown files from GitHub.

#### **Running the site locally**
To run the site locally, follow these steps:

- [Fork](https://github.com/Securityboat/workbook/fork) the repository.
- Clone the forked repository locally in the system.
- Run the below command to install mkdocs-material and required extensions:
```
pip install mkdocs-material
```
```
pip install mkdocs-exclude
```
```
pip install mkdocs-pdf
```
- Make sure you have a proper IDE installed. We will go with VS-Code. Run the following command to open VS-Code with the workbook files:
```
cd workbook
```
```
code .
```
- Run the following command to run the site locally:
```
mkdocs-serve
```
- Make changes and check them in the site running locally. Either use [GitHub Desktop](https://desktop.github.com/) or [generate a new SSH key to use for github authentication](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) to commit and sync the changes to your forked workbook repository. You can now sumbit a pull request.

We appreciate you for following the guide and providing valuable feedback the knowledge base.

!!! warning "Issues, discussions, and comments are forever"

    Please note that everything you write is permanent and will remain
    for everyone to read – forever. Therefore, please always be nice and
    constructive, follow our contribution guidelines, and comply with our
    [Code of Conduct]. Please read [rights and responsibilities](rights_and_responsibilities.md) page.

[Code of Conduct]: https://github.com/Securityboat/workbook/blob/master/CODE_OF_CONDUCT.md
[discussion board]: https://github.com/Securityboat/workbook/discussions
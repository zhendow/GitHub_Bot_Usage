# Manual Review Guide for Identifying GitHub Bot

This is a guide to a simple process of manually identifying bot activities in GitHub. 
Prior work suggests that to achieve optimal results for binary classification of bots in social or social-technical platforms, 
several tiers of data collections would support more accurate results [1, 2]. 
As bot accounts on GitHub do not have a friend network as other platforms, such as Twitter and Facebook, 
this study employs three levels of data: comment text, account meta-data, event patterns of its timeline activities. 
It is recommend to employ a machine learning classifier to analyze the comment texts [3], 
and further manually review meta-data and event patterns on bot activities. 
We operationalize the above classification steps within the protocol in this document. 
Each coder should follow this protocol to identify and collect bot information.

## Identifying Bot Activity in Repository Timeline

Given a target repository, there are several features to manually spot usages of bot services, including repository readme, 
Commit list, Issue list, Pull Request list, and Release list, as bot usually provide services for these tasks. 
The following subsections describe each part of the repository respectively.

### Repository Readme

Under the repository root directory, manually review the content of `readme.md` and `contributing.md` files. 
Developers may introduce whether they have employed any bots in their typical/expected workflow, for instance:

> "for this repository, the contributing.md file demonstrates that a CLA bot would interact with the incoming Pull Requester to collect signatures." 

Moreover, developers may provide information about bot usage such as Issue/Pull Request format, acknowledgment, and so on.

### Repository Event Actor

To our best knowledge, almost all bots on GitHub are designed by rule-based mechanisms and often triggered by certain repository events. 
Therefore, checking most critical OSS development events on GitHub yields finding substantial bot services. 
Events of Issue, Pull Request, Commit and Release provide us access to identify bot services. 
Commit Review the latest 20 Commits, and verify whether each Commit event actor, including commenter on each Commit, is a bot service.

**Issue**: Review the latest 10 open and 10 closed Issues in the Issue management system. 
Verify if each Issue event actor and Issue commenter is a bot service.

**Pull Request**: Review the latest 10 open and 10 closed Pull Requests in the Pull Request management system. 
Verify if each Pull Request event actor and commenter is a bot service.

## Profile Metadata

### Event Actor Overview

When a coder reviews the event actors under each targeting event above,
here are several indicators and features to employ while identifying if an account is a bot.

- Being listed in GitHub Apps, Marketplace, and Actions
- Having a `bot` tag next to the actor name
- Having keywords in its description and name that indicates bots

If there is a description claiming that this is a bot for some repository or a saying of the comment/description is “automatically generated”, 
Bot account name keywords include  `“bot”, “ci”, “cla”, “auto”, “logic”, “code”, “io”,` and `“assist”` [3]. 
However, be careful to determine if found any other human-like behaviors in its profile, such as following other accounts, and personal email address.

## Bot Data Collection
For each of the accounts that have been identified as a bot, record the following content.
- **Bot account name:** profile names of the actor
- **Service Medium:** whether the bot is found in GitHub (private) App or it has a profile
- **Avalibility:** whether the bot service is available to public or private to organization, free or commerialized.
- **Functionality Notes:** Notes about performed tasks of the bot, for example, the committed code is for updating dependencies according to its commit message, the issue closes due to staling for too long, the Pull Request is automatically generated to merge code from the testing branch, and label the issue due to no one is investigating (an untriaged label).
- **URLs:** to the account profile page or GitHub App.
- **Open-sourced:** whether there is any indication that the bot is transparently open-sourced, from its profile and App page.

### Example datasheet
| Name       | Service Medium | Availability | Functionality Notes                                                                                                                                                  | URLs                          | Open-sourced | Remarks |
|------------|----------------|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------|--------------|---------|
| dotnet-net | Account        | Private      | Commit code: updating dependencies <br> Assign code reviewers of pull-request <br> Label pull-requests: indicating automatic process labels <br> Merge auto-generated pull-requests | https://github.com/dotnet-bot | No           |         |



## Reference

1. Beskow, David M., and Kathleen M. Carley. "Bot-hunter: a tiered approach to detecting & characterizing automated activity on twitter." Conference paper. SBP-BRiMS: International Conference on Social Computing, Behavioral-Cultural Modeling and Prediction and Behavior Representation in Modeling and Simulation. Vol. 3. 2018.
2. Kantepe, Mücahit, and Murat Can Ganiz. "Preprocessing framework for Twitter bot detection." 2017 International conference on computer science and engineering (ubmk). IEEE, 2017.
3. Golzadeh, Mehdi, et al. "A ground-truth dataset and classification model for detecting bots in GitHub issue and PR comments." Journal of Systems and Software 175 (2021): 110911.

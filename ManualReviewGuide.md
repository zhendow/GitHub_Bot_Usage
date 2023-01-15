# Manual Review Guide for Identifying GitHub Bot

This is a guide that aims to provide improved results based on binary classifications of bots on the GitHub platforms, and therefore, as prior research suggested, several types of data are necessary for more accurate results [1, 2].  As recommended in these studies, a bot can be more accurately identified through a multi-tier identification process, typically including examining its "social network" like its following and follower relationships, comment and other generated text, account metadata, and activity patterns.

This study later employs a three-tier of identification based on GitHub activity data, including repository comment text, account meta-data, and event patterns of its timeline activities. Particularly, many bot-based event actors on GitHub do not have a "social" network as other social media platforms, and moreover, the social network features in GitHub are not as significantly changing user behaviors as they were on other social platforms. Besides, the chance of a GitHub user who is a real human but not having any followers or following anyone, is significantly higher than other social-native platforms, e.g., Twitter and Facebook, due to GitHub's technical nature. Therefore, this study argues that social network is not a reliable tier of data for bot identification, and applying this data tier would neglect the characteristics of this social-technical platform. However, other generic data tiers still apply for the context of GitHub, for instance, examining its comment data [3].

The remainder of this section introduces how the above multi-tier classification gets operationalized and provides a protocol for replicating this process for various research or practical interests. I followed this protocol to validate automated results and identify additional bots in my previous publication [4]. Given a target repository, there are several features to manually spot applications of bot services, including repository readme, Commit list, Issue list, Pull Request list, and Release list, as bots usually provide services for these tasks.

## Identifying Bot Activity in Repository Timeline

### Repository Readme

The first screening overall is to examine the *repository readme*s under a target repository root directory, including manually reviewing the content of `readme.md` and `contributing.md` files. According to our observation, substantial well-maintained and popular repositories provide these statements of whether the repository has employed any bots in their established workflow, for instance:

> "for this repository, the contributing.md file demonstrates that a CLA bot would interact with the incoming Pull Requester to collect signatures." 

In this case, its contributors have clearly indicated that this repository employs a \texttt{CLA} bot to solicit signatures from external contributions. Moreover, contributors often provide information about other bot applications such as Issue/Pull Request formatting, contribution acknowledgment, and so on.

### Repository Event Actor

Since bots are triggered by certain repository events, checking the most critical OSS development events and their *repository event actors* leads researchers to find bot services under this mechanism. GitHub's event timeline of Issue, Pull Request, Commit, and Release provides researchers access to identify bot services. Without spending too much effort on historical events, I focused on recent ones which also reflects whether the repository is running these bot services now. However for studies that are interested historical bot application, the timeframe needs to be extended. Particularly, in my study, for each type of event, we

-**Commit**: review the latest 20 Commits, and verify whether each Commit event actor, including the commenter of each commit, is a bot service.
-**Issue**: review the latest 10 open and 10 closed Issues in the Issue management system.  Verify if each Issue event actor and Issue commenter is a bot service.
-**Pull Request**: review the latest 10 open and 10 closed Pull Requests in the Pull Request management system. Verify if each Pull Request event actor and commenter is a bot service.

## Profile Metadata

From the above locations, when we found an event actor that was suspiciously repeating activity patterns or demonstrated that the content was automatically generated, we applied this multi-tier identification by first reviewing its account metadata such as GitHub profile or GitHub Marketplace/App listings, and examining its naming and description; second, reviewing the content of this GitHub account’s recent comments and activities; finally, for accounts that did not display their recent contributions, collected their activity records through GitHub API.

### Event Actor Overview

Additionally, here are several extra indicators that help to confirm whether an event actor is a bot.

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
4. Wang, Zhendong, Yi Wang, and David Redmiles. "From Specialized Mechanics to Project Butlers: the Usage of Bots in OSS Development." IEEE Software (2022).

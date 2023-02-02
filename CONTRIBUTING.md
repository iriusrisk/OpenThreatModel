# Welcome to the Open Threat Model contributing guide
Thanks for taking the time to contribute. It's early days yet, so expect big things and lots of iteration.

OTM is an open source format for defining threat modeling in a platform independent way, intended to be a future open
standard for threat modeling definition. Thus, collaborators are welcome to extend or improve its definition. Initially thought as an internal [IriusRisk](https://iriusrisk.com) - [Startleft](https://github.com/iriusrisk/startleft)
data exchange format about threat models, it was rethought and planned as a future generic threat model data exchange
standard. Due to that, it's also focused on collaboration, especially suitable for continuous community revision of the standard.

## Getting started
All needed information related to the project can be found on its [documentation page](https://github.com/iriusrisk/OpenThreatModel).

### Submit changes
For the best integration and collaboration between contributors, the [GitHub guide for contributing to projects](https://docs.github.com/en/get-started/quickstart/contributing-to-projects)
will be used. The summarized steps would be:

1. [Fork the OTM repository](https://github.com/iriusrisk/OpenThreatModel/fork).
2. Implement the proposed changes in your forked repository.
3. Create a Pull Request (PR) from the forked branch to the OTM `main` branch in the main
   repository describing the changes done and their motivations.
4. The PR will be reviewed by the owners' team using the
   [GitHub strategy](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/reviewing-proposed-changes-in-a-pull-request)
   for async communication.
5. Once approved, the PR will be merged into the `main` branch of the OTM repository and delivered in the next
   standard release.

### Versioning
As mentioned earlier in the documentation, the OTM standard is intended to use Semantic Versioning 2.0.0.
However, the proposal is already in progress, and the policy for versioning could change in the future.

### Code conventions
Because this project's purpose is to define the OTM standard, it's not expected to have any real code on it, and thus, there are
no specific code conventions that could apply in this case. The only advice is to pay special attention to the YAML syntax
and naming conventions already used and ask for any doubts about it.

### Report feedback

If you spot a problem with the OTM standard current definition, you can do two things:
* First, you can search for it, in case the issue already exists ([open issues](https://github.com/iriusrisk/OpenThreatModel/issues)).
* If you cannot find anything suitable, you can open a new issue, including if possible, an explanation that aids with its understanding.
* Alternatively, you can email us at otm@iriusrisk.com.

### Request an enhancement
To propose improvements or changes that are not properly bugs, you can also use the [issues](https://github.com/iriusrisk/OpenThreatModel/issues)
section. Please, try to be as clear as you can and include, at least:
* **Context**. Does it affect the whole standard, or only a part? In the last case, where does it apply?
* **Motivation**. How will the proposed change improve the OTM standard? 
* **Goal**. What is exactly the change that should be implemented?

Alternatively, you can email us at otm@iriusrisk.com.

## Additional resources

Here you can find several links and resources related to the project that could be useful:
* <a href="https://github.com/iriusrisk/OpenThreatModel" target="_blank">OTM documentation</a>.
* <a href="https://github.com/iriusrisk/OpenThreatModel/issues" target="_blank">OTM open issues</a>.
* <a href="https://github.com/iriusrisk/startleft" target="_blank">Startleft documentation</a>.
* <a href="https://www.threatmodelingconnect.com/" target="_blank">Threat Modeling connect forum</a>.

Furthermore, the contributing strategy for OTM is based on standardized procedures for collaborating in
GitHub Open Source  projects, so these resources may be helpful for you:

* [Finding ways to contribute to open source on GitHub](https://docs.github.com/en/get-started/exploring-projects-on-github/finding-ways-to-contribute-to-open-source-on-github).
* [Set up Git](https://docs.github.com/en/get-started/quickstart/set-up-git).
* [GitHub flow](https://docs.github.com/en/get-started/quickstart/github-flow).
* [Collaborating with pull requests](https://docs.github.com/en/github/collaborating-with-pull-requests).

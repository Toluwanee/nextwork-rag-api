<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Automate Testing with GitHub Actions

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-devops-githubactions)

**Author:** Toluwalope Oni  
**Email:** toluwalope9@gmail.com

---

![Image](http://learn.nextwork.org/compassionate_orange_mysterious_tuke/uploads/ai-devops-githubactions_i1j2k3l4)

---

## Introducing Today's Project!

In this project, I will demonstrate to build a CI/CD pipeline with GitHub Actions that automatically tests your RAG application. I'm doing this project to learn how to build CI/CD pipeline and ensure quality in the data that my RAG API gives out.



You're about to build a CI/CD pipeline with GitHub Actions that automatically tests your RAG application every time you update it.

### Key services and concepts

Services I used were docker, kubernetes. ollama, tinyllama, chromadb, python, git, github. Key concepts I learnt include containerization, orchestration, data quality, testing, continuous integration and testing, automatic deployment...

### Challenges and wins

This project took me approximately 7hrs to complete. The most challenging part was knowing when to assert specific words in the docs file, and knowing when not, so that the deployment can run successfully. It was most rewarding to a see my RAG API deployed and I have a system that ensures that helps me to check if the data quality is accurate.

### Why I did this project

I did this project because I wanted to learn how to build RAG API, and ensure the quality of data produced is accurate, and automatically deploy changes in data to production. One thing I'll apply from this is the knowledge to build several other RAG APIs after this one, especially to ensure accurate data is being given as output.

---

## Setting Up Your RAG API

I'm setting up my RAG API by first writing the code on my IDE, setting up the database, and installing the necessary dependencies for the RAG API to run. A RAG API retrieves information by looking up my knowledge base(document) to retrieve relevant information first. This foundation is needed for CI/CD because the RAG API needs to exist and be in a working state, before the CI/CD pipeline can automatically test and validate it.

### Local API verification

I tested my RAG API by sending a question with the command `curl -X POST "http://127.0.0.1:8000/query" -G --data-urlencode "q=What is Kubernetes?"
` . The API responded with `{"answer":"Kubernetes is a container orchestration platform that manages containers at scale..."}` . This confirms that my RAG API is working properly.

![Image](http://learn.nextwork.org/compassionate_orange_mysterious_tuke/uploads/ai-devops-githubactions_i9j0k1l2)

---

## Initializing Git and Pushing to GitHub

I'm initializing Git by running the command `git init` in my RAG API directory so that git can begin to track changes in my files and folder. Git tracks changes by letting you save different versions of your project over time. Version control enables CI/CD to automate testing and deployment when you push code by tracking every change and making your code available remotely (like on GitHub), it creates the foundation for continuous integration and continuous delivery

### Git initialization and first commit

I initialized Git by adding git init command. Then, I staged and committed using the "git add ." command, and "git commit" command". The .gitignore file helps by ignoring sensitive files and files that can always be regenerated, so that only necessary files are tracked.

### Pushing to GitHub for CI/CD

Pushing to GitHub means I am ensuring there is a match between what is on my local repository and what is on remote repository where others can see it and where CI will run. This enables CI/CD because github actions automatically detects any change I make on the repository based on predefined settings.

![Image](http://learn.nextwork.org/compassionate_orange_mysterious_tuke/uploads/ai-devops-githubactions_y5z6a7b8)

---

## Creating Semantic Tests

I'm creating semantic tests that verify that our RAG system returns answers with the correct meaning.

Unlike unit tests that check code logic, semantic tests validate if the RAG API returns answers with the right meaning not just the right format.

These tests ensure quality by ensuring the right words are present in the knowledge base that we are using, we are not running on the vibes of the model alone, and any interesting behaviour will be noticed on time.

### Non-deterministic output observation

When I ran the query multiple times, I noticed that the LLM generated its own response due to the data already trained with it and the non-deterministic nature of LLMs. This is a problem because it is difficult to tell if the code is actually broken or the LLM is just generating a different response because of its non-deterministic nature. For CI/CD to work reliably, we need to ensure that our tests can reliably check if our API is working correctly.

---

## Adding Mock LLM Mode

I'm adding mock LLM mode to make the API return the retrieved context directly instead of going through the real LLM. This solves the non-determinism problem by ensuring the same query goes to the same document to produce the same output. Reliable testing requires that the right information is verified to be present.

### How mock mode solves the problem

### Mock LLM mode for CI testing

Mock LLM mode returns the retrieved text directly, which makes tests deterministic and produce an exact output every single time. Without mock mode, tests would give us non-deterministic and changing results which will make it difficult to verify the presence of the required information. For automated CI, we need exact results consistently, to be sure doc and word we are referencing are truly present.

---

## Creating GitHub Actions Workflow

I'm creating a GitHub Actions workflow file that describes what to do. The workflow automates testing by ensuring that any change I make to the content or doc gets updated and skips  the manual process I would have used to effect the change. When I push code, the RAG testing and build will automatically begin on github servers.

### Workflow automation and CI testing

I created the workflow file in the .github/workflows/ directory. I pushed it using `git push` command. Once on GitHub, the workflow will run on the push trigger and when there is a change in the files specified.

---

## Testing Data Quality

I triggered the CI workflow by changing the knowledge base and observing how it will be caught. The workflow will test the presence of certain keywords to check for data quality. I expected it to fail because the keywords I was testing for were not present in the knowledge base.

### Data quality and CI protection

The missing keyword was orchestration. The semantic test failed because it was designed to assert the presence of the orchestration word, and since it wasn't present it failed. Without CI, this degraded content would have been deployed to production, and the problem will be discovered by the users, and the consequences of that cannot be controlled.

![Image](http://learn.nextwork.org/compassionate_orange_mysterious_tuke/uploads/ai-devops-githubactions_i1j2k3l4)

---

## Testing Another Data Quality Issue

### Data quality and CI protection

---

## Scaling with Multiple Documents

I'm restructuring the project to handle multiple knowledge documents and see how CI automatically tests them all! The new folder structure supports multiple documents. This approach scales better because in bigger systems multiple knowledge bases.

### Docs folder structure and CI scaling

The docs folder organizes files by putting respective knowledge bases in their respective files and ensuring they are in one place. The embed_docs.py script handles reading all files and knowledge bases in document folder... CI validated all documents and found that there are some missing keywords that should be present in the knowledge and if they are not present the CI will fail. This structure supports growth by ensuring there is data integrity in the knowledge base that is in use.

![Image](http://learn.nextwork.org/compassionate_orange_mysterious_tuke/uploads/ai-devops-githubactions_g5h6i7j8)

---

---

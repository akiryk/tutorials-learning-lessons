# DevOps

**Continuous delivery** means you're _ready_ to deliver your code to production at any time. **Continuous Deployment** means your code goes straight from checkin to production.

In order to achieve the lean, devops outcome of continuous deployment, we need to eliminate unnecessary waste, such as extra steps and approvals. In practice, this means we need robust testing. 

### The 5 Essentials of Continuous Deployment
- Build phase: build every branch on every commit; run unit tests 
- Test phase: (not unit testing but functional testing): automated ui testing, cypress, things like that
- Deployment phase: we need a good tool that can refer to scripted rules, such as yaml files. 
- Provisioning phase
- Monitoring: you may have tens or hundreds of deployments every day


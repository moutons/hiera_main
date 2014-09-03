# HIERA REPOSITORY

Goes with [my version of Gary Larizza's Puppet Repo](https://github.com/moutons/puppet_repository).

## Basically

I'm stealing this wholesale from [here](http://garylarizza.com/blog/2014/03/07/puppet-workflow-part-3b/).

### Workflow for per-environment Hiera data

Looking back on the previous post, you’ll see that the workflow for updating Hiera data is identical to the workflow for updating code to your Puppet environments. Namely, to create a new environment for testing Hiera data, you will:

* Push a branch to the Hiera repository and name it accordingly (remembering that the name you choose will be a new environment).
* Run R10k to synchronize the data down to the Puppet master
* Add your node to that environment and test out the changes

For existing environments, simply push changes to that environment’s branch and repeat the last two steps.

#### NOTE: Puppet environments and Hiera environments are linked – both tools use the same ‘environment’ concept and so environment names MUST match for the data to be shared (i.e. if you create an environment in Puppet called ‘yellow’, you will need a Hiera environment called ‘yellow’ for that data).

This tight-coupling can cause issues, and will ultimately mean that certain branches are longer-lived than others. It’s also the reason why I don’t use defaults in my `hiera()` lookups inside Puppet manifests – I WANT the early failure of a compilation error to alert me of something that needs fixed.

You will need to determine whether this tight-coupling is worth it for your organization to tie your Hiera repository directly into R10k or to handle it out-of-band.

## I Disagree

...And believe that there's a valid workflow for decoupling things somewhere but I am not going to muck about with it now.

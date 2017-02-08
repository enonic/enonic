# backup agent for Enonic Cloud
As a Devops, I want to be able to trigger a backup of the host server up to swift objectstore.

## Estimate

X days/weeks

## Requirements
- It should run in a docker container as a part of a system container set.
- I should be able to set a schedule for the agent to push backup up to swift object store.
- I should be able to schedule both full and incremental backups
- the object store has  to be unique for that server.
- All configurations should be set as environment variables so that I can change configuration without having to customise the images for that spesific host.
- Status should be pushed to a message queue for futher monitoring aswell to logging.
- There should be a status on:
    + Container startup
    + Starting backup
    + Backup finished with status of backup scripts.
- All logging shoud go to std. out.
- There should be a low memory and cpu footprint on the service.
- A simple rest api should be available so that anyone with access can:
    + Get a status on backups
    + Start a backup ( if a backup job is already running, it should give out a error back )
- The rest service should log requests to std. out
- I need to be able to authenticate with a configurable preshared key to access the rest api
- The backups should be able to run incremental backups
- It should be able to detect backup scripts from a configurable set of labels by inspecting the running containers and executing them inside of that container before and after copying out data.
- It should also detect labels for data named in configurable lables that are not inside volumes and copy those data out to a persitand docker volume belonging to the backup system.
- I should be able to specify which path ( ex. /var/lib/docker/volumes) to be copied out to server.
- I should be able to restore a set of files from backup either to the original server og to alternative destination


## Acceptance Criteria
- I should be able to start a backup of a server manually
- I should be able to verify backup status by listening on a message queue
- I should be able to restore a file/folder from the backup destination from a spesified point in time to a destination
- I should be able to restore backup to a completly empty machine.
- I should be able to se backup status from the rest api

## Suggestions
- Use duply ( http://duply.net/ ) or duplicity to handle the file backup. Duply supports different backends so its possible to reuse the same container for other destinations aswell.
- consider using multiple PGP keyes to encrypt the backups with. one dedicated for that machine and one ore two central ones incase total restore.
- For duply configuration to zetta swift store se: https://zetta.io/en/help/articles-tutorials/backup-linux-duply/
- See https://vault.esu.enonic.io/Enonic-Cloud/project-prototype/src/master/enonic/utils/docker_tools.py#L60 for how execute the post and pre commands inside the the container now.
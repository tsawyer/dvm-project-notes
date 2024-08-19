# Talkgroups

## FNE Provided

Allow the FNE to provide talkgroups.

Talkgroup section of config.yml should look like this.
```
    #
    # Talkgroupd ID ACL Configuration
    #
    talkgroup_id:
        # Full path to the talkgroup rules file.
        file: /opt/dvm/talkgroup_rules.yml
        # Amount of time between updates of talkgroup rules file. (minutes)
        time: 2
        # Flag indicating whether or not TGID ACLs are enforced.
        acl: false
```

In config.yml
* Change `updateLookups: false` to `updateLookups: true`. Load talkgroups from FNE into memory.
* Change `saveLookups: false` to `saveLookups: true`. Optional. Create or overwrite talkgroup_rules.yml.
 

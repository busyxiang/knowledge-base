# Google Cloud Platform
Create separate project for **testing** and **production**, if not will have issues when verify the project
# Digital Asset Links
## Generator
[Link](https://developers.google.com/digital-asset-links/tools/generator)
## Validate
```bash
https://digitalassetlinks.googleapis.com/v1/statements:list?
   source.web.site=https://domain.name:optional_port&
   relation=delegate_permission/common.handle_all_urls
```
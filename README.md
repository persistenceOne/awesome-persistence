# tooling
This repository has aggregation of tooling resources provided by the team and community for persistence and pstake

Project Structure:
```diagram
persistence/
  - devtools/
  - entityname_tooling.md
pstake/
  - devtools/
  - entityname_tooling.md
```

This is the proposed structure for the reposi tory.   
Example:   
- Audit.one validator gives out public api's
- Audit.one creates a doc under `persistence` repository called - `auditone_rpc_endpoints.md`
- Documents what they are how to use, if cors required, how to assign.

Example2:
- Imperator validator has a discord bot for validator uptime and governance.
- Imperator creates a doc under `persistence` repository called - `imperator_discord_bot.md`
- Documents what the bot does, where can one find it (channel_invite link).

Example3: 
- X has a certain e2e testing setup for pstake.
- X creates a doc under pstake called `x_e2e_test.md` which documents stuff about the testing setup. 
- X adds the code etc to `pstake/devtools/` repository under x_e2e_test folder, extra documents etc.

This structure can evolve as we go forward

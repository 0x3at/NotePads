
## SQL Tables

### MySQL01:
- **Human.longcodes**: 
  - Stores modem phone numbers
  - Updated during provisioning
  - ASEND uses active field to update human.sims where active = y

- **Human.sims**: 
  - Used to determine which modems are in a state to accept messages
  - All ancillary processes check this table for modem state, ASEND
  - Prevents messages from being sent to non-responding/inactive modems

### MySQL03:
- **Logs.ase**: Contains logs for every modem

## Systemd Services
- **ModemManager.service**: Modem Manager Service, accessed via `mmcli`

- **ASE.service**: One-shot service that:
  1. Shut down USB hubs
  2. Restart all USB hubs on the device
  3. Restarts modem manager after a set delay to prevent process overlap and bad data capture

## Ancillary Resources

### Text Manager Hub > Sim Tester
- **URL**: webmd02.themanualduialcompany.org
- **CID**: 5000
- Used to test SIMs and confirm network send/receive capability

After a test is sent, carriers might shut down outbound messages from the SIM:
- SIM can still receive inbound messages but is blocked from sending
- Line shutdown lasts at least a day (carriers reset statuses overnight & we reset modems every night)
- High potential that a SIM may never send again or consistently get turned off daily

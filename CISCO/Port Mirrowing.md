You can check if there are any active monitor sessions with:
`SW1#show monitor session 1`

If there is any active session, you can deactive them with:
`SW1(config)#no monitor session 1`

To create a monitor session:
`SW1(config)#monitor session 1 source interface GigabitEthernet 0/1`
`SW1(config)#monitor session 1 destination interface GigabitEthernet 0/5`

Check that the session has been created correctly
`SW1#show monitor session 1`

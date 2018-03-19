---
title: 'Disable Bitlbee OTR'
date: 2011-04-05 00:00:00 
tags: 
layout: post
---
This has taken me a while to find, so I'm posting it here for reference.

Using Bitblee as my IM gateway has been rather nice. Running 24/7 and being able to connect from anywhere without missing messages does have it's advantages. However, I keep getting a message in the main &bitlbee window telling me that some messages have been sent unencrypted from certain contacts. The quick fix I found was to run the commend 'otr disconnect' however, after a while the messages would come back again. I'm not sure why these would happen, since, to the best of my knowledge and memory, I've never enabled otr for anyone in my contact list.

Today I found a setting in Bitlbee called 'otr_policy'

```
14:16 <@EspadaV8> help set otr_policy
14:16 <@root> Type: string
14:16 <@root> Scope: global
14:16 <@root> Default: opportunistic
14:16 <@root> Possible Values: never, opportunistic, manual, always
14:16 <@root>  
14:16 <@root> This setting controls the policy for establishing Off-the-Record connections.
14:16 <@root>  
14:16 <@root> A value of "never" effectively disables the OTR subsystem. In "opportunistic"
              mode, a magic whitespace pattern will be appended to the first message sent to any 
              user. If the peer is also running opportunistic OTR, an encrypted connection will be
              set up automatically. On "manual", on the other hand, OTR connections must be 
              established explicitly using otr connect. Finally, the setting "always" enforces
              encrypted communication by causing BitlBee to refus
```

My understanding is that simply running 'set otr_policy never' will disable otr and stop my from getting these messages.

We'll see how this goes over the next couple of days :-)

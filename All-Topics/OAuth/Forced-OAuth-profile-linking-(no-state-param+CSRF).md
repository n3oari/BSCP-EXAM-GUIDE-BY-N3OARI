
# Forced OAuth profile linking (no state param + CSRF)

In this lab we found that we can link our social media accounts to our user account.

When analyzing the OAuth flow we notice that the `state` parameter is not present. This parameter is used to verify that the response arriving at the redirect endpoint actually belongs to the legitimate request initiated by the same user.

![[Forced-OAuth-profile-linking-no-state.png]]

It is important to DROP the request so that the generated code cannot be used.

![[Forced-OAuth-profile-linking-no-state-drop.png]]

We force the victim to use our code associated with our social accounts in order to later obtain administrator privileges.

![[Forced-OAuth-profile-linking-no-state-token.png]]

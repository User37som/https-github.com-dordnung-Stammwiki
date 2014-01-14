This part of the wiki shows you how to use the **colors part** of the API.

**We can not use**, because of the support on CS:GO, **morecolors in general**.   
Because of that, there is a little part in the API to work with that.


## Morecolors or not

If you wanna know if you **can use morecolors** or not, you can use the stock `STAMM_IsMoreColorsAvailable()`.

This stock simply returns, whether the **game Stamm is running on is CS:GO** or not.


## How to print for all games

So that you don't always have to check **whether morecolors is available or not**, there are two stocks to print to the chat.

Instead of using `PrintToChat` or `PrintToChatAll` just use `STAMM_PrintToChat` or `STAMM_PrintToChatAll`.

The syntax is **exactly the same**, but it will **use the colors include on CS:GO** and **morecolors on the other games**.

---------
### [Go to the next Page](Scripting-Features)
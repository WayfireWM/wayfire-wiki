The modified weston(which you can find here: https://github.com/ammen99/weston) contains several changes:

1. Custom rendering plugin - I have spoken with libweston developers, such an API may be implemented in the future, but for now it is an impossible thing to do in "stock" libweston.
2. Some changes to the way Xwayland maximized/fullscreen surfaces are handled - this way a window can be maximized using a keybinding
3. Implement closing Xwayland windows using a keybinding
4. Disable Xwayland frame shadows - By default, libweston draws shadows around the border of Xwayland windows. However, on some systems(like mine) this causes FPS drop(video/scrolling/etc in chrome starts to lag), so I disabled these shadows. If you want them, you can simply drop this commit, wayfire doesn't actually depend on it.
5. Implemented dynamic output rotation - this patch was accepted in mainline weston

The patched repository has two branches - `master`(which "should" be stable, but is actually tested only on my PC) and `testing` which I try to frequently rebase against upstream git.
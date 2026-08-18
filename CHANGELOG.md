## Phase 01 — Linux Permissions: Groups (2026-08-07)

Today I finally got the owner/group/others thing straight. I used to think the
two "thales thales" in `ls -l` was just some weird repetition, turns out it's
owner and group — two different fields that happen to have the same name
because Linux gives you a personal group by default.

Did the chmod 660 exercise: wanted owner + group to read/write, others locked
out. Did the math myself — R=4, W=2, 6 for owner, 6 for group, 0 for others.
First tried 644 by mistake (wrote group as 4 instead of 6), caught it and
fixed it.

Also messed up on chgrp. Ran `chgrp users teste-grupo.txt` and it just worked,
so I assumed it was because I'm "the superuser." Wrong — I'm not root by
default, being in the `sudo` group just means I *can* become root when I ask
for it with a password. The real reason chgrp worked without sudo: I was
already a member of the `users` group (checked with `groups` first). A regular
user can change a file's group only if they already belong to that group.
Adding yourself (or anyone) to a new group needs root — that's a different
action entirely (`usermod -aG`).

Mental model I'm keeping: permission checks always need something to exist
first. Group membership works the same way — you can't hand a file to a group
you're not part of, root is the only one who can actually add people to groups.
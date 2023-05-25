# create Appcontext

- get framebuffer handle based on current device
- get res from framebuffer
- create channels for input
- populate initial context struct
- create a quad tree for display reasons
- optional lua scripting initialization (skip)

# init bools for selected tool

# call `clear` on context with arg `deep=true`

- get ref to framebuffer
- get resolution

## call `clear` framebuffer

- get framebuffer height
- get line length
- set framebuffer pixels to i32 MAX (possibly clearing the screen?)

- depending on the `deep` arg decide which refresh to do

## `deep == true`

### call `full_refresh` on framebuffer

- create rect that is as big as the screen
- add one to a dubious `marker` atomic field of the framebuffer
- create a `whole` variable which holds the mysterious `update_data`
- match on the `frambuffer_update` field which returns the things needed to push an update to the device

  - on remarkable 1 use libcs `ioctl` to send a `SEND_UPDATE` request via system call to the remarkable device and carry the `update_data` we constructed before
  - on remarkable 2 use the swt client abstraction to do the same but with a `msgsnd` system call

- the return value of the system call is evaluated and an error message is sent when the syscall failed

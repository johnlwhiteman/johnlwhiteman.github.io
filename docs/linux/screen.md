# Screen

```bash
# Start a session
screen -S johnny

# Disconnect
ctrl+a d

# Show sessions
screen -ls

# Reconnect
ctrl+a r
ctrl+a r <session id>

# Create a new window
ctrl+a c

# Split window vertically
ctrl+a |

# Split window horizontally
ctrl+a S

# Move to the next window
ctrl+a n
ctrl+a tab

# Move to the previous window
ctrl+a p

# Create a new session window when in split mode
ctrl+a c

# Unsplit window
ctrl+a Q

# Exit
ctrl+c
pkill screen
```

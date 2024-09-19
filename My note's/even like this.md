The problem is the following: if someone updates the PATH in the environment, any executable that is in that directory should be executed without the need of inputting './'  
The fix for this is in execution_3.c:135

```c
void    ft_exec(t_data *data, t_env **env_ll, char **cmd_array)
{
    static char    *path;

    if (cmd_array[0] == NULL)
        exit (0);
    if (check_path_unset(env_ll))
        execution_absolute_path(data, cmd_array);
    data->env = env_arr_updater(env_ll);
    if (!data->env)
        exit (1);
    if (ft_strchr(cmd_array[0], '/') == NULL)
    {
        update_path(env_ll, data); // <---- This was added
        path = loop_path_for_binary(cmd_array[0], data->binary_paths);
        if (!path)
        {
            err_msg(cmd_array[0], NO_EXEC, 127);
            cleanup_and_exit(data, env_ll, cmd_array, 0);
        }
    }
    free_tokens(data->token);
    free_all_ll(env_ll);
    if (!path)
        execution_absolute_path(data, cmd_array);
    execution_with_path(data, cmd_array, path);
}
```

execution_3.c has space for functions, so I added this following function:

```c
static void    update_path(t_env **env_ll, t_data *data)
{
    if (data->binary_paths)
        free_array(data->binary_paths);
    if (!*env_ll || !env_ll)
        return ;
    find_bin(env_ll, data);
    data->binary_paths = ft_split(data->bin, ':');
    if (!data->binary_paths)
        return ;
}
```

after adding that, now the path will be updated at every single execution  
if you update the path, using my own environment as an example:

```shell
%> env
SYSTEMD_EXEC_PID=1151535
GJS_DEBUG_TOPICS=JS ERROR;JS LOG
SESSION_MANAGER=local/c3r2p2.hive.fi:@/tmp/.ICE-unix/1151511,unix/c3r2p2.hive.fi:/tmp/.ICE-unix/1151511
LANGUAGE=en
LANG=en_US.UTF-8
INVOCATION_ID=4babb912dafb4075a53a817b5041b52d
XDG_CURRENT_DESKTOP=ubuntu:GNOME
SSH_AUTH_SOCK=/run/user/5511/keyring/ssh
XDG_CONFIG_DIRS=/etc/xdg/xdg-ubuntu:/etc/xdg
GIO_LAUNCHED_DESKTOP_FILE_PID=1152241
TERMINATOR_DBUS_PATH=/net/tenshu/Terminator2
FT_HOOK_PATHNAME=login-user.d
XDG_GREETER_DATA_DIR=/var/lib/lightdm-data/fdessoy-
LIBVIRT_DEFAULT_URI=qemu:///system
GPG_AGENT_INFO=/run/user/5511/gnupg/S.gpg-agent:0:1
DESKTOP_SESSION=ubuntu
USER=fdessoy-
XDG_MENU_PREFIX=gnome-
XDG_SESSION_PATH=/org/freedesktop/DisplayManager/Session9
GJS_DEBUG_OUTPUT=stderr
HOME=/home/fdessoy-
FT_HOOK_NAME=login-user
QT_IM_MODULE=ibus
DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/5511/bus
TERMINATOR_UUID=urn:uuid:b5e2802d-9e7d-4e38-8e53-35bc38e9a11d
DOCKER_HOST=unix:///run/user/5511/docker.sock
SSH_AGENT_LAUNCHER=gnome-keyring
GTK_MODULES=gail:atk-bridge
XDG_DATA_DIRS=/usr/share/ubuntu:/usr/share/gnome:/home/fdessoy-/.local/share/flatpak/exports/share:/var/lib/flatpak/exports/share:/usr/local/share:/usr/share:/var/lib/snapd/desktop
GTK_IM_MODULE=ibus
JOURNAL_STREAM=8:2373313
XDG_SESSION_DESKTOP=ubuntu
KRB5CCNAME=FILE:/tmp/krb5cc_5511_3Gz3yH
GNOME_DESKTOP_SESSION_ID=this-is-deprecated
MANAGERPID=1150979
QT_ACCESSIBILITY=1
LOGNAME=fdessoy-
XDG_SEAT_PATH=/org/freedesktop/DisplayManager/Seat0
VTE_VERSION=6800
PATH=/home/fdessoy-/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
```

the last line is the PATH, I've taken out stuff from the environment to be able to fit everything together

```shell
%> env | grep SHLVL
2
```

Which means that you are in n shell level and you will compare later to check if you changed shell level, because we are going to execute the minishell in somewhere different.

Next step is to export and update the PATH:

```shell
%> pwd
/home/fdessoy-/projects/minishell
%> export PATH=/home/fdessoy-/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/home/fdessoy-/projects/minishell
```

The path before was:
`PATH=/home/fdessoy-/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin`

And now is:
`PATH=/home/fdessoy-/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/home/fdessoy-/projects/minishell`

We added the path to our minishell, which was:

`/home/fdessoy-/projects/minishell`  

Now, to test this you may want to do the following:

```shell
%> pwd
/home/fdessoy-/projects/minishell
%> cd
%> pwd
/home/fdessoy-
%> minishell
```

if you check your SHLVL with:

```shell
%> env | grep SHLVL
```

and you should get the value of n + 1 (n being the number of the SHLVL that you previously got when checking your SHLVL the first time.
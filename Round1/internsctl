#!/bin/bash


function display_help() {
    echo "Usage: internsctl [OPTIONS]"
    echo "Custom Linux Command for Operations"
    echo ""
    echo "Options:"
    echo "  --help   "
    echo "  --version "
    echo "  cpu getinfo "
    echo "  memory getinfo "
    echo "  Enter username: <username> Create a new user"
    echo "  user list "
    echo "  user list --sudo-only"
}


function display_version() {
    echo "internsctl v0.1.0"
}


function get_cpu_info() {
    lscpu
}
function get_memory_info() {
    free
}

function create_user() {
    if [ -z "$2" ]; then
        echo "Error: Missing username. Usage: internsctl user create <username>"
        exit 1
    fi

    sudo useradd -m "$2"
    echo "User '$2' created successfully."
}


function list_users() {
    cut -d: -f1 /etc/passwd
}


function list_sudo_users() {
    getent group sudo | cut -d: -f4 | tr ',' '\n'
}


case "$1" in
    --help)
        display_help
        ;;
    --version)
        display_version
        ;;
    cpu)
        if [ "$2" == "getinfo" ]; then
            get_cpu_info
        else
            echo "Invalid subcommand for 'cpu'. Use 'internsctl cpu getinfo'."
            exit 1
        fi
        ;;
    memory)
        if [ "$2" == "getinfo" ]; then
            get_memory_info
        else
            echo "Invalid subcommand for 'memory'. Use 'internsctl memory getinfo'."
            exit 1
        fi
        ;;
   user)
   if [ "$2" == "create" ]; then
            create_user "$@"
        elif [ "$2" == "list" ]; then
            if [ "$3" == "--sudo-only" ]; then
                list_sudo_users
            else
                list_users
            fi
        else
            echo "Invalid subcommand for 'user'. Use 'internsctl user create <username>' or 'internsctl user list [--sudo-only]'."
            exit 1
        fi
        ;;
    *)
        echo "Invalid option. Use 'internsctl --help' for usage guidelines."
        exit 1
        ;;
    
esac

#!/usr/bin/env bash

# William Killian
# 2014 March 18

configdir="${HOME}/.emacsconfig"
if ! [ -d "${configdir}" ]
then
    mkdir -p "${configdir}"
fi

function show_configs {
    pushd "${configdir}" > /dev/null
    ls | grep -v ^active$
    popd > /dev/null
}

function show_active {
    readlink "${configdir}/active" | sed "s:${configdir}/::g"
}

function show_help {
    echo "Emacs Configuration Manager!"
    echo ""
    echo "Usage:"
    echo "  $0 [flag]"
    echo ""
    echo "Flags:"
    echo " -h       - show help"
    echo " -i <tag> - initialize configuration manager and create configuration called <tag>"
    echo " -b <tag> - backup current configuration to <tag>"
    echo " -L       - list current configurations"
    echo " -a <tag> - make <tag> the active configuration"
    echo " -r <tag> - remove <tag>"
    echo ""
    echo "Note: only one flag is supported at a time"
    echo ""
}

function show_info {
    echo ""
    echo "Configurations:"
    show_configs
    echo ""
    echo "Active:"
    show_active
    echo ""
}

function show_everything {
    show_help
    show_info
}

function config_backup {
    dir="${configdir}/${@}"
    mkdir -p "${dir}"
    cp "${HOME}/.emacs" "${dir}/.emacs"
    cp -r "${HOME}/.emacs.d/" "${dir}/.emacs.d"
}

function config_activate {
    rm "${configdir}/active"
    ln -s "${configdir}/${@}" "${configdir}/active"
}

function config_remove {
    rm -rf "${configdir}/${@}"
}

function link_global {
    loc="${configdir}/active"
    rm -rf "${HOME}/.emacs" "${HOME}/.emacs.d"
    ln -s "${loc}/.emacs" "${HOME}/.emacs"
    ln -s "${loc}/.emacs.d" "${HOME}/.emacs.d"
}

args=$(getopt "hi:Lb:a:r:" "$@")
eval set -- "$args"
while [ $# -ge 1 ]; do
    case "$1" in
        --)
            shift
            break
            ;;
	-i)
            config_backup "$2"
            config_activate "$2"
            link_global
            exit 0
            ;;
	-b)
            config_backup "$2"
            exit 0
            ;;
	-L)
            show_info
            exit 0
            ;;
        -h)
            show_help
            exit 0
            ;;
	-a)
            config_activate "$2"
            exit 0
            ;;
	-r)
            config_remove "$2"
            exit 0
            ;;
    esac
    shift
done
show_everything

#!/bin/bash

set -e

get_kbdlayout() {
  layout=$(setxkbmap -query | grep -oP 'layout:\s*\K([\w,]+)')
  variant=$(setxkbmap -query | grep -oP 'variant:\s*\K(\w+)')
  echo "$layout" "$variant"
}

set_kbdlayout() {
  eval "array=($1)"
  setxkbmap "${array[@]}"
  pgrep i3status | xargs --no-run-if-empty kill -s USR1 # tell i3status to update
}

cycle() {
  current_layout=$(get_kbdlayout | xargs)
  layouts=("$@" "$1") # add the first one at the end so that it cycles
  index=0
  while [ "${layouts[$index]}" != "$current_layout" ] && [ $index -lt "${#layouts[@]}" ]; do index=$[index +1]; done
  next_index=$[index +1]
  next_layout=${layouts[$next_index]}
  set_kbdlayout "$next_layout"
}

i3status() {
  while :
  do
    read line
    block="{\"full_text\":\"$(get_kbdlayout)\"}"
    echo "${line/\[\{/\[$block,\{}"|| exit 1
  done
}

subcommand="$1"
shift || (echo "Please specify one of: get, set <layout>, cycle <layout1> <layout2> ... <layoutN>, i3status" && exit)

case $subcommand in
  "get")
    echo -n $(get_kbdlayout)
    ;;
  "set")
    set_kbdlayout "$1"
    ;;
  "cycle")
    cycle "$@"
    ;;
  "i3status")
    i3status
    ;;
esac




* Aliases
alias doom='~/.emacs.d/bin/doom'
alias node='docker run --rm -it -v ${PWD}:/app -w /app -u 1000:1000 node'
alias npm='docker run --rm -it -v ${PWD}:/app -w /app -u 1000:1000 node npm'
alias npx='docker run --rm -it -v ${PWD}:/app -w /app -u 1000:1000 node npx'
alias yarn='docker run --rm -it -v ${PWD}:/app -w /app -u 1000:1000 node yarn'
alias python='docker run --rm -it -v ${PWD}:/app -w /app -u 1000:1000 python python'
alias php='docker run --rm -it -v ${PWD}:/app -w /app -u 1000:1000 php php'

alias sitebuild-web-dev='docker run --rm -it -v ${PWD}:/app -w /app -u 1000:1000 -p 5173:5173 node yarn workspace run dev --host'
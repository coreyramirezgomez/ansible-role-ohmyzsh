ohmyzsh
=========

Install and configure ohmyzsh.

## Role Variables

See defaults/main.yml for all configurable variables.

## Example Playbook
```
    - hosts: macos
      roles:
        - role: crg.ohmyzsh
          ohmyzsh_custom_plugins:
            - repo: "https://github.com/zsh-users/zsh-autosuggestions.git"
              dest: "zsh-autosuggestions"
            - repo: "https://github.com/zsh-users/zsh-syntax-highlighting.git"
              dest: "zsh-syntax-highlighting"
          ohmyzsh_custom_themes:
            - repo: "https://github.com/romkatv/powerlevel10k.git"
              dest: "powerlevel10k"
              theme_names:
                - "powerlevel9k.zsh-theme"
                - "powerlevel10k.zsh-theme"
          ohmyzsh_theme: "powerlevel10k"
          ohmyzsh_theme_random_candidates:
            - "agnoster"
            - "avit"
            - "bira"
          ohmyzsh_case_sensitive: "true"
          ohmyzsh_hyphen_insensitive: "false"
          ohmyzsh_disable_auto_update: "false"
          ohmyzsh_disable_update_prompt: "true"
          ohmyzsh_update_zsh_days: 13
          ohmyzsh_disable_magic_functions: "true"
          ohmyzsh_disable_ls_colors: "false"
          ohmyzsh_disable_auto_title: "false"
          ohmyzsh_enable_correction: "true"
          ohmyzsh_completion_waiting_dots: "true"
          ohmyzsh_disable_untracked_files_dirty: "false"
          ohmyzsh_hist_stamps: "mm/dd/yyyy"
          ohmyzsh_custom_path: "{{ ansible_env.HOME }}/.oh-my-zsh/custom"
          ohmyzsh_plugins:
            - "zsh-autosuggestions" # Suggests commands based on history (https://github.com/zsh-users/zsh-autosuggestions)
            - "zsh-interactive-cd" # fish-shell-like cd prompt (https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/zsh-interactive-cd)
            - "zsh-syntax-highlighting" # fish-shell-like syntax-highlighting (https://github.com/zsh-users/zsh-syntax-highlighting)
          ohmyzsh_manpath: "/usr/local/man:$MANPATH"
          ohmyzsh_lang: "en_US.UTF-8"
          ohmyzsh_editor: "vim"
          ohmyzsh_disable_compfix: "true"
          ohmyzsh_shell_aliases:
            - alias: "clr"
              command: "clear"
            - alias: "du"
              command: "du -kh"
            - alias: "psg"
              command: "ps auwwwx | grep -v grep | grep"
          ohmyzsh_path_exports:
            - "$HOME/.bin"
            - "/usr/local/bin"
          ohmyzsh_shell_bindkeys:
            - key: '\033[1~'
              command: "beginning-of-line"
            - key: '\033[4~'
              command: "end-of-line"
            - key: "^[[1;3C"
              command: "forward-word"
            - key: "^[[1;3D"
              command: "backward-word"
          ohmyzsh_shell_exports:
            - name: "ZSH_COLORIZE_STYLE"
              value: "colorful"
          ohmyzsh_extra_configuration_head_blocks:
            - comment: "Enable Powerlevel10k instant prompt."
              content: |-
                if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]]; then
                  source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
                fi
              encapsulate: yes
          ohmyzsh_extra_configuration_tail_blocks:
            - comment: "Initialize pyenv"
              content: |-
                if [ -e "$HOME/.pyenv/.pyenvrc" ]; then
                  source $HOME/.pyenv/.pyenvrc
                  if [ -e "$HOME/.pyenv/completions/pyenv.zsh" ]; then
                    source $HOME/.pyenv/completions/pyenv.zsh
                  elif [ -e "/usr/local/opt/pyenv/completions/pyenv.zsh" ]; then
                    source /usr/local/opt/pyenv/completions/pyenv.zsh
                  fi
                fi
            - comment: "p10k configuration. To customize prompt, run `p10k configure` or edit ~/.p10k.zsh."
              content: "[[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh"
            - comment: "Hook direnv into shell if installed."
              content: '[ $(command -v direnv) ] && eval "$(direnv hook zsh)"'
          ohmyzsh_plugin_customizations:
            "disable tldr":
              line: "alias tldr='less'"
              path: "{{ ansible_env.HOME }}/.oh-my-zsh/plugins/lol/lol.plugin.zsh"
              state: absent
```
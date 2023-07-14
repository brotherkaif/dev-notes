# CHROMEOS: Enable NerdFonts

## Method

1. Open `chrosh` terminal with `ctrl-shift-t`
2. Open CSS inspector with `ctrl-alt-j`
3. Enter the following:

```
term_.prefs_.set('font-family', '"Hack", monospace');
term_.prefs_.set('user-css', 'https://cdn.jsdelivr.net/gh/icecream95/nerd-web-fonts@master/NerdFonts.css');
```

## References

- Blog Post: https://dev.to/davidmorais/customize-chrome-os-linux-terminal-3ame
- Nerd Web Fonts Repo: https://github.com/icecream95/nerd-web-fonts
- Powerline Fonts Repo: https://github.com/wernight/powerline-web-fonts
- CDN: https://github.com/wernight/powerline-web-fonts

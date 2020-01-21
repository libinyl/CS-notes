## flex

flex is keg-only, which means it was not symlinked into /usr/local,
because some formulae require a newer version of flex.

If you need to have flex first in your PATH run:
  echo 'export PATH="/usr/local/opt/flex/bin:$PATH"' >> ~/.zshrc

For compilers to find flex you may need to set:
  export LDFLAGS="-L/usr/local/opt/flex/lib"
  export CPPFLAGS="-I/usr/local/opt/flex/include"

macos 链接: -ll

linux 链接: -lfl
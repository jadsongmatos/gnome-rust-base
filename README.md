# gnome-rust-base

Esse é projeto exemplo

## Building

### Construindo com Flatpak + GNOME Builder

O Shortwave pode ser compilado e executado com o [GNOME Builder](https://wiki.gnome.org/Apps/Builder).
Basta clonar o repositório e clicar no botão Executar!

Você pode obter o Builder [aqui](https://wiki.gnome.org/Apps/Builder/Downloads).

### Construindo com flatpak-builder

1. `flatpak-builder --run build-dir org.gnome.Example.json`
2. `flatpak-builder --run build-dir org.gnome.Example.json ./build-dir/files/bin/gnome-rust-base`

### Construindo manualmente

1. `meson --prefix=/usr build-dir`
2. `ninja -C build-dir`
3. `./build-dir/files/bin/gnome-rust-base`

Para saber mais sobre as dependências necessárias, verifique o [manifesto Flatpak](org.gnome.Example.json).

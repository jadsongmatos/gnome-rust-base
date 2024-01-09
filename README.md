# gnome-rust-base

Um modelo padrão para começar com GTK, Rust, Meson, Flatpak feito para GNOME.

## Índice

- [Introdução](#introdução)
- [Pré-Requisitos](#pré-requisitos)
- [Construção](#construção)
  - [Com Flatpak + GNOME Builder](#com-flatpak--gnome-builder)
  - [Com flatpak-builder](#com-flatpak-builder)
  - [Manualmente](#manualmente)
- [Adicionando Suporte Multilíngue](#adicionando-suporte-multilíngue)
  - [Configuração Inicial](#configuração-inicial)
  - [Vinculando Texto da UI para Tradução](#vinculando-texto-da-ui-para-tradução)
  - [Processo de Tradução](#processo-de-tradução)
  - [Etapas Finais](#etapas-finais)
- [Solução de Problemas](#solução-de-problemas)
- [Contribuição](#contribuição)
- [Suporte e Contato](#suporte-e-contato)
- [Licença](#licença)
- [Changelog](#changelog)


## Building

### Construindo com Flatpak + GNOME Builder

O gnome-rust-base pode ser compilado e executado com o [GNOME Builder](https://wiki.gnome.org/Apps/Builder).

### Construindo com flatpak-builder

1. `flatpak-builder --user flatpak_app build-aux/org.gnome.Example.json`
2. `flatpak-builder --env=LC_ALL=pt_BR.UTF8 --run flatpak_app build-aux/org.gnome.Example.json gnome-rust-base`

### Construindo manualmente

1. `meson --prefix=/usr build-dir`
2. `ninja -C build-dir`
3. `ninja -C build-dir install`
4. `gnome-rust-base`

Para saber mais sobre as dependências necessárias, verifique o [manifesto Flatpak](org.gnome.Example.json).

## Adicionando suporte multilíngue no projeto GNOME Builder (Rust)

### Configuração inicial

1. **Gerar arquivo `.pot`:**
    - Use Meson para construir o projeto: `meson --prefix=/usr build-dir`
    - Gere o arquivo `.pot`: `ninja -C build/ gnome-rust-base-pot`
    - Isso cria `po/gnome-rust-base.pot`.

### Vinculando texto da UI para tradução

1. **Modificar arquivo UI:**
    - No arquivo `src/window.ui`, adicione `translatable=yes` à propriedade que vai ser traduzida.
      - Exemplo: `<property name="label" translatable="yes" >Hello, World!</property>`
    - Atualize o arquivo `.pot` novamente.

2. **Solução de problemas:**
    - Se o arquivo `.pot` não for criado, certifique-se de estar usando os comandos corretos e de ter feito as alterações necessárias no arquivo UI.

3. **Gere o arquivo `.pot` novamente:**
    - Comando: `ninja -C build gnome-rust-base-pot`.

### Processo de tradução

1. **Criar arquivo de idioma:**
    - Use `msginit` para criar um arquivo de tradução para o seu idioma de destino.
      - Exemplo: `msginit -l pt_BR --no-translator -i po/gnome-rust-base.pot -o po/pt_BR.po`
    - Traduza o arquivo `po/pt_BR.po` usando um editor de texto ou uma ferramenta especializada como gtranslator ou poedit.

2. **Atualizar arquivo `LINGUAS`:**
    - Adicione o novo código do idioma (por exemplo, `pt_BR`) ao arquivo `po/LINGUAS` em ordem alfabética.
    - Isto é importante para o script de compilação e instalação.

### Etapas Finais

- **Troca de idioma no aplicativo:**
  - A aplicação será exibida no idioma definido pela variável `LANG` do sistema.
  - Você pode forçar um idioma diferente definindo a variável `LC_ALL`, por exemplo, `LC_ALL=pt_BR.UTF8 your-program`.

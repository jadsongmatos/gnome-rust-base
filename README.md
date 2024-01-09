# gnome-rust-base

Um guia completo para iniciar projetos com GTK, Rust, Meson, e Flatpak no ambiente GNOME.

## Métodos de Construção

### Usando Flatpak e GNOME Builder

O gnome-rust-base pode ser compilado e executado facilmente através do [GNOME Builder](https://wiki.gnome.org/Apps/Builder).

### Usando flatpak-builder

1. `flatpak-builder --user flatpak_app build-aux/org.gnome.Example.json`
2. `flatpak-builder --env=LC_ALL=pt_BR.UTF8 --run flatpak_app build-aux/org.gnome.Example.json gnome-rust-base`

### Método Manual

1. `meson --prefix=/usr build-dir`
2. `ninja -C build-dir`
3. `ninja -C build-dir install`
4. `gnome-rust-base`

Para informações detalhadas sobre as dependências, consulte o [manifesto Flatpak](org.gnome.Example.json).

## Implementando Suporte a Múltiplos Idiomas no GNOME Builder (Rust)

### Configuração Inicial

1. **Criação do arquivo `.pot`:**
   - Construa o projeto com Meson: `meson --prefix=/usr build-dir`
   - Gere o arquivo `.pot`: `ninja -C build/ gnome-rust-base-pot`
   - Será criado em `po/gnome-rust-base.pot`.

### Preparando a UI para Tradução

1. **Alteração do arquivo UI:**
   - No arquivo `src/window.ui`, marque a propriedade a ser traduzida com `translatable=yes`.
     - Exemplo: `<property name="label" translatable="yes">Hello, World!</property>`
   - Atualize o arquivo `.pot`.

2. **Em caso de problemas:**
   - Verifique se todos os comandos foram executados corretamente e se as alterações no arquivo UI estão corretas.

3. **Regere o arquivo `.pot`:**
   - Comando: `ninja -C build gnome-rust-base-pot`.

### Processo de Tradução

1. **Criação do arquivo de idioma:**
   - Utilize `msginit` para gerar um arquivo de tradução para o idioma desejado.
     - Exemplo: `msginit -l pt_BR --no-translator -i po/gnome-rust-base.pot -o po/pt_BR.po`
   - Traduza o arquivo `po/pt_BR.po` com um editor de texto ou ferramenta especializada como gtranslator ou poedit.

2. **Atualização do arquivo `LINGUAS`:**
   - Adicione o novo código de idioma (exemplo: `pt_BR`) ao arquivo `po/LINGUAS` em ordem alfabética.
   - Isso é essencial para o processo de compilação e instalação.

### Conclusão e Testes

- **Alterando o idioma do aplicativo:**
  - O idioma do aplicativo corresponderá à variável `LANG` do sistema.
  - Para testar em um idioma específico, defina a variável `LC_ALL`, por exemplo, `LC_ALL=pt_BR.UTF8 gnome-rust-base`.
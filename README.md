# gnome-rust-base

A comprehensive guide for starting projects with GTK, Rust, Meson, and Flatpak in the GNOME environment, with a focus on implementing multiple language support.

## Building Methods

### Using Flatpak and GNOME Builder

gnome-rust-base can be easily compiled and run using [GNOME Builder](https://wiki.gnome.org/Apps/Builder).

### Using flatpak-builder

1. `flatpak-builder --user flatpak_app build-aux/org.gnome.Example.json`
2. `flatpak-builder --env=LC_ALL=pt_BR.UTF8 --run flatpak_app build-aux/org.gnome.Example.json gnome-rust-base`

### Manual Method

1. `meson --prefix=/usr build-dir`
2. `ninja -C build-dir`
3. `ninja -C build-dir install`
4. `gnome-rust-base`

For detailed information about dependencies, see the [Flatpak manifest](org.gnome.Example.json).

## Implementing Multiple Language Support in GNOME Builder (Rust)

### Initial Setup

1. **Creating the `.pot` File:**
    - Build the project with Meson: `meson --prefix=/usr build-dir`
    - Generate the `.pot` file: `ninja -C build/ gnome-rust-base-pot`
    - The file will be created at `po/gnome-rust-base.pot`.

### Preparing the UI for Translation

1. **UI File Changes:**
    - In `src/window.ui`, mark properties for translation with `translatable=yes`.
      - Example: `<property name="label" translatable="yes">Hello, World!</property>`
    - Update the `.pot` file.

2. **Troubleshooting:**
    - Ensure all commands were executed correctly and that changes to the UI file are correct.

3. **Regenerate the `.pot` File:**
    - Command: `ninja -C build gnome-rust-base-pot`.

### Translation Process

1. **Creating Language Files:**
    - Use `msginit` to generate a translation file for the desired language.
      - Example: `msginit -l pt_BR --no-translator -i po/gnome-rust-base.pot -o po/pt_BR.po`
    - Translate the `po/pt_BR.po` file using a text editor or specialized tool like gtranslator or poedit.

2. **Updating the `LINGUAS` File:**
    - Add the new language code (e.g., `pt_BR`) to the `po/LINGUAS` file in alphabetical order.
    - This step is crucial for the compilation and installation process.

### Conclusion and Testing

- **Changing the Application Language:**
  - The application's language will match the system's `LANG` variable.
  - To test in a specific language, set the `LC_ALL` variable, e.g., `LC_ALL=pt_BR.UTF8 gnome-rust-base`.

---

Special thanks to [Rafael Fontenelle](https://github.com/rffontenelle) for assisting in understanding how to implement multiple languages in GNOME.

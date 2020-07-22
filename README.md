# ChemMine Tools Documentation

Documentation for [ChemMine Tools](https://github.com/girke-lab/chemminetools). Uses [Jekyll Doc Theme](https://aksakalli.github.io/jekyll-doc-theme/). See `jekyll-doc-theme-readme.md` for the original `README.md`.

## Running Locally

Install Ruby and Bundler, if not already so. This will vary depending on your operating system:

```
# Debian, Ubuntu
apt install ruby bundler

# Arch Linux
pacman -S ruby ruby-bundler

```

Clone the documentation:

```
git clone https://github.com/girke-lab/chemminetools-docs.git
cd chemminetools-docs
```

Set the local configuration to install Ruby packages within `chemminetools-docs/vendor/bundle`:

```
bundle config set --local path vendor/bundle
```

Install Jekyll and dependencies:

```
bundle install
```

At this point you should have a fully configured workspace. To run a local Jekyll server:

```
bundle exec jekyll serve
```

# Archive management

- [tar](#tar)
- [zip](#zip)

## tar

- List the content of an archive:

  ```sh
  tar -tf filename.tar.gz
  ```

  The `-f` (file) option lets `tar` knows that we are dealing with a file.

- Extract the content of an archive in the current directory:

  ```sh
  tar -xzvf filename.tar.gz
  ```

  The `-v` (verbose) option lists the extracted files.

## zip

- Create an archive from a folder:

  ```sh
  zip -r archive-name.zip folder-name
  ```

- List the content of an archive:

  ```sh
  unzip -l filename.zip
  ```

# files-publish-action
Simple github action to publish files in a server. This action assumes that all the files have been uploaded through upload-artifact v4 action.

I made this following this guide :
https://docs.github.com/en/actions/creating-actions/creating-a-composite-action

**Important**:
- Only support **Linux** Github runner. But if you want to publish from a **Windows** or **Mac** runner, the idea is to build under **Windows**/**Mac** and publish under **Linux** using this action (see usage).
- This action removes any previous existing files in the destination path of the server
- Artifacts are uploaded/downloaded using v4 version of upload-artifact and download-artifact Github actions

## Requirements
- A local or a web server
- The server must accept SSH connections

## Input variables
* ```host``` - Server where you can execute SSH commands
* ```username``` - Username for SSH connection
* ```password:``` - Password for SSH connection
* ```dest-path``` - Full path to destination folder in the server
* ```pattern``` - File name pattern filter (default = "*")

## Usage
TODO

            echo "MY_PKG=$PKG_PATH" | Out-File -FilePath $Env:GITHUB_ENV -Encoding utf8 -Append
    
        - uses: actions/upload-artifact@v4
          # Use specific artifact identifier for publishing all R versions
          with:
            name: windows-package-${{matrix.r_version}}
            path: ${{ env.MY_PKG }}
            
        
      publish:
        needs: build
        # Only ubuntu can upload via ssh
        runs-on: ubuntu-latest
        
        steps:
        - uses: fabien-ors/cran-publish-action@v9
          with:
            host: ${{ secrets.CRAN_HOST }}
            username: ${{ secrets.CRAN_USR }}
            password: ${{ secrets.CRAN_PWD }}
            repo-path: "/path/to/cran/on/the/server"



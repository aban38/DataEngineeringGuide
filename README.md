### Q: I have redhat enterprise edition installled
how to install sqlcmd on separate path, not on system path without letting it interfere with system package?  

### Ans:  

To install `sqlcmd` on a separate path without interfering with the system packages on Red Hat Enterprise Linux (RHEL), you can follow these steps:

1. **Download the Microsoft repository configuration**:
   ```sh
   sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/8/prod.repo
   ```

2. **Create a separate directory for `sqlcmd`**:
   ```sh
   mkdir -p ~/sqlcmd-tools
   ```

3. **Download and extract the `mssql-tools` package**:
   - First, download the `mssql-tools` package without installing it:
     ```sh
     sudo yum install --downloadonly --downloaddir=~/sqlcmd-tools mssql-tools unixODBC-devel
     ```

   - Extract the downloaded RPM packages:
     ```sh
     cd ~/sqlcmd-tools
     rpm2cpio mssql-tools-*.rpm | cpio -idmv
     rpm2cpio unixODBC-devel-*.rpm | cpio -idmv
     ```

4. **Add the `sqlcmd` binary to your custom path**:
   - Add the custom path to your `.bashrc` or `.bash_profile`:
     ```sh
     echo 'export PATH="$PATH:$HOME/sqlcmd-tools/opt/mssql-tools/bin"' >> ~/.bashrc
     source ~/.bashrc
     ```

5. **Verify the installation**:
   - Check if `sqlcmd` is available in your custom path:
     ```sh
     which sqlcmd
     sqlcmd -?
     ```

By following these steps, you will have `sqlcmd` installed in a separate directory (`~/sqlcmd-tools`) and added to your custom path without interfering with the system packages.

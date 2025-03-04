RPM 和 DEB 是 Linux 系统下常见的两种安装包格式，本文介绍如何使用 RPM 或 DEB 文件在一台机器上快速安装 NebulaGraph。

!!! note

    部署 NebulaGraph 集群的方式参见[使用 RPM/DEB 包部署集群](https://docs.nebula-graph.com.cn/{{nebula.release}}/4.deployment-and-installation/2.compile-and-install-nebula-graph/deploy-nebula-graph-cluster/)。<!--这里用外链。-->

{{ ent.ent_begin }}
!!! enterpriseonly

    企业版请[联系我们](https://www.nebula-graph.com.cn/contact)。

{{ ent.ent_end }}

## 前提条件

安装 wget

## 下载安装包

### 阿里云 OSS 下载

- 下载 release 版本

    URL 格式如下：

    ```bash
    //Centos 7
    https://oss-cdn.nebula-graph.com.cn/package/<release_version>/nebula-graph-<release_version>.el7.x86_64.rpm

    //Centos 8
    https://oss-cdn.nebula-graph.com.cn/package/<release_version>/nebula-graph-<release_version>.el8.x86_64.rpm

    //Ubuntu 1604
    https://oss-cdn.nebula-graph.com.cn/package/<release_version>/nebula-graph-<release_version>.ubuntu1604.amd64.deb

    //Ubuntu 1804
    https://oss-cdn.nebula-graph.com.cn/package/<release_version>/nebula-graph-<release_version>.ubuntu1804.amd64.deb

    //Ubuntu 2004
    https://oss-cdn.nebula-graph.com.cn/package/<release_version>/nebula-graph-<release_version>.ubuntu2004.amd64.deb
    ```

    例如要下载适用于`Centos 7.5`的`{{ nebula.release }}`安装包：

    ```bash
    wget https://oss-cdn.nebula-graph.com.cn/package/{{ nebula.release }}/nebula-graph-{{ nebula.release }}.el7.x86_64.rpm
    wget https://oss-cdn.nebula-graph.com.cn/package/{{ nebula.release }}/nebula-graph-{{ nebula.release }}.el7.x86_64.rpm.sha256sum.txt
    ```

    下载适用于`ubuntu 1804`的`{{ nebula.release }}`安装包：
    ```bash
    wget https://oss-cdn.nebula-graph.com.cn/package/{{ nebula.release }}/nebula-graph-{{ nebula.release }}.ubuntu1804.amd64.deb
    wget https://oss-cdn.nebula-graph.com.cn/package/{{ nebula.release }}/nebula-graph-{{ nebula.release }}.ubuntu1804.amd64.deb.sha256sum.txt
    ```

- 下载日常开发版本 (nightly)

  !!! danger
  
      - nightly 版本通常用于测试新功能、新特性，请**不要**在生产环境中使用 nightly 版本。
      - nightly 版本不保证每日都能完整发布，也不保证是否会更改文件名。

    URL 格式如下：

    ```bash
    //Centos 7
    https://oss-cdn.nebula-graph.com.cn/package/nightly/<yyyy.mm.dd>/nebula-graph-<yyyy.mm.dd>-nightly.el7.x86_64.rpm

    //Centos 8
    https://oss-cdn.nebula-graph.com.cn/package/nightly/<yyyy.mm.dd>/nebula-graph-<yyyy.mm.dd>-nightly.el8.x86_64.rpm

    //Ubuntu 1604
    https://oss-cdn.nebula-graph.com.cn/package/nightly/<yyyy.mm.dd>/nebula-graph-<yyyy.mm.dd>-nightly.ubuntu1604.amd64.deb

    //Ubuntu 1804
    https://oss-cdn.nebula-graph.com.cn/package/nightly/<yyyy.mm.dd>/nebula-graph-<yyyy.mm.dd>-nightly.ubuntu1804.amd64.deb

    //Ubuntu 2004
    https://oss-cdn.nebula-graph.com.cn/package/nightly/<yyyy.mm.dd>/nebula-graph-<yyyy.mm.dd>-nightly.ubuntu2004.amd64.deb
    ```

    例如要下载`2021.11.24`适用于`Centos 7.5`的`2.x`安装包：

    ```bash
    wget https://oss-cdn.nebula-graph.com.cn/package/nightly/2021.11.24/nebula-graph-2021.11.24-nightly.el7.x86_64.rpm
    wget https://oss-cdn.nebula-graph.com.cn/package/nightly/2021.11.24/nebula-graph-2021.11.24-nightly.el7.x86_64.rpm.sha256sum.txt
    ```

    要下载`2021.11.24`适用于`Ubuntu 1804`的`2.x`安装包：
    ```bash
    wget https://oss-cdn.nebula-graph.com.cn/package/nightly/2021.11.24/nebula-graph-2021.11.24-nightly.ubuntu1804.amd64.deb
    wget https://oss-cdn.nebula-graph.com.cn/package/nightly/2021.11.24/nebula-graph-2021.11.24-nightly.ubuntu1804.amd64.deb.sha256sum.txt
    ```

<!--
### GitHub 下载

- 下载 release 版本

   + 登录 [NebulaGraph Releases](https://github.com/vesoft-inc/nebula/releases) 页面，确认需要的版本，单击** Assets**。

   ![Select a NebulaGraph release version](https://github.com/vesoft-inc/nebula-docs/raw/master/docs-2.0/figs/4.deployment-and-installation/2.complie-and-install-nebula-graph/2.install-nebula-graph-by-rpm-or-deb/releases-page.png?raw=true)

   + 在** Assets **区域找到机器运行所需的安装包，下载文件到机器上。

- 下载 nightly 版本

    >**禁止**：nightly 版本通常用于测试新功能、新特性，请**不要**在生产环境中使用 nightly 版本。

   + 登录 [NebulaGraph package](https://github.com/vesoft-inc/nebula/actions/workflows/package.yaml) 页面，单击顶部最新的** package**。

   ![Select a NebulaGraph nightly version](https://github.com/vesoft-inc/nebula-docs/raw/master/docs-2.0/figs/4.deployment-and-installation/2.complie-and-install-nebula-graph/2.install-nebula-graph-by-rpm-or-deb/nightly-page.png?raw=true)

   + 在** Artifacts **区域找到机器运行所需的安装包，下载文件到机器上。
-->

## 安装 NebulaGraph

- 安装 RPM 包

  ```bash
  $ sudo rpm -ivh --prefix=<installation_path> <package_name>
  ```
  
  `--prefix`为可选项，用于指定安装路径。如不设置，系统会将 NebulaGraph 安装到默认路径`/usr/local/nebula/`。

  例如，要在默认路径下安装{{nebula.release}}版本的 RPM 包，运行如下命令：

  ```bash
  sudo rpm -ivh nebula-graph-{{nebula.release}}.el7.x86_64.rpm
  ``` 

- 安装 DEB 包

  ```bash
  $ sudo dpkg -i <package_name>
  ```

  !!! note
        使用 DEB 包安装 NebulaGraph 时不支持自定义安装路径。默认安装路径为`/usr/local/nebula/`。

  例如安装{{nebula.release}}版本的 DEB 包：

  ```bash
  sudo dpkg -i nebula-graph-{{nebula.release}}.ubuntu1804.amd64.deb
  ```

## 后续操作

{{ ent.ent_begin }}
- （企业版）[设置 License](https://docs.nebula-graph.com.cn/{{nebula.release}}/4.deployment-and-installation/deploy-license)

{{ ent.ent_end }}

- [启动 NebulaGraph](https://docs.nebula-graph.com.cn/{{nebula.release}}/2.quick-start/5.start-stop-service/)<!--这里用外链。-->
- [连接 NebulaGraph](https://docs.nebula-graph.com.cn/{{nebula.release}}/2.quick-start/3.connect-to-nebula-graph/)<!--这里用外链。-->

---
title: Diretrizes de instalação para SQL Server em Linux
titleSuffix: SQL Server
description: Instale, atualize e desinstale o SQL Server em Linux. Este artigo aborda cenários online, offline e autônomos.
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sqlfreshmay19
ms.technology: linux
ms.assetid: 565156c3-7256-4e63-aaf0-884522ef2a52
ms.openlocfilehash: a6cd31b1f67d37f1316db9db5d4356bbb5e31d3b
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593662"
---
# <a name="installation-guidance-for-sql-server-on-linux"></a>Diretrizes de instalação para SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo fornece diretrizes para instalar, atualizar e desinstalar o SQL Server 2017 e o SQL Server 2019 no Linux.

Para ver outros cenários de implantação, confira:

- [Windows](../database-engine/install-windows/install-sql-server.md)
- [Contêineres do Docker](../linux/sql-server-linux-configure-docker.md)
- [Kubernetes – Clusters de Big Data](../big-data-cluster/deploy-get-started.md)

> [!TIP]
> Este guia cobre vários cenários de implantação. Se você estiver procurando apenas instruções de instalação passo a passo, vá para um dos guias de início rápido:
> - [Início rápido do RHEL](quickstart-install-connect-red-hat.md)
> - [Início rápido do SLES](quickstart-install-connect-suse.md)
> - [Início rápido do Ubuntu](quickstart-install-connect-ubuntu.md)
> - [Início rápido do Docker](quickstart-install-connect-docker.md)

Para obter respostas a perguntas frequentes, confira as [Perguntas frequentes sobre o SQL Server em Linux](../linux/sql-server-linux-faq.md).

## <a id="supportedplatforms"></a> Plataformas compatíveis

O SQL Server é compatível com o Red Hat Enterprise Linux (RHEL), o SUSE Linux Enterprise Server (SLES) e o Ubuntu. Também tem suporte como uma imagem do Docker, que pode ser executada em um Mecanismo do Docker em Linux ou Docker for Windows/Mac.

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

| Plataforma | Versões compatíveis | Obter
|-----|-----|-----
| **Red Hat Enterprise Linux** | 7.3, 7.4, 7.5, 7.6 | [Obter RHEL 7.6](https://access.redhat.com/products/red-hat-enterprise-linux/evaluation)
| **SUSE Linux Enterprise Server** | v12 SP2 | [Obter o SLES v12 SP2](https://www.suse.com/products/server)
| **Ubuntu** | 16.04 | [Obter o Ubuntu 16.04](http://releases.ubuntu.com/xenial/)
| **Mecanismo do Docker** | 1.8+ | [Obter o Docker](https://www.docker.com/get-started)

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

| Plataforma | Versões compatíveis | Obter
|-----|-----|-----
| **Red Hat Enterprise Linux** | 7.3, 7.4, 7.5, 7.6 | [Obter RHEL 7.6](https://access.redhat.com/products/red-hat-enterprise-linux/evaluation)
| **SUSE Linux Enterprise Server** | v12 SP2, SP3, SP4 | [Obter o SLES v12](https://www.suse.com/products/server)
| **Ubuntu** | 16.04 | [Obter o Ubuntu 16.04](http://releases.ubuntu.com/xenial/)
| **Mecanismo do Docker** | 1.8+ | [Obter o Docker](https://www.docker.com/get-started)

::: moniker-end

A Microsoft também dá suporte para implantar e gerenciar contêineres do SQL Server usando o OpenShift e o Kubernetes.

> [!NOTE]
> O SQL Server é testado e compatível no Linux para as distribuições listadas anteriormente. Se você optar por instalar o SQL Server em um sistema operacional sem suporte, examine a seção **Política de suporte** da [Política de suporte técnico para Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server) para entender as implicações de suporte.

## <a id="system"></a> Requisitos do sistema

O SQL Server tem os seguintes requisitos de sistema para o Linux:

|||
|-----|-----|
| **Memória** | 2 GB |
| **Sistema de Arquivos** | **XFS** ou **EXT4** (outros sistemas de arquivos, como **BTRFS**, não têm suporte) |
| **Espaço em Disco** | 6 GB |
| **Velocidade do processador** | 2 GHz |
| **Núcleos de processador** | 2 núcleos |
| **Tipo de processador** | Compatível somente com x64 |

Se você usar compartilhamentos remotos **NFS (Network File System)** em produção, observe os seguintes requisitos de suporte:

- Use o NFS versão **4.2 ou superior**. As versões mais antigas do NFS não dão suporte aos recursos necessários, como fallocate e criação de arquivos esparsos, comuns aos sistemas de arquivos modernos.
- Localize somente os diretórios **/var/opt/mssql** na montagem NFS. Não há suporte para outros arquivos, como os binários do sistema SQL Server.
- Verifique se os clientes NFS usam a opção 'nolock' ao montar o compartilhamento remoto.

## <a id="repositories"></a> Configurar repositórios de origem

Ao instalar ou atualizar o SQL Server, você obtém a versão mais recente do SQL Server de seu repositório Microsoft configurado. Os guias de início rápido usam o repositório **CU** (Atualização Cumulativa) para o SQL Server. Porém, em vez disso, você pode configurar um repositório de **GDR**. Para obter mais informações sobre repositórios e como configurá-los, confira [Configurar repositórios para SQL Server em Linux.](sql-server-linux-change-repo.md)

## <a id="platforms"></a> Instalar o SQL Server

Você pode instalar o SQL Server 2017 ou o SQL Server 2019 no Linux por meio da linha de comando. Para obter instruções passo a passo, veja um dos seguintes guias de início rápido:

| Plataforma | Guias de início rápido de instalação |
|---|---|
| Red Hat Enterprise Linux (RHEL) | [2017](quickstart-install-connect-red-hat.md?view=sql-server-2017) \| [2019](quickstart-install-connect-red-hat.md?view=sql-server-linux-ver15) |
| SUSE Linux Enterprise Server (SLES) | [2017](quickstart-install-connect-suse.md?view=sql-server-2017) \| [2019](quickstart-install-connect-suse.md?view=sql-server-linux-ver15) |
| Ubuntu | [2017](quickstart-install-connect-ubuntu.md?view=sql-server-2017) \| [2019](quickstart-install-connect-ubuntu.md?view=sql-server-linux-ver15) |
| Docker | [2017](quickstart-install-connect-docker.md?view=sql-server-2017) \| [2019](quickstart-install-connect-docker.md?view=sql-server-linux-ver15) |

Você também pode executar o SQL Server em Linux em uma máquina virtual do Azure. Para obter mais informações, confira [Provisionar uma VM do SQL no Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json).

Após a instalação, considere fazer alterações de configuração adicionais para obter um desempenho ideal. Para obter mais informações, confira [Práticas recomendadas de desempenho e diretrizes de configuração do SQL Server em Linux](sql-server-linux-performance-best-practices.md).

## <a id="upgrade"></a> Atualizar ou fazer upgrade do SQL Server

Para atualizar o pacote **mssql-server** para a versão mais recente, use um dos seguintes comandos com base em sua plataforma:

| Plataforma | Comando(s) de atualização de pacote |
|-----|-----|
| RHEL | `sudo yum update mssql-server` |
| SLES | `sudo zypper update mssql-server` |
| Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server` |

Esses comandos baixam o pacote mais recente e substituem os binários localizados em `/opt/mssql/`. Os bancos de dados gerados pelo usuário e os bancos de dados do sistema não são afetados por essa operação.

Para atualizar o SQL Server, primeiro [altere o repositório configurado](sql-server-linux-change-repo.md) para a versão desejada do SQL Server. Em seguida, use o mesmo comando **update** para atualizar sua versão do SQL Server. Isso será possível apenas se o caminho de atualização for compatível entre os dois repositórios.

## <a id="rollback"></a> Reverter o SQL Server

Para reverter ou fazer downgrade do SQL Server para uma versão anterior, use as seguintes etapas:

1. Identifique o número de versão do pacote do SQL Server para o qual você deseja fazer downgrade. Para obter uma lista de números de pacote, confira as [Notas sobre a versão](../linux/sql-server-linux-release-notes.md).

1. Faça o downgrade para uma versão anterior do SQL Server. Nos comandos a seguir, substitua `<version_number>` pelo número de versão do SQL Server que você identificou na etapa um.

   | Plataforma | Comando(s) de atualização de pacote |
   |-----|-----|
   | RHEL | `sudo yum downgrade mssql-server-<version_number>.x86_64` |
   | SLES | `sudo zypper install --oldpackage mssql-server=<version_number>` |
   | Ubuntu | `sudo apt-get install mssql-server=<version_number>`<br/>`sudo systemctl start mssql-server` |

> [!NOTE]
> Só há suporte para fazer downgrade para uma liberação dentro da mesma versão principal, como SQL Server 2019.

## <a id="versioncheck"></a> Verificar a versão do SQL Server instalada

Para verificar a versão e a edição atuais do SQL Server em Linux, siga este procedimento:

1. Se ainda não estiverem instaladas, instale as [ferramentas de linha de comando do SQL Server](sql-server-linux-setup-tools.md).

1. Use o **sqlcmd** para executar um comando Transact-SQL que exibe sua versão e sua edição do SQL Server.

   ```bash
   sqlcmd -S localhost -U SA -Q 'select @@VERSION'
   ```

## <a id="uninstall"></a> Desinstalar o SQL Server

Para remover o pacote **mssql-server** no Linux, use um dos seguintes comandos com base em sua plataforma:

| Plataforma | Comando(s) de remoção de pacote |
|-----|-----|
| RHEL | `sudo yum remove mssql-server` |
| SLES | `sudo zypper remove mssql-server` |
| Ubuntu | `sudo apt-get remove mssql-server` |

A remoção do pacote não exclui os arquivos de banco de dados gerados. Se você quiser excluir os arquivos de banco de dados, use o seguinte comando:

```bash
sudo rm -rf /var/opt/mssql/
```

## Instalação autônoma <a id="unattended"></a>

Você pode executar uma instalação autônoma da seguinte maneira:

- Siga as etapas iniciais nos [guias de início rápido](#platforms) para registrar os repositórios e instalar o SQL Server.
- Ao executar o `mssql-conf setup`, defina as [variáveis de ambiente](sql-server-linux-configure-environment-variables.md) e use a opção `-n` (sem prompt).

O exemplo a seguir configura a edição Developer do SQL Server com a variável de ambiente **MSSQL_PID**. Ele também aceita o EULA (**ACCEPT_EULA**) e define a senha de usuário SA (**MSSQL_SA_PASSWORD**). O parâmetro `-n` executa uma instalação não solicitada em que os valores de configuração são extraídos das variáveis de ambiente.

```bash
sudo MSSQL_PID=Developer ACCEPT_EULA=Y MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' /opt/mssql/bin/mssql-conf -n setup
```

Você também pode criar um script que executa outras ações. Por exemplo, você pode instalar outros pacotes do SQL Server.

Para obter um script de exemplo mais detalhado, confira os exemplos a seguir:

- [Script de instalação autônoma do Red Hat](sample-unattended-install-redhat.md)
- [Script de instalação autônoma do SUSE](sample-unattended-install-suse.md)
- [Script de instalação autônoma do Ubuntu](sample-unattended-install-ubuntu.md)

## Instalação offline do <a id="offline"></a>

Se o computador Linux não tiver acesso aos repositórios online usados nos [guias de início rápido](#platforms), você poderá baixar os arquivos de pacote diretamente. Esses pacotes estão localizados no repositório da Microsoft, [https://packages.microsoft.com](https://packages.microsoft.com).

> [!TIP]
> Se tiver realizado a instalação com êxito seguindo as etapas nos guias de início rápido, não será necessário baixar ou instalar manualmente os pacotes do SQL Server. Esta seção vale apenas para o cenário offline.

1. **Baixe o pacote do mecanismo de banco de dados para sua plataforma**. Encontre links para baixar o pacote na seção detalhes do pacote das [Notas sobre a versão](../linux/sql-server-linux-release-notes.md).

1. **Mova o pacote baixado para o computador Linux**. Se você usou um computador diferente para baixar os pacotes, uma maneira de mover os pacotes para o computador Linux é com o comando **scp**.

1. **Instale o pacote do mecanismo de banco de dados**. Use um dos comandos a seguir com base em sua plataforma. Substitua o nome do arquivo de pacote neste exemplo pelo nome exato que você baixou.

   | Plataforma | Comando de instalação de pacote |
   |-----|-----|
   | RHEL | `sudo yum localinstall mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `sudo zypper install mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `sudo dpkg -i mssql-server_versionnumber_amd64.deb` |

    > [!NOTE]
    > Você também pode instalar os pacotes RPM (RHEL e SLES) com o comando `rpm -ivh`, mas os comandos na tabela anterior instalam dependências automaticamente, se disponíveis de repositórios aprovados.

1. **Resolver dependências ausentes**: Você pode ter dependências ausentes neste momento. Caso contrário, você pode ignorar esta etapa. No Ubuntu, se você tiver acesso a repositórios aprovados que contenham essas dependências, a solução mais fácil será usar o comando `apt-get -f install`. Esse comando também conclui a instalação do SQL Server. Para inspecionar dependências manualmente, use os seguintes comandos:

   | Plataforma | Comando de listar dependências |
   |-----|-----|
   | RHEL | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `dpkg -I mssql-server_versionnumber_amd64.deb` |

   Depois de resolver as dependências ausentes, tente instalar o pacote mssql-server outra vez.

1. **Conclua a instalação do SQL Server**. Use **mssql-conf** para concluir a configuração do SQL Server:

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

## <a name="licensing-and-pricing"></a>Licenciamento e preços

O SQL Server é licenciado da mesma forma para Linux e Windows. Para obter mais informações sobre licenciamento e preços do SQL Server, confira [Como licenciar o SQL Server](https://www.microsoft.com/sql-server/sql-server-2017-pricing).

## <a name="optional-sql-server-features"></a>Recursos opcionais do SQL Server

Após a instalação, você também pode instalar ou habilitar recursos opcionais do SQL Server.

- [Ferramentas de linha de comando do SQL Server](sql-server-linux-setup-tools.md)
- [SQL Server Agent](sql-server-linux-setup-sql-agent.md)
- [Pesquisa de Texto Completo do SQL Server](sql-server-linux-setup-full-text-search.md)
- [Serviços de Machine Learning (R, Python)](sql-server-linux-setup-machine-learning.md)
- [SQL Server Integration Services](sql-server-linux-setup-ssis.md)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

> [!TIP]
> Para obter respostas a perguntas frequentes, confira as [Perguntas frequentes sobre o SQL Server em Linux](sql-server-linux-faq.md).

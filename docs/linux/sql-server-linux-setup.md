---
title: Instalar o SQL Server de 2017 no Linux | Microsoft Docs
description: "Instalar, atualizar e desinstalar o SQL Server no Linux. Este tópico abrange cenários autônomos online e offline."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 08/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 565156c3-7256-4e63-aaf0-884522ef2a52
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: c5bd1be5cbe08e9454b1640d9dd58584aa54955f
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="installation-guidance-for-sql-server-on-linux"></a>Orientação de instalação do SQL Server no Linux

Este tópico explica como instalar, atualizar e desinstalar o SQL Server 2017 no Linux. SQL Server 2017 RC2 tem suporte no Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server (SLES) e Ubuntu. Ele também está disponível como uma imagem do Docker, que pode ser executado no mecanismo do Docker no Linux ou o Docker para Windows/Mac.

> [!TIP]
> Para começar rapidamente, ir para um dos tutoriais do início rápido para [RHEL](quickstart-install-connect-red-hat.md), [SLES](quickstart-install-connect-suse.md), [Ubuntu](quickstart-install-connect-ubuntu.md), ou [Docker](quickstart-install-connect-docker.md).

## <a id="supportedplatforms"></a>Plataformas com suporte

Há suporte para o SQL Server 2017 nas seguintes plataformas Linux:

| Plataforma | Versões com suporte | Obter
|-----|-----|-----
| **Red Hat Enterprise Linux** | 7.3 | [Obter RHEL 7.3](http://access.redhat.com/products/red-hat-enterprise-linux/evaluation)
| **SUSE Linux Enterprise Server** | SP2 v12 | [Obter SLES v12 SP2](https://www.suse.com/products/server)
| **Ubuntu** | 16.04 | [Obter Ubuntu 16.04](http://www.ubuntu.com/download/server)
| **Mecanismo do docker** | 1.8+ | [Obter o Docker](http://www.docker.com/products/overview)

## <a id="system"></a>Requisitos do sistema

SQL Server 2017 tem os seguintes requisitos de sistema para Linux:

|||
|-----|-----|
| **Memória** | 3,25 GB |
| **Sistema de Arquivos** | **XFS** ou **EXT4** (outros sistemas de arquivos, como **BTRFS**, não têm suporte) |
| **Espaço em disco** | 6 GB |
| **Velocidade do processador** | 2 GHz |
| **Núcleos de processador** | 2 núcleos |
| **Tipo de processador** | compatível x64 somente |

> [!NOTE]
> Mecanismo do SQL Server foi testado até 1 TB de memória no momento.

## <a id="platforms"></a>Instalar o SQL Server

Você pode instalar o SQL Server no Linux na linha de comando. Para obter instruções, consulte um dos seguintes tutoriais de início rápido:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)

## <a id="upgrade"></a>Atualize o SQL Server

Para atualizar o **mssql server** pacote no Linux, use um dos comandos a seguir com base em sua plataforma:

| Plataforma | Comando de atualização de pacote |
|-----|-----|
| RHEL | `sudo yum update mssql-server` |
| SLES | `sudo zypper update mssql-server` |
| Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server` |

Esses comandos baixar o pacote mais recente e substitua os binários localizados em `/opt/mssql/`. O usuário gerou bancos de dados e bancos de dados do sistema não são afetados por essa operação.

## <a id="uninstall"></a>Desinstalar o SQL Server

Para remover o **mssql server** pacote no Linux, use um dos comandos a seguir com base em sua plataforma:

| Plataforma | Comando de remoção do pacote |
|-----|-----|
| RHEL | `sudo yum remove mssql-server` |
| SLES | `sudo zypper remove mssql-server` |
| Ubuntu | `sudo apt-get remove mssql-server` |

A remoção do pacote não exclui os arquivos de banco de dados gerado. Se você deseja excluir os arquivos de banco de dados, use o seguinte comando:

```bash
sudo rm -rf /var/opt/mssql/
```

## <a id="unattended"></a>Instalação autônoma

Você pode executar uma instalação autônoma da seguinte maneira:

- Siga etapas inicial de [tutoriais de início rápido](#platforms) para registrar os repositórios e instalar o SQL Server.
- Quando você executa `mssql-conf setup`, defina [variáveis de ambiente](sql-server-linux-configure-environment-variables.md) e usar o `-n` (nenhum prompt) opção.

O exemplo a seguir configura a edição de desenvolvedor do SQL Server com o **MSSQL_PID** variável de ambiente. Ele também aceita o EULA (**ACCEPT_EULA**) e define a senha do usuário (**MSSQL_SA_PASSWORD**). O `-n` parâmetro executa uma instalação unprompted onde os valores de configuração são extraídos de variáveis de ambiente.

```bash
sudo MSSQL_PID=Developer ACCEPT_EULA=Y MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' /opt/mssql/bin/mssql-conf -n setup
```

Você também pode criar um script que executa outras ações. Por exemplo, você pode instalar outros pacotes do SQL Server.

Para um script de exemplo mais detalhado, consulte os exemplos a seguir:

- [Red Hat script de instalação autônoma](sample-unattended-install-redhat.md)
- [SUSE script de instalação autônoma](sample-unattended-install-suse.md)
- [Ubuntu script de instalação autônoma](sample-unattended-install-ubuntu.md)

## <a id="offline"></a>Instalação offline

Se o computador Linux não tem acesso aos repositórios online usados no [inícios rápidos](#platforms), você pode baixar os arquivos de pacote diretamente. Esses pacotes estão localizados no repositório Microsoft, [https://packages.microsoft.com](https://packages.microsoft.com).

> [!TIP]
> Se você instalou com êxito com as etapas de início rápido, você não precisa baixar ou instalar manualmente os pacotes a seguir. Esta seção é apenas para o cenário offline.

1. **Baixe o pacote de mecanismo de banco de dados para sua plataforma**. Encontrar links de download do pacote na seção de detalhes do pacote da [notas de versão](sql-server-linux-release-notes.md).

1. **Mover o pacote baixado para o computador Linux**. Se você usou uma máquina diferente para baixar os pacotes, uma maneira de mover os pacotes para o computador Linux é com o **scp** comando.

1. **Instalar o pacote do mecanismo de banco de dados**. Use um dos comandos a seguir com base em sua plataforma. Substitua o nome do arquivo de pacote neste exemplo com o nome exato que você baixou.

   | Plataforma | Comando de remoção do pacote |
   |-----|-----|
   | RHEL | `sudo yum localinstall mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `sudo zypper install mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `sudo dpkg -i mssql-server_versionnumber_amd64.deb` |

    > [!NOTE]
    > Você também pode instalar os pacotes RPM (RHEL e SLES) com o `rpm -ivh` comando, mas os comandos na tabela anterior instalam automaticamente as dependências se aprovada disponíveis de repositórios.

1. **Resolver dependências ausentes**: você pode ter dependências ausentes neste momento. Caso contrário, você pode ignorar esta etapa. No Ubuntu, se você tem acesso a repositórios aprovados que contém essas dependências, a solução mais fácil é usar o `apt-get -f install` comando. Este comando também conclui a instalação do SQL Server. Para verificar manualmente as dependências, use os seguintes comandos:

   | Plataforma | Comando de dependências de lista |
   |-----|-----|
   | RHEL | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `dpkg -I mssql-server_versionnumber_amd64.deb` |

   Depois de resolver as dependências ausentes, tente instalar o pacote mssql server novamente.

1. **Concluir a instalação do SQL Server**. Use **mssql conf** para concluir a instalação do SQL Server:

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

## <a name="next-steps"></a>Próximas etapas

Após a instalação, você também pode instalar outros pacotes opcionais do SQL Server.

- [Ferramentas de linha de comando do SQL Server](sql-server-linux-setup-tools.md)
- [SQL Server Agent](sql-server-linux-setup-sql-agent.md)
- [Pesquisa de texto completo do SQL Server](sql-server-linux-setup-full-text-search.md)
- [SQL Server Integration Services (Ubuntu)](sql-server-linux-setup-ssis.md)

Conecte-se à instância do SQL Server para começar a criar e gerenciar bancos de dados. Para começar, consulte os tutoriais de início rápido:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)


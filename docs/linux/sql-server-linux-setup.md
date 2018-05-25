---
title: Diretrizes de instalação para SQL Server 2017 no Linux | Microsoft Docs
description: Instalar, atualizar e desinstalar o SQL Server no Linux. Este artigo aborda cenários autônomos online e offline.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/06/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 565156c3-7256-4e63-aaf0-884522ef2a52
ms.openlocfilehash: bbf781d365174042f9358fd1e78a26d916f81f99
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="installation-guidance-for-sql-server-on-linux"></a>Orientação de instalação do SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo fornece orientações para instalar, atualizar e desinstalar o SQL Server 2017 no Linux.

> [!TIP]
> Este guia coves vários cenários de implantação. Se você estiver apenas procurando as instruções de instalação passo a passo, saltar para um dos guias de início rápido:
> - [Início rápido do RHEL](quickstart-install-connect-red-hat.md)
> - [SLES quickstart](quickstart-install-connect-suse.md)
> - [Início rápido do Ubuntu](quickstart-install-connect-ubuntu.md)
> - [Início rápido do docker](quickstart-install-connect-docker.md)

Para obter respostas para perguntas frequentes, consulte o [SQL Server nas perguntas frequentes sobre o Linux](../linux/sql-server-linux-faq.md).

## <a id="supportedplatforms"></a> Plataformas com suporte

Há suporte para o SQL Server 2017 no Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server (SLES) e Ubuntu. Ele também tem suporte como uma imagem do Docker, que pode ser executados no mecanismo de Docker em Linux ou o Docker para Windows/Mac.

| Plataforma | Versões com suporte | Obter
|-----|-----|-----
| **Red Hat Enterprise Linux** | 7.3 ou 7.4 | [Obter RHEL 7.4](http://access.redhat.com/products/red-hat-enterprise-linux/evaluation)
| **SUSE Linux Enterprise Server** | v12 SP2 | [Obter SLES v12 SP2](https://www.suse.com/products/server)
| **Ubuntu** | 16.04 | [Obter Ubuntu 16.04](http://www.ubuntu.com/download/server)
| **Mecanismo do docker** | 1.8+ | [Obter o Docker](http://www.docker.com/products/overview)

A Microsoft também suporta a implantar e gerenciar contêineres do SQL Server usando OpenShift e Kubernetes.

> [!NOTE]
> SQL Server é testado e suportado no Linux para as distribuições listadas anteriormente. Se você optar por instalar o SQL Server em um sistema operacional sem suporte, examine o **política de suporte** seção o [política de suporte técnico para o Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server) a entender o suporte implicações.

## <a id="system"></a> Requisitos do sistema

SQL Server 2017 tem os seguintes requisitos de sistema para Linux:

|||
|-----|-----|
| **Memória** | 2 GB |
| **Sistema de Arquivos** | **XFS** ou **EXT4** (outros sistemas de arquivos, como **BTRFS**, não têm suporte) |
| **Espaço em disco** | 6 GB |
| **Velocidade do processador** | 2 GHz |
| **Núcleos de processador** | 2 núcleos |
| **Tipo de processador** | compatível x64 somente |

Se você usar **sistema de arquivos de rede (NFS)** compartilhamentos remotos em produção, observe os seguintes requisitos de suporte:

- Versão do NFS Use **4.2 ou superior**. Versões mais antigas do NFS não dão suporte a recursos obrigatórios, como fallocate e criação de arquivo esparso, comum para sistemas de arquivos modernos.
- Localizar somente o **/var/opt/mssql** diretórios na montagem do NFS. Não há suporte para outros arquivos, como os binários do sistema do SQL Server.
- Certifique-se de que os clientes NFS usem a opção 'nolock' ao montar o compartilhamento remoto.

## <a id="repositories"></a> Configurar repositórios de origem

Quando você instala ou atualiza o SQL Server, você obter a versão mais recente do SQL Server 2017 do seu repositório Microsoft configurado. Usam os guias de início rápido do **atualização cumulativa (CU)** repositório. Mas em vez disso, você pode configurar o **GDR** repositório. Para obter mais informações sobre repositórios e como configurá-las, consulte [configurar repositórios para o SQL Server no Linux](sql-server-linux-change-repo.md).

> [!IMPORTANT]
> Se você instalou anteriormente um CTP ou a versão RC do SQL Server 2017, remova o repositório de visualização e registrar uma disponibilidade geral (GA) um. Para obter mais informações, consulte [configurar repositórios para o SQL Server no Linux](sql-server-linux-change-repo.md).

## <a id="platforms"></a> Instalar o SQL Server

Você pode instalar o SQL Server no Linux da linha de comando. Para obter instruções, consulte um dos tutoriais a seguir:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-docker.md)
- [Provisionar uma VM SQL no Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

## <a id="upgrade"></a> Atualize o SQL Server

Para atualizar o **mssql server** para a versão mais recente do pacote, use um dos comandos a seguir com base em sua plataforma:

| Plataforma | Comando de atualização de pacote |
|-----|-----|
| RHEL | `sudo yum update mssql-server` |
| SLES | `sudo zypper update mssql-server` |
| Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server` |

Esses comandos baixar o pacote mais recente e substitua os binários localizados em `/opt/mssql/`. O usuário gerou bancos de dados e bancos de dados do sistema não são afetados por essa operação.

## <a id="rollback"></a> Reversão SQL Server

A reversão ou fazer downgrade do SQL Server para uma versão anterior, use as seguintes etapas:

1. Identifique o número de versão para o pacote do SQL Server que você deseja fazer o downgrade. Para obter uma lista de números de pacote, consulte o [notas de versão](sql-server-linux-release-notes.md).

1. Fazer o downgrade para uma versão anterior do SQL Server. Nos comandos a seguir, substitua `<version_number>` com o número de versão do SQL Server identificado na etapa um.

   | Plataforma | Comando de atualização de pacote |
   |-----|-----|
   | RHEL | `sudo yum downgrade mssql-server-<version_number>.x86_64` |
   | SLES | `sudo zypper install --oldpackage mssql-server=<version_number>` |
   | Ubuntu | `sudo apt-get install mssql-server=<version_number>`<br/>`sudo systemctl start mssql-server` |

> [!NOTE]
> Somente há suporte para fazer o downgrade para uma versão dentro da mesma versão principal, como SQL Server 2017.

## <a id="versioncheck"></a> Verificar a versão instalada do SQL Server

Para verificar a versão atual e a edição do SQL Server no Linux, use o procedimento a seguir:

1. Se ainda não estiver instalado, instale o [ferramentas de linha de comando do SQL Server](sql-server-linux-setup-tools.md).

1. Use **sqlcmd** para executar um comando de Transact-SQL que exibe a versão do SQL Server e a edição.

   ```bash
   sqlcmd -S localhost -U SA -Q 'select @@VERSION'
   ```

## <a id="uninstall"></a> Desinstalar o SQL Server

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

## <a id="unattended"></a> Instalação autônoma

Você pode executar uma instalação autônoma da seguinte maneira:

- Siga etapas inicial de [início rápido](#platforms) para registrar os repositórios e instalar o SQL Server.
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

## <a id="offline"></a> Instalação offline

Se o computador Linux não tem acesso aos repositórios online usados no [inícios rápidos](#platforms), você pode baixar os arquivos de pacote diretamente. Esses pacotes estão localizados no repositório Microsoft, [ https://packages.microsoft.com ](https://packages.microsoft.com).

> [!TIP]
> Se você instalou com êxito com as etapas de início rápido, você não precisa baixar ou instalar manualmente os pacotes do SQL Server. Esta seção é apenas para o cenário offline.

1. **Baixe o pacote de mecanismo de banco de dados para sua plataforma**. Encontrar links de download do pacote na seção de detalhes do pacote da [notas de versão](sql-server-linux-release-notes.md).

1. **Mover o pacote baixado para o computador Linux**. Se você usou uma máquina diferente para baixar os pacotes, uma maneira de mover os pacotes para o computador Linux é com o **scp** comando.

1. **Instalar o pacote do mecanismo de banco de dados**. Use um dos comandos a seguir com base em sua plataforma. Substitua o nome do arquivo de pacote neste exemplo com o nome exato que você baixou.

   | Plataforma | Comando de instalação do pacote |
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

## <a name="optional-sql-server-features"></a>Recursos opcionais do SQL Server

Após a instalação, você também pode instalar ou habilitar recursos opcionais do SQL Server.

- [Ferramentas de linha de comando do SQL Server](sql-server-linux-setup-tools.md)
- [SQL Server Agent](sql-server-linux-setup-sql-agent.md)
- [Pesquisa de texto completo do SQL Server](sql-server-linux-setup-full-text-search.md)
- [SQL Server Integration Services (Ubuntu)](sql-server-linux-setup-ssis.md)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

> [!TIP]
> Para obter respostas para perguntas frequentes, consulte o [SQL Server nas perguntas frequentes sobre o Linux](sql-server-linux-faq.md).

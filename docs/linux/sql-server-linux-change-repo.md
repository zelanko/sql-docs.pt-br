---
title: Configurar repositórios do Linux para o SQL Server 2017 e 2019
description: Verifique e configure repositórios de origem para o SQL Server 2019 e o SQL Server 2017 no Linux. O repositório de origem afeta a versão do SQL Server que é aplicada durante a instalação e a atualização.
author: VanMSFT
ms.author: vanto
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
zone_pivot_groups: ld2-linux-distribution
ms.openlocfilehash: c1def0c2cfbdc4b3feed191e9eb2673b8e788f82
ms.sourcegitcommit: 76fb3ecb79850a8ef2095310aaa61a89d6d93afd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2020
ms.locfileid: "75776380"
---
# <a name="configure-repositories-for-installing-and-upgrading-sql-server-on-linux"></a>Configurar repositórios para instalação e atualização do SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

::: zone pivot="ld2-rhel"
Este artigo descreve como configurar o repositório correto para instalações e atualizações do SQL Server 2017 e do SQL Server 2019 no Linux. Na parte superior, a seleção atual é **RHEL (Red Hat)** .
::: zone-end

::: zone pivot="ld2-sles"
Este artigo descreve como configurar o repositório correto para instalações e atualizações do SQL Server 2017 e do SQL Server 2019 no Linux. Na parte superior, a seleção atual é **SLES (SUSE)** .
::: zone-end

::: zone pivot="ld2-ubuntu"
Este artigo descreve como configurar o repositório correto para instalações e atualizações do SQL Server 2017 e do SQL Server 2019 no Linux. Na parte superior, a seleção atual é **Ubuntu**.
::: zone-end

> [!TIP]
> O SQL Server 2019 já está disponível. Para experimentá-la, use este artigo para configurar o novo repositório **mssql-server-2019**. Em seguida, instale-a usando as instruções descritas no [guia de instalação](sql-server-linux-setup.md).

## <a id="repositories"></a> Repositórios

Ao instalar o SQL Server em Linux, é necessário configurar um repositório da Microsoft. Esse repositório é usado para adquirir o pacote do mecanismo de banco de dados, o **mssql-server** e os pacotes do SQL Server relacionados. Atualmente, há cinco repositórios principais:

| Repositório | Nome | DESCRIÇÃO |
|---|---|---|
| **2019** | **mssql-server-2019** | Repositório do SQL Server 2019 CU (atualização cumulativa). |
| **GDR de 2019** | **mssql-server-2019-gdr** | Repositório do SQL Server 2019 GDR apenas para atualizações críticas. |
| **Versão prévia de 2019** | **mssql-server-preview** | Repositório do SQL Server 2019 Preview e RC. |
| **2017** | **mssql-server-2017** | Repositório do SQL Server 2017 CU (atualização cumulativa). |
| **GDR de 2017** | **mssql-server-2017-gdr** | Repositório do SQL Server 2017 GDR apenas para atualizações críticas. |

## <a id="cuversusgdr"></a> Atualização cumulativa versus GDR

É importante observar que há dois tipos principais de repositórios para cada distribuição:

- **CU (atualizações cumulativas)** : O repositório CU (atualização cumulativa) contém pacotes para a versão base do SQL Server e as correções de bug ou as melhorias desde essa versão. As atualizações cumulativas são específicas para uma versão de lançamento, como o SQL Server 2019. Elas são liberadas em uma cadência regular.

- **GDR**: O repositório GDR contém pacotes para a versão base do SQL Server e apenas correções críticas e atualizações de segurança desde essa versão. Essas atualizações também são adicionadas à próxima versão de CU.

Cada versão de CU e GDR contém o pacote completo do SQL Server e todas as atualizações anteriores para esse repositório. Há suporte para a atualização de uma versão de GDR para uma versão de CU alterando o repositório configurado para o SQL Server. Faça também um [downgrade](sql-server-linux-setup.md#rollback) para qualquer versão na versão principal (por ex.: 2017).

> [!NOTE]
> Você pode atualizar de uma versão de GDR para versão de CU a qualquer momento alterando os repositórios. Não há suporte para a atualização de uma versão de CU para uma versão de GDR.

## <a name="configure-repositories"></a>Configurar repositórios

::: zone pivot="ld2-rhel"
Use as etapas nas seções a seguir para configurar repositórios no RHEL (Red Hat Enterprise Server).
::: zone-end

::: zone pivot="ld2-sles"
Use as etapas nas seções a seguir para configurar repositórios no SLES (SUSE Linux Enterprise Server).
::: zone-end

::: zone pivot="ld2-ubuntu"
Use as etapas nas seções a seguir para configurar repositórios no Ubuntu.
::: zone-end

## <a name="check-for-previously-configured-repositories"></a>Verificar os repositórios configurados anteriormente

<!--RHEL-->
::: zone pivot="ld2-rhel"
Primeiro, verifique se você já registrou um repositório do SQL Server.

1. Exiba os arquivos no diretório **/etc/yum.repos.d** com o seguinte comando:

   ```bash
   sudo ls /etc/yum.repos.d
   ```

2. Procure um arquivo que configure o diretório do SQL Server, como **mssql-server.repo**.

3. Imprima o conteúdo do arquivo.

   ```bash
   sudo cat /etc/yum.repos.d/mssql-server.repo
   ```

4. A propriedade **name** é o repositório configurado. Você pode identificá-lo com a tabela na seção [Repositórios](#repositories) deste artigo.

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
Primeiro, verifique se você já registrou um repositório do SQL Server.

1. Use **zypper info** para obter informações sobre qualquer repositório configurado anteriormente.

   ```bash
   sudo zypper info mssql-server
   ```

2. A propriedade **Repository** é o repositório configurado. Você pode identificá-lo com a tabela na seção [Repositórios](#repositories) deste artigo.

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
Primeiro, verifique se você já registrou um repositório do SQL Server.

1. Exiba o conteúdo do arquivo **/etc/apt/sources.list**.

   ```bash
   sudo cat /etc/apt/sources.list
   ```

2. Examine a URL do pacote de mssql-server. Você pode identificá-lo com a tabela na seção [Repositórios](#repositories) deste artigo.

::: zone-end

## <a name="remove-old-repository"></a>Remover o repositório antigo

<!--RHEL-->
::: zone pivot="ld2-rhel"
Se necessário, remova o repositório antigo com o comando a seguir.

```bash
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

Esse comando pressupõe que o arquivo identificado na seção anterior seja chamado **mssql-server.repo**.

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
Se necessário, remova o repositório antigo. Use um dos comandos a seguir com base no tipo de repositório configurado anteriormente.

| Repositório | Comando para remoção |
|---|---|
| **Versão prévia (2019)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-preview'` |
| **CU de 2019** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2019'` |
| **GDR de 2019** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2019-gdr'`|
| **CU de 2017** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
| **GDR de 2017** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
Se necessário, remova o repositório antigo. Use um dos comandos a seguir com base no tipo de repositório configurado anteriormente.

| Repositório | Comando para remoção |
|---|---|
| **Versão prévia (2019)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview xenial main'` |
| **CU de 2019** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019 xenial main'` | 
| **GDR de 2019** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019-gdr xenial main'` |
| **CU de 2017** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
| **GDR de 2017** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

::: zone-end

## <a name="configure-new-repository"></a>Configurar o novo repositório

<!--RHEL-->
::: zone pivot="ld2-rhel"
Configure o novo repositório a ser usado para instalações e atualizações do SQL Server. Use um dos comandos a seguir para configurar o repositório de sua escolha.

> [!NOTE]
> Os seguintes comandos do SQL Server 2019 apontam para o repositório do RHEL 8. O RHEL 8 não vem pré-instalado com o Python 2, que é exigido pelo SQL Server. Para obter mais informações, consulte blog a seguir sobre como instalar o Python 2 e configurá-lo como o interpretador padrão: https://www.redhat.com/en/blog/installing-microsoft-sql-server-red-hat-enterprise-linux-8-beta.
>
> Se você estiver usando o RHEL 7, altere o caminho abaixo para `/rhel/7` em vez de `/rhel/8`.

| Repositório | Versão | Comando |
|---|---|---|
| **CU de 2019** | 2019 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/mssql-server-2019.repo` |
| **GDR de 2019** | 2019 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/mssql-server-2019-gdr.repo` |
| **CU de 2017** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **GDR de 2017** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
Configure o novo repositório a ser usado para instalações e atualizações do SQL Server. Use um dos comandos a seguir para configurar o repositório de sua escolha.

| Repositório | Versão | Comando |
|---|---|---|
| **CU de 2019** | 2019 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2019.repo` |
| **GDR de 2019** | 2019 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2019-gdr.repo` |
| **CU de 2017** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
| **GDR de 2017** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
Configure o novo repositório a ser usado para instalações e atualizações do SQL Server.

1. Importe as chaves GPG do repositório público.

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Use um dos comandos a seguir para configurar o repositório de sua escolha.

   | Repositório | Versão | Comando |
   |---|---|---|
   | **CU de 2019** | 2019 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"` |
   | **GDR de 2019** | 2019 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019-gdr.list)"` |
   | **CU de 2017** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"` |
   | **GDR de 2017** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)"` |

3. Execute **apt-get update**.

   ```bash
   sudo apt-get update
   ```

::: zone-end

## <a name="next-steps"></a>Próximas etapas

Depois de configurar o repositório correto, você poderá continuar para [instalar](sql-server-linux-setup.md#platforms) ou [atualizar](sql-server-linux-setup.md#upgrade) o SQL Server e todos os pacotes relacionados do novo repositório.

::: zone pivot="ld2-rhel"
> [!IMPORTANT]
> Neste ponto, se você optar por usar o [início rápido do RHEL](quickstart-install-connect-red-hat.md), lembre-se de que você já configurou o repositório de destino. Não repita essa etapa nos tutoriais. Isso será especialmente verdadeiro se você configurar o repositório GDR, pois o início rápido usa o repositório CU.
::: zone-end

::: zone pivot="ld2-sles"
> [!IMPORTANT]
> Neste ponto, se você optar por usar o [início rápido do SLES](quickstart-install-connect-suse.md), lembre-se de que você já configurou o repositório de destino. Não repita essa etapa nos tutoriais. Isso será especialmente verdadeiro se você configurar o repositório GDR, pois o início rápido usa o repositório CU.
::: zone-end

::: zone pivot="ld2-ubuntu"
> [!IMPORTANT]
> Neste ponto, se você optar por usar o [início rápido do Ubuntu](quickstart-install-connect-ubuntu.md), lembre-se de que você já configurou o repositório de destino. Não repita essa etapa nos tutoriais. Isso será especialmente verdadeiro se você configurar o repositório GDR, pois o início rápido usa o repositório CU.
::: zone-end

Para obter mais informações sobre como instalar o SQL Server 2017 no Linux, confira [Diretrizes de instalação para o SQL Server em Linux](sql-server-linux-setup.md).

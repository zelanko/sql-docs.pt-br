---
title: Configurar repositórios do Linux para SQL Server 2017 e 2019
description: Verifique e configure os repositórios de código-fonte para 2019 do SQL Server e SQL Server 2017 no Linux. O repositório de origem afeta a versão do SQL Server que é aplicada durante a instalação e atualização.
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 02/11/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
zone_pivot_groups: ld2-linux-distribution
ms.openlocfilehash: 05299a2efd374dc7d58b5e32fcdea918b12fc1d3
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834080"
---
# <a name="configure-repositories-for-installing-and-upgrading-sql-server-on-linux"></a>Configurar repositórios para instalar e atualizar o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

::: zone pivot="ld2-rhel"
Este artigo descreve como configurar o repositório correto para atualizações e instalações do SQL Server 2017 e 2019 do SQL Server no Linux. Na parte superior, é sua seleção atual **RHEL (Red Hat)** .
::: zone-end

::: zone pivot="ld2-sles"
Este artigo descreve como configurar o repositório correto para atualizações e instalações do SQL Server 2017 e 2019 do SQL Server no Linux. Na parte superior, é sua seleção atual **SLES (SUSE)** .
::: zone-end

::: zone pivot="ld2-ubuntu"
Este artigo descreve como configurar o repositório correto para atualizações e instalações do SQL Server 2017 e 2019 do SQL Server no Linux. Na parte superior, é sua seleção atual **Ubuntu**.
::: zone-end

> [!TIP]
> Visualização do SQL Server 2019 agora está disponível! Para testá-la, use este artigo para configurar o novo **mssql-server-visualização** repositório. Em seguida, instale usando as instruções na [guia de instalação](sql-server-linux-setup.md).

## <a id="repositories"></a>Repositórios

Quando você instala o SQL Server no Linux, você deve configurar um repositório da Microsoft. Esse repositório é usado para adquirir o pacote do mecanismo de banco de dados, **mssql-server**e relacionadas a pacotes do SQL Server. Atualmente, há três repositórios principais:

| Repositório | Nome | Descrição |
|---|---|---|
| **Preview (2017)** | **mssql-server** | Repositório do SQL Server 2017 CTP e RC (Descontinuado). |
| **Preview (2019)** | **mssql-server-preview** | Visualização do SQL Server 2019 e repositório RC. |
| **CU** | **mssql-server-2017** | Repositório do SQL Server 2017 atualização cumulativa (CU). |
| **GDR** | **mssql-server-2017-gdr** | Repositório do SQL Server 2017 GDR somente para atualizações críticas. |

## <a id="cuversusgdr"></a> Atualização cumulativa versus GDR

É importante observar que há dois tipos principais de repositórios para cada distribuição:

- **As atualizações cumulativas (CU)** : O repositório de atualização cumulativa (CU) contém os pacotes para a versão base do SQL Server e correções de bug ou melhorias desde essa versão. As atualizações cumulativas são específicas para uma versão de lançamento, como o SQL Server 2017. Elas são lançadas em um ritmo regular.

- **GDR**: O repositório GDR contém pacotes para a versão base do SQL Server e apenas correções críticas e atualizações de segurança desde essa versão. Essas atualizações também são adicionadas para a próxima versão CU.

Cada versão de CU e GDR contém o pacote completo do SQL Server e todas as atualizações anteriores para esse repositório. Há suporte para a atualização de uma versão GDR para uma versão de CU, alterando seu repositório configurado para o SQL Server. Você também pode [fazer o downgrade](sql-server-linux-setup.md#rollback) para qualquer versão dentro de sua versão principal (por exemplo: 2017).

> [!NOTE]
> Você pode atualizar de uma versão GDR para atualização cumulativa, alterando os repositórios de versão a qualquer momento. Atualizar de uma versão de atualização cumulativa para uma versão GDR não tem suporte.

## <a name="configure-repositories"></a>Configurar repositórios

::: zone pivot="ld2-rhel"
Use as etapas nas seções a seguir para configurar repositórios no Red Hat Enterprise Server (RHEL).
::: zone-end

::: zone pivot="ld2-sles"
Use as etapas nas seções a seguir para configurar repositórios no SUSE Linux Enterprise Server (SLES).
::: zone-end

::: zone pivot="ld2-ubuntu"
Use as etapas nas seções a seguir para configurar os repositórios no Ubuntu.
::: zone-end

## <a name="check-for-previously-configured-repositories"></a>Verificação de repositórios previamente configurados

<!--RHEL-->
::: zone pivot="ld2-rhel"
Primeiro, verifique se você já tiver registrado um repositório do SQL Server.

1. Exibir os arquivos a **/etc/yum.repos.d** diretório com o seguinte comando:

   ```bash
   sudo ls /etc/yum.repos.d
   ```

2. Procure um arquivo que configura o diretório do SQL Server, tais como **mssql server.repo**.

3. Imprima o conteúdo do arquivo.

   ```bash
   sudo cat /etc/yum.repos.d/mssql-server.repo
   ```

4. O **nome** propriedade é o repositório configurado. Você pode identificá-lo com a tabela na [repositórios](#repositories) seção deste artigo.

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
Primeiro, verifique se você já tiver registrado um repositório do SQL Server.

1. Use **zypper informações** para obter informações sobre qualquer repositório configurado anteriormente.

   ```bash
   sudo zypper info mssql-server
   ```

2. O **repositório** propriedade é o repositório configurado. Você pode identificá-lo com a tabela na [repositórios](#repositories) seção deste artigo.

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
Primeiro, verifique se você já tiver registrado um repositório do SQL Server.

1. Exibir o conteúdo a **/etc/apt/sources.list** arquivo.

   ```bash
   sudo cat /etc/apt/sources.list
   ```

2. Examine a URL do pacote para o mssql-server. Você pode identificá-lo com a tabela na [repositórios](#repositories) seção deste artigo.

::: zone-end

## <a name="remove-old-repository"></a>Remover o repositório antigo

<!--RHEL-->
::: zone pivot="ld2-rhel"
Se necessário, remova o repositório antigo com o comando a seguir.

```bash
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

Esse comando presume que o arquivo identificado na seção anterior foi nomeado **mssql server.repo**.

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
Se necessário, remova o repositório antigo. Use um dos comandos a seguir com base no tipo de repositório configurado anteriormente.

| Repositório | Comando para remover |
|---|---|
| **Preview (2017)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
| **Preview (2019)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-preview'` |
| **CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
| **GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
Se necessário, remova o repositório antigo. Use um dos comandos a seguir com base no tipo de repositório configurado anteriormente.

| Repositório | Comando para remover |
|---|---|
| **Preview (2017)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` |
| **Preview (2019)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview xenial main'` |
| **CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
| **GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

::: zone-end

## <a name="configure-new-repository"></a>Configurar o novo repositório

<!--RHEL-->
::: zone pivot="ld2-rhel"
Configure o novo repositório a ser usado para atualizações e instalações do SQL Server. Use um dos comandos a seguir para configurar o repositório de sua escolha.

| Repositório | Version | Comando |
|---|---|---|
| **Preview (2019)** | 2019 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo` |
| **CU** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **GDR** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
Configure o novo repositório a ser usado para atualizações e instalações do SQL Server. Use um dos comandos a seguir para configurar o repositório de sua escolha.

| Repositório | Version | Comando |
|---|---|---|
| **Preview (2019)** | 2019 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-preview.repo` |
| **CU** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
| **GDR** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
Configure o novo repositório a ser usado para atualizações e instalações do SQL Server.

1. Importe as chaves GPG repositório público.

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Use um dos comandos a seguir para configurar o repositório de sua escolha.

   | Repositório | Version | Comando |
   |---|---|---|
   | **Preview (2019)** | 2019 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"` |
   | **CU** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"` |
   | **GDR** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)"` |

3. Execute **apt-get atualização**.

   ```bash
   sudo apt-get update
   ```

::: zone-end

## <a name="next-steps"></a>Próximas etapas

Depois de configurar o repositório correto, você poderá [instale](sql-server-linux-setup.md#platforms) ou [atualizar](sql-server-linux-setup.md#upgrade) do SQL Server e qualquer relacionadas a pacotes do novo repositório.

::: zone pivot="ld2-rhel"
> [!IMPORTANT]
> Neste ponto, se você optar por usar o [início rápido do RHEL](quickstart-install-connect-red-hat.md), lembre-se de que você já configurou o repositório de destino. Não repita essa etapa nos tutoriais. Isso é especialmente verdadeiro se você configurar o repositório GDR, porque o guia de início rápido usa o repositório CU.
::: zone-end

::: zone pivot="ld2-sles"
> [!IMPORTANT]
> Neste ponto, se você optar por usar o [início rápido do SLES](quickstart-install-connect-suse.md), lembre-se de que você já configurou o repositório de destino. Não repita essa etapa nos tutoriais. Isso é especialmente verdadeiro se você configurar o repositório GDR, porque o guia de início rápido usa o repositório CU.
::: zone-end

::: zone pivot="ld2-ubuntu"
> [!IMPORTANT]
> Neste ponto, se você optar por usar o [início rápido do Ubuntu](quickstart-install-connect-ubuntu.md), lembre-se de que você já configurou o repositório de destino. Não repita essa etapa nos tutoriais. Isso é especialmente verdadeiro se você configurar o repositório GDR, porque o guia de início rápido usa o repositório CU.
::: zone-end

Para obter mais informações sobre como instalar o SQL Server 2017 no Linux, consulte [orientação de instalação do SQL Server no Linux](sql-server-linux-setup.md).

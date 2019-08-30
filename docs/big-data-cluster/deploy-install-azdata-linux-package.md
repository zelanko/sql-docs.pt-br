---
title: Instalar o azdata com o instalador no Linux
titleSuffix: SQL Server big data clusters
description: Saiba como instalar a ferramenta azdata para instalar e gerenciar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] o (versão prévia) com o instalador (Linux).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e11e4851294ac8ffd8efa66e2156dcd47bce3aa0
ms.sourcegitcommit: 71fac5fee00e0eca57e555f44274dd7e08d47e1e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70160682"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-on-linux"></a>Instalar `azdata` para gerenciar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Linux

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como instalar `azdata` o para SQL Server a versão Release Candidate de clusters de Big data do 2019 no Linux. Antes que esses gerenciadores de pacotes estivessem `azdata` disponíveis `pip`, a instalação do é necessária.

Os gerenciadores de pacotes são projetados para vários sistemas operacionais e distribuições.

- Para Linux (Ubuntu), [Instale `azdata` com `apt` ](#azdata-apt)

Neste momento, não há gerenciadores de pacotes para instalar `azdata` em outros sistemas operacionais ou distribuições. Para essas plataformas, consulte [instalar `azdata` sem o Gerenciador de pacotes](./deploy-install-azdata.md).

## <a id="linux"></a>Instalar `azdata` para Linux

`azdata`o pacote de instalação está disponível para `apt`o Ubuntu com.

### <a id="azdata-apt"></a>Instalar `azdata` com apt (Ubuntu)

>[!NOTE]
>O `azdata` pacote não usa o Python do sistema, em vez disso, instala seu próprio interpretador do Python.

1. Obtenha os pacotes necessários para o processo de instalação:

    ```bash
    sudo apt-get update
    sudo apt-get install gnupg ca-certificates curl apt-transport-https lsb-release -y
    ```

2. Baixe e instale a chave de assinatura:

    ```bash
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add –
    ```

3. Adicione as `azdata` informações do repositório:

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
    ```

4. Atualizar informações do repositório e `azdata`instalar:

    ```bash
    sudo apt-get update
    sudo apt-get install -y azdata-cli
    ```

5. Verificar instalação:

    ```bash
    azdata --version
    ```

### <a name="update"></a>Atualização

Somente `azdata` atualização:

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

### <a name="uninstall"></a>Desinstalar

1. Desinstalar com apt-obter remoção:

    ```bash
    sudo apt-get remove -y azdata-cli
    ```

2. Remova as `azdata` informações do repositório:

    >[!NOTE]
    >Esta etapa não é necessária se você planeja instalar `azdata` no futuro

    ```bash
    sudo rm /etc/apt/sources.list.d/azdata-cli.list
    ```

3. Remova a chave de assinatura:

    ```bash
    sudo rm /etc/apt/trusted.gpg.d/dpgswdist.v1.asc.gpg
    ```

4. Remova as dependências desnecessárias que foram instaladas com a CLI do Azdata:

    ```bash
    sudo apt autoremove
    ```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters Big Data, consulte [o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]que são?](big-data-cluster-overview.md).

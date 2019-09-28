---
title: Instalar o azdata com o instalador no Linux
titleSuffix: SQL Server big data clusters
description: Saiba como instalar a ferramenta azdata para instalar e gerenciar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (versão prévia) com o instalador (Linux).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2795178cb975ecb620528c4a5dc8715b70d447fd
ms.sourcegitcommit: c4875c097e3aae1b76233777d15e0a0ec8e0d681
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71342010"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-on-linux"></a>Instalar o `azdata` para gerenciar o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Linux

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como instalar `azdata` para a versão Release Candidate de clusters de Big data do SQL Server 2019 no Linux. Antes que esses gerenciadores de pacotes estivessem disponíveis, a instalação do `azdata` exigia `pip`.

Os gerenciadores de pacotes são projetados para vários sistemas operacionais e distribuições.

- Para Linux (Ubuntu), [Instale o `azdata` com `apt`](#azdata-apt)

Neste momento, não há gerenciadores de pacotes para instalar `azdata` em outros sistemas operacionais ou distribuições. Para essas plataformas, consulte [instalar `azdata` sem Gerenciador de pacotes](./deploy-install-azdata.md).

## <a id="linux"></a>Instalar o `azdata` para Linux

o pacote de instalação `azdata` está disponível para Ubuntu com `apt`.

### <a id="azdata-apt"></a>Instalar o `azdata` com apt (Ubuntu)

>[!NOTE]
>O pacote `azdata` não usa o Python do sistema, em vez disso, instala seu próprio interpretador do Python.

1. Obtenha os pacotes necessários para o processo de instalação:

    ```bash
    sudo apt-get update
    sudo apt-get install gnupg ca-certificates curl apt-transport-https lsb-release -y
    ```

2. Baixe e instale a chave de assinatura:

    ```bash
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

3. Adicione as informações do repositório `azdata`:

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
    ```

4. Atualize as informações do repositório e instale `azdata`:

    ```bash
    sudo apt-get update
    sudo apt-get install -y azdata-cli
    ```

5. Verificar instalação:

    ```bash
    azdata --version
    ```

### <a name="update"></a>Update

Atualizar somente `azdata`:

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

### <a name="uninstall"></a>Desinstalar

1. Desinstalar com apt-obter remoção:

    ```bash
    sudo apt-get remove -y azdata-cli
    ```

2. Remova as informações do repositório `azdata`:

    >[!NOTE]
    >Esta etapa não é necessária se você planeja instalar o `azdata` no futuro

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

Para obter mais informações sobre clusters Big Data, consulte [o que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).

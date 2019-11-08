---
title: Instalar azdata com o instalador no Linux
titleSuffix: SQL Server big data clusters
description: Saiba como instalar a ferramenta azdata para instalar e gerenciar clusters de Big Data do SQL Server com o instalador (Linux).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9d8d4a34e89de7c136e1e80b43929531a2d10eba
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532068"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-on-linux"></a>Instale `azdata` para gerenciar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Linux

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como instalar `azdata` para clusters de Big Data do SQL Server 2019 no Linux. Antes que esses gerenciadores de pacotes estivessem disponíveis, a instalação de `azdata` exigia `pip`.

Os gerenciadores de pacotes foram projetados para vários sistemas operacionais e distribuições.

- Para Windows e Linux (distribuição Ubuntu), você pode instalar com um [gerenciador de pacotes](./deploy-install-azdata-installer.md) para ter uma experiência mais simples.
- Para Linux (Ubuntu), [instale `azdata` com `apt`](#azdata-apt)

Neste momento, não há gerenciadores de pacotes para instalar `azdata` em outros sistemas operacionais ou distribuições. Para essas plataformas, confira [Instalar o `azdata` sem o gerenciador de pacotes](./deploy-install-azdata.md).

## <a id="linux"></a>Instalar `azdata` para Linux

O pacote de instalação `azdata` está disponível para o Ubuntu com `apt`.

### <a id="azdata-apt"></a>Instalar `azdata` com apt (Ubuntu)

>[!NOTE]
>O pacote `azdata` não usa o Python do sistema, em vez disso, ele instala seu próprio interpretador do Python.

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
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"
    ```

4. Atualize as informações do repositório e instale `azdata`:

    ```bash
    sudo apt-get update
    sudo apt-get install -y azdata-cli
    ```

5. Verifique a instalação:

    ```bash
    azdata --version
    ```

### <a name="update"></a>Update

Atualize somente `azdata`:

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

### <a name="uninstall"></a>Desinstalar

1. Desinstale com apt-get remove:

    ```bash
    sudo apt-get remove -y azdata-cli
    ```

2. Remova as informações do repositório `azdata`:

    >[!NOTE]
    >Esta etapa não será necessária se você planeja instalar `azdata` no futuro

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

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).

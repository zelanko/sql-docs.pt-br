---
title: Instalar azdata com o instalador no Linux
titleSuffix: ''
description: Saiba como instalar a ferramenta azdata com o instalador (Linux).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2dc1c3d58ee5f7b6ea032a2e41f7c18431229881
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90914972"
---
# <a name="install-azdata-with-apt"></a>Instalar `azdata` com apt

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/azdata.md)]

Este artigo descreve como instalar o `azdata` no Linux. Antes que esses gerenciadores de pacotes estivessem disponíveis, a instalação de `azdata` exigia `pip`.

[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-azdata-for-linux"></a><a id="linux"></a>Instalar `azdata` para Linux

O pacote de instalação `azdata` está disponível para o Ubuntu com `apt`.

### <a name="install-azdata-with-apt-ubuntu"></a><a id="azdata-apt"></a>Instalar `azdata` com apt (Ubuntu)

>[!NOTE]
>O pacote `azdata` não usa o Python do sistema, em vez disso, ele instala seu próprio interpretador do Python.

1. Obtenha os pacotes necessários para o processo de instalação:

    ```bash
    sudo apt-get update
    sudo apt-get install gnupg ca-certificates curl wget software-properties-common apt-transport-https lsb-release -y
    ```

2. Baixe e instale a chave de assinatura:

    ```bash
    curl -sL https://packages.microsoft.com/keys/microsoft.asc |
    gpg --dearmor |
    sudo tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null
    ```

3. Adicione as informações do repositório `azdata`.

   Para a execução do cliente Ubuntu 16.04:
    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
    ```

   Para a execução do cliente Ubuntu 18.04:
    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/prod.list)"
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

### <a name="update"></a>Atualizar

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

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md).

Usar o azdata com [serviços de dados habilitados o Azure Arc](/azure/azure-arc/data/)
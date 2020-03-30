---
title: Instalar azdata com o instalador no Linux
titleSuffix: SQL Server big data clusters
description: Saiba como instalar a ferramenta azdata para instalar e gerenciar clusters de Big Data do SQL Server com o instalador (Linux).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ac50d0c20f76e78aaa5016f62cefb8c7cc7f075a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75728577"
---
# <a name="install-azdata-with-apt"></a>Instalar `azdata` com apt

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como instalar `azdata` para clusters de Big Data do SQL Server 2019 no Linux. Antes que esses gerenciadores de pacotes estivessem disponíveis, a instalação de `azdata` exigia `pip`.

[!INCLUDE [azdata-package-installation-remove-pip-install](../includes/azdata-package-installation-remove-pip-install.md)]

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
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"
    ```

   Para a execução do cliente Ubuntu 18.04:
    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2019.list)"
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

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).

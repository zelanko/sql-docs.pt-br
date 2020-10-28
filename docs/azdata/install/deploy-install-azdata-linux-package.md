---
title: Instalar a CLI de Dados do Azure (azdata) com o apt
description: Saiba como instalar a ferramenta de CLI de Dados do Azure (azdata) com o apt.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2f248978e09be4670d702805873a5ae6f4f7c9de
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257457"
---
# <a name="install-azure-data-cli-azdata-with-apt"></a>Instalar [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] com apt

[!INCLUDE[azdata](../../includes/applies-to-version/azdata.md)]

Para distribuições do Linux com o `apt`, há um pacote para o `azdata-cli`. O pacote do CLI foi testado em versões do Linux que usam `apt`:

- Ubuntu 16.04, Ubuntu 18.04

[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-apt"></a>Instalar com apt

>[!IMPORTANT]
> O pacote RPM da CLI do `azdata-cli` depende do pacote python3. Em seu sistema, isso pode ser uma versão do Python que antecede o requisito do *Python 3.6.x* . Se isso é um problema para você, localize um pacote python3 substituto ou siga as instruções de instalação manual que usam [`pip`](../install/deploy-install-azdata-pip.md).

1. Instale as dependências necessárias para instalar o `azdata-cli`.

   ```bash
   sudo apt-get update
   sudo apt-get install gnupg ca-certificates curl wget software-properties-common apt-transport-https lsb-release -y
   ```

2. Importe a chave do repositório da Microsoft.

   ```bash
   curl -sL https://packages.microsoft.com/keys/microsoft.asc |
   gpg --dearmor |
   sudo tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null
   ```

3. Crie informações sobre o repositório local.

   Para a execução do cliente Ubuntu 16.04:

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
    ```

   Para a execução do cliente Ubuntu 18.04:

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/prod.list)"
    ```

   Para a execução do cliente Ubuntu 20.04:

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/20.04/prod.list)
    ```

4. Instale o `azdata-cli`.

   ```bash
   sudo apt-get update
   sudo apt-get install -y azdata-cli
   ```

## <a name="verify-install"></a>Verificar instalação

```bash
azdata
azdata --version
```

## <a name="update"></a>Atualizar

Atualize o `azdata-cli` com os comandos `apt-get update` e `apt-get install`.

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

## <a name="uninstall"></a>Desinstalar

1. Remova o pacote do seu sistema.

   ```bash
   sudo apt-get remove -y azdata-cli
   ```

2. Remova as informações do repositório se você não pretende reinstalar o `azdata-cli`.

   ```bash
   sudo rm /etc/apt/sources.list.d/azdata-cli.list
   ```

3. Remova a chave do repositório.

   ```bash
   sudo rm /etc/apt/trusted.gpg.d/dpgswdist.v1.asc.gpg
   ```

4. A remoção de dependências não é mais necessária.

   ```bash
   sudo apt autoremove
   ```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md).

Usar o azdata com [serviços de dados habilitados o Azure Arc](/azure/azure-arc/data/)
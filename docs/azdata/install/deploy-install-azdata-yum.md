---
title: Instalar o azdata com o yum
titleSuffix: ''
description: Saiba como instalar a ferramenta azdata com o yum.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7f2f06c22b56e2afbe7c51198efbbfe1eecbc8c4
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725261"
---
# <a name="install-azdata-with-yum"></a>Instalar o `azdata` com o yum

[!INCLUDE[azdata](../../includes/applies-to-version/azdata.md)]

Para distribuições do Linux com o `yum`, há um pacote para o `azdata-cli`. O pacote do CLI foi testado em versões do Linux que usam `yum`:

- RHEL 7, RHEL 8

[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-yum"></a>Instalar com yum

>[!IMPORTANT]
> O pacote RPM da CLI do `azdata-cli` depende do pacote python3. Em seu sistema, isso pode ser uma versão do Python que antecede o requisito do *Python 3.6.x*. Se isso é um problema para você, localize um pacote python3 substituto ou siga as instruções de instalação manual que usam [`pip`](../install/deploy-install-azdata-pip.md).

1. Instale as dependências necessárias para instalar o `azdata-cli`.

   ```bash
   sudo yum install -y curl
   ```

1. Importe a chave do repositório da Microsoft.

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

1. Crie informações sobre o repositório local.

   Para um cliente RHEL 7, execute:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```
  
   Para um cliente RHEL 8, execute:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/prod.repo
   ```

1. Instale o `azdata-cli`.

   ```bash
   sudo yum install azdata-cli
   ```

## <a name="verify-install"></a>Verificar instalação

```bash
azdata
azdata --version
```

## <a name="update"></a>Atualizar

Atualize a `azdata-cli` com o comando `yum update`.

```bash
sudo yum update azdata-cli
```

## <a name="uninstall"></a>Desinstalar

1. Remova o pacote do seu sistema.

   ```bash
   sudo yum remove azdata-cli
   ```

1. Remova as informações do repositório se você não pretende reinstalar o `azdata-cli`.

   ```bash
   sudo rm /etc/yum.repos.d/azdata-cli.repo
   ```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md).

Usar o azdata com [serviços de dados habilitados o Azure Arc](/azure/azure-arc/data/)

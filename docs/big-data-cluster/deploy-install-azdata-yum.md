---
title: Instalar o azdata com o yum
titleSuffix: SQL Server big data clusters
description: Saiba como instalar a ferramenta azdata para instalar e gerenciar clusters de Big Data com o yum.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cf6e061b0ca4fca7c843575a87038a801ab8f758
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75728547"
---
# <a name="install-azdata-with-yum"></a>Instalar o `azdata` com o yum

Para distribuições do Linux com o `yum`, há um pacote para o `azdata-cli`. O pacote do CLI foi testado em versões do Linux que usam `yum`:

- RHEL 7, RHEL 8


[!INCLUDE [azdata-package-installation-remove-pip-install](../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-yum"></a>Instalar com yum

>[!IMPORTANT]
> O pacote RPM da CLI do `azdata-cli` depende do pacote python3. Em seu sistema, isso pode ser uma versão do Python que antecede o requisito do *Python 3.6.x*. Se isso é um problema para você, localize um pacote python3 substituto ou siga as instruções de instalação manual que usam [`pip`](deploy-install-azdata-pip.md).

1. Importar a chave do repositório da Microsoft

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

1. Criar informações sobre o repositório do local

   Para um cliente RHEL 7, execute:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2019.repo
   ```
  
   Para um cliente RHEL 8, execute:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/mssql-server-2019.repo
   ```

1. Instalar com o comando `yum install`

   ```bash
   sudo yum install azdata-cli
   ```

## <a name="verify-install"></a>Verificar instalação

```
azdata
azdata --version
```

## <a name="update"></a>Atualizar

Atualize a `azdata-cli` com o comando `yum update`.

```bash
sudo yum update azdata-cli
```

## <a name="uninstall"></a>Desinstalar

1. Remover o pacote do seu sistema

   ```bash
   sudo yum remove azdata-cli
   ```

1. Remover as informações do repositório se você não pretende reinstalar a `azdata-cli`

   ```bash
   sudo rm /etc/yum.repos.d/azdata-cli.repo
   ```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).

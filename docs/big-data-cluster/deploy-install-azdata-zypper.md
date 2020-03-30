---
title: Instalar o azdata com o zypper
titleSuffix: SQL Server big data clusters
description: Saiba como instalar a ferramenta azdata para instalar e gerenciar Clusters de Big Data com o zypper.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a02b4f0707d98d8acc9e65a2a27cee8d886c1ae7
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75728567"
---
# <a name="install-azdata-with-zypper"></a>Instalar o `azdata` com o zypper

Para distribuições do Linux com o `zypper`, há um pacote para o `azdata-cli`. O pacote do CLI foi testado em versões do Linux que usam `zyper`:

- openSUSE 42.2 (leap) +
- SLES 12 SP 2 +

[!INCLUDE [azdata-package-installation-remove-pip-install](../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-zypper"></a>Instalar com zypper
>[!IMPORTANT]
>O pacote RPM da CLI do `azdata-cli` depende do pacote python3. Em seu sistema, isso pode ser uma versão do Python que antecede o requisito do *Python 3.6.x*. Se isso é um problema para você, localize um pacote python3 substituto ou siga as instruções de instalação manual que usam [`pip`](deploy-install-azdata-pip.md).

1. Instalar dependências necessárias para instalar `azdata-cli`

   ```bash
   sudo zypper install -y curl
   ```

1. Importar a chave do repositório da Microsoft

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

1. Criar informações sobre o repositório do local

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2019.repo
   ```

1. Instalar

   ```bash
   sudo zypper install --from packages-microsoft-com-mssql-server-2019 -y azdata-cli
   ```

## <a name="verify-install"></a>Verificar instalação

   ```bash
   azdata
   azdata --version
   ```

## <a name="update"></a>Atualizar

Atualize a `azdata-cli` com o comando `zypper update`.

   ```bash
   sudo zypper refresh
   sudo zypper update azdata-cli
   ```

## <a name="uninstall"></a>Desinstalar

Remover o pacote do seu sistema

```bash
   sudo zypper removerepo azdata-cli
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).

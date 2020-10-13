---
title: Instalar o azdata com o zypper
titleSuffix: ''
description: Saiba como instalar a ferramenta azdata com o zypper.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ec87d5739e3707c056f7945a2c882eb00700464d
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725249"
---
# <a name="install-azdata-with-zypper"></a>Instalar o `azdata` com o zypper

[!INCLUDE[azdata](../../includes/applies-to-version/azdata.md)]

Para distribuições do Linux com o `zypper`, há um pacote para o `azdata-cli`. O pacote do CLI foi testado em versões do Linux que usam `zypper`:

- openSUSE 42.2 (leap) +
- SLES 12 SP 2 +

[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-zypper"></a>Instalar com zypper

>[!IMPORTANT]
>O pacote RPM da CLI do `azdata-cli` depende do pacote python3. Em seu sistema, isso pode ser uma versão do Python que antecede o requisito do *Python 3.6.x*. Se isso é um problema para você, localize um pacote python3 substituto ou siga as instruções de instalação manual que usam [`pip`](../install/deploy-install-azdata-pip.md).

1. Instale as dependências necessárias para instalar o `azdata-cli`.

   ```bash
   sudo zypper install -y curl
   ```

1. Importe a chave do repositório da Microsoft.

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

1. Crie informações sobre o repositório local.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo
   ```

1. Instale o `azdata-cli`.

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

Remova o pacote do seu sistema.

```bash
sudo zypper removerepo azdata-cli
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md).

Usar o azdata com [serviços de dados habilitados o Azure Arc](/azure/azure-arc/data/)
---
title: Instalar o azdata para macOS
titleSuffix: SQL Server big data clusters
description: Saiba como instalar a ferramenta azdata para instalar e gerenciar Clusters de Big Data para macOS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f6662a5ff7ced4c260e2b1a3fbd1efe5a285cf4a
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89733482"
---
# <a name="install-azdata-on-macos"></a>Instalar o `azdata` no macOS

Para a plataforma macOS, você pode instalar a `azdata-cli` com o gerenciador de pacotes homebrew. O pacote da CLI foi testado em versões do macOS: 
* 10.13 High Sierra
* 10.14 Mojave
* 10.15 Catalina

## <a name="install-with-homebrew"></a>Instalar com o Homebrew

```bash
brew tap microsoft/azdata-cli-release
brew update
brew install azdata-cli
```

>[!IMPORTANT]
>O `azdata-cli` tem uma dependência dos pacotes `python3`, `freetds`, `unixodbc` e `zeromq` do Homebrew e os instalará. Há garantia de compatibilidade do `azdata-cli` com a versão mais recente do publicada no Homebrew.

## <a name="verify-install"></a>Verificar instalação

```bash
azdata
azdata --version
```

## <a name="update"></a>Atualizar

Atualize as informações do repositório local e atualize o pacote `azdata-cli`.

```bash
brew tap microsoft/azdata-cli-release
brew update
brew upgrade azdata-cli
```

## <a name="uninstall"></a>Desinstalar

Use o homebrew para desinstalar o pacote `azdata-cli`.

```bash
brew uninstall azdata-cli
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md).
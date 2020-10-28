---
title: Instalar a CLI de Dados do Azure (azdata) para macOS
titleSuffix: ''
description: Saiba como instalar a ferramenta azdata (CLI de Dados do Azure) no macOS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0e3d7217ef917c794f1c497f7c5548588c2da1ba
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257376"
---
# <a name="install-azure-data-cli-azdata-on-macos"></a>Instalar o [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] no macOS

Para a plataforma macOS, você pode instalar o `azdata-cli` com o gerenciador de pacotes Homebrew. O pacote da CLI foi testado em versões do macOS:

- 10.13 High Sierra
- 10.14 Mojave
- 10.15 Catalina

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

Use o Homebrew para desinstalar o pacote `azdata-cli`.

```bash
brew uninstall azdata-cli
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md).

Usar o azdata com [serviços de dados habilitados o Azure Arc](/azure/azure-arc/data/)

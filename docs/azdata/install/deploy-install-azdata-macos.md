---
title: Instalar o azdata para macOS
titleSuffix: ''
description: Saiba como instalar a ferramenta azdata no macOS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c812600394546cba8adb0eacab59fa450b7c4bd2
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90914910"
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

Usar o azdata com [serviços de dados habilitados o Azure Arc](/azure/azure-arc/data/)

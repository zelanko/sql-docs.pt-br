---
title: Instalar azdata usando pip
titleSuffix: SQL Server big data clusters
description: Saiba como instalar a ferramenta azdata para instalar e gerenciar clusters de Big Data com o pip.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 51faf26a6414854ad3b2b1c2d205304e9b3dfb36
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89733481"
---
# <a name="install-azdata-with-pip"></a>Instalar `azdata` com `pip`

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

Este artigo descreve como instalar a ferramenta `azdata` no Windows ou Linux usando `pip`.

Para Windows e Linux (distribuição Ubuntu), você pode instalar com um [gerenciador de pacotes](./deploy-install-azdata-installer.md) para ter uma experiência mais simples.

## <a name="prerequisites"></a><a id="prerequisites"></a> Pré-requisitos

`azdata` é um utilitário de linha de comando escrito em Python que permite aos administradores de cluster inicializar e gerenciar o cluster de Big Data por meio de APIs REST. A versão mínima do Python necessária é v3.5. `pip` é necessário para baixar e instalar a ferramenta `azdata`. As instruções a seguir fornecem exemplos para o Windows e o Ubuntu. Para instalar o Python em outras plataformas, confira a [Documentação do Python](https://wiki.python.org/moin/BeginnersGuide/Download).
Além disso, instale e atualize a versão mais recente do pacote de Python `requests`:

```bash
pip3 install -U requests
```

> [!IMPORTANT]
> Se estiver instalando uma versão mais recente dos clusters de Big Data, faça backup dos dados e exclua o cluster antigo atualizando `azdata` e instalando a nova versão. Para obter mais informações, confira [Atualizando para uma nova versão](../../big-data-cluster/deployment-upgrade.md).

## <a name="windows-azdata-installation"></a><a id="windows"></a> Instalação de `azdata` no Windows

1. Em um cliente Windows, baixe o pacote de Python necessário em [https://www.python.org/downloads/](https://www.python.org/downloads/). Para o python3.5.3 e posterior, o pip3 também é instalado quando você instala o Python. 

   > [!TIP] 
   > Ao instalar o Python3, selecione para adicionar o Python ao seu `PATH`. Se não fizer isso, você poderá descobrir mais tarde onde o pip3 está localizado e adicioná-lo manualmente ao seu `PATH`.

1. Abra uma nova sessão do Windows PowerShell para que ela obtenha o caminho mais recente que contém o Python.

1. Caso você tenha versões anteriores de `azdata` instaladas, será importante desinstalá-las primeiro antes de instalar a última versão.

   Para o CTP 3.2 ou RC1, execute o comando a seguir.

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```
   ou
   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. Instale `azdata` com o seguinte comando:

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a name="linux-azdata-installation"></a><a id="linux"></a> Instalação de `azdata` em Linux

No Linux, você deve instalar o Python 3.5 e, em seguida, atualizar o pip. O exemplo a seguir mostra os comandos que funcionariam para o Ubuntu. Para outras plataformas Linux, confira a [Documentação do Python](https://wiki.python.org/moin/BeginnersGuide/Download).

1. Instale os pacotes de Python necessários:

   ```bash
   sudo apt-get update && \
   sudo apt-get install -y python3 && \
   sudo apt-get install -y python3-pip && \
   sudo apt-get install -y libkrb5-dev && \
   sudo apt-get install -y libsqlite3-dev && \
   sudo apt-get install -y unixodbc-dev
   ```

1. Atualizar o pip3:

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. Caso você tenha versões anteriores de `azdata` instaladas, será importante desinstalá-las primeiro antes de instalar a última versão.

   Para o CTP 3.2 ou RC1, execute o comando a seguir.

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```
   ou
   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. Instale `azdata` com o seguinte comando:

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > O comutador `--user` instala `azdata` no diretório de instalação do usuário do Python. Normalmente, ele é `~/.local/bin` no Linux. Adicione esse diretório ao seu caminho ou navegue até o diretório de instalação do usuário e execute `./azdata` nele.

## <a name="install-azdata-on-macos-or-os-x"></a><a id="macOSX"></a> Instalar `azdata` no macOS ou no OS X

Para instalar o `azdata` no macOS ou no OS X, conclua estas etapas. Para cada etapa, execute o exemplo no Terminal.

1. Em um cliente do macOS, instale o [Homebrew](https://brew.sh) se ainda não o tiver:

   ```
   /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   ```

1. Instale o Python e o pip, com a versão mínima 3.0:

   ```
   brew install python3
   ```

1. Instale as dependências:

   ```
   pip3 install -U requests
   brew install freetds
   ```

1. Caso você tenha versões anteriores da ferramenta instaladas, será importante desinstalá-las primeiro antes de instalar a última versão de `azdata`. O comando a seguir remove a versão de `azdata`.

   ```
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. Instale `azdata` com o seguinte comando:

   ```
   pip3 install -r https://aka.ms/azdata
   ```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md).

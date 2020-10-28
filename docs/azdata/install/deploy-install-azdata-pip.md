---
title: Instalar CLI de Dados do Azure (azdata) usando o pip
titleSuffix: ''
description: Saiba como instalar a ferramenta azdata com o pip.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4aa52ebe56cbe4af3d2983a9ed800ebbc1538971
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257439"
---
# <a name="install-azure-data-cli-azdata-with-pip"></a>Instalar [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] com `pip`

[!INCLUDE[azdata](../../includes/applies-to-version/azdata.md)]

Este artigo descreve como instalar a ferramenta [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] no Windows, Linux ou macOS/OS X usando o `pip`.

> [!TIP]
> Para obter uma experiência mais simples, o `azdata` pode ser instalado com um [gerenciador de pacotes](./deploy-install-azdata.md) para Windows, Linux (distribuições Ubuntu, Debian, RHEL, CentOS, openSUSE e SLE) e macOS.

## <a name="prerequisites"></a><a id="prerequisites"></a> Pré-requisitos

O `azdata` é um utilitário de linha de comando escrito em Python que permite aos administradores de cluster inicializar e gerenciar os recursos de dados por meio de APIs REST. A versão mínima do Python necessária é v3.5. O `pip` é necessário para baixar e instalar a ferramenta `azdata`. As instruções a seguir fornecem exemplos para Windows, Linux (Ubuntu) e macOS/OS X. Para instalar o Python em outras plataformas, confira a [documentação do Python](https://wiki.python.org/moin/BeginnersGuide/Download). Além disso, instale e atualize a versão mais recente do pacote de Python `requests`:

```bash
pip3 install -U requests
```

## <a name="windows-azdata-installation"></a><a id="windows"></a> Instalação de `azdata` no Windows

1. Em um cliente Windows, baixe o pacote de Python necessário em [https://www.python.org/downloads/](https://www.python.org/downloads/). Para o Python 3.5.3 e posterior, o pip3 também será instalado ao instalar o Python.

   > [!TIP]
   > Ao instalar o Python3, selecione para adicionar o Python ao seu `PATH`. Se não fizer isso, você poderá descobrir mais tarde onde o pip3 está localizado e adicioná-lo manualmente ao seu `PATH`.

1. Abra uma nova sessão do Windows PowerShell para que ela obtenha o caminho mais recente que contém o Python.

1. Na versão SQL Server 2019 CU5 e posteriores, o azdata tem uma versão semântica independente do servidor. Caso você tenha versões anteriores de `azdata` instaladas antes disso, será importante desinstalá-las antes de instalar a última versão.

   Por exemplo, para o 2019-cu4, execute o seguinte comando:

   ```powershell
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-cu4/requirements.txt
   ```

  > [!NOTE]
  > Nos exemplos anteriores, substitua `2019-cu6` pela versão e a CU da sua instalação do `azdata`. 

1. Instale o `azdata`.

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

1. Atualize o pip3.

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. Na versão SQL Server 2019 CU5 e posteriores, o azdata tem uma versão semântica independente do servidor. Caso você tenha versões anteriores de `azdata` instaladas antes disso, será importante desinstalá-las antes de instalar a última versão.

   Por exemplo, para `2019-cu6`, execute o seguinte comando:

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-cu6/requirements.txt
   ```

  > [!NOTE]
  > Nos exemplos anteriores, substitua `2019-cu6` pela versão e a CU da sua instalação do `azdata`.

1. Instale o `azdata`.

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > O comutador `--user` instala `azdata` no diretório de instalação do usuário do Python. Normalmente, ele é `~/.local/bin` no Linux. Adicione esse diretório ao seu caminho ou navegue até o diretório de instalação do usuário e execute `./azdata` nele.

## <a name="install-azdata-on-macos-or-os-x"></a><a id="macOSX"></a> Instalar `azdata` no macOS ou no OS X

Para instalar o `azdata` no macOS ou no OS X, conclua estas etapas. Para cada etapa, execute o exemplo no Terminal.

1. Em um cliente do macOS, instale o [Homebrew](https://brew.sh) se ainda não o tiver:

   ```bash
   /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   ```

1. Instale o Python e o pip, com a versão mínima 3.0:

   ```bash
   brew install python3
   ```

1. Instale as dependências:

   ```bash
   pip3 install -U requests
   brew install freetds
   ```

1. Na versão SQL Server 2019 CU5 e posteriores, o azdata tem uma versão semântica independente do servidor. Caso você tenha versões anteriores de `azdata` instaladas antes disso, será importante desinstalá-las antes de instalar a última versão. Por exemplo, o seguinte comando remove a versão RC1 do `azdata`:

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. Instale a CLI de Dados do Azure.

   ```bash
   pip3 install -r https://aka.ms/azdata
   ```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md).

Usar o azdata com [serviços de dados habilitados o Azure Arc](/azure/azure-arc/data/)

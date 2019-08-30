---
title: Instalar o azdata usando Pip
titleSuffix: SQL Server big data clusters
description: Saiba como instalar a ferramenta azdata para instalar e gerenciar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (versão prévia) com Pip.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a72e2ab39a17adef6c330f1ae17dcdc8a5dd8ddf
ms.sourcegitcommit: 71fac5fee00e0eca57e555f44274dd7e08d47e1e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70160729"
---
# <a name="install-azdata-for-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-using-pip"></a>Instalar `azdata` para[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] o usando`pip`

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como instalar a ferramenta `azdata` para a versão release candidate no Windows ou Linux usando `pip`o.

## <a id="prerequisites"></a> Pré-requisitos

`azdata`o é um utilitário de linha de comando escrito em Python que permite aos administradores de cluster inicializar e gerenciar o cluster de Big Data por meio de APIs REST. A versão mínima do Python necessária é v3.5. Você também deve ter `pip` o que é usado para baixar e `azdata` instalar a ferramenta. As instruções a seguir fornecem exemplos para o Windows e o Ubuntu. Para instalar o Python em outras plataformas, confira a [Documentação do Python](https://wiki.python.org/moin/BeginnersGuide/Download).
Além disso, você também precisa instalar e atualizar a versão mais recente do pacote de Python *requests*:
```bash
pip3 install -U requests
```

> [!IMPORTANT]
> Se você estiver instalando uma versão mais recente de clusters do Big data, deverá fazer backup dos dados e excluir o cluster `azdata` antigo antes de atualizar e instalar a nova versão. Para obter mais informações, confira [Atualizando para uma nova versão](deployment-upgrade.md).

## <a id="windows"></a>Instalação `azdata` do Windows

1. Em um cliente Windows, baixe o pacote de Python necessário em [https://www.python.org/downloads/](https://www.python.org/downloads/). Para o python3.5.3 e posterior, o pip3 também é instalado quando você instala o Python. 

   > [!TIP] 
   > Ao instalar o Python3, selecione para adicionar o Python ao seu **CAMINHO**. Se não fizer isso, você poderá descobrir mais tarde onde o pip3 está localizado e adicioná-lo manualmente ao seu **CAMINHO**.

1. Abra uma nova sessão do Windows PowerShell para que ela obtenha o caminho mais recente que contém o Python.

1. Se você tiver versões anteriores da ferramenta instaladas (antes do CTP 3,2, a ferramenta foi chamada **mssqlctl**), é importante desinstalá-la primeiro antes de instalar a versão mais recente `azdata`do. O comando a seguir remove a versão CTP 3,1 do **mssqlctl**.

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Se você tiver versões anteriores do `azdata` instaladas, será importante desinstalá-la primeiro antes de instalar a versão mais recente.

   Para o CTP 3,2, execute o comando a seguir.

   ```powershell
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```

1. Instale `azdata` com o seguinte comando:

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a id="linux"></a>Instalação `azdata` do Linux

No Linux, você deve instalar o Python 3.5 e, em seguida, atualizar o pip. O exemplo a seguir mostra os comandos que funcionariam para o Ubuntu. Para outras plataformas Linux, confira a [Documentação do Python](https://wiki.python.org/moin/BeginnersGuide/Download).

1. Instale os pacotes de Python necessários:

   ```bash
   sudo apt-get update && \
   sudo apt-get install -y python3 && \
   sudo apt-get install -y python3-pip
   ```

1. Atualizar o pip3:

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. Se você tiver versões anteriores da ferramenta instaladas (antes do CTP 3,2, a ferramenta foi chamada **mssqlctl**), é importante desinstalá-la primeiro antes de instalar a versão mais recente `azdata`do. O comando a seguir remove a versão CTP 3,1 do **mssqlctl**.

   ```bash
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Se você tiver versões anteriores do `azdata` instaladas, será importante desinstalá-la primeiro antes de instalar a versão mais recente.

   Para o CTP 3,2, execute o comando a seguir.

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```

1. Instale `azdata` com o seguinte comando:

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > O `--user` comutador `azdata` é instalado no diretório de instalação do usuário do Python. Normalmente, ele é `~/.local/bin` no Linux. Adicione esse diretório ao seu caminho ou navegue até o diretório de instalação do usuário e execute `./azdata` nele.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters Big Data, consulte [o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]que são?](big-data-cluster-overview.md).

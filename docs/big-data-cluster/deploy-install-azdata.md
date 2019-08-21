---
title: Instalar o azdata
titleSuffix: SQL Server big data clusters
description: Saiba como instalar a ferramenta azdata para instalar e gerenciar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] o (versão prévia).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e95fe15877dd6d22ca575b79f9fb213b6104d3aa
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652413"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Instalar o azdata para gerenciar[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como instalar a ferramenta **azdata** para CTP 3.2 no Windows ou Linux.

## <a id="prerequisites"></a> Pré-requisitos

**azdata** é um utilitário de linha de comando escrito em Python que permite aos administradores de cluster inicializar e gerenciar o cluster de Big Data por meio de APIs REST. A versão mínima do Python necessária é v3.5. Você também precisa ter `pip` o que é usado para baixar e instalar a ferramenta **azdata**. As instruções a seguir fornecem exemplos para o Windows e o Ubuntu. Para instalar o Python em outras plataformas, confira a [Documentação do Python](https://wiki.python.org/moin/BeginnersGuide/Download).
Além disso, você também precisa instalar e atualizar a versão mais recente do pacote de Python *requests*:
```bash
pip3 install -U requests
```

> [!IMPORTANT]
> Se estiver instalando uma versão mais recente de clusters de Big Data, você deverá fazer backup dos dados e excluir o cluster antigo *antes* de atualizar **azdata** e instalar a nova versão. Para obter mais informações, confira [Atualizando para uma nova versão](deployment-upgrade.md).

## <a id="windows"></a> Instalação de azdata do Windows

1. Em um cliente Windows, baixe o pacote de Python necessário em [https://www.python.org/downloads/](https://www.python.org/downloads/). Para o python3.5.3 e posterior, o pip3 também é instalado quando você instala o Python. 

   > [!TIP] 
   > Ao instalar o Python3, selecione para adicionar o Python ao seu **CAMINHO**. Se não fizer isso, você poderá descobrir mais tarde onde o pip3 está localizado e adicioná-lo manualmente ao seu **CAMINHO**.

1. Abra uma nova sessão do Windows PowerShell para que ela obtenha o caminho mais recente que contém o Python.

1. Caso você tenha versões anteriores do da ferramenta instaladas (chamada anteriormente de **mssqlctl**), é importante desinstalá-las primeiro antes de instalar a última versão de **azdata**.

   Para o CTP 3.1 ou anterior, execute o comando a seguir. Substitua `ctp3.1` no comando pela versão do **mssqlctl** que está sendo desinstalada. 

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Caso você tenha versões anteriores de **azdata** instaladas, será importante desinstalá-las primeiro antes de instalar a última versão.

   Para o CTP 3.2 ou superior, execute o comando a seguir. Substitua `ctp3.2` no comando pela versão do **azdata** que está sendo desinstalada.

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. Instale **azdata** com o seguinte comando:

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a id="linux"></a> Instalação de azdata no Linux

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

1. Caso você tenha versões anteriores do da ferramenta instaladas (chamada anteriormente de **mssqlctl**), é importante desinstalá-las primeiro antes de instalar a última versão de **azdata**.

   Para o CTP 3.1 ou anterior, execute o comando a seguir. Substitua `ctp3.1` no comando pela versão do **mssqlctl** que está sendo desinstalada. 

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Caso você tenha versões anteriores de **azdata** instaladas, será importante desinstalá-las primeiro antes de instalar a última versão.

   Para o CTP 3.2 ou superior, execute o comando a seguir. Substitua `ctp3.2` no comando pela versão do **azdata** que está sendo desinstalada.

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. Instale **azdata** com o seguinte comando:

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > O comutador `--user` instala o azdata no diretório de instalação do usuário do Python. Normalmente, ele é `~/.local/bin` no Linux. Adicione esse diretório ao seu caminho ou navegue até o diretório de instalação do usuário e execute `./azdata` nele.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters Big Data, consulte [o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]que são?](big-data-cluster-overview.md).

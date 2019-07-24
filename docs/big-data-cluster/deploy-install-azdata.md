---
title: Instalar o azdata
titleSuffix: SQL Server big data clusters
description: Saiba como instalar a ferramenta azdata para instalar e gerenciar SQL Server clusters de Big Data 2019 (versão prévia).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9444842081456563f411ad618f32b8dbd59f7513
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426436"
---
# <a name="install-azdata-to-manage-sql-server-big-data-clusters"></a>Instalar o azdata para gerenciar clusters de Big Data de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como instalar a ferramenta **azdata** para CTP 3,2 no Windows ou Linux.

## <a id="prerequisites"></a> Pré-requisitos

**azdata** é um utilitário de linha de comando escrito em Python que permite aos administradores de cluster inicializar e gerenciar o cluster de Big data por meio de APIs REST. A versão mínima do Python necessária é v 3.5. Você também deve ter `pip` o que é usado para baixar e instalar a ferramenta **azdata** . As instruções a seguir fornecem exemplos para o Windows e o Ubuntu. Para instalar o Python em outras plataformas, consulte a [documentação do Python](https://wiki.python.org/moin/BeginnersGuide/Download).
Além disso, você também deve instalar e atualizar a versão mais recente do pacote Python de *solicitações* :
```bash
pip3 install -U requests
```

> [!IMPORTANT]
> Se você estiver instalando uma versão mais recente de clusters do Big Data, deverá fazer backup dos dados e excluir o cluster antigo *antes* de atualizar o **azdata** e instalar a nova versão. Para obter mais informações, consulte [Atualizando para uma nova versão](deployment-upgrade.md).

## <a id="windows"></a>Instalação do Windows azdata

1. Em um cliente Windows, baixe o pacote Python necessário do [https://www.python.org/downloads/](https://www.python.org/downloads/). Para o Python 3.5.3 e posterior, o pip3 também é instalado quando você instala o Python. 

   > [!TIP] 
   > Ao instalar o Python3, selecione para adicionar o Python ao seu **caminho**. Se você não fizer isso, poderá encontrar mais tarde onde pip3 está localizado e adicioná-lo manualmente ao seu **caminho**.

1. Abra uma nova sessão do Windows PowerShell para que ela obtenha o caminho mais recente com Python nela.

1. Se você tiver versões anteriores da ferramenta instaladas (PREVIOSLY denominada **mssqlctl**), será importante desinstalá-la primeiro antes de instalar a versão mais recente do **azdata**.

   Para o CTP 3,1 ou inferior, execute o comando a seguir. Substitua `ctp3.1` no comando pela versão do **mssqlctl** que você está desinstalando. 

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Se você tiver versões anteriores do **azdata** instaladas, será importante desinstalá-la primeiro antes de instalar a versão mais recente.

   Para o CTP 3,2 ou superior, execute o comando a seguir. Substitua `ctp3.2` no comando pela versão do **azdata** que você está desinstalando.

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. Instale o **azdata** com o seguinte comando:

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a id="linux"></a>Instalação do Linux azdata

No Linux, você deve instalar o Python 3,5 e, em seguida, atualizar o Pip. O exemplo a seguir mostra os comandos que funcionariam para o Ubuntu. Para outras plataformas Linux, consulte a [documentação do Python](https://wiki.python.org/moin/BeginnersGuide/Download).

1. Instale os pacotes python necessários:

   ```bash
   sudo apt-get update && /
   sudo apt-get install -y python3 && /
   sudo apt-get install -y python3-pip
   ```

1. Atualizar pip3:

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. Se você tiver versões anteriores da ferramenta instaladas (anteriormente denominada **mssqlctl**), é importante desinstalá-la primeiro antes de instalar a versão mais recente do **azdata**.

   Para o CTP 3,1 ou inferior, execute o comando a seguir. Substitua `ctp3.1` no comando pela versão do **mssqlctl** que você está desinstalando. 

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Se você tiver versões anteriores do **azdata** instaladas, será importante desinstalá-la primeiro antes de instalar a versão mais recente.

   Para o CTP 3,2 ou superior, execute o comando a seguir. Substitua `ctp3.2` no comando pela versão do **azdata** que você está desinstalando.

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. Instale o **azdata** com o seguinte comando:

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > O `--user` comutador instala o azdata no diretório de instalação do usuário do Python. Isso normalmente `~/.local/bin` é no Linux. Adicione esse diretório ao seu caminho ou navegue até o diretório de instalação do usuário e `./azdata` execute a partir daí.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters Big Data, consulte [o que são SQL Server 2019 Big data clusters?](big-data-cluster-overview.md).

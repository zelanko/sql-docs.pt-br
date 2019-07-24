---
title: Atualizar para uma nova versão
titleSuffix: SQL Server big data clusters
description: Saiba como atualizar SQL Server clusters de Big Data 2019 (versão prévia) para uma nova versão.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7bdb1eb59fd36d065df9dba0f6d6879c1a294914
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419389"
---
# <a name="how-to-upgrade-sql-server-big-data-clusters"></a>Como atualizar SQL Server clusters de Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo fornece orientação sobre como atualizar um cluster SQL Server Big Data para uma nova versão. As etapas neste artigo se aplicam especificamente a como atualizar entre versões de visualização.

## <a name="backup-and-delete-the-old-cluster"></a>Fazer backup e excluir o cluster antigo

Atualmente, a única maneira de atualizar um cluster Big Data para uma nova versão é remover manualmente e recriar o cluster. Cada versão tem uma versão exclusiva do **azdata** que não é compatível com a versão anterior. Além disso, se um cluster mais antigo tiver que baixar uma imagem em um novo nó, a imagem mais recente poderá não ser compatível com as imagens mais antigas no cluster. Para atualizar para a versão mais recente, use as seguintes etapas:

1. Antes de excluir o cluster antigo, faça backup dos dados na instância mestra do SQL Server e no HDFS. Para a instância mestra de SQL Server, você pode usar [SQL Server Backup e restauração](data-ingestion-restore-database.md). Para o HDFS, você [pode copiar os dados com **ondulação**](data-ingestion-curl.md).

1. Exclua o cluster antigo com `azdata delete cluster` o comando.

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > Use a versão do **azdata** que corresponde ao seu cluster. Não exclua um cluster mais antigo com a versão mais recente do **azdata**.

1. Antes do CTP 3,2, o **azdata** era chamado de **mssqlctl**. Se você tiver versões anteriores do **mssqlctl** ou **azdata** instaladas, é importante desinstalar primeiro antes de instalar a versão mais recente do **azdata**.

   Para o CTP 2,3 ou superior, execute o comando a seguir. Substitua `ctp3.1` no comando pela versão do **mssqlctl** que você está desinstalando. Se a versão for anterior ao CTP 3,1, adicione um traço antes do número de versão (por exemplo `ctp-2.5`,).

   ```powershell
   pip3 uninstall -r https://mcr.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Instale a versão mais recente do **azdata**. Os comandos a seguir instalam o **azdata** para CTP 3,2:

   **Windows:**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux:**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > Para cada versão, o caminho para **azdata** é alterado. Mesmo que você tenha instalado anteriormente o **azdata** ou o **mssqlctl**, você deve reinstalar a partir do caminho mais recente antes de criar o novo cluster.

## <a id="azdataversion"></a>Verificar a versão do azdata

Antes de implantar um novo cluster Big data, verifique se você está usando a versão mais recente do **azdata** com `--version` o parâmetro:

```bash
azdata --version
```

## <a name="install-the-new-release"></a>Instalar a nova versão

Depois de remover o cluster de Big Data anterior e instalar o **azdata**mais recente, implante o novo cluster de Big data usando as instruções de implantação atuais. Para obter mais informações, consulte [como implantar SQL Server clusters de Big data no kubernetes](deployment-guidance.md). Em seguida, restaure todos os bancos de dados ou arquivos necessários.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters Big Data, consulte [o que são SQL Server Big data clusters](big-data-cluster-overview.md).

---
title: Atualizar para uma nova versão
titleSuffix: SQL Server big data clusters
description: Saiba como atualizar clusters de Big Data do SQL Server 2019 (versão prévia) para uma nova versão.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 29bdd3996112154b222ffb7d43390050c9af2d02
ms.sourcegitcommit: 0d89bcaebdf87db3bd26db2ca263be9c671b0220
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2019
ms.locfileid: "68731086"
---
# <a name="how-to-upgrade-sql-server-big-data-clusters"></a>Como atualizar clusters de Big Data do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo fornece diretrizes sobre como atualizar um cluster de Big Data do SQL Server para uma nova versão. As etapas deste artigo se aplicam especificamente a como fazer a atualização entre versões prévias.

## <a name="backup-and-delete-the-old-cluster"></a>Fazer backup e excluir o cluster antigo

Atualmente, a única maneira de atualizar um cluster de Big Data para uma nova versão é remover o cluster manualmente e recriá-lo. Cada versão tem uma versão exclusiva do **azdata** que não é compatível com a versão anterior. Além disso, se um cluster mais antigo precisar baixar uma imagem em um novo nó, a imagem mais recente poderá não ser compatível com as imagens mais antigas no cluster. Para fazer a atualização para a última versão, use as seguintes etapas:

1. Antes de excluir o cluster antigo, faça backup dos dados na instância mestra do SQL Server e no HDFS. Para a instância mestra do SQL Server, você poderá usar [Backup e restauração do SQL Server](data-ingestion-restore-database.md). Para o HDFS, você [pode copiar os dados com o **cURL**](data-ingestion-curl.md).

1. Exclua o cluster antigo com o comando `azdata delete cluster`.

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > Use a versão do **azdata** que corresponde ao cluster. Não exclua um cluster mais antigo com a versão mais recente do **azdata**.

1. Antes do CTP 3.2, o **azdata** era chamado **mssqlctl**. Caso você tenha versões anteriores do **mssqlctl** ou do **azdata** instaladas, será importante desinstalá-las primeiro antes de instalar a última versão do **azdata**.

   Para o CTP 2.3 ou superior, execute o comando a seguir. Substitua `ctp3.1` no comando pela versão do **mssqlctl** que está sendo desinstalada. Se a versão for anterior ao CTP 3.1, adicione um traço antes do número de versão (por exemplo, `ctp-2.5`).

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Instale a última versão do **azdata**. Os seguintes comandos instalam o **azdata** para o CTP 3.2:

   **Windows:**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux:**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > Em cada versão, o caminho para **azdata** é alterado. Mesmo que você tenha instalado o **azdata** ou o **mssqlctl** anteriormente, você precisará reinstalar com base no caminho mais recente antes de criar o cluster.

## <a id="azdataversion"></a> Verificar a versão do azdata

Antes de implantar um novo cluster de Big Data, verifique se você está usando a última versão do **azdata** com o parâmetro `--version`:

```bash
azdata --version
```

## <a name="install-the-new-release"></a>Instalar a nova versão

Depois de remover o cluster de Big Data anterior e instalar o **azdata** mais recente, implante o novo cluster de Big Data usando as instruções de implantação atuais. Para obter mais informações, confira [Como implantar clusters de Big Data do SQL Server no Kubernetes](deployment-guidance.md). Em seguida, restaure os bancos de dados ou os arquivos necessários.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre os clusters de Big Data, confira [O que são clusters de Big Data do SQL Server](big-data-cluster-overview.md).

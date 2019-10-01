---
title: Atualizar para uma nova versão
titleSuffix: SQL Server big data clusters
description: Saiba como atualizar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (versão prévia) para uma nova versão.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bb1bf33c9ccb342e6afc4d22d67463791c0d67b6
ms.sourcegitcommit: 36c3ead6f2a3628f58040acf47f049f0b0957b8a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/30/2019
ms.locfileid: "71688270"
---
# <a name="how-to-upgrade-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Como atualizar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo fornece diretrizes sobre como atualizar um cluster de Big Data do SQL Server para uma nova versão. As etapas deste artigo se aplicam especificamente a como fazer a atualização entre versões prévias.

## <a name="backup-and-delete-the-old-cluster"></a>Fazer backup e excluir o cluster antigo

Atualmente, a única maneira de atualizar um cluster de Big Data para uma nova versão é remover o cluster manualmente e recriá-lo. Cada versão tem uma versão exclusiva do `azdata` que não é compatível com a versão anterior. Além disso, se um cluster mais antigo precisar baixar uma imagem em um novo nó, a imagem mais recente poderá não ser compatível com as imagens mais antigas no cluster. Para fazer a atualização para a última versão, use as seguintes etapas:

1. Antes de excluir o cluster antigo, faça backup dos dados na instância mestra do SQL Server e no HDFS. Para a instância mestra do SQL Server, você poderá usar [Backup e restauração do SQL Server](data-ingestion-restore-database.md). Para o HDFS, você [pode copiar os dados com `curl`](data-ingestion-curl.md).

1. Exclua o cluster antigo com o comando `azdata delete cluster`.

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > Use a versão do `azdata` que corresponde ao seu cluster. Não exclua um cluster mais antigo com a versão mais recente do `azdata`.

   > [!Note]
   > Emitir um comando `azdata bdc delete` resultará em todos os objetos criados no namespace identificado com o nome do cluster de Big Data a ser excluído, mas não no próprio namespace. O namespace pode ser reutilizado para implantações subsequentes, desde que esteja vazio e nenhum outro aplicativo tenha sido criado no.

1. Antes do CTP 3,2, `azdata` foi chamado `mssqlctl`. Se você tiver versões anteriores do `mssqlctl` ou do `azdata` instalados, será importante desinstalar primeiro antes de instalar a versão mais recente do `azdata`.

   Para o CTP 2.3 ou superior, execute o comando a seguir. Substitua `ctp3.1` no comando pela versão do `mssqlctl` que você está desinstalando. Se a versão for anterior ao CTP 3.1, adicione um traço antes do número de versão (por exemplo, `ctp-2.5`).

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. Instale a versão mais recente do `azdata`. Os comandos a seguir instalam `azdata` para a versão Release Candidate:

   **Windows:**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux:**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > Para cada versão, o caminho para `azdata` é alterado. Mesmo que você tenha instalado `azdata` ou `mssqlctl` anteriormente, será necessário reinstalar a partir do caminho mais recente antes de criar o novo cluster.

## <a id="azdataversion"></a> Verificar a versão do azdata

Antes de implantar um novo cluster Big Data, verifique se você está usando a versão mais recente do `azdata` com o parâmetro `--version`:

```bash
azdata --version
```

## <a name="install-the-new-release"></a>Instalar a nova versão

Depois de remover o cluster de Big Data anterior e instalar o `azdata` mais recente, implante o novo cluster de Big Data usando as instruções de implantação atuais. Para obter mais informações, consulte [como implantar o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no kubernetes](deployment-guidance.md). Em seguida, restaure os bancos de dados ou os arquivos necessários.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters Big Data, consulte [o que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](big-data-cluster-overview.md).

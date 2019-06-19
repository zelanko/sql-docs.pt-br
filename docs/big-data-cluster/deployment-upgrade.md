---
title: Atualizar para uma nova versão
titleSuffix: SQL Server big data clusters
description: Saiba como atualizar clusters do SQL Server 2019 big data (visualização) para uma nova versão.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3af688d607e8ec2d9dad7efe0d2275840c48cba8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66782236"
---
# <a name="how-to-upgrade-sql-server-big-data-clusters"></a>Como atualizar clusters de grandes dados do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo fornece orientação sobre como atualizar um cluster de big data do SQL Server para uma nova versão. As etapas neste artigo se aplicam especificamente ao como atualizar entre versões de visualização.

## <a name="backup-and-delete-the-old-cluster"></a>Fazer backup e excluir o cluster antigo

Atualmente, a única maneira de atualizar um cluster de big data para uma nova versão é remover e recriar o cluster manualmente. Cada versão tem uma versão exclusiva do **mssqlctl** que não é compatível com a versão anterior. Além disso, se tiver um cluster mais antigo baixar uma imagem em um novo nó, a imagem mais recente não ficará compatível com as imagens mais antigas no cluster. Para atualizar para a versão mais recente, use as seguintes etapas:

1. Antes de excluir o cluster antigo, fazer backup dos dados na instância mestre do SQL Server e no HDFS. Para a instância mestre do SQL Server, você pode usar [SQL Server backup e restauração](data-ingestion-restore-database.md). Para o HDFS, você [pode copiar os dados com **curl**](data-ingestion-curl.md).

1. Excluir o cluster antigo com o `mssqlctl delete cluster` comando.

   ```bash
    mssqlctl cluster delete --name <old-cluster-name>
   ```

   > [!Important]
   > Use a versão do **mssqlctl** que corresponde ao seu cluster. Não exclua um cluster mais antigo com a versão mais recente do **mssqlctl**.

1. Se você tiver quaisquer versões anteriores do **mssqlctl** instalado, é importante desinstalar **mssqlctl** primeiro antes de instalar a versão mais recente.

   Se você estiver desinstalando **mssqlctl** correspondente CTP 2.2 ou inferior de execução:

   ```powershell
   pip3 uninstall mssqlctl
   ```

   Para o CTP 2.3 ou superior, execute o comando a seguir. Substitua `ctp-2.5` no comando com a versão do **mssqlctl** que você está desinstalando:

   ```powershell
   pip3 uninstall -r  https://private-repo.microsoft.com/python/ctp-2.5/mssqlctl/requirements.txt
   ```

1. Instale a versão mais recente do **mssqlctl**. Os seguintes comandos instalam **mssqlctl** para o CTP 3.0:

   **Windows:**

   ```powershell
   pip3 install -r  https://private-repo.microsoft.com/python/ctp3.0/mssqlctl/requirements.txt
   ```

   **Linux:**

   ```bash
   pip3 install -r  https://private-repo.microsoft.com/python/ctp3.0/mssqlctl/requirements.txt --user
   ```

   > [!IMPORTANT]
   > Para cada versão, o caminho para **mssqlctl** alterações. Mesmo se você instalou anteriormente **mssqlctl**, você deverá reinstalar do caminho mais recente antes de criar o novo cluster.

## <a id="mssqlctlversion"></a> Verifique se a versão mssqlctl

Antes de implantar um novo cluster de big data, verifique se que você está usando a versão mais recente do **mssqlctl** com o `--version` parâmetro:

```bash
mssqlctl --version
```

## <a name="install-the-new-release"></a>Instale a nova versão

Depois de remover o cluster de big data anterior e instalar a versão mais recente **mssqlctl**, implantar o novo cluster de big data usando as instruções de implantação atual. Para obter mais informações, consulte [clusters de como implantar grandes de dados do SQL Server em Kubernetes](deployment-guidance.md). Em seguida, restaure todos os bancos de dados necessários ou arquivos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de big data, consulte [quais são os clusters de grandes dados do SQL Server](big-data-cluster-overview.md).

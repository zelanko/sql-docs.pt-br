---
title: Executar scripts durante a sincronização (programação Transact-SQL de replicação) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- synchronization [SQL Server replication], scripts
- scripts [SQL Server replication], synchronization and
- sp_addscriptexec
ms.assetid: b58a0877-4e43-4fab-a281-24e6022d3fb1
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7cfc7873669eb49d3fc3e160ff33f56371517e6c
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768109"
---
# <a name="execute-scripts-during-synchronization-replication-transact-sql-programming"></a>Executar scripts durante a sincronização (Programação Transact-SQL de replicação)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A replicação dá suporte à execução de scripts sob demanda para Assinantes para publicações transacionais e de mesclagem. Essa funcionalidade copia o script no diretório que executa a replicação e usa **sqlcmd** para aplicar o script no Assinante. Por padrão, se houver uma falha ao aplicar o script para uma assinatura em uma publicação transacional, o Agente de Distribuição se deterá. Você pode especificar um script [!INCLUDE[tsql](../../includes/tsql-md.md)] para ser executado programaticamente usando procedimentos armazenados de replicação.  
  
### <a name="to-specify-a-script-to-run-for-all-subscribers-to-a-snapshot-transactional-or-merge-publication"></a>Para especificar um script para ser executado para todos os Assinantes para uma publicação de instantâneo, transacional ou de mesclagem  
  
1.  Componha e teste o script [!INCLUDE[tsql](../../includes/tsql-md.md)] que será executado sob demanda.  
  
2.  Salve o arquivo de script em um local em que possa ser acessado pelo Snapshot Agent para a publicação.  
  
3.  No Publicador no banco de dados de publicação, execute [sp_addscriptexec &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md). Especifique **@publication** , o nome do arquivo do script com caminho UNC completo criado na etapa 2 para **@scriptfile** e um dos seguintes valores para **@skiperror** :  
  
    -   **0** - o agente deixará de executar o script se um erro for encontrado.  
  
    -   **1** - o agente fará log dos erros e continuará executando o script quando forem encontrados erros.  
  
4.  O script especificado será executado para cada Assinante na próxima vez que o agente for executado para sincronizar a assinatura.  
  
## <a name="see-also"></a>Consulte Também  
 [Sincronizar dados](../../relational-databases/replication/synchronize-data.md)  
  
  

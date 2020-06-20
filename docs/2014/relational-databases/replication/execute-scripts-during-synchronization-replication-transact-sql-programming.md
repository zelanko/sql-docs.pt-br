---
title: Executar scripts durante a sincronização (programação Transact-SQL de replicação) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 4bc217ad160a0238cc4247600d65eb32f156071f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010702"
---
# <a name="execute-scripts-during-synchronization-replication-transact-sql-programming"></a>Executar scripts durante a sincronização (Programação Transact-SQL de replicação)
  A replicação dá suporte à execução de scripts sob demanda para Assinantes para publicações transacionais e de mesclagem. Essa funcionalidade copia o script no diretório que executa a replicação e usa **sqlcmd** para aplicar o script no Assinante. Por padrão, se houver uma falha ao aplicar o script para uma assinatura em uma publicação transacional, o Agente de Distribuição se deterá. Você pode especificar um script [!INCLUDE[tsql](../../includes/tsql-md.md)] para ser executado programaticamente usando procedimentos armazenados de replicação.  
  
### <a name="to-specify-a-script-to-run-for-all-subscribers-to-a-snapshot-transactional-or-merge-publication"></a>Para especificar um script para ser executado para todos os Assinantes para uma publicação de instantâneo, transacional ou de mesclagem  
  
1.  Componha e teste o script [!INCLUDE[tsql](../../includes/tsql-md.md)] que será executado sob demanda.  
  
2.  Salve o arquivo de script em um local em que possa ser acessado pelo Snapshot Agent para a publicação.  
  
3.  No Publicador no banco de dados de publicação, execute [sp_addscriptexec &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql). Especifique a ** \@ publicação**, o nome do arquivo de script com o caminho UNC completo criado na etapa 2 para ** \@ scriptfile**e um dos valores a seguir para ** \@ skiperror**:  
  
    -   **0** - o agente deixará de executar o script se um erro for encontrado.  
  
    -   **1** - o agente fará log dos erros e continuará executando o script quando forem encontrados erros.  
  
4.  O script especificado será executado para cada Assinante na próxima vez que o agente for executado para sincronizar a assinatura.  
  
## <a name="see-also"></a>Consulte Também  
 [Sincronizar dados](synchronize-data.md)  
  
  

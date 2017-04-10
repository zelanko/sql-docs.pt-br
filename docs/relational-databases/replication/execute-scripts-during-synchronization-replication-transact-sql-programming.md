---
title: "Executar scripts durante a sincroniza&#231;&#227;o (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sincronização [replicação do SQL Server], scripts"
  - "scripts [replicação do SQL Server], sincronização e"
  - "sp_addscriptexec"
ms.assetid: b58a0877-4e43-4fab-a281-24e6022d3fb1
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Executar scripts durante a sincroniza&#231;&#227;o (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o)
  A replicação dá suporte à execução de scripts sob demanda para Assinantes para publicações transacionais e de mesclagem. Essa funcionalidade copia o script para a pasta de trabalho de replicação e, em seguida, usa **sqlcmd** para aplicar o script no assinante. Por padrão, se houver uma falha ao aplicar o script para uma assinatura em uma publicação transacional, o Agente de Distribuição se deterá. Você pode especificar um script [!INCLUDE[tsql](../../includes/tsql-md.md)] para ser executado programaticamente usando procedimentos armazenados de replicação.  
  
### Para especificar um script para ser executado para todos os Assinantes para uma publicação de instantâneo, transacional ou de mesclagem  
  
1.  Componha e teste o script [!INCLUDE[tsql](../../includes/tsql-md.md)] que será executado sob demanda.  
  
2.  Salve o arquivo de script em um local em que possa ser acessado pelo Snapshot Agent para a publicação.  
  
3.  No publicador do banco de dados de publicação, execute [sp_addscriptexec & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md). Especifique **@publication**, o nome do arquivo de script com o caminho UNC completo criado na etapa 2 para **@scriptfile**, e um dos seguintes valores para **@skiperror**:  
  
    -   **0** -o agente irá parar de executar o script se um erro for encontrado.  
  
    -   **1** -o agente registrará erros e continuar executando o script quando são encontrados erros.  
  
4.  O script especificado será executado para cada Assinante na próxima vez que o agente for executado para sincronizar a assinatura.  
  
## Consulte também  
 [Sincronizar dados](../../relational-databases/replication/synchronize-data.md)  
  
  
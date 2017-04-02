---
title: "Configurar o trabalho do conjunto de transa&#231;&#245;es para um Publicador Oracle (programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
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
  - "sp_publisherproperty"
  - "publicação Oracle [replicação do SQL Server], configurando"
ms.assetid: beea1a5c-0053-4971-a68f-0da53063fcbb
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Configurar o trabalho do conjunto de transa&#231;&#245;es para um Publicador Oracle (programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o)
  O **Xactset** trabalho é um trabalho de banco de dados Oracle criado pela replicação é executado em um editor Oracle para criar conjuntos de transação quando o Log Reader Agent não está conectado ao publicador. Você pode ativar e configurar esse trabalho do Distribuidor usando os procedimentos armazenados de replicação programaticamente. Para obter mais informações, consulte o [ajuste de desempenho para editores Oracle](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md).  
  
### Habilitar o conjunto de trabalho de transação  
  
1.  No editor Oracle, defina a **job_queue_processes** parâmetro de inicialização para um valor suficiente para permitir a execução do trabalho Xactset. Para obter mais informações sobre esse parâmetro, veja a documentação de banco de dados para o Editor Oracle.  
  
2.  No distribuidor, execute [sp_publisherproperty & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Especifique o nome do editor Oracle para **@publisher**, um valor de **xactsetbatching** para **@propertyname**, e um valor de **habilitado** para **@propertyvalue**.  
  
3.  No distribuidor, execute [sp_publisherproperty & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Especifique o nome do editor Oracle para **@publisher**, um valor de **xactsetjobinterval** para **@propertyname**, e o intervalo do trabalho, em minutos, para **@propertyvalue**.  
  
4.  No distribuidor, execute [sp_publisherproperty & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Especifique o nome do editor Oracle para **@publisher**, um valor de **xactsetjob** para **@propertyname**, e um valor de **habilitado** para **@propertyvalue**.  
  
### Para configurar o trabalho de conjunto de transação  
  
1.  (Opcional) No distribuidor, execute [sp_publisherproperty & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Especifique o nome do Editor Oracle como **@publisher**. Isso retorna propriedades do **Xactset** trabalho no Editor.  
  
2.  No distribuidor, execute [sp_publisherproperty & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Especifique o nome do editor Oracle para **@publisher**, o nome da propriedade do trabalho Xactset está sendo definido para **@propertyname**, e as novas configurações de **@propertyvalue**.  
  
3.  (Opcional) Repita a etapa 2 para cada propriedade de trabalho Xactset que estiver sendo definida. Ao alterar o **xactsetjobinterval** propriedade, você deve reiniciar o trabalho no editor Oracle para o novo intervalo entre em vigor.  
  
### Para exibir as propriedades do trabalho de conjunto de transação  
  
1.  No distribuidor, execute [sp_helpxactsetjob](../../../relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql.md). Especifique o nome do Editor Oracle como **@publisher**.  
  
### Para desativar o trabalho de conjunto de transação  
  
1.  No distribuidor, execute [sp_publisherproperty & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Especifique o nome do editor Oracle para **@publisher**, um valor de **xactsetjob** para **@propertyname**, e um valor de **desabilitado** para **@propertyvalue**.  
  
## Exemplo  
 O exemplo a seguir habilita o trabalho `Xactset` e define um intervalo de três minutos entre as execuções.  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../relational-databases/replication/codesnippet/tsql/configure the transactio_1.sql)]  
  
## Consulte também  
 [Ajuste de desempenho para Editores Oracle](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)   
 [Conceitos dos procedimentos armazenados do sistema de replicação](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  
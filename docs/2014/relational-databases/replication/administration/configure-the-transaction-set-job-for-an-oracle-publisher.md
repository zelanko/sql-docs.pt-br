---
title: Configurar o trabalho de conjunto de transações para um publicador Oracle (programação Transact-SQL de replicação) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_publisherproperty
- Oracle publishing [SQL Server replication], configuring
ms.assetid: beea1a5c-0053-4971-a68f-0da53063fcbb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 48282f08df588f54b6f03a0b99c58a2f0cf039ac
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793536"
---
# <a name="configure-the-transaction-set-job-for-an-oracle-publisher-replication-transact-sql-programming"></a>Configurar o trabalho do conjunto de transações para um Publicador Oracle (programação Transact-SQL de replicação)
  O trabalho **Xactset** é um banco de dados Oracle criado pela replicação em execução em um Editor Oracle, para criar conjuntos de transações, quando o Log Reader Agent não está conectado ao Publicador. Você pode ativar e configurar esse trabalho do Distribuidor usando os procedimentos armazenados de replicação programaticamente. Para obter mais informações, consulte [Ajuste de desempenho para Publicadores Oracle](../non-sql/performance-tuning-for-oracle-publishers.md).  
  
### <a name="to-enable-the-transaction-set-job"></a>Habilitar o conjunto de trabalho de transação  
  
1.  No Editor Oracle, defina o parâmetro de inicialização **job_queue_processes** com um valor que seja suficiente para permitir a execução do trabalho Xactset. Para obter mais informações sobre esse parâmetro, veja a documentação de banco de dados para o Editor Oracle.  
  
2.  No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique o nome do publicador Oracle para  **\@publisher**, um valor de `xactsetbatching` para  **\@propertyname**e um valor de `enabled` para  **\@propertyvalue**.  
  
3.  No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique o nome do publicador Oracle para  **\@publisher**, um valor de `xactsetjobinterval` para  **\@propertyname**e o intervalo do trabalho, em minutos, para  **\@propertyvalue**.  
  
4.  No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique o nome do publicador Oracle para  **\@publisher**, um valor de `xactsetjob` para  **\@propertyname**e um valor de `enabled` para  **\@propertyvalue**.  
  
### <a name="to-configure-the-transaction-set-job"></a>Para configurar o trabalho de conjunto de transação  
  
1.  (opcional) No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique o nome do publicador Oracle para  **\@publisher**. Isso retorna as propriedades do trabalho **Xactset** no Publicador.  
  
2.  No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique o nome do publicador Oracle para  **\@publisher**, o nome da propriedade trabalho Xactset que está sendo definida para  **\@propertyname**e as novas configurações para  **\@propertyvalue**.  
  
3.  (Opcional) Repita a etapa 2 para cada propriedade de trabalho Xactset que estiver sendo definida. Ao alterar o `xactsetjobinterval` propriedade, você deve reiniciar o trabalho no editor Oracle para o novo intervalo entre em vigor.  
  
### <a name="to-view-properties-of-the-transaction-set-job"></a>Para exibir as propriedades do trabalho de conjunto de transação  
  
1.  No Distributor, execute [sp_helpxactsetjob](/sql/relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql). Especifique o nome do publicador Oracle para  **\@publisher**.  
  
### <a name="to-disable-the-transaction-set-job"></a>Para desativar o trabalho de conjunto de transação  
  
1.  No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique o nome do publicador Oracle para  **\@publisher**, um valor de `xactsetjob` para  **\@propertyname**e um valor de `disabled` para  **\@propertyvalue**.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir habilita o trabalho `Xactset` e define um intervalo de três minutos entre as execuções.  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../snippets/tsql/SQL15/replication/howto/tsql/enablexactsetjob.sql#sp_enable_xactsetjob)]  
  
## <a name="see-also"></a>Consulte também  
 [Ajuste de desempenho para Publicadores Oracle](../non-sql/performance-tuning-for-oracle-publishers.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)  
  
  

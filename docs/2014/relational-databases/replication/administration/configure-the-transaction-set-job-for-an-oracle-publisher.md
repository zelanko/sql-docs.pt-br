---
title: Configurar o trabalho do conjunto de transações para um Publicador Oracle (Programação Transact-SQL de replicação) | Microsoft Docs
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
ms.openlocfilehash: 43a25ce755a505f0efd7c25243b8969a962ea701
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065978"
---
# <a name="configure-the-transaction-set-job-for-an-oracle-publisher-replication-transact-sql-programming"></a>Configurar o trabalho do conjunto de transações para um Publicador Oracle (programação Transact-SQL de replicação)
  O trabalho **Xactset** é um banco de dados Oracle criado pela replicação em execução em um Editor Oracle, para criar conjuntos de transações, quando o Log Reader Agent não está conectado ao Publicador. Você pode ativar e configurar esse trabalho do Distribuidor usando os procedimentos armazenados de replicação programaticamente. Para obter mais informações, consulte [Ajuste de desempenho para Publicadores Oracle](../non-sql/performance-tuning-for-oracle-publishers.md).  
  
### <a name="to-enable-the-transaction-set-job"></a>Habilitar o conjunto de trabalho de transação  
  
1.  No Editor Oracle, defina o parâmetro de inicialização **job_queue_processes** com um valor que seja suficiente para permitir a execução do trabalho Xactset. Para obter mais informações sobre esse parâmetro, veja a documentação de banco de dados para o Editor Oracle.  
  
2.  No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique o nome do editor Oracle para o ** \@ Publicador**, um valor de `xactsetbatching` para ** \@ PropertyName**e um valor de `enabled` para ** \@ PropertyValue**.  
  
3.  No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique o nome do editor Oracle para o ** \@ Publicador**, um valor de `xactsetjobinterval` para ** \@ PropertyName**e o intervalo de trabalho, em minutos, para ** \@ PropertyValue**.  
  
4.  No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique o nome do editor Oracle para o ** \@ Publicador**, um valor de `xactsetjob` para ** \@ PropertyName**e um valor de `enabled` para ** \@ PropertyValue**.  
  
### <a name="to-configure-the-transaction-set-job"></a>Para configurar o trabalho de conjunto de transação  
  
1.  (opcional) No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique o nome do editor Oracle para o ** \@ Publicador**. Isso retorna as propriedades do trabalho **Xactset** no Publicador.  
  
2.  No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique o nome do editor Oracle para o ** \@ Publicador**, o nome da Propriedade do trabalho Xactset que está sendo definida para ** \@ PropertyName**e a nova configuração para ** \@ PropertyValue**.  
  
3.  (Opcional) Repita a etapa 2 para cada propriedade de trabalho Xactset que estiver sendo definida. Ao alterar a `xactsetjobinterval` propriedade, você deve reiniciar o trabalho no Publicador Oracle para que o novo intervalo entre em vigor.  
  
### <a name="to-view-properties-of-the-transaction-set-job"></a>Para exibir as propriedades do trabalho de conjunto de transação  
  
1.  No Distributor, execute [sp_helpxactsetjob](/sql/relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql). Especifique o nome do editor Oracle para o ** \@ Publicador**.  
  
### <a name="to-disable-the-transaction-set-job"></a>Para desativar o trabalho de conjunto de transação  
  
1.  No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique o nome do editor Oracle para o ** \@ Publicador**, um valor de `xactsetjob` para ** \@ PropertyName**e um valor de `disabled` para ** \@ PropertyValue**.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir habilita o trabalho `Xactset` e define um intervalo de três minutos entre as execuções.  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../snippets/tsql/SQL15/replication/howto/tsql/enablexactsetjob.sql#sp_enable_xactsetjob)]  
  
## <a name="see-also"></a>Consulte Também  
 [Ajuste de desempenho para Publicadores Oracle](../non-sql/performance-tuning-for-oracle-publishers.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)  
  
  

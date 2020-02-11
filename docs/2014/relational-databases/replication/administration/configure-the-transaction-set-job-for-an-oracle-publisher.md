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
manager: craigg
ms.openlocfilehash: 48282f08df588f54b6f03a0b99c58a2f0cf039ac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67793536"
---
# <a name="configure-the-transaction-set-job-for-an-oracle-publisher-replication-transact-sql-programming"></a>Configurar o trabalho do conjunto de transações para um Publicador Oracle (programação Transact-SQL de replicação)
  O trabalho **Xactset** é um banco de dados Oracle criado pela replicação em execução em um Editor Oracle, para criar conjuntos de transações, quando o Log Reader Agent não está conectado ao Publicador. Você pode ativar e configurar esse trabalho do Distribuidor usando os procedimentos armazenados de replicação programaticamente. Para obter mais informações, consulte [Ajuste de desempenho para Publicadores Oracle](../non-sql/performance-tuning-for-oracle-publishers.md).  
  
### <a name="to-enable-the-transaction-set-job"></a>Habilitar o conjunto de trabalho de transação  
  
1.  No Editor Oracle, defina o parâmetro de inicialização **job_queue_processes** com um valor que seja suficiente para permitir a execução do trabalho Xactset. Para obter mais informações sobre esse parâmetro, veja a documentação de banco de dados para o Editor Oracle.  
  
2.  No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique o nome `enabled` do editor Oracle para `xactsetbatching` ** \@o Publicador**, um valor de para ** \@PropertyName**e um valor de para ** \@PropertyValue**.  
  
3.  No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique o nome do editor Oracle `xactsetjobinterval` para ** \@o Publicador**, um valor de para ** \@PropertyName**e o intervalo de trabalho, em minutos, para ** \@PropertyValue**.  
  
4.  No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique o nome `enabled` do editor Oracle para `xactsetjob` ** \@o Publicador**, um valor de para ** \@PropertyName**e um valor de para ** \@PropertyValue**.  
  
### <a name="to-configure-the-transaction-set-job"></a>Para configurar o trabalho de conjunto de transação  
  
1.  (opcional) No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique o nome do Publicador Oracle em **\@publisher**. Isso retorna as propriedades do trabalho **Xactset** no Publicador.  
  
2.  No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique o nome do Publicador Oracle em **\@publisher**, o nome da propriedade do trabalho Xactset que está sendo definida em **\@propertyname** e a nova configuração em **\@propertyvalue**.  
  
3.  (Opcional) Repita a etapa 2 para cada propriedade de trabalho Xactset que estiver sendo definida. Ao alterar a `xactsetjobinterval` Propriedade, você deve reiniciar o trabalho no Publicador Oracle para que o novo intervalo entre em vigor.  
  
### <a name="to-view-properties-of-the-transaction-set-job"></a>Para exibir as propriedades do trabalho de conjunto de transação  
  
1.  No Distributor, execute [sp_helpxactsetjob](/sql/relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql). Especifique o nome do Publicador Oracle em **\@publisher**.  
  
### <a name="to-disable-the-transaction-set-job"></a>Para desativar o trabalho de conjunto de transação  
  
1.  No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique o nome `disabled` do editor Oracle para `xactsetjob` ** \@o Publicador**, um valor de para ** \@PropertyName**e um valor de para ** \@PropertyValue**.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir habilita o trabalho `Xactset` e define um intervalo de três minutos entre as execuções.  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../snippets/tsql/SQL15/replication/howto/tsql/enablexactsetjob.sql#sp_enable_xactsetjob)]  
  
## <a name="see-also"></a>Consulte Também  
 [Ajuste de desempenho para Publicadores Oracle](../non-sql/performance-tuning-for-oracle-publishers.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)  
  
  

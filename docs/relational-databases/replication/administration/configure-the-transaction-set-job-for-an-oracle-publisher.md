---
title: Configurar o trabalho do conjunto de transações para um Publicador Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 2a38f122dd4a0f184ab4fd3e564c143d0e24a924
ms.sourcegitcommit: 26715b4dbef95d99abf2ab7198a00e6e2c550243
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70275749"
---
# <a name="configure-the-transaction-set-job-for-an-oracle-publisher"></a>Configurar o trabalho do conjunto de transações para um Publicador Oracle
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O trabalho **Xactset** é um banco de dados Oracle criado pela replicação em execução em um Editor Oracle, para criar conjuntos de transações, quando o Log Reader Agent não está conectado ao Publicador. Você pode ativar e configurar esse trabalho do Distribuidor usando os procedimentos armazenados de replicação programaticamente. Para obter mais informações, consulte [Ajuste de desempenho para Publicadores Oracle](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md).  
  
### <a name="to-enable-the-transaction-set-job"></a>Habilitar o conjunto de trabalho de transação  
  
1.  No Editor Oracle, defina o parâmetro de inicialização **job_queue_processes** com um valor que seja suficiente para permitir a execução do trabalho Xactset. Para obter mais informações sobre esse parâmetro, veja a documentação de banco de dados para o Editor Oracle.  
  
2.  No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Especifique o nome do Publicador Oracle em **\@publisher**, um valor igual a **xactsetbatching** em **\@propertyname** e um valor igual a **enabled** em **\@propertyvalue**.  
  
3.  No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Especifique o nome do Publicador Oracle em **\@publisher**, um valor igual a **xactsetjobinterval** em **\@propertyname** e o intervalo do trabalho, em minutos, em **\@propertyvalue**.  
  
4.  No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Especifique o nome do Publicador Oracle em **\@publisher**, um valor igual a **xactsetjob** em **\@propertyname** e um valor igual a **enabled** em **\@propertyvalue**.  
  
### <a name="to-configure-the-transaction-set-job"></a>Para configurar o trabalho de conjunto de transação  
  
1.  (opcional) No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Especifique o nome do Publicador Oracle em **\@publisher**. Isso retorna as propriedades do trabalho **Xactset** no Publicador.  
  
2.  No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Especifique o nome do Publicador Oracle em **\@publisher**, o nome da propriedade do trabalho Xactset que está sendo definida em **\@propertyname** e a nova configuração em **\@propertyvalue**.  
  
3.  (Opcional) Repita a etapa 2 para cada propriedade de trabalho Xactset que estiver sendo definida. Ao alterar a propriedade **xactsetjobinterval** , é necessário reiniciar o trabalho no Editor Oracle para que o novo intervalo entre em vigor.  
  
### <a name="to-view-properties-of-the-transaction-set-job"></a>Para exibir as propriedades do trabalho de conjunto de transação  
  
1.  No Distributor, execute [sp_helpxactsetjob](../../../relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql.md). Especifique o nome do Publicador Oracle em **\@publisher**.  
  
### <a name="to-disable-the-transaction-set-job"></a>Para desativar o trabalho de conjunto de transação  
  
1.  No Distribuidor, execute [sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Especifique o nome do Publicador Oracle em **\@publisher**, um valor igual a **xactsetjob** em **\@propertyname** e um valor igual a **disabled** em **\@propertyvalue**.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir habilita o trabalho `Xactset` e define um intervalo de três minutos entre as execuções.  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../relational-databases/replication/codesnippet/tsql/configure-the-transactio_1.sql)]  
  
## <a name="see-also"></a>Consulte Também  
 [Ajuste de desempenho para Publicadores Oracle](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  

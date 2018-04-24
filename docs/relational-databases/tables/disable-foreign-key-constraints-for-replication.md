---
title: Desabilitar restrições Foreign Key para replicação | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- constraints [SQL Server], foreign keys
- foreign keys [SQL Server], disabling constraints
- disabling constraints
ms.assetid: 4211f2fd-d16a-4081-995c-43f1f0827f0b
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: fe8e218b469cc68c425fc36888cfc32166eba450
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="disable-foreign-key-constraints-for-replication"></a>Desabilitar restrições FOREIGN KEY para replicação
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Você pode desabilitar as restrições de chave estrangeira para replicação no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Isso pode ser útil se você publicar dados de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Se uma tabela for publicada utilizando replicação, as restrições de chave estrangeira serão desabilitadas automaticamente para operações executadas por agentes de replicação. Quando um agente de replicação executa uma inserção, atualização ou exclusão em um Assinante, a restrição não é verificada; se um usuário executar uma inserção, atualização ou exclusão, a restrição será verificada. A restrição está desabilitada para o agente de replicação porque a restrição já foi verificada no Publicador quando os dados foram inseridos, atualizados ou excluídos originalmente.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para desabilitar uma restrição de chave estrangeira para replicação usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-disable-a-foreign-key-constraint-for-replication"></a>Para desabilitar uma restrição de chave estrangeira para replicação  
  
1.  No **Pesquisador de Objetos**, expanda a tabela com a restrição de chave estrangeira que você deseja modificar e expanda a pasta **Chaves** .  
  
2.  Clique com o botão direito do mouse na restrição de chave estrangeira e clique em **Modificar**.  
  
3.  Na caixa de diálogo **Relações de Chaves Estrangeiras** , selecione o valor **Não** em **Impor para Replicação**.  
  
4.  Clique em **Fechar**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-disable-a-foreign-key-constraint-for-replication"></a>Para desabilitar uma restrição de chave estrangeira para replicação  
  
1.  Para executar esta tarefa no [!INCLUDE[tsql](../../includes/tsql-md.md)], descarte a restrição de chave estrangeira. Em seguida, adicione uma nova restrição de chave estrangeira e especifique a opção NOT FOR REPLICATION.  
  
 Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
###  <a name="TsqlExample"></a>  

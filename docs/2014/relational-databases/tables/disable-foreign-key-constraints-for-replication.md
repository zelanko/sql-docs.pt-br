---
title: Desabilitar restrições Foreign Key para replicação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- constraints [SQL Server], foreign keys
- foreign keys [SQL Server], disabling constraints
- disabling constraints
ms.assetid: 4211f2fd-d16a-4081-995c-43f1f0827f0b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2cd2e4f3e5ee16c02ba48c6cd8ced98c06133dfb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62761082"
---
# <a name="disable-foreign-key-constraints-for-replication"></a>Desabilitar restrições FOREIGN KEY para replicação
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
  
 Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
###  <a name="TsqlExample"></a>  

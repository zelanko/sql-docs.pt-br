---
title: Desabilitar verificação de restrições para replicação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- CHECK constraints, disabling
- constraints [SQL Server], disabling
- disabling constraints
- constraints [SQL Server], check
ms.assetid: af98fc70-24dd-4bd3-a0a3-f701dfa67b2c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f0ffb9af3b02bf8c92041d64b54d06b55a24f42a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061566"
---
# <a name="disable-check-constraints-for-replication"></a>Desabilitar verificação de restrições para replicação
  Você pode desabilitar restrições de verificação no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Você também poderá desabilitar explicitamente as verificações de restrições de replicações, o que pode ser útil se você estiver publicando dados de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Se a uma tabela for publicada utilizando replicação, as verificações de restrições serão desabilitadas automaticamente em operações executadas por agentes de replicação. Quando um agente de replicação executa uma inserção, atualização ou exclusão em um Assinante, a restrição não é verificada; se um usuário executar uma inserção, atualização ou exclusão, a restrição será verificada. A restrição está desabilitada para o agente de replicação porque a restrição já foi verificada no Publicador quando os dados foram inseridos, atualizados ou excluídos originalmente. Para obter mais informações, veja [Especificar opções de esquema](../replication/publish/specify-schema-options.md).  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-disable-a-check-constraint-for-replication"></a>Desabilitar uma verificação de restrição de replicação  
  
1.  No **Pesquisador de Objetos**, expanda a tabela com a restrição de verificação a ser modificada e expanda a pasta **Restrições** .  
  
2.  Clique com o botão direito do mouse na restrição de verificação que você deseja modificar e clique em **Modificar**.  
  
3.  Na caixa de diálogo **Verificar Restrições** , em **Designer de Tabela**, selecione um valor de **Não** para **Impor para replicação**.  
  
4.  Clique em **Fechar**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-disable-a-check-constraint-for-replication"></a>Desabilitar uma verificação de restrição de replicação  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo cria uma tabela com uma coluna IDENTITY e uma restrição CHECK na tabela. Em seguida, o exemplo remove a restrição e a recria especificando a cláusula NOT FOR REPLICATION.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE dbo.doc_exd (column_a int IDENTITY (1,1)   
    CONSTRAINT exd_check CHECK (column_a > 1))   
  
    ALTER TABLE dbo.doc_exd   
    DROP CONSTRAINT exd_check;   
    GO  
    ALTER TABLE dbo.doc_exd    
    ADD CONSTRAINT exd_check CHECK NOT FOR REPLICATION (column_a > 1);  
    ```  
  
 Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
###  <a name="TsqlExample"></a>   
## <a name="see-also"></a>Consulte também  
 [Especificar opções de esquema](../replication/publish/specify-schema-options.md)  
  
  

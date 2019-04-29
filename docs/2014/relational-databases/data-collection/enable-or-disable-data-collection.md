---
title: Habilitar ou desabilitar a coleta de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collector [SQL Server], disabling
- data collector [SQL Server], enabling
ms.assetid: 0137971b-fb48-4a3e-822a-3df2b9bb09d7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 61a5e8c1e3dad99318f14a49f1386757a4ebabe3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62873427"
---
# <a name="enable-or-disable-data-collection"></a>Habilitar ou desabilitar a coleta de dados
  Este tópico descreve como habilitar ou desabilitar a coleta de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para habilitar ou desabilitar a coleta de dados usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 É necessária a associação na função de banco de dados fixa **dc_admin** ou **dc_operator** (com a permissão EXECUTE) para executar esse procedimento.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-enable-the-data-collector"></a>Para habilitar o coletor de dados  
  
1.  No Pesquisador de Objetos, expanda o nó **Gerenciamento** .  
  
2.  Clique com o botão direito do mouse em **Coleta de Dados**e clique em **Habilitar Coleta de Dados**.  
  
#### <a name="to-disable-the-data-collector"></a>Para desabilitar o coletor de dados  
  
1.  No Pesquisador de Objetos, expanda o nó **Gerenciamento** .  
  
2.  Clique com o botão direito do mouse em **Coleta de Dados**e clique em **Desabilitar Coleta de Dados**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-enable-the-data-collector"></a>Para habilitar o coletor de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo usa [sp_syscollector_enable_collector](/sql/relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql) para habilitar o coletor de dados.  
  
```sql  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_enable_collector ;  
```  
  
#### <a name="to-disable-the-data-collector"></a>Para desabilitar o coletor de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo usa [sp_syscollector_disable_collector](/sql/relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql) para desabilitar o coletor de dados.  
  
```sql  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_disable_collector;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Coleta de Dados](data-collection.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)  
  
  

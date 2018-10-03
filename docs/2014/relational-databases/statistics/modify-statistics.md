---
title: Modificar as estatísticas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- statistics [SQL Server], modifying
- modifying statistics
ms.assetid: b06299ca-ed52-411a-b245-45eac4628c99
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0532f2b9ab931eccda5403501a6fe74b3603525c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48165836"
---
# <a name="modify-statistics"></a>Modificar estatísticas
  Você pode modificar as estatísticas existentes no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para modificar as estatísticas usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer que:  
  
-   O usuário tenha a permissão ALTER na tabela ou exibição.  
  
-   O usuário como o proprietário da tabela ou exibição indexada ou um membro de uma das seguintes funções: função de servidor fixa **sysadmin** , função de banco de dados fixa **db_owner** ou a função de banco de dados fixa **db_ddladmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-modify-statistics"></a>Para modificar as estatísticas  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o banco de dados no qual você deseja modificar uma estatística.  
  
2.  Clique no sinal de adição para expandir a pasta **Tabelas** .  
  
3.  Clique no sinal de adição para expandir a tabela na qual você deseja modificar uma estatística.  
  
4.  Clique no sinal de adição para expandir a pasta **Estatísticas** .  
  
5.  Clique com o botão direito do mouse no objeto de estatísticas que você deseja modificar e selecione **Propriedades**.  
  
6.  Na caixa de diálogo **Propriedades de Estatísticas –** *statistics_name* , na página **Geral** , clique em **Adicionar**, **Remover**, **Mover para Cima**, **Mover para Baixo**, any combination, to alter the properties of the statistics. Lembre-se de que o local de uma coluna na grade **Colunas de Estatísticas** pode afetar substancialmente a utilidade das estatísticas.  
  
7.  Clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para modificar as estatísticas**  
  
 Esta tarefa não pode ser executada usando instruções Transact-SQL. Para modificar as estatísticas usando Transact-SQL, primeiro você deve excluir a estatística existente e depois recriá-la com novos atributos.  
  
 Para obter mais informações, veja [DROP STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-statistics-transact-sql) e [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
  

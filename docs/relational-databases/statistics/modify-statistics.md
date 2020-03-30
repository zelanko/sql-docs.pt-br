---
title: Modificar as estatísticas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- statistics [SQL Server], modifying
- modifying statistics
ms.assetid: b06299ca-ed52-411a-b245-45eac4628c99
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c6f34bf5db992f1d7062f9def1805996701eda5f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "72906205"
---
# <a name="modify-statistics"></a>Modificar estatísticas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Você pode modificar as estatísticas existentes no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para modificar as estatísticas usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer que:  
  
-   O usuário tenha a permissão ALTER na tabela ou exibição.  
  
-   O usuário como o proprietário da tabela ou exibição indexada ou um membro de uma das seguintes funções: função de servidor fixa **sysadmin** , função de banco de dados fixa **db_owner** ou a função de banco de dados fixa **db_ddladmin** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-modify-statistics"></a>Para modificar as estatísticas  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o banco de dados no qual você deseja modificar uma estatística.  
  
2.  Clique no sinal de adição para expandir a pasta **Tabelas** .  
  
3.  Clique no sinal de adição para expandir a tabela na qual você deseja modificar uma estatística.  
  
4.  Clique no sinal de adição para expandir a pasta **Estatísticas** .  
  
5.  Clique com o botão direito do mouse no objeto de estatísticas que você deseja modificar e selecione **Propriedades**.  
  
6.  Na caixa de diálogo **Propriedades de Estatísticas –** *statistics_name*, na página **Geral**, clique em **Adicionar**, **Remover**, **Mover para Cima**, **Mover para Baixo**, qualquer combinação, para alterar as propriedades das estatísticas. Lembre-se de que a localização de uma coluna na grade **Colunas de Estatísticas** pode afetar substancialmente a utilidade das estatísticas.  
  
7.  Clique em **OK**.  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para modificar as estatísticas**  
  
 Esta tarefa não pode ser executada usando instruções Transact-SQL. Para modificar as estatísticas usando Transact-SQL, primeiro você deve excluir a estatística existente e depois recriá-la com novos atributos.  
  
 Para obter mais informações, veja [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md) e [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md).  
  
  

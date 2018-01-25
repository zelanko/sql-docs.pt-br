---
title: Alterar a ordem das colunas em uma tabela| Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- columns [SQL Server], change order in a table
- column order, change
ms.assetid: cd99ef56-9085-431a-a0fc-58e7add5399f
caps.latest.revision: "15"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 00fc2cf4f974b02abb6d73ff9d39dc1a8a2f75a7
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="change-column-order-in-a-table"></a>Alterar ordem de colunas em uma tabela
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Você pode alterar a ordem das colunas no Designer de Tabela do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
> [!CAUTION]  
>  A alteração da ordem das colunas de uma tabela pode afetar o código e os aplicativos que dependam da ordem específica das colunas. Isso inclui consultas, exibições, procedimentos armazenados, funções definidas pelo usuário e aplicativos clientes. Analise cuidadosamente todas as alterações que deseja fazer à ordem das colunas antes fazê-las. A prática recomendada é especificar a ordem em que as colunas serão retornadas nos níveis de aplicativo e de consulta. Você não deve confiar no uso de SELECT * para retornar todas as colunas na ordem esperada com base na ordem em que são definidas na tabela. Sempre especifique as colunas por nome em suas consultas e aplicativos na ordem em que você gostaria que elas aparecessem.  
  
 **Neste tópico**  
  
-   **Para alterar a ordem das colunas usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-change-the-column-order"></a>Para alterar a ordem das colunas  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela cujas colunas você deseja reordenar e clique em **Design**.  
  
2.  Selecione a caixa à esquerda do nome da coluna que você deseja reordenar.  
  
3.  Arraste a coluna para outro local dentro da tabela.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para alterar a ordem das colunas**  
  
 Esta tarefa não pode ser executada usando instruções Transact-SQL.  
  
###  <a name="TsqlExample"></a>  

---
title: Alterar a ordem das colunas em uma tabela| Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], change order in a table
- column order, change
ms.assetid: cd99ef56-9085-431a-a0fc-58e7add5399f
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6263a1ad69b1c7bac5511a5fc3433b2517d1f3d5
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38040244"
---
# <a name="change-column-order-in-a-table"></a>Alterar ordem de colunas em uma tabela
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

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

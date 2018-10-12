---
title: Modificar Restrições de Borda | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- alter edge constraints
- edge constraints [SQL Server]
- CONNECTION constraints
- edge constraints [Azure SQL Database]
- graph edge constraints
- SQL Graph
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e5b6a471156f0b1371c727ce96aac72f4f812dac
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47650244"
---
# <a name="modify-edge-constraints"></a>Modificar Restrições de Borda
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  Você pode modificar uma restrição de borda no [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Você pode modificar a restrição de borda de uma tabela de borda alterando a ordem de cláusulas da restrição de borda ou adicionando uma nova cláusula.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para modificar uma restrição de borda usando:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL
 Para modificar uma restrição de borda usando o Transact-SQL, exclua primeiramente a restrição de borda existente e, em seguida, recrie-a com a nova definição. Para obter mais informações, consulte [Excluir restrição de borda](../../relational-databases/tables/delete-edge-constraint.md) e [Criar restrições de borda](../../relational-databases/tables/create-edge-constraints.md).    
 

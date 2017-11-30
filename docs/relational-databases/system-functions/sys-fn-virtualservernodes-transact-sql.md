---
title: fn_virtualservernodes (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- fn_virtualservernodes
- fn_virtualservernodes_TSQL
dev_langs: TSQL
helpviewer_keywords:
- nodes [Faillover Clustering], virtual servers
- nodes [Faillover Clustering]
- virtual servers [Faillover Clustering]
- failover clustering [SQL Server], nodes
- fn_virtualservernodes function
- sys.fn_virtualservernodes function
ms.assetid: 257f3b8d-93c0-4444-87f1-ea211bd8cad0
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 96cd4eb10e25a06b0ea4bf3258ef56ef72ac30d1
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="sysfnvirtualservernodes-transact-sql"></a>sys.fn_virtualservernodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Retorna uma lista de nós de instância em cluster de failover nos quais uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser executada. Essas informações são úteis em ambientes de failover em cluster.  
  
> [!IMPORTANT]  
>  Isso [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a função do sistema é incluída para compatibilidade com versões anteriores. Recomendamos que você use [sys.DM os_cluster_nodes &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn_virtualservernodes()  
```  
  
## <a name="tables-returned"></a>Tabelas retornadas  
 Se o servidor atual é um servidor clusterizado, **fn_virtualservernodes** retorna uma lista de nós de instância de cluster de failover no qual essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi definido.  
  
 Se a instância de servidor atual não é um servidor clusterizado, **fn_virtualservernodes** retorna um conjunto de linhas vazio.  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ter permissão de VIEW SERVER STATE para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte usa `fn_virtualservernodes` para consultar em uma instância de servidor clusterizado:  
  
```  
SELECT * FROM fn_virtualservernodes();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 NodeName  
  
 -------\-  
  
 SS3-CLUSN1  
  
 SS3-CLUSN2  
  
## <a name="see-also"></a>Consulte também  
 [sys.DM os_cluster_nodes &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [sys.fn_servershareddrives &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-servershareddrives-transact-sql.md)  
  
  

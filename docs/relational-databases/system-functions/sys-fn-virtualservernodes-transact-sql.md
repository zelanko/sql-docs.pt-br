---
title: sys.fn_virtualservernodes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_virtualservernodes
- fn_virtualservernodes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- nodes [Faillover Clustering], virtual servers
- nodes [Faillover Clustering]
- virtual servers [Faillover Clustering]
- failover clustering [SQL Server], nodes
- fn_virtualservernodes function
- sys.fn_virtualservernodes function
ms.assetid: 257f3b8d-93c0-4444-87f1-ea211bd8cad0
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0ec290179cdbf3e61f0e5033acbf3156dbc6441a
ms.sourcegitcommit: 8515bb2021cfbc7791318527b8554654203db4ad
ms.contentlocale: pt-BR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86091658"
---
# <a name="sysfn_virtualservernodes-transact-sql"></a>sys.fn_virtualservernodes (Transact-SQL)
[!INCLUDE [sql-asdbmi-pdw](../../includes/applies-to-version/sql-asdbmi-pdw.md)]

  Retorna uma lista de nós de instância em cluster de failover nos quais uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser executada. Essas informações são úteis em ambientes de failover em cluster.  
  
> [!IMPORTANT]
>  Essa [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] função do sistema está incluída para compatibilidade com versões anteriores. É recomendável usar [Sys. dm_os_cluster_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn_virtualservernodes()  
```  
  
## <a name="tables-returned"></a>Tabelas retornadas  
 Se o servidor atual for um servidor em cluster, **fn_virtualservernodes** retornará uma lista de nós de instância clusterizada de failover em que essa instância do foi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definida.  
  
 Se a instância do servidor atual não for um servidor clusterizado, **fn_virtualservernodes** retornará um conjunto de linhas vazio.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [sys. dm_os_cluster_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [sys.fn_servershareddrives &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-servershareddrives-transact-sql.md)  
  
  

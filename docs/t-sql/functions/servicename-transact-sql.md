---
title: '@@SERVICENAME (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- '@@SERVICENAME_TSQL'
- '@@SERVICENAME'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@SERVICENAME function'
- names [SQL Server], registry keys
- registry keys [SQL Server]
ms.assetid: 5b0b35be-50ae-411d-a607-bf7464b73624
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 457749a5374f208e78cf26f495fdf026779a80f4
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37785377"
---
# <a name="x40x40servicename-transact-sql"></a>&#x40;&#x40;SERVICENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Retorna o nome da chave do Registro na qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executado. @@SERVICENAME retornará 'MSSQLSERVER' se a instância atual for a instância padrão; essa função retornará o nome da instância se a atual for uma instância nomeada.  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
@@SERVICENAME  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar**  
  
## <a name="remarks"></a>Remarks  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado como um serviço denominado MSSQLServer.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra o uso de `@@SERVICENAME`.  
  
```  
SELECT @@SERVICENAME AS 'Service Name';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Service Name                    
------------------------------  
MSSQLSERVER                     
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de configuração &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [Gerenciar os serviços do Mecanismo de Banco de Dados](../../database-engine/configure-windows/manage-the-database-engine-services.md)  
  
  

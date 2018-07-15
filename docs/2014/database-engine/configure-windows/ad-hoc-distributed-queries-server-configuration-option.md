---
title: Opção de configuração de servidor ad hoc distributed queries | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OPENROWSET function, ad hoc distributed queries option
- Ad Hoc Distributed Queries option
- ad hoc distributed queries
- 7415 (Database Engine Error)
- OPENDATASOURCE function, ad hoc distributed queries option
- ad hoc access
ms.assetid: 5b982015-e196-44c3-83b8-275fb9d769b2
caps.latest.revision: 27
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2451cdb31019da9c21efabec216fdf24b7c71bbe
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37286032"
---
# <a name="ad-hoc-distributed-queries-server-configuration-option"></a>Opção de configuração de servidor ad hoc distributed queries
  Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não permite consultas distribuídas ad hoc que usam OPENROWSET e OPENDATASOURCE. Quando esta opção é definida como 1, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite acesso ad hoc. Quando esta opção não é definida ou é definida como 0, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não permite o acesso ad hoc.  
  
 As consultas distribuídas ad hoc usam as funções OPENROWSET e OPENDATASOURCE para se conectarem a fontes de dados remotas que usam OLE DB. OPENROWSET e OPENDATASOURCE devem ser usados apenas para fazer referência a fontes de dados OLE DB que são acessadas com pouca frequência. Para qualquer fonte de dados que será acessada muitas vezes, defina um servidor vinculado.  
  
> [!IMPORTANT]  
>  A habilitação do uso de nomes ad hoc indica que qualquer logon autenticado para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode acessar o provedor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Os administradores devem habilitar esse recurso para provedores seguros, que podem ser acessados por qualquer logon local.  
  
## <a name="remarks"></a>Remarks  
 Tentar fazer uma conexão ad hoc com a opção **Ad Hoc Distributed Queries** não habilitada resultará em erro: Msg 7415, Level 16, State 1, Line 1  
  
 Acesso ad hoc negado ao provedor OLE DB 'Microsoft.ACE.OLEDB.12.0'. É necessário acessar esse provedor através de um servidor vinculado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir habilita consultas distribuídas ad hoc e, em seguida, consulta um servidor chamado `Seattle1` usando a função `OPENROWSET` .  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
sp_configure 'Ad Hoc Distributed Queries', 1;  
RECONFIGURE;  
GO  
  
SELECT a.*  
FROM OPENROWSET('SQLNCLI', 'Server=Seattle1;Trusted_Connection=yes;',  
     'SELECT GroupName, Name, DepartmentID  
      FROM AdventureWorks2012.HumanResources.Department  
      ORDER BY GroupName, Name') AS a;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [Servidores vinculados &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [OPENDATASOURCE &#40;Transact-SQL&#41;](/sql/t-sql/functions/opendatasource-transact-sql)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)  
  
  

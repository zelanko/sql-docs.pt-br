---
title: dbo. server_quotas (banco de dados do SQL Azure) | Microsoft Docs
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 08/02/2016
ms.prod: 
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.server_quotas
- dbo.server_quotas_TSQL
- server_quotas
- server_quotas_TSQL
dev_langs: TSQL
helpviewer_keywords: server_quotas
ms.assetid: 34423903-1aaa-4a55-88a6-8228315d84e7
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 612f4d0a819c1271ca9b5e8b9fda8f224ae6fbe6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="dboserverquotas-azure-sql-database"></a>dbo.server_quotas (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> **IMPORTANTE:** Isso se aplica a  **[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11 apenas!**  
>   
>  Esse recurso está em um estado de visualização. Não usa uma dependência na implementação específica desse recurso porque o recurso pode ser alterado ou removido em uma versão futura.  
  
 Retorna os tipos de quota de bancos de dados disponíveis no servidor.  
  
|Nome da coluna|Tipo de Dados|Description|  
|-----------------|---------------|-----------------|  
|quota_name|**nvarchar**|O tipo de quota para o servidor. O tipo **Premium_database** é equivalente a bancos de dados com uma reserva de recurso.|  
|quota_value|**int**|O número do tipo de quota permitido no servidor.|  
  
## <a name="permissions"></a>Permissões  
 Essa exibição está disponível para todas as funções de usuário com permissões para se conectar ao virtual **mestre** banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando bancos de dados Premium](http://go.microsoft.com/fwlink/?LinkID=311927)  
  
  

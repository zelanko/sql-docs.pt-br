---
title: dbo. server_quotas (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- dbo.server_quotas
- dbo.server_quotas_TSQL
- server_quotas
- server_quotas_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server_quotas
ms.assetid: 34423903-1aaa-4a55-88a6-8228315d84e7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 657376be08e4cd404ce53d78114604cdd11fbda2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63005832"
---
# <a name="dboserverquotas-azure-sql-database"></a>dbo.server_quotas (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> **IMPORTANTE:** Isso se aplica ao  **[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11 apenas!**  
>   
>  Esse recurso está em um estado de visualização. Não usa uma dependência na implementação específica desse recurso porque o recurso pode ser alterado ou removido em uma versão futura.  
  
 Retorna os tipos de quota de bancos de dados disponíveis no servidor.  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|  
|quota_name|**nvarchar**|O tipo de quota para o servidor. O tipo **Premium_database** é equivalente a bancos de dados com uma reserva de recursos.|  
|quota_value|**int**|O número do tipo de quota permitido no servidor.|  
  
## <a name="permissions"></a>Permissões  
 Essa exibição está disponível para todas as funções de usuário com permissões para se conectar ao virtual **mestre** banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando bancos de dados Premium](https://go.microsoft.com/fwlink/?LinkID=311927)  
  
  

---
title: sys. database_usage (banco de dados do SQL Azure) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- database_usage
- database_usage_TSQL
- sys.database_usage_TSQL
- sys.database_usage
dev_langs:
- TSQL
helpviewer_keywords:
- database_usage
- sys.database_usage
ms.assetid: be6820de-60bf-4ddd-ace7-4077893d630f
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 670c1a9c7028d495141247b5f2b8b35f85142d6f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sysdatabaseusage-azure-sql-database"></a>sys.database_usage (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **Observação: Isso se aplica somente a V11 de banco de dados do SQL Azure.**  
  
 Lista o número, tipo e duração de bancos de dados sobre o [!INCLUDE[ssSDS](../../includes/sssds-md.md)] server.  
  
 O **sys. database_usage** exibição contém as seguintes colunas.  
  
|Nome da coluna|Description|  
|-----------------|-----------------|  
|time|A data em que os eventos de uso ocorreram.|  
|sku|O tipo de camada de serviço para o banco de dados: **Web**, **Business**, **básica**, **padrão**, **Premium**|  
|quantity|O número máximo de bancos de dados de um tipo de SKU que existiu durante o dia.|  
  
## <a name="permissions"></a>Permissões  
 Acesso somente leitura a essa exibição está disponível para todos os usuários com permissões para conectar o **mestre** banco de dados.  
  
## <a name="remarks"></a>Comentários  
 O **sys. database_usage** exibição retorna uma linha para cada dia da sua assinatura.  
  
## <a name="see-also"></a>Consulte também  
 [Detalhes de preços de banco de dados SQL](http://go.microsoft.com/fwlink/?LinkID=394978)   
 [Contas e cobrança no banco de dados do Microsoft SQL Azure](http://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  

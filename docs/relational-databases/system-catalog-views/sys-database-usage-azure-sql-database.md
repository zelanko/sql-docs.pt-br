---
title: sys. database_usage (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 1816ab7f6e4ad35453c61fed8670c27b1f0ac833
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43027381"
---
# <a name="sysdatabaseusage-azure-sql-database"></a>sys.database_usage (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **Observação: Isso se aplica somente à V11 de banco de dados SQL do Azure.**  
  
 Lista o número, tipo e duração dos bancos de dados sobre o [!INCLUDE[ssSDS](../../includes/sssds-md.md)] server.  
  
 O **sys. database_usage** exibição contém as colunas a seguir.  
  
|Nome da coluna|Description|  
|-----------------|-----------------|  
|time|A data em que os eventos de uso ocorreram.|  
|sku|O tipo de camada de serviço para o banco de dados: **Web**, **Business**, **básica**, **padrão**, **Premium**|  
|quantity|O número máximo de bancos de dados de um tipo de SKU que existiu durante o dia.|  
  
## <a name="permissions"></a>Permissões  
 Acesso somente leitura a essa exibição está disponível para todos os usuários com permissões para conectar o **mestre** banco de dados.  
  
## <a name="remarks"></a>Remarks  
 O **sys. database_usage** exibição retorna uma linha para cada dia da sua assinatura.  
  
## <a name="see-also"></a>Consulte também  
 [Detalhes de preços de banco de dados SQL](http://go.microsoft.com/fwlink/?LinkID=394978)   
 [Contas e cobrança no Windows Azure SQL Database](http://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  

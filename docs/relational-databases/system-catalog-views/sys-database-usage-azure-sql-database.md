---
description: sys.database_usage (Banco de Dados SQL do Azure)
title: sys.database_usage (banco de dados SQL do Azure) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
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
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current
ms.openlocfilehash: e80549106907d042a16197b3ecaf4d6b2dd3f6c7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475197"
---
# <a name="sysdatabase_usage-azure-sql-database"></a>sys.database_usage (Banco de Dados SQL do Azure)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  **Observação: isso se aplica somente ao banco de dados SQL do Azure v11.**  
  
 Lista o número, o tipo e a duração dos bancos de dados no [!INCLUDE[ssSDS](../../includes/sssds-md.md)] servidor.  
  
 A exibição **Sys.database_usage** contém as colunas a seguir.  
  
|Nome da coluna|Descrição|  
|-----------------|-----------------|  
|time|A data em que os eventos de uso ocorreram.|  
|sku|O tipo de camada de serviço para o banco de dados: **Web**, **Business**, **Basic**, **Standard**, **Premium**|  
|quantidade|O número máximo de bancos de dados de um tipo de SKU que existiu durante o dia.|  
  
## <a name="permissions"></a>Permissões  
 O acesso somente leitura a essa exibição está disponível para todos os usuários com permissões para se conectar ao banco de dados **mestre** .  
  
## <a name="remarks"></a>Comentários  
 A exibição **Sys.database_usage** retorna uma linha para cada dia da sua assinatura.  
  
## <a name="see-also"></a>Consulte Também  
 [Detalhes de preços do banco de dados SQL](https://go.microsoft.com/fwlink/?LinkID=394978)   
 [Contas e cobrança no Banco de dados SQL do Azure](/previous-versions/azure/ee621788(v=azure.100))  
  

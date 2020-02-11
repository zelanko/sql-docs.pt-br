---
title: sys. database_usage (banco de dados SQL do Azure) | Microsoft Docs
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
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 0a0789ebd9a5aa4bd10605d69afa59a586ce75b2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70155541"
---
# <a name="sysdatabase_usage-azure-sql-database"></a>sys.database_usage (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **Observação: isso se aplica somente ao banco de dados SQL do Azure v11.**  
  
 Lista o número, o tipo e a duração dos bancos de dados no [!INCLUDE[ssSDS](../../includes/sssds-md.md)] servidor.  
  
 A exibição **Sys. database_usage** contém as colunas a seguir.  
  
|Nome da coluna|DESCRIÇÃO|  
|-----------------|-----------------|  
|time|A data em que os eventos de uso ocorreram.|  
|sku|O tipo de camada de serviço para o banco de dados: **Web**, **Business**, **Basic**, **Standard**, **Premium**|  
|quantidade|O número máximo de bancos de dados de um tipo de SKU que existiu durante o dia.|  
  
## <a name="permissions"></a>Permissões  
 O acesso somente leitura a essa exibição está disponível para todos os usuários com permissões para se conectar ao banco de dados **mestre** .  
  
## <a name="remarks"></a>Comentários  
 A exibição **Sys. database_usage** retorna uma linha para cada dia da sua assinatura.  
  
## <a name="see-also"></a>Consulte Também  
 [Detalhes de preços do banco de dados SQL](https://go.microsoft.com/fwlink/?LinkID=394978)   
 [Contas e cobrança no Banco de dados SQL do Azure](https://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  

---
title: sys. fulltext_catalogs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.fulltext_catalogs_TSQL
- sys.fulltext_catalogs
- fulltext_catalogs
- fulltext_catalogs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_catalogs catalog view
ms.assetid: cf1489ff-4819-41fa-a62a-4ed797a16207
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1f4d19de44beaf6e63a7ae84ba15e8d7353945e0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysfulltextcatalogs-transact-sql"></a>sys.fulltext_catalogs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada catálogo de texto completo.  
  
> [!NOTE]  
>  As colunas a seguir serão removidas em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **data_space_id**, **file_id**, e **caminho**. Não as utilize em novos desenvolvimentos e, assim que possível, modifique os aplicativos que atualmente utilizam alguma dessas colunas.  
 
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|fulltext_catalog_id|**Int**|Identificação do catálogo de texto completo. É exclusivo nos catálogos de texto completo do banco de dados.|  
|nome|**sysname**|Nome do catálogo. É exclusiva no banco de dados.|  
|path|**nvarchar(260)**|Nome do diretório de catálogo no sistema de arquivos.|  
|is_default|**bit**|O catálogo de texto completo padrão.<br /><br /> True = É padrão.<br /><br /> False = Não é padrão.|  
|is_accent_sensitivity_on|**bit**|Configuração da distinção de acentos do catálogo.<br /><br /> True = Diferencia acentos.<br /><br /> False = Não diferencia acentos.|  
|data_space_id|**Int**|Grupo de arquivos no qual esse catálogo foi criado.|  
|file_id|**Int**|ID do arquivo de texto completo associado ao catálogo.|  
|principal_id|**Int**|ID da entidade de segurança do banco de dados que é proprietária do catálogo de texto completo.|  
|is_importing|**bit**|Indica se o catálogo de texto completo está sendo importado:<br /><br /> 1 = O catálogo está sendo importado.<br /><br /> 2 = O catálogo não está sendo importado.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [CRIAR o catálogo de texto completo & #40; Transact-SQL & #41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [DROP FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)  
  
  

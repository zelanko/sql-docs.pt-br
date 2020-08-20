---
description: sys.fulltext_catalogs (Transact-SQL)
title: sys. fulltext_catalogs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
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
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 886f8d99e286fd026e5e4435c8daa9192d22ce99
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498350"
---
# <a name="sysfulltext_catalogs-transact-sql"></a>sys.fulltext_catalogs (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada catálogo de texto completo.  
  
> [!NOTE]  
>  As colunas a seguir serão removidas em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] : **data_space_id**, **file_id**e **Path**. Não as utilize em novos desenvolvimentos e, assim que possível, modifique os aplicativos que atualmente utilizam alguma dessas colunas.  
 
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|fulltext_catalog_id|**int**|Identificação do catálogo de texto completo. É exclusivo nos catálogos de texto completo do banco de dados.|  
|name|**sysname**|Nome do catálogo. É exclusiva no banco de dados.|  
|caminho|**nvarchar(260)**|Nome do diretório de catálogo no sistema de arquivos.|  
|is_default|**bit**|O catálogo de texto completo padrão.<br /><br /> True = É padrão.<br /><br /> False = Não é padrão.|  
|is_accent_sensitivity_on|**bit**|Configuração da distinção de acentos do catálogo.<br /><br /> True = Diferencia acentos.<br /><br /> False = Não diferencia acentos.|  
|data_space_id|**int**|Grupo de arquivos no qual esse catálogo foi criado.|  
|file_id|**int**|ID do arquivo de texto completo associado ao catálogo.|  
|principal_id|**int**|ID da entidade de segurança do banco de dados que é proprietária do catálogo de texto completo.|  
|is_importing|**bit**|Indica se o catálogo de texto completo está sendo importado:<br /><br /> 1 = O catálogo está sendo importado.<br /><br /> 2 = O catálogo não está sendo importado.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [ALTERAR o catálogo de texto completo &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [DROP FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)  
  
  

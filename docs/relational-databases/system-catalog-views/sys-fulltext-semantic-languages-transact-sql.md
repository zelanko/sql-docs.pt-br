---
title: sys.fulltext_semantic_languages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fulltext_semantic_languages
- fulltext_semantic_languages_TSQL
- sys.fulltext_semantic_languages
- sys.fulltext_semantic_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_semantic_languages catalog view
ms.assetid: b42a85e6-1db9-4a22-8a70-014574c95198
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
ms.openlocfilehash: f1acc995223ba9785055839beb5e12b11ea7494f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "64945657"
---
# <a name="sysfulltextsemanticlanguages-transact-sql"></a>sys.fulltext_semantic_languages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada idioma cujo modelo de estatística está registrado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando um modelo de idioma está registrado, o idioma é habilitado para indexação semântica.  
  
 Esta exibição do catálogo é semelhante à [sys. fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).  
    
||||  
|-|-|-|  
|**Nome da coluna**|**Tipo**|**Descrição**|  
|lcid|INT|LCID (ID de localidade do Microsoft Windows) do idioma.|  
|nome|sysname|É o valor do alias em [sys. syslanguages &#40;Transact-SQL&#41; ](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) correspondente ao valor de **lcid**, ou a representação de cadeia de caracteres do LCID numérico.|  
  
## <a name="general-remarks"></a>Comentários gerais  
 Para obter mais informações, veja [Instalar e configurar a pesquisa semântica](../../relational-databases/search/install-and-configure-semantic-search.md).  
  
## <a name="metadata"></a>Metadados  
 Para obter mais informações sobre o banco de dados de estatísticas semânticas de idioma que está instalado para dar suporte à indexação semântica, consulte a exibição do catálogo [sys. fulltext_semantic_language_statistics_database &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md).  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 A visibilidade dos metadados em exibições do catálogo está limitada aos protegíveis que pertencem a um usuário ou para os quais o usuário recebeu permissão.  
  
## <a name="examples"></a>Exemplos  
 A exemplo a seguir mostra como consultar **sys. fulltext_semantic_languages** para obter informações sobre todos os modelos de idioma registrados para indexação semântica na instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
SELECT * FROM sys.fulltext_semantic_languages;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Instalar e configurar a pesquisa semântica](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  

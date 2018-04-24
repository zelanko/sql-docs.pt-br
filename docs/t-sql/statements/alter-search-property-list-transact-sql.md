---
title: ALTER SEARCH PROPERTY LIST (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER_SEARCH_PROPERTY_TSQL
- ALTER_SEARCH_PROPERTY_LIST_TSQL
- ALTER SEARCH PROPERTY LIST
- ALTER SEARCH PROPERTY
- ALTER_SEARCH_TSQL
- ALTER SEARCH
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search property lists [SQL Server], altering
- ALTER SEARCH PROPERTY LIST statement
ms.assetid: 0436e4a8-ca26-4d23-93f1-e31e2a1c8bfb
caps.latest.revision: 55
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: be317f32f0308766e6ad50374d677c2784218ebc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="alter-search-property-list-transact-sql"></a>ALTER SEARCH PROPERTY LIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Adiciona uma propriedade de pesquisa especificada ou a remove da lista de propriedades de pesquisa especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ALTER SEARCH PROPERTY LIST list_name  
{  
   ADD 'property_name'  
     WITH   
      (   
          PROPERTY_SET_GUID = 'property_set_guid'  
        , PROPERTY_INT_ID = property_int_id  
      [ , PROPERTY_DESCRIPTION = 'property_description' ]  
      )  
 | DROP 'property_name'   
}  
;  
```  
  
## <a name="arguments"></a>Argumentos  
 *list_name*  
 É o nome da lista de propriedades que está sendo alterada. *list_name* é um identificador.  
  
 Para exibir os nomes das listas de propriedades existentes, use a exibição do catálogo [sys.registered_search_property_lists](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md), da seguinte maneira:  
  
```  
SELECT name FROM sys.registered_search_property_lists;  
```  
  
 ADD  
 Adiciona uma propriedade de pesquisa especificada à lista de propriedades especificada por *list_name*. A propriedade é registrada para a lista de propriedades de pesquisa. Para que as propriedades recém-adicionadas possam ser usadas para pesquisa de propriedade, os índices ou o índice de texto completo deve ser populado novamente. Para obter mais informações, consulte [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md).  
  
> [!NOTE]  
>  Para adicionar determinada propriedade de pesquisa a uma lista de propriedades de pesquisa, você precisa fornecer sua GUID do conjunto de propriedades (*property_set_guid*) e a ID int da propriedade (*property_int_id*). Para obter mais informações, consulte "Obtendo GUIDS e identificações do conjunto de propriedades" posteriormente neste tópico.  
  
 *property_name*  
 Especifica o nome a ser usado para identificar a propriedade em consultas de texto completo. *property_name* deve identificar a propriedade exclusivamente dentro do conjunto de propriedades. Um nome de propriedade pode conter espaços internos. O tamanho máximo do *property_name* é de 256 caracteres. Esse nome pode ser um nome amigável, como Autor ou Endereço Residencial ou pode ser o nome canônico do Windows da propriedade, como **System.Author** ou **System.Contact.HomeAddress**.  
  
 Os desenvolvedores precisarão usar o valor que você especificar para *property_name* para identificar a propriedade no predicado [CONTAINS](../../t-sql/queries/contains-transact-sql.md). Portanto, ao adicionar uma propriedade, é importante especificar um valor que representa significativamente a propriedade definida pelo GUID do conjunto de propriedades (*property_set_guid*) e o identificador da propriedade (*property_int_id*) especificados. Para obter mais informações sobre nomes de propriedades, consulte “Comentários”, posteriormente neste tópico.  
  
 Para exibir os nomes das propriedades existentes em uma lista de propriedades de pesquisa do banco de dados atual, use a exibição do catálogo [sys.registered_search_properties](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md), da seguinte maneira:  
  
```  
SELECT property_name FROM sys.registered_search_properties;  
```  
  
 PROPERTY_SET_GUID ='*property_set_guid*'  
 Especifica o identificador do conjunto de propriedades ao qual a propriedade pertence. Esse é um GUID (identificador global exclusivo). Para obter informações sobre como obter esse valor, consulte “Comentários”, posteriormente neste tópico.  
  
 Para exibir o GUID do conjunto de propriedades de qualquer propriedade existente em uma lista de propriedades do banco de dados atual, use a exibição do catálogo [sys.registered_search_properties](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md), da seguinte maneira:  
  
```  
SELECT property_set_guid FROM sys.registered_search_properties;  
```  
  
 PROPERTY_INT_ID =*property_int_id*  
 Especifica o inteiro que identifica a propriedade dentro do conjunto de propriedades correspondente. Para obter informações sobre como obter esse valor, consulte "Comentários".  
  
 Para exibir o identificador de inteiro de qualquer propriedade existente em uma lista de propriedades do banco de dados atual, use a exibição do catálogo [sys.registered_search_properties](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md), da seguinte maneira:  
  
```  
SELECT property_int_id FROM sys.registered_search_properties;  
```  
  
> [!NOTE]  
>  Uma combinação especificada de *property_set_guid* e *property_int_id* deve ser exclusiva em uma lista de propriedades de pesquisa. Se você tentar adicionar uma combinação existente, haverá falha na operação ALTER SEARCH PROPERTY LIST e um erro será gerado. Isso significa que você pode definir apenas um nome para uma determinada propriedade.  
  
 PROPERTY_DESCRIPTION ='*property_description*'  
 Especifica uma descrição definida pelo usuário da propriedade. *property_description* é uma cadeia de caracteres de até 512 caracteres. Essa opção é opcional.  
  
 DROP  
 Remove a propriedade especificada da lista de propriedades especificada por *list_name*. O cancelamento de uma propriedade cancela seu registro, portanto, ela não será mais pesquisável.  
  
## <a name="remarks"></a>Remarks  
 Cada índice de texto completo pode ter apenas uma lista de propriedades de pesquisa.  
  
 Para habilitar consultas em uma determinada propriedade de pesquisa, você deve adicioná-la à lista de propriedades de pesquisa do índice de texto completo e, em seguida, popular o índice novamente.  
  
 Ao especificar uma propriedade, você pode organizar as cláusulas PROPERTY_SET_GUID, PROPERTY_INT_ID e PROPERTY_DESCRIPTION em qualquer ordem, como uma lista separada por vírgulas dentro de parênteses, por exemplo:  
  
```  
ALTER SEARCH PROPERTY LIST CVitaProperties  
ADD 'System.Author'   
WITH (   
      PROPERTY_DESCRIPTION = 'Author or authors of a given document.',  
      PROPERTY_SET_GUID   = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9',   
      PROPERTY_INT_ID = 4   
      );  
```  
  
> [!NOTE]  
>  Esse exemplo usa o nome de propriedade, `System.Author`, que é semelhante ao conceito de nomes de propriedades canônicos introduzido no Windows Vista (nome canônico do Windows).  
  
## <a name="obtaining-property-values"></a>Obtendo valores de propriedades  
 A pesquisa de texto completo mapeia uma propriedade de pesquisa para um índice de texto completo por meio do uso do GUID de seu conjunto de propriedades e ID de inteiro da propriedade. Para obter informações sobre como obtê-los para propriedades definidas pela Microsoft, consulte [Localizar GUIDs do conjunto de propriedades e IDs de inteiro de propriedade para propriedades de pesquisa](../../relational-databases/search/find-property-set-guids-and-property-integer-ids-for-search-properties.md). Para obter informações sobre propriedades definidas por um ISV (fornecedor independente de software), consulte a documentação daquele fornecedor.  
  
## <a name="making-added-properties-searchable"></a>Tornando pesquisáveis as propriedades adicionadas  
 A adição de uma propriedade de pesquisa a uma lista de propriedades de pesquisa registra a propriedade. Uma propriedade recém-adicionada pode ser especificada imediatamente em consultas [CONTAINS](../../t-sql/queries/contains-transact-sql.md). Porém, consultas de texto completo com escopo de propriedade em uma propriedade recém-adicionada não retornarão documentos até que o índice de texto completo associado esteja populado novamente. Por exemplo, a seguinte consulta com escopo na propriedade em uma propriedade recém-adicionada, *new_search_property*, não retornará nenhum documento até que o índice de texto completo associado à tabela de destino (*table_name*) seja populado novamente:  
  
```  
SELECT column_name  
FROM table_name  
WHERE CONTAINS( PROPERTY( column_name, 'new_search_property' ), 
               'contains_search_condition');  
GO   
```  
  
 Para iniciar uma população completa, use a seguinte instrução [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md):  
  
```  
USE database_name;  
GO  
ALTER FULLTEXT INDEX ON table_name START FULL POPULATION;  
GO  
```  
  
> [!NOTE]  
>  A repopulação não é necessária depois que uma propriedade é removida de uma lista de propriedades, porque apenas as propriedades que permanecem na lista de propriedades de pesquisa estão disponíveis para consulta de texto completo.  
  
## <a name="related-references"></a>Referências relacionadas  
 **Para criar uma lista de propriedades**  
  
-   [CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)  
  
 **Para remover uma lista de propriedades**  
  
-   [DROP SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)  
  
 **Para adicionar ou remover uma lista de propriedades em um índice de texto completo**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
 **Para executar uma população em um índice de texto completo**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
##  <a name="Permissions"></a> Permissões  
 Requer a permissão CONTROL na lista de propriedades.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-adding-a-property"></a>A. Adicionando uma propriedade  
 O exemplo a seguir adiciona várias propriedades — `Title`, `Author` e `Tags` — à lista de propriedades denominada `DocumentPropertyList`.  
  
> [!NOTE]  
>  Para obter um exemplo que cria uma lista de propriedades `DocumentPropertyList`, consulte [CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-search-property-list-transact-sql.md).  
  
```  
ALTER SEARCH PROPERTY LIST DocumentPropertyList  
   ADD 'Title'   
   WITH ( PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9', PROPERTY_INT_ID = 2,   
      PROPERTY_DESCRIPTION = 'System.Title - Title of the item.' );  
  
ALTER SEARCH PROPERTY LIST DocumentPropertyList   
    ADD 'Author'  
   WITH ( PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9', PROPERTY_INT_ID = 4,   
      PROPERTY_DESCRIPTION = 'System.Author - Author or authors of the item.' );  
  
ALTER SEARCH PROPERTY LIST DocumentPropertyList   
    ADD 'Tags'  
   WITH ( PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9', PROPERTY_INT_ID = 5,   
      PROPERTY_DESCRIPTION = 
          'System.Keywords - Set of keywords (also known as tags) assigned to the item.' );  
```  
  
> [!NOTE]  
>  Você deve associar uma determinada lista de propriedades de pesquisa a um índice de texto completo antes de usá-la para consultas com escopo de propriedade. Para fazer isso, use uma instrução [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) e especifique a cláusula SET SEARCH PROPERTY LIST.  
  
### <a name="b-dropping-a-property"></a>B. Cancelando uma propriedade  
 O exemplo a seguir cancela a propriedade `Comments` da lista de propriedades `DocumentPropertyList`.  
  
```  
ALTER SEARCH PROPERTY LIST DocumentPropertyList  
DROP 'Comments' ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)   
 [DROP SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)   
 [sys.registered_search_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)   
 [Pesquisar propriedades de documento com listas de propriedades de pesquisa](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [Localizar GUIDs do conjunto de propriedades e IDs de inteiro de propriedade para propriedades de pesquisa](../../relational-databases/search/find-property-set-guids-and-property-integer-ids-for-search-properties.md)  
  
  

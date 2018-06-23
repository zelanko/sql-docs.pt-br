---
title: Editor de lista de propriedades de pesquisa | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.spl.searchpropertylisteditor.f1
ms.assetid: 0f3ced6e-0dfd-49fc-b175-82378c3d668e
caps.latest.revision: 26
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e34bcf522675e13e9b1fa987f0f3bfc6aba36efb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115700"
---
# <a name="search-property-list-editor"></a>Editor da Lista de Propriedades de Pesquisa
  Use esta caixa de diálogo para adicionar ou excluir propriedades em uma lista de propriedades de pesquisa.  
  
## <a name="to-use-sql-server-management-studio-to-manage-search-property-lists"></a>Para usar o SQL Server Management Studio para gerenciar listas de propriedades de pesquisa  
 Para obter informações sobre como criar, exibir ou excluir uma lista de propriedades de pesquisa e sobre como configurar um índice de texto completo para pesquisa de propriedade, consulte [pesquisar propriedades de documento com listas de propriedades de pesquisa](../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
## <a name="options"></a>Opções  
 **Nome da propriedade**  
 Especifique o nome a ser usado para identificar a propriedade em consultas de texto completo. Um nome de propriedade pode conter espaços internos. O tamanho máximo do **Nome da Propriedade** é de 256 caracteres. Esse nome pode ser um nome amigável, como "Autor" ou "Endereço Residencial" ou pode ser o nome canônico do Windows da propriedade, como `System.Author` ou `System.Contact.HomeAddress`. O**Nome da Propriedade** deve identificar a propriedade exclusivamente dentro do conjunto de propriedades.  
  
 Os desenvolvedores usam o nome da propriedade para identificar a propriedade no [contém](/sql/t-sql/queries/contains-transact-sql) predicado. Portanto, ao adicionar uma propriedade, é importante especificar um valor que represente significativamente a propriedade.  
  
 **GUID do conjunto de propriedade**  
 Especifique o identificador do conjunto de propriedades ao qual a propriedade pertence. Esse é um GUID (identificador global exclusivo). Um conjunto de propriedades é um grupo de propriedades logicamente relacionadas. Para obter informações sobre como obter esse valor, consulte “Comentários”, posteriormente neste tópico.  
  
 **ID Int de propriedade**  
 Especifique o identificador inteiro da propriedade. Esse valor pré-atribuído é um inteiro positivo que é exclusivo dentro do conjunto de propriedades. Para obter informações sobre como obter esse valor, consulte “Comentários”, posteriormente neste tópico.  
  
> [!NOTE]  
>  Propriedades de documento que usam identificadores de cadeia de caracteres não têm suporte da pesquisa de texto completo.  
  
 **Descrição da propriedade**  
 Opcionalmente, especifique uma descrição da propriedade. Esta é uma cadeia de caracteres de até 512 caracteres. Por exemplo, uma descrição pode conter informações sobre o conjunto de propriedades da propriedade ou informações sobre uma propriedade que não é evidente a partir de seu nome.  
  
## <a name="remarks"></a>Remarks  
 Para adicionar uma propriedade de pesquisa a uma lista de propriedades de pesquisa, você deve especificar o GUID (identificador global exclusivo) do conjunto de propriedades ao qual a propriedade pertence e o identificador inteiro da propriedade. Uma determinada combinação disso deve ser exclusiva em uma determinada lista de propriedades de pesquisa. Se você tentar adicionar uma combinação existente, haverá falha na operação e um erro será gerado. Isso significa que você pode configurar apenas um nome para uma determinada propriedade.  
  
 A descrição da propriedade é opcional.  
  
 **Para configurar uma lista de propriedades de pesquisa para um índice de texto completo**  
  
-   [Pesquisar propriedades de documento com listas de propriedades de pesquisa](../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
## <a name="permissions"></a>Permissões  
 Consulte [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-search-property-list-transact-sql).  
  
## <a name="see-also"></a>Consulte também  
 [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-search-property-list-transact-sql)   
 [Pesquisar propriedades de documento com listas de propriedades de pesquisa](../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql)  
  
  

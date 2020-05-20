---
title: Nova lista de propriedades de pesquisa | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.spl.newsearchpropertylist.f1
ms.assetid: ffca78e9-8608-4b15-bd38-b2d78da4247a
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 23941f8fcf11b874cb459c3a77308534c24ca81f
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000810"
---
# <a name="new-search-property-list"></a>Nova Lista de Propriedades de Pesquisa
  Use essa caixa de diálogo para criar uma lista de propriedades de pesquisa.  
  
## <a name="options"></a>Opções  
 **Nome da lista de propriedades de pesquisa**  
 Insira o nome da lista de propriedades de pesquisa.  
  
 **Proprietário**  
 Especifique o proprietário da lista de propriedades de pesquisa. Para atribuir a propriedade a você, ou seja, para o usuário atual, deixe esse campo em branco. Para especificar um usuário diferente, clique no botão Procurar.  
  
### <a name="create-search-property-list-options"></a>Opções para Criar Lista de Propriedades de Pesquisa  
 Clique em uma das opções a seguir:  
  
 **Criar uma lista de propriedades de pesquisa vazia**  
 Cria uma lista de propriedades de pesquisa sem nenhuma propriedade.  
  
 **Criar de uma lista de propriedades de pesquisa existente**  
 Copia as propriedades de uma lista de propriedades de pesquisa existente na nova lista de propriedades. As listas de propriedades de pesquisa são objetos de banco de dados, de modo que você deve especificar o banco de dados que contém a lista de propriedades que deseja copiar.  
  
 **Banco de dados de origem**  
 Especifique o nome do banco de dados ao qual a lista de propriedades de pesquisa existente pertence. Por padrão, o banco de dados atual é selecionado. Se desejar, você pode usar a caixa de listagem para selecionar outro banco de dados, se sua conexão atual estiver associada a uma ID de usuário nesse banco de dados.  
  
 **Lista de propriedades de pesquisa de origem**  
 Selecione o nome de uma lista de propriedades de pesquisa existente pertencente ao banco de dados selecionado.  
  
## <a name="permissions"></a>Permissões  
 Consulte [criar lista de propriedades de pesquisa &#40;&#41;Transact-SQL ](/sql/t-sql/statements/create-search-property-list-transact-sql).  
  
## <a name="to-use-sql-server-management-studio-to-manage-search-property-lists"></a>Para usar o SQL Server Management Studio para gerenciar listas de propriedades de pesquisa  
 Para obter informações sobre como criar, exibir, alterar ou excluir uma lista de propriedades de pesquisa, e sobre como configurar um índice de texto completo para a pesquisa de propriedades, consulte [Search Document Properties with Search Property Lists](../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
## <a name="see-also"></a>Consulte Também  
 [CRIAR lista de propriedades de pesquisa &#40;&#41;Transact-SQL](/sql/t-sql/statements/create-search-property-list-transact-sql)   
 [Pesquisar Propriedades do documento com listas de propriedades de pesquisa](../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql)  
  
  

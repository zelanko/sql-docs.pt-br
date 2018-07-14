---
title: Propriedades do índice de texto completo (página colunas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.fulltextindexproperties.columns.f1
ms.assetid: 75e52edb-0d07-4393-9345-8b5af4561e35
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 2e1f9e7a0b6f7c9b62e431062f1cd778fe3ef998
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37201996"
---
# <a name="full-text-index-properties-columns-page"></a>Propriedades do Índice de Texto Completo (página Colunas)
  **Para exibir ou alterar as propriedades de um índice de texto completo**  
  
-   [Administrar índices de texto completo](../relational-databases/indexes/indexes.md)  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Índice exclusivo**  
 Selecione um índice na lista suspensa. O índice deve ser um índice não nulo, exclusivo e de coluna de chave única.  
  
 **Selecione as colunas qualificadas que serão indexada com texto completo**  
 A grade exibe as colunas da tabela que estão disponíveis para esse índice de texto completo. As colunas indexadas atualmente com texto completo são verificadas. Opcionalmente, você pode verificar colunas adicionais que deseja que sejam indexadas com texto completo.  
  
> [!IMPORTANT]  
>  Verifique se pelo menos uma coluna está verificada antes de clicar em OK.  
  
|||  
|-|-|  
|**Colunas disponíveis**|O nome da coluna.|  
|**Idioma do separador de palavras**|O idioma cujos separadores de palavras e lematizadores executam a análise linguística em todos os dados indexados com texto completo.<br /><br /> Para obter mais informações, consulte [configurar e gerenciar separadores de palavras e lematizadores para pesquisa](../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md) e [escolher um idioma ao criar um índice de texto completo](../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).|  
|**Tipo**|O nome da coluna da tabela que mantém o tipo de documento da coluna selecionada. Trata-se de uma propriedade somente leitura.|  
|**Semântica Estatística**|Especifique se habilitará a indexação semântica da coluna selecionada. Para obter mais informações, veja [Pesquisa semântica &#40;SQL Server&#41;](../relational-databases/search/semantic-search-sql-server.md).<br /><br /> Se você selecionar um **Idioma** antes de selecionar **Semântica Estatística**, e o idioma selecionado não tiver um Modelo de Idioma Semântico associado, a caixa de seleção **Semântica Estatística** será desabilitada. Se você selecionar **Semântica Estatística** antes de selecionar um **Idioma**, os idiomas disponíveis na caixa de combinação suspensa serão restringidos a esses para os quais o Modelo de Idioma Semântico dá suporte.|  
  
## <a name="see-also"></a>Consulte também  
 [Popular índices de texto completo](../relational-databases/search/populate-full-text-indexes.md)  
  
  

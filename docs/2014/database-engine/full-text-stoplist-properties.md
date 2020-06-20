---
title: Propriedades da autostoplist de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftstoplistproperties.general.f1
- sql12.swb.fulltextsearch.ftstoplistproperties.schedule.f1
ms.assetid: 2e907f5b-0cf9-484a-afcf-a4e7f1e2f87f
author: rothja
ms.author: jroth
ms.openlocfilehash: 4ff27a1258d5164e3e93d34b6ff757993d6f6363
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84932937"
---
# <a name="full-text-stoplist-properties"></a>Propriedades da lista de palavras irrelevantes (stoplist) de texto completo
  Use esta caixa de diálogo para adicionar ou excluir palavras irrelevantes individuais, para excluir todas as palavras irrelevantes em um idioma específico ou para limpar a lista de palavras irrelevantes atual. Uma palavra irrelevante é uma palavra usada comumente que é incluída em uma lista de palavras irrelevantes. As palavras irrelevantes são omitidas da indexação de texto completo para tabelas que usam a lista de palavras irrelevantes. Para obter mais informações, veja [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes para pesquisa de texto completo](../relational-databases/search/full-text-search.md).  
  
 **Para usar o SQL Server Management Studio para alterar propriedades da lista de palavras irrelevantes**  
  
-   [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes (stoplists) para pesquisa de texto completo](../relational-databases/search/full-text-search.md)  
  
## <a name="options"></a>Opções  
 **Ação**  
 Especifica a ação que você deseja executar.  
  
 **Adicionar palavra irrelevante**  
 Adicione uma palavra comumente usada à lista de palavras irrelevantes.  
  
 **Excluir palavra irrelevante**  
 Exclua uma palavra irrelevante da lista de palavras irrelevantes.  
  
 **Excluir todas as palavras irrelevantes**  
 Exclua todas as palavras irrelevantes para um idioma específico.  
  
 **Limpar lista de palavras irrelevantes**  
 Limpe a lista de palavras irrelevantes, excluindo todas as palavras irrelevantes para todos os idiomas.  
  
 **Palavra irrelevante**  
 Se você selecionou **Adicionar palavra irrelevante** ou **Excluir palavra irrelevante**, insira a palavra irrelevante no campo **Palavra irrelevante** . Uma nova palavra irrelevante deve ser exclusiva; ou seja, ainda não deve estar na lista de palavras irrelevantes para o idioma selecionado.  
  
 **Idioma de texto completo**  
 Se você selecionou **Adicionar palavra irrelevante**, **Excluir palavra irrelevante**, ou **Excluir todas as palavras irrelevantes**, selecione o idioma da palavra irrelevante ou palavras irrelevantes na caixa de listagem. Isso lista todos os idiomas de texto completo que têm suporte na instância de servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [sys. fulltext_stopwords &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql)   
 [sys. fulltext_stoplists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql)   
 [Configurar e gerenciar palavras irrelevantes e palavras irrelevantes para pesquisa de texto completo](../relational-databases/search/full-text-search.md)   
 [ALTER FULLTEXT STOPlist &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)   
 [CRIAR ponto de interrupção de texto completo &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)   
 [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-stoplist-transact-sql)  
  
  

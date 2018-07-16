---
title: Localizar frases chave em documentos com pesquisa semântica | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], key phrase queries
ms.assetid: 6ee3676e-ed5d-43ec-aeca-1eed78967111
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c3a9cb8c4903580c4b5879b431b1be6de1b77f97
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37234956"
---
# <a name="find-key-phrases-in-documents-with-semantic-search"></a>Localizar frases chave em documentos com pesquisa semântica
  Descreve como localizar as frases chave em documentos ou colunas de texto configuradas para indexação semântica estatística.  
  
##  <a name="BasicsQueryKey"></a> Localizando frases chave em documentos  
  
###  <a name="howtofind"></a> Como: localizar as frases-chave em documentos com SEMANTICKEYPHRASETABLE  
 Para identificar as frases chave em documentos específicos, ou para identificar documentos que contêm frases chave específicas, veja a função [semantickeyphrasetable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semantickeyphrasetable-transact-sql).  
  
 SEMANTICKEYPHRASETABLE retorna uma tabela com zero, uma ou mais linhas para essas frases-chave associadas às colunas da tabela especificada. Essa função de conjunto de linhas pode ser referenciada na cláusula FROM de uma instrução SELECT como se fosse um nome de tabela comum.  
  
> [!NOTE]  
>  No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], somente palavras únicas são indexadas para pesquisa semântica; frases com várias palavras (ngrams) não são indexadas. Além disso, várias formas da mesma palavra são indexadas separadamente; por exemplo, "computador" e "computadores" são indexadas separadamente.  
  
 Para obter informações detalhadas sobre os parâmetros exigidos pela função SEMANTICKEYPHRASETABLE, e sobre a tabela de resultados que ela retorna, veja [semantickeyphrasetable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semantickeyphrasetable-transact-sql).  
  
> [!IMPORTANT]  
>  As colunas de destino devem ter a indexação de texto completo e semântica habilitada.  
  
###  <a name="HowToTopPhrases"></a> Exemplo 1: Localizar as principais frases chave em um documento específico  
 O exemplo a seguir recupera as 10 principais frases-chave do documento especificado pela variável @DocumentId na coluna Document da tabela Production.Document do banco de dados de exemplo AdventureWorks. A variável @DocumentId representa um valor da coluna de chave do índice de texto completo.  
  
```tsql  
SELECT TOP(10) KEYP_TBL.keyphrase  
FROM SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document,  
    @DocumentId  
    ) AS KEYP_TBL  
ORDER BY KEYP_TBL.score DESC;  
GO  
```  
  
 A função **SEMANTICKEYPHRASETABLE** recupera esses resultados com eficácia usando uma busca de índice em vez de um exame de tabela.  
  
###  <a name="HowToTopDocuments"></a> Exemplo 2: Localizar os principais documentos que contêm uma frase chave específica  
 O exemplo a seguir recupera os 25 principais documentos que contêm a frase-chave Bracket da coluna Document da tabela Production.Document do banco de dados de exemplo AdventureWorks.  
  
```tsql  
SELECT TOP (25) DOC_TBL.DocumentID, DOC_TBL.DocumentSummary  
FROM Production.Document AS DOC_TBL  
    INNER JOIN SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document  
    ) AS KEYP_TBL  
ON DOC_TBL.DocumentID = KEYP_TBL.document_key  
WHERE KEYP_TBL.keyphrase = 'Bracket'  
ORDER BY KEYP_TBL.Score DESC;  
GO  
```  
  
  

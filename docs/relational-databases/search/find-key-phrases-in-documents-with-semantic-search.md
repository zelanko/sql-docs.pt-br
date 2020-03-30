---
title: Localizar frases-chave em documentos com a pesquisa semântica
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], key phrase queries
ms.assetid: 6ee3676e-ed5d-43ec-aeca-1eed78967111
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.custom: seo-lt-2019
ms.openlocfilehash: 64060ae1662d9d1448695426da9e555afbf6869a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74056195"
---
# <a name="find-key-phrases-in-documents-with-semantic-search"></a>Localizar frases chave em documentos com pesquisa semântica
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Descreve como localizar as frases chave em documentos ou colunas de texto configuradas para indexação semântica estatística.  

##  <a name="find-the-key-phrases-in-documents-with-semantickeyphrasetable"></a><a name="howtofind"></a> Localizar frases chave em documentos com SEMANTICKEYPHRASETABLE  
 Para identificar as frases chave em documentos específicos, ou para identificar documentos que contêm frases chave específicas, veja a função [semantickeyphrasetable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md).  
  
 SEMANTICKEYPHRASETABLE retorna uma tabela com zero, uma ou mais linhas para essas frases-chave associadas às colunas da tabela especificada. Essa função de conjunto de linhas pode ser referenciada na cláusula FROM de uma instrução SELECT como se fosse um nome de tabela comum.  
  
> [!NOTE]  
>  Nessa versão, somente palavras únicas são indexadas para pesquisa semântica. Frases com várias palavras (ngrams) não são indexadas. Além disso, várias formas da mesma palavra são indexadas separadamente; por exemplo, "computador" e "computadores" são indexadas separadamente.  
  
 Para obter informações detalhadas sobre os parâmetros exigidos pela função SEMANTICKEYPHRASETABLE, e sobre a tabela de resultados que ela retorna, veja [semantickeyphrasetable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md).  
  
> [!IMPORTANT]  
>  As colunas de destino devem ter a indexação de texto completo e semântica habilitada.  
  
###  <a name="example-1-find-the-top-key-phrases-in-a-specific-document"></a><a name="HowToTopPhrases"></a> Example 1: Find the top key phrases in a specific document  
 O exemplo a seguir recupera as 10 principais frases-chave do documento especificado pela variável @DocumentId na coluna Document da tabela Production.Document do banco de dados de exemplo AdventureWorks. A variável @DocumentId representa um valor da coluna de chave do índice de texto completo.  
  
```sql  
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
  
###  <a name="example-2-find-the-top-documents-that-contain-a-specific-key-phrase"></a><a name="HowToTopDocuments"></a> Example 2: Find the top documents that contain a specific key phrase  
 O exemplo a seguir recupera os 25 principais documentos que contêm a frase-chave "Bracket" da coluna Document da tabela Production.Document do banco de dados de exemplo AdventureWorks.  
  
```sql  
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
  
  

---
title: Localizar documentos semelhantes e relacionados com a pesquisa semântica | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], document similarity queries
ms.assetid: 9f527883-031b-442f-8e95-24bc0151ecbf
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b11493b5b04fa9308e3afbe56176251225248338
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85004175"
---
# <a name="find-similar-and-related-documents-with-semantic-search"></a>Localizar documentos semelhantes e relacionados com a pesquisa semântica
  Descreve como localizar documentos ou valores de texto semelhantes ou relacionados, e informações sobre como eles são semelhantes ou relacionados, em colunas configuradas para indexação semântica estatística.  
  
##  <a name="finding-similar-or-related-documents"></a><a name="BasicsQuerySimilar"></a>Localizando documentos semelhantes ou relacionados  
  
###  <a name="how-to-find-similar-or-related-documents-with-semanticsimilaritytable"></a><a name="HowToQuerySimilar"></a>Como localizar documentos semelhantes ou relacionados com o SEMANTICSIMILARITYTABLE  
 Para identificar documentos semelhantes ou relacionados em uma coluna específica, consulte a função [semanticsimilaritytable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritytable-transact-sql).  
  
 **SEMANTICSIMILARITYTABLE** retorna uma tabela de zero, uma ou mais linhas cujo conteúdo na coluna especificada é semanticamente semelhante ao documento especificado. Essa função de conjunto de linhas pode ser referenciada na cláusula FROM de uma instrução SELECT como um nome de tabela normal.  
  
 Não é possível consultar documentos similares em colunas. A função **SEMANTICSIMILARITYTABLE** apenas recupera resultados da mesma coluna que a coluna de origem, identificada pelo argumento **source_key** .  
  
 Para obter informações detalhadas sobre os parâmetros exigidos pela função **SEMANTICSIMILARITYTABLE**, e sobre a tabela de resultados que ela retorna, veja [semanticsimilaritytable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritytable-transact-sql).  
  
> [!IMPORTANT]  
>  As colunas de destino devem ter a indexação de texto completo e semântica habilitada.  
  
###  <a name="example-find-the-top-documents-that-are-similar-to-another-document"></a><a name="HowToIdentifySimilar"></a>Exemplo: localizar os principais documentos semelhantes a outro documento  
 O exemplo a seguir recupera os 10 principais candidatos que são semelhantes ao candidato especificado pelo *@CandidateID* da tabela HumanResources. JobCandidate no banco de dados de exemplo AdventureWorks2012.  
  
```scr  
SELECT TOP(10) KEY_TBL.matched_document_key AS Candidate_ID  
FROM SEMANTICSIMILARITYTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume,  
    @CandidateID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
GO  
```  
  
##  <a name="finding-information-about-how-documents-are-similar-or-related"></a><a name="BasicsQuerySimilarity"></a>Localizando informações sobre como os documentos são semelhantes ou relacionados  
  
###  <a name="how-to-find-information-about-how-documents-are-similar-or-related-with-semanticsimilaritydetailstable"></a><a name="HowToQuerySimilarity"></a>Como encontrar informações sobre como os documentos são semelhantes ou relacionados ao SEMANTICSIMILARITYDETAILSTABLE  
 Para obter informações sobre as frases-chave que tornam documentos semelhantes ou relacionados, consulte a função [semanticsimilaritydetailstable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql).  
  
 **SEMANTICSIMILARITYDETAILSTABLE** retorna uma tabela de zero, uma ou mais linhas de frases-chave comuns entre dois documentos (um documento de origem e um documento correspondente) cujo conteúdo é semanticamente semelhante. Essa função de conjunto de linhas pode ser referenciada na cláusula FROM de uma instrução SELECT como um nome de tabela normal.  
  
 Para obter informações detalhadas sobre os parâmetros exigidos pela função **SEMANTICSIMILARITYDETAILSTABLE** e sobre a tabela de resultados que ela retorna, veja [semanticsimilaritydetailstable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql).  
  
> [!IMPORTANT]  
>  As colunas de destino devem ter a indexação de texto completo e semântica habilitada.  
  
###  <a name="example-find-the-top-key-phrases-that-are-similar-between-documents"></a><a name="HowToSimilarPhrases"></a>Exemplo: localizar as principais frases-chave que são semelhantes entre os documentos  
 O exemplo a seguir recupera as cinco frases-chave com a pontuação de similaridade mais alta entre os candidatos especificados na tabela **HumanResources.JobCandidate** do banco de dados de exemplo AdventureWorks2012.  
  
```sql  
SELECT TOP(5) KEY_TBL.keyphrase, KEY_TBL.score  
FROM SEMANTICSIMILARITYDETAILSTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume, @CandidateID,  
    Resume, @MatchedID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
GO  
```  
  
  

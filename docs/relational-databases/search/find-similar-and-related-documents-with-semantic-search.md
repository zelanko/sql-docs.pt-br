---
title: Localizar documentos semelhantes e relacionados com a pesquisa semântica | Microsoft Docs
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], document similarity queries
ms.assetid: 9f527883-031b-442f-8e95-24bc0151ecbf
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 051e0a70bedaf7c7731b5f8cd0b9dfe91f078fea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68082804"
---
# <a name="find-similar-and-related-documents-with-semantic-search"></a>Localizar documentos semelhantes e relacionados com a pesquisa semântica
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Descreve como localizar documentos ou valores de texto semelhantes ou relacionados, e informações sobre como eles são semelhantes ou relacionados, em colunas configuradas para indexação semântica estatística.  
   
##  <a name="HowToQuerySimilar"></a> Localizar documentos semelhantes ou relacionados com SEMANTICSIMILARITYTABLE  
 Para identificar documentos semelhantes ou relacionados em uma coluna específica, consulte a função [semanticsimilaritytable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md).  
  
 **SEMANTICSIMILARITYTABLE** retorna uma tabela de zero, uma ou mais linhas cujo conteúdo na coluna especificada é semanticamente semelhante ao documento especificado. Essa função de conjunto de linhas pode ser referenciada na cláusula FROM de uma instrução SELECT como um nome de tabela normal.  
  
 Não é possível consultar documentos similares em colunas. A função **SEMANTICSIMILARITYTABLE** apenas recupera resultados da mesma coluna que a coluna de origem, identificada pelo argumento **source_key**.  
  
 Para obter informações detalhadas sobre os parâmetros exigidos pela função **SEMANTICSIMILARITYTABLE**, e sobre a tabela de resultados que ela retorna, veja [semanticsimilaritytable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md).  
  
> [!IMPORTANT]  
>  As colunas de destino devem ter a indexação de texto completo e semântica habilitada.  
  
###  <a name="HowToIdentifySimilar"></a> Exemplo: localize os principais documentos semelhantes a outro documento  
 O exemplo a seguir recuperar os 10 principais candidatos que são semelhantes ao candidato especificado por *@CandidateID* da tabela HumanResources.JobCandidate no banco de dados de exemplo AdventureWorks2012.  
  
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
  
##  <a name="HowToQuerySimilarity"></a>Localizar informações sobre como documentos são semelhantes ou relacionados com SEMANTICSIMILARITYDETAILSTABLE  
 Para obter informações sobre as frases-chave que tornam documentos semelhantes ou relacionados, consulte a função [semanticsimilaritydetailstable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md).  
  
 **SEMANTICSIMILARITYDETAILSTABLE** retorna uma tabela de zero, uma ou mais linhas de frases-chave comuns entre dois documentos (um documento de origem e um documento correspondente) cujo conteúdo é semanticamente semelhante. Essa função de conjunto de linhas pode ser referenciada na cláusula FROM de uma instrução SELECT como um nome de tabela normal.  
  
 Para obter informações detalhadas sobre os parâmetros exigidos pela função **SEMANTICSIMILARITYDETAILSTABLE** e sobre a tabela de resultados que ela retorna, veja [semanticsimilaritydetailstable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md).  
  
> [!IMPORTANT]  
>  As colunas de destino devem ter a indexação de texto completo e semântica habilitada.  
  
###  <a name="HowToSimilarPhrases"></a> Exemplo: localize as principais frases-chave semelhantes entre documentos  
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
  
  

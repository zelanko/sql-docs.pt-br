---
description: Funções Pesquisa de Texto Completo e Pesquisa Semântica (Transact-SQL)
title: Funções pesquisa de texto completo e pesquisa semântica (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- semantic search [SQL Server], system functions
ms.assetid: a61a3694-7604-4583-962e-fc30f771c6fa
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: deb790da4e4e263318717c3ee81cc8ee8d467ae6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474619"
---
# <a name="full-text-search-and-semantic-search-functions-transact-sql"></a>Funções Pesquisa de Texto Completo e Pesquisa Semântica (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Esta seção descreve as funções do sistema relacionadas à pesquisa semântica e de texto completo.  
  
## <a name="full-text-search-functions"></a>Funções de pesquisa de texto completo  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)  
 Retorna uma tabela com zero, uma ou mais linhas para as colunas que contêm correspondências precisas ou difusas (menos precisas) com palavras individuais e frases, a proximidade entre as palavras em uma determinada distância ou correspondências ponderadas.  
  
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)  
 Retorna uma tabela de zero, uma ou mais linhas para as colunas que contêm valores que correspondem ao significado, e não apenas às palavras exatas, do texto no *freetext_string*especificado.  
  
## <a name="semantic-search-functions"></a>Funções de pesquisa semântica  
 [semantickeyphrasetable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md)  
 Retorna uma tabela com zero, uma ou mais linhas para essas frases-chave associadas às colunas da tabela especificada.  
  
 [semanticsimilaritydetailstable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md)  
 Retorna uma tabela de zero, uma ou mais linhas de frases-chave comuns em dois documentos (um documento de origem e um documento correspondente) cujo conteúdo é semanticamente semelhante.  
  
 [semanticsimilaritytable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md)  
 Retorna uma tabela de zero, uma ou mais linhas para as colunas cujo conteúdo é semanticamente similar a um documento especificado.  
  
  

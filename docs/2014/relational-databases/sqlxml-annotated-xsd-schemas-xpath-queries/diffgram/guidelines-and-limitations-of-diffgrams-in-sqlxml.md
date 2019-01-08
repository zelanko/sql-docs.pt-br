---
title: Diretrizes e limitações de DiffGrams no SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4ca731cab8a88364b3b87dfc282c10fa14ebf283
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52804338"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>Diretrizes e limitações de DiffGrams no SQLXML
  Lembre-se das recomendações a seguir ao usar DiffGrams com o SQLXML 4.0:  
  
-   Os tipos BLOB (objeto grande binário) como `text/ntext` e as imagens não devem ser usados no bloco `<diffgr:before>` ao trabalhar com DiffGrams, porque assim eles serão incluídos para ser usados em controle simultâneo. Isso pode causar problemas com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devido às limitações de comparação para tipos BLOB. Por exemplo, a palavra-chave LIKE é usada na cláusula WHERE para comparar entre colunas do tipo de dados `text`; entretanto, as comparações falharão no caso de tipos BLOB em que o tamanho dos dados seja maior do que 8KB.  
  
-   Caracteres especiais em dados `ntext` podem causar problemas com o SQLXML 4.0 devido às limitações de comparação para tipos BLOB. Por exemplo, o uso de "[Serializable]" no bloco `<diffgr:before>` de um DiffGram quando usado na verificação simultânea de uma coluna de tipo `ntext` falhará com a descrição do erro do SQLOLEDB a seguir:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  

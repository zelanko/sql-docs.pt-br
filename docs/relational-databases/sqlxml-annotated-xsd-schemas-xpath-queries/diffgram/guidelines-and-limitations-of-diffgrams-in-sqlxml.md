---
title: Diretrizes e limitações de DiffGrams no SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9f63bc4259d60cdca7a82057dacafad21573156a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38051524"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>Diretrizes e limitações de DiffGrams no SQLXML
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Lembre-se das recomendações a seguir ao usar DiffGrams com o SQLXML 4.0:  
  
-   Tipos de objeto binário grande (BLOB), como **texto/ntext** e imagens não devem ser usadas na  **\<diffgr: antes de >** bloquear ao trabalhar com DiffGrams, porque isso incluirá para uso em controle de simultaneidade. Isso pode causar problemas com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devido às limitações de comparação para tipos BLOB. Por exemplo, a palavra-chave LIKE é usada na cláusula WHERE para comparar entre colunas do **texto** de tipo de dados; no entanto, as comparações falharão no caso de tipos BLOB onde o tamanho dos dados é maior que 8 KB.  
  
-   Caracteres especiais no **ntext** dados podem causar problemas com o SQLXML 4.0 devido às limitações de comparação para tipos BLOB. Por exemplo, o uso de "[Serializable]" na  **\<diffgr: antes de >** bloco de um DiffGram quando usado na verificação simultânea de uma coluna de **ntext** tipo falhará com o SQLOLEDB a seguir Descrição do erro:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  

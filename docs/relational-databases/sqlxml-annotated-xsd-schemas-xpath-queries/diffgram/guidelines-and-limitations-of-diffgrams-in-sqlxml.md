---
title: "Diretrizes e limitações de DiffGrams no SQLXML | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2af871b240d318aaa027402a52a9c31498521b99
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>Diretrizes e limitações de DiffGrams no SQLXML
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Lembre-se das recomendações a seguir ao usar DiffGrams com o SQLXML 4.0:  
  
-   Tipos de objeto binário grande (BLOB) como **texto/ntext** e imagens não devem ser usadas no  **\<diffgr: antes de >** bloco em ao trabalhar com DiffGrams, porque isso incluirá para uso em controle de simultaneidade. Isso pode causar problemas com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devido às limitações de comparação para tipos BLOB. Por exemplo, a palavra-chave LIKE é usada na cláusula WHERE para comparar entre colunas do **texto** de tipo de dados; no entanto, as comparações falharão no caso de tipos BLOB onde o tamanho dos dados é maior que 8 KB.  
  
-   Caracteres especiais em **ntext** dados podem causar problemas com o SQLXML 4.0 devido às limitações de comparação para tipos BLOB. Por exemplo, o uso de "[Serializable]" no  **\<diffgr: antes de >** bloco de um DiffGram quando usado na verificação simultânea de uma coluna de **ntext** tipo falhará com o SQLOLEDB a seguir Descrição do erro:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  

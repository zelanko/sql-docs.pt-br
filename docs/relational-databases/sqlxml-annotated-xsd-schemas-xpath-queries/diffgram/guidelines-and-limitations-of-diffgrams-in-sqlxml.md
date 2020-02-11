---
title: Diretrizes e limitações de DiffGrams no SQLXML
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: eae0b81b3c55a4afe611cd8ed6fdbb495b498c61
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75246595"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>Diretrizes e limitações de DiffGrams no SQLXML
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Lembre-se das recomendações a seguir ao usar DiffGrams com o SQLXML 4.0:  
  
-   Tipos BLOB (objeto binário grande) como **Text/ntext** e images não devem ser usados no bloco ** \<diffgr: Before>** no ao trabalhar com DiffGrams, pois isso os incluirá para uso no controle de simultaneidade. Isso pode causar problemas com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devido às limitações de comparação para tipos BLOB. Por exemplo, a palavra-chave LIKE é usada na cláusula WHERE para comparar entre colunas do tipo de dados **Text** ; no entanto, as comparações falharão no caso de tipos de BLOB em que o tamanho dos dados seja maior que 8K.  
  
-   Caracteres especiais em dados **ntext** podem causar problemas com o SQLXML 4,0 devido às limitações de comparação para tipos de BLOB. Por exemplo, o uso de "[Serializable]" no bloco ** \<diffgr: Before>** de um DiffGram quando usado na verificação de simultaneidade de uma coluna de tipo **ntext** falhará com a seguinte descrição de erro SQLOLEDB:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  

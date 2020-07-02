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
ms.openlocfilehash: 113090c317e88d3e9a7e7db2bfcb7d4d14b4ea1f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85650064"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>Diretrizes e limitações de DiffGrams no SQLXML
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Lembre-se das recomendações a seguir ao usar DiffGrams com o SQLXML 4.0:  
  
-   Tipos BLOB (objeto binário grande) como **Text/ntext** e images não devem ser usados no **\<diffgr:before>** bloco in ao trabalhar com DiffGrams, pois isso os incluirá para uso no controle de simultaneidade. Isso pode causar problemas com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devido às limitações de comparação para tipos BLOB. Por exemplo, a palavra-chave LIKE é usada na cláusula WHERE para comparar entre colunas do tipo de dados **Text** ; no entanto, as comparações falharão no caso de tipos de BLOB em que o tamanho dos dados seja maior que 8K.  
  
-   Caracteres especiais em dados **ntext** podem causar problemas com o SQLXML 4,0 devido às limitações de comparação para tipos de BLOB. Por exemplo, o uso de "[Serializable]" no **\<diffgr:before>** bloco de DiffGram quando usado na verificação de simultaneidade de uma coluna de tipo **ntext** falhará com a seguinte descrição de erro SQLOLEDB:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  

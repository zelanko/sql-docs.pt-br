---
title: Diretrizes e limitações de DiffGrams no SQLXML | Microsoft Docs
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
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d30c7a93906f9de5fb3826ac4d8a8e1f845f1693
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47779164"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>Diretrizes e limitações de DiffGrams no SQLXML
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Lembre-se das recomendações a seguir ao usar DiffGrams com o SQLXML 4.0:  
  
-   Tipos de objeto binário grande (BLOB), como **texto/ntext** e imagens não devem ser usadas na  **\<diffgr: antes de >** bloquear ao trabalhar com DiffGrams, porque isso incluirá para uso em controle de simultaneidade. Isso pode causar problemas com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devido às limitações de comparação para tipos BLOB. Por exemplo, a palavra-chave LIKE é usada na cláusula WHERE para comparar entre colunas do **texto** de tipo de dados; no entanto, as comparações falharão no caso de tipos BLOB onde o tamanho dos dados é maior que 8 KB.  
  
-   Caracteres especiais no **ntext** dados podem causar problemas com o SQLXML 4.0 devido às limitações de comparação para tipos BLOB. Por exemplo, o uso de "[Serializable]" na  **\<diffgr: antes de >** bloco de um DiffGram quando usado na verificação simultânea de uma coluna de **ntext** tipo falhará com o SQLOLEDB a seguir Descrição do erro:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  

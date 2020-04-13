---
title: Suporte a namespace no modo PATH | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- PATH FOR XML mode, namespace support
- namespaces [XML in SQL Server]
ms.assetid: 5f128ea2-0ceb-4b23-bce7-c8b3fd615466
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f75729d1e31989bde851d1fde3a05ab932b6f460
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "80665027"
---
# <a name="namespace-support-in-path-mode"></a>Suporte a namespace em modo PATH
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  O suporte a namespace em modo PATH é fornecido usando WITH NAMESPACES. Por exemplo, a consulta a seguir demonstra a sintaxe de WITH NAMESPACES para declarar um namespace ("a:") que pode , em seguida, ser usado na instrução SELECT subsequente.  
  
```  
WITH XMLNAMESPACES('a' as a)  
SELECT 1 as 'a:b'  
FOR XML PATH  
```  
  
## <a name="examples"></a>Exemplos  
 Esses exemplos ilustram o uso do modo PATH para gerar XML de uma consulta SELECT. Muitas dessas consultas são especificadas em relação a documentos XML de instruções da fabricação de bicicletas que são armazenados na coluna Instructions da tabela ProductModel.  
  
## <a name="see-also"></a>Consulte Também  
 [Usar o modo PATH com FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  

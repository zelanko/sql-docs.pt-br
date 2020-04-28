---
title: Cache XSL (SQLXML)
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- XSL caching [SQLXML]
ms.assetid: 91994142-32f0-4d8d-a8cf-eb0d8b1f1999
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 265ce1db6f57f378dfaa7c0818914edd121b7d30
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75257330"
---
# <a name="xsl-caching-sqlxml-40"></a>Cache de XSL (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  O armazenamento em cache de folhas de estilo XSL melhora o desempenho. Em sua primeira execução, uma folha de estilo XSL permanecerá na memória se o cache de XSL for definido como ON; isto melhora o desempenho para processamento subsequente. A configuração padrão é ON.  
  
 Você pode definir o tamanho do cache XSL adicionando a seguinte chave no Registro:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\XSLCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 O tamanho de cache XSL deve ser definido com base na memória disponível e no número de folhas de estilo XSL que você está usando. O padrão de tamanho de **XSLCacheSize** é 31. Você poderá aumentar o tamanho do cache se o acesso de XSL parecer lento, ou diminuir o tamanho do cache se a memória for pouca.  
  
 Para obter melhor desempenho, é recomendado que você defina **XSLCacheSize** mais alto que o número de folhas de estilo XSL geralmente usado. Se **XSLCacheSize** for menor que o número de folhas de estilo XSL que você terá, o desempenho degradará à medida que o número de folhas de estilo XSL aumentar. O **XSLCacheSize** pode ser definido como 128, no máximo.  
  
 Sempre que a folha de estilo XSL armazenada em cache é usada, a hora de modificação do arquivo XSL é verificada para determinar se ele precisa ser atualizado. Isso ocorre porque a cópia em disco é mais recente do que a cópia em cache.  
  
## <a name="see-also"></a>Consulte Também  
 [Cache de modelos &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)   
 [Cache de esquema &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)  
  
  

---
title: Cache de XSL (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- XSL caching [SQLXML]
ms.assetid: 91994142-32f0-4d8d-a8cf-eb0d8b1f1999
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b95f2970c7d1d9848d6b58c4feaeb462c084d369
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019988"
---
# <a name="xsl-caching-sqlxml-40"></a>Cache de XSL (SQLXML 4.0)
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
  
## <a name="see-also"></a>Consulte também  
 [Cache de modelo &#40;SQLXML 4.0&#41;](template-caching-sqlxml-4-0.md)   
 [Cache de esquemas &#40;SQLXML 4.0&#41;](schema-caching-sqlxml-4-0.md)  
  
  
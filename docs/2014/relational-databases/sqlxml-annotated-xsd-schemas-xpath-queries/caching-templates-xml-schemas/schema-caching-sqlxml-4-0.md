---
title: Esquema de cache (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- schemas [SQLXML]
ms.assetid: 7e5fda21-b435-41fd-b637-8b616560a93f
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6ddf2b95f9b72a0def960f6159cd8646a6b4439c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012858"
---
# <a name="schema-caching-sqlxml-40"></a>Cache de esquemas (SQLXML 4.0)
  Com uma instalação lado a lado do XML para SQLXML 3.0, Microsoft SQLXML 2.0 e Microsoft SQL Server 2000 Web versão 1, você pode controlar explicitamente a cache de esquemas em todas as versões usando as seguintes chaves do registro:  
  
 Versão da Web 1:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXMLX\SchemaCacheSize  
```  
  
 SQLXML 2.0:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML2\SchemaCacheSize  
```  
  
 SQLXML 3.0:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML3\SchemaCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 Para obter mais informações sobre a instalação lado a lado, consulte [Novidades no SQLXML 4.0 SP1](../../sqlxml/what-s-new-in-sqlxml-4-0-sp1.md).  
  
 O cache de esquemas aprimora significativamente o desempenho de uma consulta XPath. Quando uma consulta XPath é executada em um esquema de mapeamento, o esquema é armazenado na memória e as estruturas de dados necessárias são criadas na memória. Se o cache de esquemas estiver definido, o esquema permanece na memória, aprimorando assim o desempenho de consultas XPath subsequentes.  
  
 Você pode definir o tamanho do cache de esquemas adicionando a chave acima ao Registro  
  
 O tamanho do esquema é definido com base na memória disponível e no número de esquemas utilizados. O padrão **SchemaCacheSize** tamanho é 31. Se você definir **SchemaCacheSize** maior, mais memória é usada. Portando, você pode aumentar o tamanho do cache se o acesso ao esquema parecer lento ou diminuir o tamanho do cache se houver pouca memória.  
  
 Por motivos de desempenho, é recomendável que você defina **SchemaCacheSize** maior que o número de esquemas de mapeamento, você geralmente usa. Como aumenta o número de esquemas, se **SchemaCacheSize** é menor que o número de esquemas, degrada o desempenho.  
  
> [!NOTE]  
>  Durante o desenvolvimento, é recomendável não armazenar os esquemas em cache, pois as alterações dos esquemas não se refletem no cache por aproximadamente dois minutos.  
  
## <a name="see-also"></a>Consulte também  
 [Cache de modelo &#40;SQLXML 4.0&#41;](template-caching-sqlxml-4-0.md)   
 [Cache de XSL &#40;SQLXML 4.0&#41;](xsl-caching-sqlxml-4-0.md)  
  
  
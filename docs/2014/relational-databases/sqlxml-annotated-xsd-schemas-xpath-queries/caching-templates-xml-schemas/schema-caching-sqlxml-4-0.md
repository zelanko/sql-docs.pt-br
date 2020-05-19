---
title: Cache de esquema (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- schemas [SQLXML]
ms.assetid: 7e5fda21-b435-41fd-b637-8b616560a93f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c6c481dbba3f8e077854b12e755544d97af5f692
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703315"
---
# <a name="schema-caching-sqlxml-40"></a>Cache de esquemas (SQLXML 4.0)
  Com uma instalação lado a lado do XML para Microsoft SQL Server 2000 versão da Web 1, do Microsoft SQLXML 2.0 e do SQLXML 3.0, é possível controlar explicitamente o cache de esquemas em todas as versões usando as seguintes chaves do Registro:  
  
 Versão da Web 1:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXMLX\SchemaCacheSize  
```  
  
 SQLXML 2,0:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML2\SchemaCacheSize  
```  
  
 SQLXML 3.0:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML3\SchemaCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 Para obter mais informações sobre a instalação lado a lado, consulte [What ' s New in SQLXML 4,0 SP1](../../sqlxml/what-s-new-in-sqlxml-4-0-sp1.md).  
  
 O cache de esquemas aprimora significativamente o desempenho de uma consulta XPath. Quando uma consulta XPath é executada em um esquema de mapeamento, o esquema é armazenado na memória e as estruturas de dados necessárias são criadas na memória. Se o cache de esquemas estiver definido, o esquema permanece na memória, aprimorando assim o desempenho de consultas XPath subsequentes.  
  
 Você pode definir o tamanho do cache de esquemas adicionando a chave acima ao Registro  
  
 O tamanho do esquema é definido com base na memória disponível e no número de esquemas utilizados. O tamanho de **SchemaCacheSize** padrão é 31. Se você definir **SchemaCacheSize** mais alto, mais memória será usada. Portando, você pode aumentar o tamanho do cache se o acesso ao esquema parecer lento ou diminuir o tamanho do cache se houver pouca memória.  
  
 Por motivos de desempenho, é recomendável que você defina **SchemaCacheSize** maior do que o número de esquemas de mapeamento que você geralmente usa. Conforme aumenta o número de esquemas, se **SchemaCacheSize** for menor que o número de esquemas que você tem, o desempenho degradará.  
  
> [!NOTE]  
>  Durante o desenvolvimento, é recomendável não armazenar os esquemas em cache, pois as alterações dos esquemas não se refletem no cache por aproximadamente dois minutos.  
  
## <a name="see-also"></a>Consulte Também  
 [Cache de modelos &#40;SQLXML 4,0&#41;](template-caching-sqlxml-4-0.md)   
 [Cache XSL &#40;SQLXML 4,0&#41;](xsl-caching-sqlxml-4-0.md)  
  
  

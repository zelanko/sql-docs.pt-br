---
title: Cache de esquemas (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- schemas [SQLXML]
ms.assetid: 7e5fda21-b435-41fd-b637-8b616560a93f
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: f6b9e9a8a6d9406def9e2adc90e1ef7e9b8545a1
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39559636"
---
# <a name="schema-caching-sqlxml-40"></a>Cache de esquemas (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Com uma instalação lado a lado do XML para Microsoft SQL Server 2000 Web versão 1, o Microsoft SQLXML 2.0 e o SQLXML 3.0, você pode controlar explicitamente a cache de esquemas em todas as versões usando as seguintes chaves do registro:  
  
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
  
 Para obter mais informações sobre a instalação lado a lado, consulte [Novidades no SQLXML 4.0 SP1](../../../relational-databases/sqlxml/what-s-new-in-sqlxml-4-0-sp1.md).  
  
 O cache de esquemas aprimora significativamente o desempenho de uma consulta XPath. Quando uma consulta XPath é executada em um esquema de mapeamento, o esquema é armazenado na memória e as estruturas de dados necessárias são criadas na memória. Se o cache de esquemas estiver definido, o esquema permanece na memória, aprimorando assim o desempenho de consultas XPath subsequentes.  
  
 Você pode definir o tamanho do cache de esquemas adicionando a chave acima ao Registro  
  
 O tamanho do esquema é definido com base na memória disponível e no número de esquemas utilizados. O padrão **SchemaCacheSize** tamanho é 31. Se você definir **SchemaCacheSize** maior, mais memória é usada. Portando, você pode aumentar o tamanho do cache se o acesso ao esquema parecer lento ou diminuir o tamanho do cache se houver pouca memória.  
  
 Por motivos de desempenho, é recomendável que você defina **SchemaCacheSize** maior do que o número de esquemas de mapeamento, você geralmente usa. À medida que aumenta o número de esquemas, se **SchemaCacheSize** é menor que o número de esquemas, degrada o desempenho.  
  
> [!NOTE]  
>  Durante o desenvolvimento, é recomendável não armazenar os esquemas em cache, pois as alterações dos esquemas não se refletem no cache por aproximadamente dois minutos.  
  
## <a name="see-also"></a>Consulte também  
 [Cache de modelo &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)   
 [Cache de XSL &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
  
  

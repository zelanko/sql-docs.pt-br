---
title: Cache de modelos, XSL e esquemas (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLXML, caching
- cache [SQLXML]
- memory [SQLXML]
ms.assetid: 80b4fa79-243f-442c-9f22-74ad66186501
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 77e400841542e8e372ccb48f85ffd3a130f9e264
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="caching-templates-xsl-and-schemas-sqlxml-40"></a>Armazenando modelos, XSL e esquemas em cache (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Para melhorar o desempenho, o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 dá suporte ao cache de modelos, XSL e esquemas.  
  
 Todos os esquemas, modelos e arquivos XSL (exceto os arquivos de um local http:// ou ftp://) são armazenados em cache. Os arquivos armazenados em cache permanecem na memória enquanto o processo está em execução. Quando o processo é encerrado, todo o cache é perdido. Assim, se você executar um processo por consulta, talvez a vantagem do cache não seja notável.  
  
 Os tópicos nesta seção fornecem mais informações sobre o cache.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Cache de modelo &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)  
 Descreve e fornece uma chave do Registro o cache de modelos.  
  
 [Cache de XSL & #40; SQLXML 4.0 & #41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
 Descreve e fornece uma chave do Registro o cache de XSL.  
  
 [Cache de esquemas & #40; SQLXML 4.0 & #41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)  
 Discute problemas de instalação lado a lado do SQLXML relacionados ao cache de esquemas e fornece chaves do Registro para o cache de esquemas.  
  
  

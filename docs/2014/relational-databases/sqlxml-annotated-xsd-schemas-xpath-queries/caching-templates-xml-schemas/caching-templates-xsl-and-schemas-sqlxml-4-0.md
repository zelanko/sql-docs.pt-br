---
title: Caching de modelos, XSL e esquemas (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, caching
- cache [SQLXML]
- memory [SQLXML]
ms.assetid: 80b4fa79-243f-442c-9f22-74ad66186501
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 82b943a170c42010b650033841f6612338d99119
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66013247"
---
# <a name="caching-templates-xsl-and-schemas-sqlxml-40"></a>Armazenando modelos, XSL e esquemas em cache (SQLXML 4.0)
  Para melhorar o desempenho, o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 dá suporte ao cache de modelos, XSL e esquemas.  
  
 Todos os esquemas, modelos e arquivos XSL (exceto os arquivos de um local http:// ou ftp://) são armazenados em cache. Os arquivos armazenados em cache permanecem na memória enquanto o processo está em execução. Quando o processo é encerrado, todo o cache é perdido. Assim, se você executar um processo por consulta, talvez a vantagem do cache não seja notável.  
  
 Os tópicos nesta seção fornecem mais informações sobre o cache.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Cache de modelos &#40;SQLXML 4,0&#41;](template-caching-sqlxml-4-0.md)  
 Descreve e fornece uma chave do Registro o cache de modelos.  
  
 [Cache XSL &#40;SQLXML 4,0&#41;](xsl-caching-sqlxml-4-0.md)  
 Descreve e fornece uma chave do Registro o cache de XSL.  
  
 [Cache de esquema &#40;SQLXML 4,0&#41;](schema-caching-sqlxml-4-0.md)  
 Discute problemas de instalação lado a lado do SQLXML relacionados ao cache de esquemas e fornece chaves do Registro para o cache de esquemas.  
  
  

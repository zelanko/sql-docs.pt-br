---
title: "Outras anotações (SQLXML 4.0) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- url-encode annotation
- sql:key-fields
- use-cdata annotation
- sql:is-mapping-schema
- sql:url-encode
- sql:id-prefix
- sql:use-cdata
- key-fields annotation
- id-prefix annotation [SQLXML]
- is-mapping-schema annotation
ms.assetid: f7b4d37b-d6d3-4ac3-b2fd-a0b534a924e4
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 72a8024f46921af6b8e52222c86d89fce1c8dc7b
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
---
# <a name="annotation-interpretation---other-annotations"></a>Interpretação de anotação - outras anotações
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Além das anotações discutidas nos tópicos anteriores nesta seção, o carregamento em massa de XML interpreta estas outras anotações:  
  
 **sql:id-prefix**  
 Se o esquema especificar prefixos aos dados XML, o carregamento em massa de XML removerá os prefixos antes de enviar os dados ao Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **sql:use-cdata**  
 O carregamento em massa de XML lê o texto que é armazenado nas seções CDATA e os envia para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **sql:url-encode**  
 O carregamento em massa de XML não dá suporte esta anotação. Por exemplo, você não pode especificar uma URL na entrada de dados XML e esperar que o carregamento em massa de XML leia os dados desse local para armazená-los no banco de dados.  
  
 **sql:is-mapping-schema**  
 O carregamento em massa de XML não dá suporte esta anotação, nem dá suporte a **sql:id**.  
  
> [!NOTE]  
>  O carregamento em massa de XML não dá suporte a esquemas de mapeamento embutidos.  
  
 **sql:key-fields**  
 O carregamento em massa de XML sempre ignora esta anotação.  
  
## <a name="see-also"></a>Consulte também  
 [Interpretação de anotação &#40; SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sqlxml-4-0.md)  
  
  

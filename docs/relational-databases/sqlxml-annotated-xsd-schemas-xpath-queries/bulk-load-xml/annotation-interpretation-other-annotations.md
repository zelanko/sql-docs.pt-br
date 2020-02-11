---
title: Outras anotações (SQLXML)
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
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
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7eb01a084ec968adbd9fe8ff86623bcca5f9eb26
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75246827"
---
# <a name="annotation-interpretation---other-annotations"></a>Interpretação de anotação – Outras anotações
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
  
## <a name="see-also"></a>Consulte Também  
 [Interpretação de anotação &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sqlxml-4-0.md)  
  
  

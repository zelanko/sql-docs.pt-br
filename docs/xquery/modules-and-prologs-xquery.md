---
title: "Módulos e Prólogos (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- XQuery, prolog
- prolog
ms.assetid: 0f17b4a4-6234-41d4-a996-6db4e27bff7e
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f424809019ad7de0c27b91d4c43563256697c90c
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="modules-and-prologs-xquery"></a>Módulos e prólogos (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [Prólogo do XQuery](../xquery/modules-and-prologs-xquery-prolog.md) é uma série de declarações de namespace. Ao utilizar o declare namespace no prólogo, você pode especificar o prefixo da associação de namespace e usar o prefixo no corpo de consulta.  
  
## <a name="implementation-limitations"></a>Limitações de implementação  
 As seguintes especificações de XQuery não têm suporte nesta implementação:  
  
-   Declaração de módulo (`version`)  
  
-   Declaração de módulo (`module namespace`)  
  
-   Xmpspacedeclaration (`xmlspace`)  
  
-   Declaração padrão de agrupamento (`declare default collation`)  
  
-   Declaração de URI base (`declare base-uri`)  
  
-   Declaração de construção (`declare construction`)  
  
-   Declaração padrão de ordenação (`declare ordering`)  
  
-   Importação de esquema (`import schema namespace`)  
  
-   Importação de módulo (`import module`)  
  
-   Declaração de variável no prólogo (`declare variable`)  
  
-   Declaração de função (`declare function`)  
  
## <a name="in-this-section"></a>Nesta seção  
 [Prólogo do XQuery](../xquery/modules-and-prologs-xquery-prolog.md)  
 Descreve o prólogo do XQuery.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  

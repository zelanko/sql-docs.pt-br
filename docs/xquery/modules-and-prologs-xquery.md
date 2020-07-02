---
title: Módulos e Prologs (XQuery) | Microsoft Docs
description: Saiba quais especificações não são suportadas ao declarar um namespace em um prólogo XQuery.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, prolog
- prolog
ms.assetid: 0f17b4a4-6234-41d4-a996-6db4e27bff7e
author: rothja
ms.author: jroth
ms.openlocfilehash: c7d982e8c944ff1c596dfa4178ce613ec3be709e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85759493"
---
# <a name="modules-and-prologs-xquery"></a>Módulos e prólogos (XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  O [XQuery prólogo](../xquery/modules-and-prologs-xquery-prolog.md) é uma série de declarações de namespace. Ao utilizar o declare namespace no prólogo, você pode especificar o prefixo da associação de namespace e usar o prefixo no corpo de consulta.  
  
## <a name="implementation-limitations"></a>Limitações de implementação  
 As seguintes especificações de XQuery não têm suporte nesta implementação:  
  
-   Declaração de módulo (`version`)  
  
-   Declaração de módulo (`module namespace`)  
  
-   Xmpspacedeclaration ( `xmlspace` )  
  
-   Declaração padrão de ordenação (`declare default collation`)  
  
-   Declaração de URI base (`declare base-uri`)  
  
-   Declaração de construção (`declare construction`)  
  
-   Declaração padrão de ordenação (`declare ordering`)  
  
-   Importação de esquema (`import schema namespace`)  
  
-   Importação de módulo (`import module`)  
  
-   Declaração de variável no prólogo (`declare variable`)  
  
-   Declaração de função (`declare function`)  
  
## <a name="in-this-section"></a>Nesta seção  
 [Prólogo XQuery](../xquery/modules-and-prologs-xquery-prolog.md)  
 Descreve o prólogo do XQuery.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  

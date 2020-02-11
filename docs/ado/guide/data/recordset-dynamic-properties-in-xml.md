---
title: Propriedades dinâmicas do conjunto de registros em XML | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset dynamic properties in XML [ADO]
ms.assetid: 52f8e379-812a-4db8-9210-94458926301c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a058a2d0c5a808f29807744c6ba01f658bebc120
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924440"
---
# <a name="recordset-dynamic-properties-in-xml"></a>Propriedades dinâmicas do conjunto de registros em XML
As propriedades específicas do provedor de conjunto de registros a seguir (do mecanismo de cursor do cliente) atualmente persistem no formato XML:  
  
-   Atualizar ressincronização  
  
-   Tabela única  
  
-   Esquema exclusivo  
  
-   Catálogo exclusivo  
  
-   Comando Ressync  
  
-   IRowsetChange  
  
-   IRowsetUpdate  
  
-   CommandTimeOut  
  
-   BatchSize  
  
-   UpdateCriteria  
  
-   Remodelar nome  
  
-   AutoRecalc  
  
 Essas propriedades são salvas na seção de esquema como atributos da definição do elemento para o conjunto de registros que está sendo persistido. Esses atributos são definidos no namespace do esquema do conjunto de linhas e devem ter o prefixo "RS:".  
  
## <a name="see-also"></a>Consulte Também  
 [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)

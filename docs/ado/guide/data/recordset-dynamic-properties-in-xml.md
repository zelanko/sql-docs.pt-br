---
title: Propriedades do conjunto de registros dinâmicos em XML | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924440"
---
# <a name="recordset-dynamic-properties-in-xml"></a>Propriedades dinâmicas do conjunto de registros em XML
Atualmente, as seguintes propriedades específicas do provedor de conjunto de registros (do mecanismo de Cursor de cliente) são persistidas no formato XML:  
  
-   Ressincronização de atualização  
  
-   Tabela única  
  
-   Esquema exclusivo  
  
-   Catálogo exclusivo  
  
-   Comando de ressincronização  
  
-   IRowsetChange  
  
-   IRowsetUpdate  
  
-   CommandTimeOut  
  
-   BatchSize  
  
-   UpdateCriteria  
  
-   Alterar a forma de nome  
  
-   AutoRecalc  
  
 Essas propriedades são salvos na seção esquema como atributos da definição de elemento para o conjunto de registros que estão sendo mantido. Esses atributos são definidos no namespace do esquema de conjunto de linhas e deve ter o prefixo "rs:".  
  
## <a name="see-also"></a>Consulte também  
 [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)

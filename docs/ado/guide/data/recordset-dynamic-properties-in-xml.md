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
author: rothja
ms.author: jroth
ms.openlocfilehash: d9d19ded093cd10a7670b31cd2d5c78a475950d2
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760962"
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

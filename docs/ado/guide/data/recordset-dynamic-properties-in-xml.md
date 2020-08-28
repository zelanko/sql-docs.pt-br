---
description: Propriedades dinâmicas do conjunto de registros em XML
title: Propriedades dinâmicas do conjunto de registros em XML | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset dynamic properties in XML [ADO]
ms.assetid: 52f8e379-812a-4db8-9210-94458926301c
author: rothja
ms.author: jroth
ms.openlocfilehash: 395a81108e3ceaed99ad8ccf1fbab29831dd116d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979887"
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

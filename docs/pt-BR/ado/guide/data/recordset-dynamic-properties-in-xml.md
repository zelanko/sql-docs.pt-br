---
title: Propriedades de conjunto de registros dinâmicos no XML | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset dynamic properties in XML [ADO]
ms.assetid: 52f8e379-812a-4db8-9210-94458926301c
caps.latest.revision: 3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 84619cdbe7070cc971d9347b2bfd3b7b5ba5c6a5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="recordset-dynamic-properties-in-xml"></a>Propriedades de conjunto de registros dinâmicos no XML
Atualmente, as seguintes propriedades específico do provedor de conjunto de registros (do mecanismo de Cursor de cliente) são mantidas no formato XML:  
  
-   Ressincronização de atualização  
  
-   Tabela exclusiva  
  
-   Esquema exclusivo  
  
-   Catálogo exclusivo  
  
-   Sincronizar de comando  
  
-   IRowsetChange  
  
-   IRowsetUpdate  
  
-   CommandTimeOut  
  
-   BatchSize  
  
-   UpdateCriteria  
  
-   Alterar a forma de nome  
  
-   AutoRecalc  
  
 Essas propriedades são salvos na seção de esquema como atributos da definição do elemento do conjunto de registros sendo persistente. Esses atributos são definidos no namespace do esquema de conjunto de linhas e deve ter o prefixo "rs:".  
  
## <a name="see-also"></a>Consulte também  
 [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)

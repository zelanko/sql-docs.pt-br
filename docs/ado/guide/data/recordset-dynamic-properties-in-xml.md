---
title: "Propriedades de conjunto de registros dinâmicos no XML | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Recordset dynamic properties in XML [ADO]
ms.assetid: 52f8e379-812a-4db8-9210-94458926301c
caps.latest.revision: "3"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 925981765184f05deadfda8ca8b27a929a6387ab
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
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

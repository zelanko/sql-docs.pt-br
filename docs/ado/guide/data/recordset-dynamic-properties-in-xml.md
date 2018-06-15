---
title: Propriedades de conjunto de registros dinâmicos no XML | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: cd874d0db6d026b82ddbc8055a17a073194c6e07
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272325"
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

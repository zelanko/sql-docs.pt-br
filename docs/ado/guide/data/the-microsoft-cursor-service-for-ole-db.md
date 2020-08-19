---
description: O Microsoft Cursor Service para OLE DB
title: O serviço de cursor da Microsoft para OLE DB | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursor service for ole db [ADO]
- cursors [ADO], cursor service for OLE DB
ms.assetid: 1ac3bd9b-2d45-4cc8-88ec-bd8a218cfb49
author: rothja
ms.author: jroth
ms.openlocfilehash: f3646ec86f76fcba2f6b82759a4784de7d463279
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452738"
---
# <a name="the-microsoft-cursor-service-for-ole-db"></a>O Microsoft Cursor Service para OLE DB
Quando você seleciona um cursor do lado do cliente ou define a propriedade **CursorLocation** como **adUseClient**, você está invocando o serviço de cursor da Microsoft para OLE DB. Você também pode ver referências ao "mecanismo de cursor do cliente", que é essencialmente a mesma coisa no contexto do ADO. Esse serviço complementa as funções de suporte ao cursor de provedores de dados. Como resultado, você pode perceber uma funcionalidade relativamente uniforme de todos os provedores de dados.  
  
 O serviço de cursor para OLE DB torna as propriedades dinâmicas disponíveis e aprimora o comportamento de determinados métodos. Por exemplo, a propriedade **otimizar** dinâmico permite a criação de índices temporários para facilitar determinadas operações, como o método **Find** .  
  
 O serviço de cursor habilita o suporte para atualização em lotes em todos os casos. Ele também simula tipos de cursor mais capacitados, como cursores dinâmicos, quando um provedor de dados só pode fornecer cursores menos capacitados, como cursores estáticos.  
  
## <a name="see-also"></a>Consulte Também  
 [Serviço de cursor da Microsoft para OLE DB (componente de serviço ADO)](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)

---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aeac8c848f01f01e8969f94c571ad15f5e7f615a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923914"
---
# <a name="the-microsoft-cursor-service-for-ole-db"></a>O Microsoft Cursor Service para OLE DB
Quando você seleciona um cursor do lado do cliente ou define a propriedade **CursorLocation** como **adUseClient**, você está invocando o serviço de cursor da Microsoft para OLE DB. Você também pode ver referências ao "mecanismo de cursor do cliente", que é essencialmente a mesma coisa no contexto do ADO. Esse serviço complementa as funções de suporte ao cursor de provedores de dados. Como resultado, você pode perceber uma funcionalidade relativamente uniforme de todos os provedores de dados.  
  
 O serviço de cursor para OLE DB torna as propriedades dinâmicas disponíveis e aprimora o comportamento de determinados métodos. Por exemplo, a propriedade **otimizar** dinâmico permite a criação de índices temporários para facilitar determinadas operações, como o método **Find** .  
  
 O serviço de cursor habilita o suporte para atualização em lotes em todos os casos. Ele também simula tipos de cursor mais capacitados, como cursores dinâmicos, quando um provedor de dados só pode fornecer cursores menos capacitados, como cursores estáticos.  
  
## <a name="see-also"></a>Consulte Também  
 [Serviço de cursor da Microsoft para OLE DB (componente de serviço ADO)](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)

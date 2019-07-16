---
title: O Microsoft Cursor Service para OLE DB | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923914"
---
# <a name="the-microsoft-cursor-service-for-ole-db"></a>O Microsoft Cursor Service para OLE DB
Quando você seleciona um cursor do lado do cliente, ou defina as **CursorLocation** propriedade **adUseClient**, você está invocando o Microsoft Cursor Service para OLE DB. Você também poderá ver referências para o "cliente Cursor mecanismo", que é essencialmente a mesma coisa no contexto do ADO. Esse serviço complementa as funções de suporte de cursor de provedores de dados. Como resultado, você pode perceber funcionalidade relativamente uniforme de todos os provedores de dados.  
  
 O Cursor Service para OLE DB disponibiliza as propriedades dinâmicas e aprimora o comportamento de determinados métodos. Por exemplo, o **otimizar** propriedade dinâmica permite a criação de índices temporários para facilitar a determinadas operações, como o **localizar** método.  
  
 O serviço de Cursor habilita o suporte para atualização em lote em todos os casos. Ele também simula o mais compatível com tipos de cursor, como cursores dinâmicos, quando um provedor de dados pode fornecer apenas cursores com menor capacidade, como os cursores estáticos.  
  
## <a name="see-also"></a>Consulte também  
 [Microsoft Cursor Service para OLE DB (componente de serviço do ADO)](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)

---
title: "Determinando o que há suporte para | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- editing data [ADO], Supports method
- Supports method [ADO]
ms.assetid: 65090cba-6d46-4775-8d61-f6838e7752a6
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 31d9ca56af28416f68555511a3d4a8439d370200
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="determining-what-is-supported"></a>Determinando o que tem suporte
O **dá suporte a** método é usado para determinar se um especificado **registros** objeto oferece suporte a um determinado tipo de funcionalidade. Ele tem a seguinte sintaxe:  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="remarks"></a>Remarks  
 O **suporta** método retorna um valor booliano que indica se o provedor oferece suporte a todos os recursos identificados pelo argumento CursorOptions. Você pode usar o **dá suporte a** método para determinar quais tipos de funcionalidade um **registros** objeto oferece suporte. Se o **registros** objeto suporta os recursos cujos constantes correspondentes estão em *CursorOptions*, o **dá suporte a** método retorna **True**. Caso contrário, retornará **False**.  
  
 Usando o **dá suporte a** método, você pode verificar a capacidade do **registros** objeto para adicionar novos registros, usar marcadores, use o **localizar** método, use a rolagem, use o  **Índice** propriedade e para executar atualizações em lotes. Para obter uma lista completa das constantes e seus significados, consulte [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md).  
  
 Embora o **dá suporte a** método pode retornar **True** para uma determinada funcionalidade, ele não garante que o provedor pode tornar o recurso disponível em todas as circunstâncias. O **suporta** método simplesmente retorna se o provedor pode oferecer suporte a funcionalidade especificada, supondo que determinadas condições forem atendidas. Por exemplo, o **dá suporte a** método pode indicar que um **registros** objeto dá suporte a atualizações, mesmo que o cursor estiver baseado em uma junção de várias tabelas — algumas colunas que não são atualizáveis.

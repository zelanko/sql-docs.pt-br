---
title: Determinando o que há suporte para | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], Supports method
- Supports method [ADO]
ms.assetid: 65090cba-6d46-4775-8d61-f6838e7752a6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c6af51d8d69f5897021733468ee93290e1b5e280
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702100"
---
# <a name="determining-what-is-supported"></a>Determinar o que é compatível
O **dá suporte a** método é usado para determinar se um especificado **Recordset** objeto dá suporte a um determinado tipo de funcionalidade. Ele tem a seguinte sintaxe:  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="remarks"></a>Comentários  
 O **dá suporte a** método retorna um valor booliano que indica se o provedor oferece suporte a todos os recursos identificados pelo argumento CursorOptions. Você pode usar o **dá suporte a** método para determinar quais tipos de funcionalidade um **Recordset** objeto dá suporte. Se o **conjunto de registros** objeto suporta os recursos cujos constantes correspondentes estão no *CursorOptions*, o **dá suporte a** retorno do método **True**. Caso contrário, retornará **falsos**.  
  
 Usando o **dá suporte a** método, você pode verificar a capacidade dos **conjunto de registros** objeto para adicionar novos registros, usar indicadores, use o **localizar** método, o uso de rolagem, use o  **Índice** propriedade e para executar atualizações em lotes. Para obter uma lista completa de constantes e seus significados, consulte [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md).  
  
 Embora o **suporta** método pode retornar **verdadeiro** para uma determinada funcionalidade, ele não garante que o provedor pode disponibilizar o recurso em todas as circunstâncias. O **dá suporte a** método simplesmente retorna se o provedor pode dar suporte a funcionalidade especificada, supondo que determinadas condições forem atendidas. Por exemplo, o **dá suporte a** método pode indicar que um **Recordset** objeto dá suporte a atualizações, mesmo que o cursor é baseado em uma associação de tabela de várias - algumas colunas que não são atualizáveis.

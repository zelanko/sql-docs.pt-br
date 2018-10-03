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
manager: craigg
ms.openlocfilehash: 835584da4c51f5e65306d0609b4e69f78a7d58b9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47707564"
---
# <a name="determining-what-is-supported"></a>Determinar o que é compatível
O **dá suporte a** método é usado para determinar se um especificado **Recordset** objeto dá suporte a um determinado tipo de funcionalidade. Ele tem a seguinte sintaxe:  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="remarks"></a>Comentários  
 O **dá suporte a** método retorna um valor booliano que indica se o provedor oferece suporte a todos os recursos identificados pelo argumento CursorOptions. Você pode usar o **dá suporte a** método para determinar quais tipos de funcionalidade um **Recordset** objeto dá suporte. Se o **conjunto de registros** objeto suporta os recursos cujos constantes correspondentes estão no *CursorOptions*, o **dá suporte a** retorno do método **True**. Caso contrário, retornará **falsos**.  
  
 Usando o **dá suporte a** método, você pode verificar a capacidade dos **conjunto de registros** objeto para adicionar novos registros, usar indicadores, use o **localizar** método, o uso de rolagem, use o  **Índice** propriedade e para executar atualizações em lotes. Para obter uma lista completa de constantes e seus significados, consulte [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md).  
  
 Embora o **suporta** método pode retornar **verdadeiro** para uma determinada funcionalidade, ele não garante que o provedor pode disponibilizar o recurso em todas as circunstâncias. O **dá suporte a** método simplesmente retorna se o provedor pode dar suporte a funcionalidade especificada, supondo que determinadas condições forem atendidas. Por exemplo, o **dá suporte a** método pode indicar que um **Recordset** objeto dá suporte a atualizações, mesmo que o cursor estiver baseado em uma junção de várias tabelas — algumas colunas que não são atualizáveis.

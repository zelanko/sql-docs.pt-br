---
description: Determinar o que é compatível
title: Determinando o que é suportado | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1936048f0ced1a15a8134a81bc3de2a09244803d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453488"
---
# <a name="determining-what-is-supported"></a>Determinar o que é compatível
O método de **suporte** é usado para determinar se um objeto **Recordset** especificado dá suporte a um tipo específico de funcionalidade. Ele tem a seguinte sintaxe:  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="remarks"></a>Comentários  
 O método de **suporte** retorna um valor booliano que indica se o provedor dá suporte a todos os recursos identificados pelo argumento CursorOptions. Você pode usar o método de **suporte** para determinar os tipos de funcionalidade aos quais um objeto **Recordset** dá suporte. Se o objeto **Recordset** der suporte aos recursos cujas constantes correspondentes estão em *CursorOptions*, o método de **suporte** retornará **true**. Caso contrário, retornará **false**.  
  
 Usando o método de **suporte** , você pode verificar a capacidade do objeto **Recordset** de adicionar novos registros, usar indicadores, usar o método **Find** , usar a rolagem, usar a propriedade **index** e executar atualizações em lote. Para obter uma lista completa de constantes e seus significados, consulte [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md).  
  
 Embora o método de **suporte** possa retornar **true** para uma determinada funcionalidade, ele não garante que o provedor possa disponibilizar o recurso em todas as circunstâncias. O método de **suporte** simplesmente retorna se o provedor pode dar suporte à funcionalidade especificada, supondo que determinadas condições sejam atendidas. Por exemplo, o método de **suporte** pode indicar que um objeto **Recordset** dá suporte a atualizações, mesmo que o cursor se baseie em uma junção com várias tabelas – algumas colunas das quais não são atualizáveis.

---
description: Coleção Errors (ADO)
title: Coleta de erros (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Errors
- Connection15::get_Errors
- Connection15::GetErrors
helpviewer_keywords:
- Errors collection [ADO]
ms.assetid: 290819e1-7b39-4e1e-a93b-801257138b00
author: rothja
ms.author: jroth
ms.openlocfilehash: 6f4719c9dcf182b6840ad950373b35c7ea8f0361
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443948"
---
# <a name="errors-collection-ado"></a>Coleção Errors (ADO)
Contém todos os objetos de [erro](../../../ado/reference/ado-api/error-object.md) criados em resposta a uma falha relacionada a um único provedor.  
  
## <a name="remarks"></a>Comentários  
 Qualquer operação que envolva objetos ADO pode gerar um ou mais erros de provedor. Como ocorre cada erro, um ou mais objetos de **erro** podem ser colocados na coleção de **erros** do objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) . Quando outra operação ADO gera um erro, a coleção de **erros** é desmarcada e o novo conjunto de objetos de **erro** pode ser colocado na coleção de **erros** .  
  
 Cada objeto de **erro** representa um erro de provedor específico, não um erro de ADO. Os erros do ADO são expostos ao mecanismo de tratamento de exceção de tempo de execução. Por exemplo, no Microsoft Visual Basic, a ocorrência de um erro específico do ADO irá disparar um evento [OnError](../../../ado/reference/rds-api/onerror-event-rds.md) e aparecerá no objeto **Err** .  
  
 As operações ADO que não geram um erro não têm nenhum efeito na coleção de **erros** . Use o método [Clear](../../../ado/reference/ado-api/clear-method-ado.md) para limpar manualmente a coleção de **erros** .  
  
 O conjunto de objetos de **erro** na coleção de **erros** descreve todos os erros que ocorreram em resposta a uma única instrução. A enumeração dos erros específicos na coleção de **erros** permite que suas rotinas de tratamento de erros determinem mais precisamente a causa e a origem de um erro e tomem as medidas apropriadas para a recuperação.  
  
 Algumas propriedades e métodos retornam avisos que aparecem como objetos de **erro** na coleção de **erros** , mas não interrompem a execução de um programa. Antes de chamar os métodos [Ressync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)ou [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) em um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) , o método [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) em um objeto **Connection** ou definir a propriedade [Filter](../../../ado/reference/ado-api/filter-property.md) em um objeto **Recordset** , chame o método **Clear** na coleção **Errors** . Dessa forma, você pode ler a propriedade [Count](../../../ado/reference/ado-api/count-property-ado.md) da coleção de **erros** para testar os avisos retornados.  
  
> [!NOTE]
>  Consulte o tópico objeto de **erro** para obter uma explicação mais detalhada do modo como uma única operação ADO pode gerar vários erros.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos da coleção de erros](../../../ado/reference/ado-api/errors-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto de erro](../../../ado/reference/ado-api/error-object.md)   
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)

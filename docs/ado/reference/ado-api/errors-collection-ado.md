---
title: "Coleção de erros (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::Errors
- Connection15::get_Errors
- Connection15::GetErrors
helpviewer_keywords:
- Errors collection [ADO]
ms.assetid: 290819e1-7b39-4e1e-a93b-801257138b00
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 27ca46528314f34b769d505269ade0c73fb1b051
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="errors-collection-ado"></a>Coleção de erros (ADO)
Contém todos os [erro](../../../ado/reference/ado-api/error-object.md) objetos criados em resposta a uma única falha de provedor.  
  
## <a name="remarks"></a>Comentários  
 Qualquer operação que envolva objetos ADO pode gerar um ou mais erros do provedor. Como cada erro, um ou mais **erro** objetos podem ser colocados no **erros** coleção do [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto. Quando outra operação ADO gera um erro, o **erros** coleção é desmarcada e o novo conjunto de **erro** objetos podem ser colocados no **erros** coleção.  
  
 Cada **erro** objeto representa um erro de provedor específico, não um erro de ADO. Erros de ADO são expostos para o mecanismo de tratamento de exceções de tempo de execução. Por exemplo, no Microsoft Visual Basic, a ocorrência de um erro específico de ADO irá disparar um [onError](../../../ado/reference/rds-api/onerror-event-rds.md) evento e aparece no **Err** objeto.  
  
 Operações de ADO que não geram erros não têm nenhum efeito o **erros** coleção. Use o [limpar](../../../ado/reference/ado-api/clear-method-ado.md) método limpar manualmente o **erros** coleção.  
  
 O conjunto de **erro** objetos no **erros** coleção descreve todos os erros que ocorreram em resposta a uma única instrução. Enumeração de erros específicos no **erros** coleção permite que suas rotinas de tratamento de erros determinar a causa e origem de um erro com mais precisão e execute as etapas apropriadas para recuperar.  
  
 Algumas propriedades e métodos retornam os avisos que aparecem como **erro** objetos no **erros** coleção, mas não interromper a execução do programa. Antes de chamar o [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), ou [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) métodos em um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto, o [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md) método em um **Conexão** de objeto, ou definir o [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade em um **Recordset** de objeto, chame o **limpar**método sobre o **erros** coleção. Dessa forma, você pode ler o [contagem](../../../ado/reference/ado-api/count-property-ado.md) propriedade o **erros** avisos retornados de coleção para testar.  
  
> [!NOTE]
>  Consulte o **erro** tópico para obter uma explicação mais detalhada da maneira como uma única operação ADO pode gerar vários erros.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Eventos, métodos e propriedades de coleção de erros](../../../ado/reference/ado-api/errors-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Error](../../../ado/reference/ado-api/error-object.md)   
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)


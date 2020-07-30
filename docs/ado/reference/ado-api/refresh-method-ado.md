---
title: Método Refresh (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Collection::Refresh
- Parameters::Refresh
- Properties::Refresh
helpviewer_keywords:
- Refresh method [ADO]
ms.assetid: 089b7ca7-684f-4259-8032-5bd1ecc54426
author: rothja
ms.author: jroth
ms.openlocfilehash: 0688fc8b45f444ca8c711f3229623484fa2139a8
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242576"
---
# <a name="refresh-method-ado"></a>Método Refresh (ADO)
Atualiza os objetos em uma coleção para refletir objetos disponíveis de e específicos para o provedor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
collection.Refresh  
```  
  
## <a name="remarks"></a>Comentários  
 O método **Refresh** realiza diferentes tarefas, dependendo da coleção da qual você a chama.  
  
### <a name="parameters"></a>parâmetros  
 O uso do método **Refresh** na coleção [Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md) de um objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) recupera informações de parâmetro do lado do provedor para o procedimento armazenado ou a consulta parametrizada especificada no objeto **Command** . A coleção estará vazia para provedores que não dão suporte a chamadas de procedimento armazenado ou consultas parametrizadas.  
  
 Você deve definir a [propriedade ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) do objeto **de comando** como um objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) válido, a propriedade [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) para um comando válido e a propriedade [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) como **adCmdStoredProc** antes de chamar o método **Refresh** .  
  
 Se você acessar a coleção de **parâmetros** antes de chamar o método **Refresh** , o ADO chamará automaticamente o método e preencherá a coleção para você.  
  
> [!NOTE]
>  Se você usar o método **Refresh** para obter informações de parâmetro do provedor e ele retornar um ou mais objetos de [parâmetro](../../../ado/reference/ado-api/parameter-object.md) de tipo de dados de comprimento variável, o ADO poderá alocar memória para os parâmetros com base em seu tamanho máximo potencial, o que causará um erro durante a execução. Você deve definir explicitamente a propriedade [size](../../../ado/reference/ado-api/size-property-ado-parameter.md) para esses parâmetros antes de chamar o método [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) para evitar erros.  
  
### <a name="fields"></a>Campos  
 O uso do método **Refresh** na coleção [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) não tem efeito visível. Para recuperar as alterações da estrutura de banco de dados subjacente, você deve usar o método [Requery](../../../ado/reference/ado-api/requery-method.md) ou, se o objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) não oferecer suporte a indicadores, o método [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) .  
  
### <a name="properties"></a>Propriedades  
 O uso do método **Refresh** em uma coleção **Properties** de alguns objetos popula a coleção com as propriedades dinâmicas que o provedor expõe. Essas propriedades fornecem informações sobre a funcionalidade específica para o provedor, além das propriedades internas que o ADO dá suporte.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Coleção de eixos](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)  
        [Coleção de colunas](../../../ado/reference/adox-api/columns-collection-adox.md)  
        [Coleção CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)  
        [Coleção Dimensions](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)  
        [Coleção de erros](../../../ado/reference/ado-api/errors-collection-ado.md)  
        [Coleção Fields](../../../ado/reference/ado-api/fields-collection-ado.md)  
        [Coleção de grupos](../../../ado/reference/adox-api/groups-collection-adox.md)  
    :::column-end:::
    :::column:::
        [Coleção de hierarquias](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)  
        [Coleção de índices](../../../ado/reference/adox-api/indexes-collection-adox.md)  
        [Coleção de chaves](../../../ado/reference/adox-api/keys-collection-adox.md)  
        [Coleção de níveis](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)  
        [Coleção de membros](../../../ado/reference/ado-md-api/members-collection-ado-md.md)  
        [Coleção Parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md)  
    :::column-end:::
    :::column:::
        [Coleção de posições](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)  
        [Coleção de procedimentos](../../../ado/reference/adox-api/procedures-collection-adox.md)  
        [Coleção de propriedades](../../../ado/reference/ado-api/properties-collection-ado.md)  
        [Coleção de tabelas](../../../ado/reference/adox-api/tables-collection-adox.md)  
        [Coleção de usuários](../../../ado/reference/adox-api/users-collection-adox.md)  
        [Coleção views](../../../ado/reference/adox-api/views-collection-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Refresh (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Exemplo do método Refresh (VC + +)](../../../ado/reference/ado-api/refresh-method-example-vc.md)   
 [Propriedade Count (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Método Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)

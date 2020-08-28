---
description: Método Refresh (ADO)
title: Método Refresh (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 66324860f931a919cccc36d3de9464d2ad2e48d0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989607"
---
# <a name="refresh-method-ado"></a>Método Refresh (ADO)
Atualiza os objetos em uma coleção para refletir objetos disponíveis de e específicos para o provedor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
collection.Refresh  
```  
  
## <a name="remarks"></a>Comentários  
 O método **Refresh** realiza diferentes tarefas, dependendo da coleção da qual você a chama.  
  
### <a name="parameters"></a>Parâmetros  
 O uso do método **Refresh** na coleção [Parameters](./parameters-collection-ado.md) de um objeto de [comando](./command-object-ado.md) recupera informações de parâmetro do lado do provedor para o procedimento armazenado ou a consulta parametrizada especificada no objeto **Command** . A coleção estará vazia para provedores que não dão suporte a chamadas de procedimento armazenado ou consultas parametrizadas.  
  
 Você deve definir a [propriedade ActiveConnection](./activeconnection-property-ado.md) do objeto **de comando** como um objeto de [conexão](./connection-object-ado.md) válido, a propriedade [CommandText](./commandtext-property-ado.md) para um comando válido e a propriedade [CommandType](./commandtype-property-ado.md) como **adCmdStoredProc** antes de chamar o método **Refresh** .  
  
 Se você acessar a coleção de **parâmetros** antes de chamar o método **Refresh** , o ADO chamará automaticamente o método e preencherá a coleção para você.  
  
> [!NOTE]
>  Se você usar o método **Refresh** para obter informações de parâmetro do provedor e ele retornar um ou mais objetos de [parâmetro](./parameter-object.md) de tipo de dados de comprimento variável, o ADO poderá alocar memória para os parâmetros com base em seu tamanho máximo potencial, o que causará um erro durante a execução. Você deve definir explicitamente a propriedade [size](./size-property-ado-parameter.md) para esses parâmetros antes de chamar o método [Execute](./execute-method-ado-command.md) para evitar erros.  
  
### <a name="fields"></a>Campos  
 O uso do método **Refresh** na coleção [Fields](./fields-collection-ado.md) não tem efeito visível. Para recuperar as alterações da estrutura de banco de dados subjacente, você deve usar o método [Requery](./requery-method.md) ou, se o objeto [Recordset](./recordset-object-ado.md) não oferecer suporte a indicadores, o método [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md) .  
  
### <a name="properties"></a>Propriedades  
 O uso do método **Refresh** em uma coleção **Properties** de alguns objetos popula a coleção com as propriedades dinâmicas que o provedor expõe. Essas propriedades fornecem informações sobre a funcionalidade específica para o provedor, além das propriedades internas que o ADO dá suporte.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Coleção de eixos](../ado-md-api/axes-collection-ado-md.md)  
        [Coleção de colunas](../adox-api/columns-collection-adox.md)  
        [Coleção CubeDefs](../ado-md-api/cubedefs-collection-ado-md.md)  
        [Coleção Dimensions](../ado-md-api/dimensions-collection-ado-md.md)  
        [Coleção de erros](./errors-collection-ado.md)  
        [Coleção Fields](./fields-collection-ado.md)  
        [Coleção de grupos](../adox-api/groups-collection-adox.md)  
    :::column-end:::
    :::column:::
        [Coleção de hierarquias](../ado-md-api/hierarchies-collection-ado-md.md)  
        [Coleção de índices](../adox-api/indexes-collection-adox.md)  
        [Coleção de chaves](../adox-api/keys-collection-adox.md)  
        [Coleção de níveis](../ado-md-api/levels-collection-ado-md.md)  
        [Coleção de membros](../ado-md-api/members-collection-ado-md.md)  
        [Coleção Parâmetros](./parameters-collection-ado.md)  
    :::column-end:::
    :::column:::
        [Coleção de posições](../ado-md-api/positions-collection-ado-md.md)  
        [Coleção de procedimentos](../adox-api/procedures-collection-adox.md)  
        [Coleção de propriedades](./properties-collection-ado.md)  
        [Coleção de tabelas](../adox-api/tables-collection-adox.md)  
        [Coleção de usuários](../adox-api/users-collection-adox.md)  
        [Coleção views](../adox-api/views-collection-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Refresh (VB)](./refresh-method-example-vb.md)   
 [Exemplo do método Refresh (VC + +)](./refresh-method-example-vc.md)   
 [Propriedade Count (ADO)](./count-property-ado.md)   
 [Método Refresh (RDS)](../rds-api/refresh-method-rds.md)
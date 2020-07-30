---
title: Propriedade ActiveConnection (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::ActiveConnection
- Recordset15::get_ActiveConnection
- _Record::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO]
ms.assetid: 52d0a96c-14fb-4ad9-b004-4d821bc0a6db
author: rothja
ms.author: jroth
ms.openlocfilehash: 375f0a0b81f71294b67200f8137ee381a638b8ac
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242906"
---
# <a name="activeconnection-property-ado"></a>Propriedade ActiveConnection (ADO)
Indica a qual objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) o [comando](../../../ado/reference/ado-api/command-object-ado.md), [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)ou objeto de [registro](../../../ado/reference/ado-api/record-object-ado.md) especificado atualmente pertence.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de **cadeia de caracteres** que contém uma definição para uma conexão se a conexão for fechada ou uma **variante** que contém o objeto de **conexão** atual se a conexão estiver aberta. O padrão é uma referência de objeto nulo. Consulte a propriedade [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) .  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **ActiveConnection** para determinar o objeto de **conexão** sobre o qual o objeto de **comando** especificado será executado ou o **conjunto de registros** especificado será aberto.  
  
## <a name="command"></a>Comando  
 Para objetos de **comando** , a propriedade **ActiveConnection** é de leitura/gravação.  
  
 Se você tentar chamar o método [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) em um objeto **Command** antes de definir essa propriedade como um objeto de **conexão** aberta ou uma cadeia de conexão válida, ocorrerá um erro.  
  
 Se um objeto de **conexão** for atribuído à propriedade **ActiveConnection** , o objeto deverá ser aberto. A atribuição de um objeto de conexão fechado causa um erro.  
  
### <a name="note"></a>Observação  
 **Visual Basic da Microsoft** Definir a propriedade **ActiveConnection** como *Nothing* desassocia o objeto **Command** da **conexão** atual e faz com que o provedor libere todos os recursos associados na fonte de dados. Em seguida, você pode associar o objeto de **comando** ao mesmo ou a outro objeto de **conexão** . Alguns provedores permitem que você altere a configuração de propriedade de uma **conexão** para outra, sem precisar primeiro definir a propriedade como *Nothing*.  
  
 Se a coleção [Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md) do objeto **Command** contiver parâmetros fornecidos pelo provedor, a coleção será desmarcada se você definir a propriedade **ActiveConnection** como *Nothing* ou como outro objeto **Connection** . Se você criar manualmente objetos de [parâmetro](../../../ado/reference/ado-api/parameter-object.md) e usá-los para preencher a coleção de **parâmetros** do objeto de **comando** , a definição da propriedade **ActiveConnection** como *Nothing* ou outro objeto de **conexão** deixará a coleção de **parâmetros** intacta.  
  
 Fechar o objeto de **conexão** ao qual um objeto de **comando** está associado define a propriedade **ActiveConnection** como *Nothing*. A definição dessa propriedade como um objeto de **conexão** fechado gera um erro.  
  
## <a name="recordset"></a>Conjunto de registros  
 Para objetos Open **Recordset** ou objetos **Recordset** cuja propriedade [Source](../../../ado/reference/ado-api/source-property-ado-recordset.md) está definida como um objeto **Command** válido, a propriedade **ActiveConnection** é somente leitura. Caso contrário, será leitura/gravação.  
  
 Você pode definir essa propriedade como um objeto de **conexão** válido ou com uma cadeia de conexão válida. Nesse caso, o provedor cria um novo objeto de **conexão** usando essa definição e abre a conexão. Além disso, o provedor pode definir essa propriedade como o novo objeto de **conexão** para dar a você uma maneira de acessar o objeto de **conexão** para obter informações de erro estendidas ou executar outros comandos.  
  
 Se você usar o argumento *ActiveConnection* do método [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) para abrir um objeto **Recordset** , a propriedade **ActiveConnection** irá herdar o valor do argumento.  
  
 Se você definir a propriedade **Source** do objeto **Recordset** como uma variável de **objeto Command** válida, a propriedade **ActiveConnection** do conjunto de **registros** herdará a configuração da propriedade **ActiveConnection** do objeto **Command** .  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** Quando usado em um objeto **Recordset** do lado do cliente, essa propriedade pode ser definida somente como uma cadeia de conexão ou (no Microsoft Visual Basic ou Visual Basic, Scripting Edition) como *Nothing*.  
  
## <a name="record"></a>Record  
 Essa propriedade é de leitura/gravação quando o objeto de **registro** é fechado e pode conter uma cadeia de conexão ou referência a um objeto de **conexão** aberta. Essa propriedade é somente leitura quando o objeto de **registro** está aberto e contém uma referência a um objeto de **conexão** aberta.  
  
 Um objeto de **conexão** é criado implicitamente quando o objeto de **registro** é aberto a partir de uma URL. Abra o **registro** com um objeto de **conexão** aberto existente atribuindo o objeto de **conexão** a essa propriedade ou usando o objeto de **conexão** como um parâmetro na chamada do método [Open](../../../ado/reference/ado-api/open-method-ado-record.md) . Se o **registro** for aberto a partir de um **registro** ou [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)existente, ele será associado automaticamente a esse **registro** ou objeto de **conexão** do objeto **Recordset** .  
  
> [!NOTE]
>  As URLs que usam o esquema http invocarão automaticamente o [provedor do Microsoft OLE DB para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [URLs absolutas e relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Objeto de conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Propriedade ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)

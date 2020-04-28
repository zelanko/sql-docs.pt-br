---
title: Objeto Command (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command
helpviewer_keywords:
- Command object [ADO]
ms.assetid: a02c22fb-542d-465e-a629-30fd59dcbebf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bbce299e2e9f67b705f940480913c7d8ac367d0d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67919792"
---
# <a name="command-object-ado"></a>Objeto Command (ADO)
Define um comando específico que você pretende executar em uma fonte de dados.  
  
## <a name="remarks"></a>Comentários  
 Use um objeto de **comando** para consultar um banco de dados e retornar registros em um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) , para executar uma operação em massa ou para manipular a estrutura de um banco de dados. Dependendo da funcionalidade do provedor, algumas coleções de **comandos** , métodos ou propriedades podem gerar um erro quando são referenciados.  
  
 Com as coleções, métodos e propriedades de um objeto de **comando** , você pode fazer o seguinte:  
  
-   Defina o texto executável do comando (por exemplo, uma instrução SQL) com a propriedade [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) . Como alternativa, para estruturas de comando ou de consulta que não sejam cadeias de caracteres simples (por exemplo, consultas de modelo XML), defina o comando com a propriedade [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) .  
  
-   Opcionalmente, indique o dialeto de comando usado em **CommandText** ou **CommandStream** com a propriedade [Dialect](../../../ado/reference/ado-api/dialect-property.md) .  
  
-   Defina consultas parametrizadas ou argumentos de procedimento armazenado com objetos de [parâmetro](../../../ado/reference/ado-api/parameter-object.md) e a coleção de [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) .  
  
-   Indique se os nomes de parâmetro devem ser passados para o provedor com a propriedade [namedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md) .  
  
-   Execute um comando e retorne um objeto **Recordset** , se apropriado, com o método [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) .  
  
-   Especifique o tipo de comando com a propriedade [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) antes da execução para otimizar o desempenho.  
  
-   Controle se o provedor salva uma versão preparada (ou compilada) do comando antes da execução com a propriedade [preparada](../../../ado/reference/ado-api/prepared-property-ado.md) .  
  
-   Defina o número de segundos que um provedor aguardará até que um comando seja executado com a propriedade [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md) .  
  
-   Associe uma conexão aberta a um objeto de **comando** definindo sua propriedade [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) .  
  
-   Defina a propriedade [Name](../../../ado/reference/ado-api/name-property-ado.md) para identificar o objeto de **comando** como um método no objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) associado.  
  
-   Passe um objeto de **comando** para a propriedade [Source](../../../ado/reference/ado-api/source-property-ado-recordset.md) de um **conjunto de registros** para obter dados.  
  
-   Acesse atributos específicos do provedor com a coleção [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) .  
  
> [!NOTE]
>  Para executar uma consulta sem usar um objeto **Command** , passe uma cadeia de caracteres de consulta para o método [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) de um objeto **Connection** ou para o método [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) de um objeto **Recordset** . No entanto, um objeto de **comando** é necessário quando você deseja manter o texto do comando e executá-lo novamente, ou usar parâmetros de consulta.  
  
 Para criar um objeto de **comando** independentemente de um objeto de **conexão** definido anteriormente, defina sua propriedade **ActiveConnection** como uma cadeia de conexão válida. O ADO ainda cria um objeto de **conexão** , mas não atribui esse objeto a uma variável de objeto. No entanto, se você estiver associando vários objetos de **comando** com a mesma conexão, deverá criar e abrir explicitamente um objeto de **conexão** ; Isso atribui o objeto de **conexão** a uma variável de objeto. Verifique se o objeto de **conexão** foi aberto com êxito antes de atribuí-lo à propriedade **ActiveConnection** do objeto **Command** , pois a atribuição de um objeto de **conexão** fechado causa um erro. Se você não definir a propriedade **ActiveConnection** do objeto de **comando** para essa variável de objeto, o ADO criará um novo objeto de **conexão** para cada objeto de **comando** , mesmo se você usar a mesma cadeia de conexão.  
  
 Para executar um **comando**, chame-o por sua propriedade [Name](../../../ado/reference/ado-api/name-property-ado.md) no objeto de **conexão** associado. O **comando** deve ter sua propriedade **ActiveConnection** definida como o objeto **Connection** . Se o **comando** tiver parâmetros, passe seus valores como argumentos para o método.  
  
 Se dois ou mais objetos de **comando** forem executados na mesma conexão e o objeto de **comando** for um procedimento armazenado com parâmetros de saída, ocorrerá um erro. Para executar cada objeto de **comando** , use conexões separadas ou desconecte todos os outros objetos de **comando** da conexão.  
  
 A coleção **Parameters** é o membro padrão do objeto **Command** . Como resultado, as duas instruções de código a seguir são equivalentes.  
  
```  
objCmd.Parameters.Item(0)  
objCmd(0)  
```  
  
-   O objeto de **comando** não é seguro para scripts.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto Command](../../../ado/reference/ado-api/command-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto de conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Coleção Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)

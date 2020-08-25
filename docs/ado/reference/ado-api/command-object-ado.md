---
description: Objeto Command (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: d876be4883844790815a0640d26cee2933ca17f2
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776155"
---
# <a name="command-object-ado"></a>Objeto Command (ADO)
Define um comando específico que você pretende executar em uma fonte de dados.  
  
## <a name="remarks"></a>Comentários  
 Use um objeto de **comando** para consultar um banco de dados e retornar registros em um objeto [Recordset](./recordset-object-ado.md) , para executar uma operação em massa ou para manipular a estrutura de um banco de dados. Dependendo da funcionalidade do provedor, algumas coleções de **comandos** , métodos ou propriedades podem gerar um erro quando são referenciados.  
  
 Com as coleções, métodos e propriedades de um objeto de **comando** , você pode fazer o seguinte:  
  
-   Defina o texto executável do comando (por exemplo, uma instrução SQL) com a propriedade [CommandText](./commandtext-property-ado.md) . Como alternativa, para estruturas de comando ou de consulta que não sejam cadeias de caracteres simples (por exemplo, consultas de modelo XML), defina o comando com a propriedade [CommandStream](./commandstream-property-ado.md) .  
  
-   Opcionalmente, indique o dialeto de comando usado em **CommandText** ou **CommandStream** com a propriedade [Dialect](./dialect-property.md) .  
  
-   Defina consultas parametrizadas ou argumentos de procedimento armazenado com objetos de [parâmetro](./parameter-object.md) e a coleção de [parâmetros](./parameters-collection-ado.md) .  
  
-   Indique se os nomes de parâmetro devem ser passados para o provedor com a propriedade [namedParameters](./namedparameters-property-ado.md) .  
  
-   Execute um comando e retorne um objeto **Recordset** , se apropriado, com o método [Execute](./execute-method-ado-command.md) .  
  
-   Especifique o tipo de comando com a propriedade [CommandType](./commandtype-property-ado.md) antes da execução para otimizar o desempenho.  
  
-   Controle se o provedor salva uma versão preparada (ou compilada) do comando antes da execução com a propriedade [preparada](./prepared-property-ado.md) .  
  
-   Defina o número de segundos que um provedor aguardará até que um comando seja executado com a propriedade [CommandTimeout](./commandtimeout-property-ado.md) .  
  
-   Associe uma conexão aberta a um objeto de **comando** definindo sua propriedade [ActiveConnection](./activeconnection-property-ado.md) .  
  
-   Defina a propriedade [Name](./name-property-ado.md) para identificar o objeto de **comando** como um método no objeto de [conexão](./connection-object-ado.md) associado.  
  
-   Passe um objeto de **comando** para a propriedade [Source](./source-property-ado-recordset.md) de um **conjunto de registros** para obter dados.  
  
-   Acesse atributos específicos do provedor com a coleção [Properties](./properties-collection-ado.md) .  
  
> [!NOTE]
>  Para executar uma consulta sem usar um objeto **Command** , passe uma cadeia de caracteres de consulta para o método [Execute](./execute-method-ado-connection.md) de um objeto **Connection** ou para o método [Open](./open-method-ado-recordset.md) de um objeto **Recordset** . No entanto, um objeto de **comando** é necessário quando você deseja manter o texto do comando e executá-lo novamente, ou usar parâmetros de consulta.  
  
 Para criar um objeto de **comando** independentemente de um objeto de **conexão** definido anteriormente, defina sua propriedade **ActiveConnection** como uma cadeia de conexão válida. O ADO ainda cria um objeto de **conexão** , mas não atribui esse objeto a uma variável de objeto. No entanto, se você estiver associando vários objetos de **comando** com a mesma conexão, deverá criar e abrir explicitamente um objeto de **conexão** ; Isso atribui o objeto de **conexão** a uma variável de objeto. Verifique se o objeto de **conexão** foi aberto com êxito antes de atribuí-lo à propriedade **ActiveConnection** do objeto **Command** , pois a atribuição de um objeto de **conexão** fechado causa um erro. Se você não definir a propriedade **ActiveConnection** do objeto de **comando** para essa variável de objeto, o ADO criará um novo objeto de **conexão** para cada objeto de **comando** , mesmo se você usar a mesma cadeia de conexão.  
  
 Para executar um **comando**, chame-o por sua propriedade [Name](./name-property-ado.md) no objeto de **conexão** associado. O **comando** deve ter sua propriedade **ActiveConnection** definida como o objeto **Connection** . Se o **comando** tiver parâmetros, passe seus valores como argumentos para o método.  
  
 Se dois ou mais objetos de **comando** forem executados na mesma conexão e o objeto de **comando** for um procedimento armazenado com parâmetros de saída, ocorrerá um erro. Para executar cada objeto de **comando** , use conexões separadas ou desconecte todos os outros objetos de **comando** da conexão.  
  
 A coleção **Parameters** é o membro padrão do objeto **Command** . Como resultado, as duas instruções de código a seguir são equivalentes.  
  
```  
objCmd.Parameters.Item(0)  
objCmd(0)  
```  
  
-   O objeto de **comando** não é seguro para scripts.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto Command](./command-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto de conexão (ADO)](./connection-object-ado.md)   
 [Coleção Parameters (ADO)](./parameters-collection-ado.md)   
 [Coleção Properties (ADO)](./properties-collection-ado.md)   
 [Apêndice A: Provedores](../../guide/appendixes/appendix-a-providers.md)
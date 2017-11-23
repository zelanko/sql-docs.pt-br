---
title: Comando de objeto (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Command
helpviewer_keywords: Command object [ADO]
ms.assetid: a02c22fb-542d-465e-a629-30fd59dcbebf
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2f4aab59ac3a5296d4dcd75927b632f7a6915d46
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="command-object-ado"></a>Objeto de comando (ADO)
Define um comando específico que você pretende executar em relação a uma fonte de dados.  
  
## <a name="remarks"></a>Comentários  
 Use um **comando** objeto para consultar um banco de dados e retornar os registros em um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto, para executar uma operação em massa, ou para manipular a estrutura de um banco de dados. Dependendo da funcionalidade do provedor, alguns **comando** coleções, métodos ou propriedades podem gerar um erro quando eles são referenciados.  
  
 Com as coleções, métodos e propriedades de um **comando** do objeto, você pode fazer o seguinte:  
  
-   Definir o texto do executável do comando (por exemplo, uma instrução SQL) com o [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propriedade. Como alternativa, para o comando ou consulta estruturas que não seja simples cadeias de caracteres (por exemplo, consultas de modelo XML) definem o comando com o [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) propriedade.  
  
-   Opcionalmente, indicar o dialeto do comando usado no **CommandText** ou **CommandStream** com o [dialeto](../../../ado/reference/ado-api/dialect-property.md) propriedade.  
  
-   Definir consultas com parâmetros ou argumentos de procedimento armazenado com [parâmetro](../../../ado/reference/ado-api/parameter-object.md) objetos e o [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção.  
  
-   Indica se os nomes de parâmetros devem ser passados para o provedor com o [NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md) propriedade.  
  
-   Executar um comando e retornar um **registros** objeto de acordo com o [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) método.  
  
-   Especifique o tipo de comando com o [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) propriedade antes da execução para otimizar o desempenho.  
  
-   Controlar se o provedor salva uma versão preparada (ou compilada) do comando antes da execução com o [preparado](../../../ado/reference/ado-api/prepared-property-ado.md) propriedade.  
  
-   Definir o número de segundos que um provedor irá aguardar um comando seja executado com o [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md) propriedade.  
  
-   Associar uma conexão aberta com um **comando** objeto definindo seu [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propriedade.  
  
-   Definir o [nome](../../../ado/reference/ado-api/name-property-ado.md) propriedade para identificar o **comando** objeto como um método em associado [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
-   Passar um **comando** o objeto para o [fonte](../../../ado/reference/ado-api/source-property-ado-recordset.md) propriedade de um **Recordset** para obter dados.  
  
-   Acessar atributos específicos do provedor com o [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção.  
  
> [!NOTE]
>  Para executar uma consulta sem usar um **comando** de objeto, passe uma cadeia de caracteres de consulta para o [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) método de um **Conexão** objeto ou o [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)método de um **registros** objeto. No entanto, um **comando** objeto é necessário quando você deseja manter o texto de comando e execute novamente ou use parâmetros de consulta.  
  
 Para criar um **comando** objeto independentemente definido anteriormente **Conexão** do objeto, defina seu **ActiveConnection** propriedade como uma cadeia de caracteres de conexão válido. ADO ainda cria um **Conexão** objeto, mas ele não atribui esse objeto para uma variável de objeto. No entanto, se você estiver associando várias **comando** objetos com a mesma conexão, você deve criar explicitamente e abrir um **Conexão** objeto; essa atribui a **Conexão** objeto a uma variável de objeto. Certifique-se de que o **Conexão** objeto foi aberto com êxito antes de atribuí-lo para o **ActiveConnection** propriedade o **comando** objeto, pois a atribuição de um fechado **Conexão** objeto causa um erro. Se você não definir a **ActiveConnection** propriedade o **comando** objeto para essa variável de objeto ADO cria um novo **Conexão** objeto para cada  **Comando** do objeto, mesmo se você usa a mesma cadeia de conexão.  
  
 Para executar um **comando**, chamá-lo seu [nome](../../../ado/reference/ado-api/name-property-ado.md) propriedade associado **Conexão** objeto. O **comando** deve ter seu **ActiveConnection** propriedade definida como o **Conexão** objeto. Se o **comando** tem parâmetros, passe os valores como argumentos para o método.  
  
 Se dois ou mais **comando** objetos são executados na mesma conexão e o **comando** objeto é um procedimento armazenado com parâmetros output, ocorrerá um erro. Para executar cada **comando** do objeto, use conexões separadas ou desconecte todos os outros **comando** objetos da conexão.  
  
 O **parâmetros** coleção é o membro padrão da **comando** objeto. Como resultado, as duas instruções de código a seguir são equivalentes.  
  
```  
objCmd.Parameters.Item(0)  
objCmd(0)  
```  
  
-   O **comando** o objeto não é seguro para script.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades do objeto de comando, métodos e eventos](../../../ado/reference/ado-api/command-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Coleção de parâmetros (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Coleção de propriedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)

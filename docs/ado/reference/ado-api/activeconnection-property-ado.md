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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0f423eb2d06ccdc925402d0db5d8a459f7ffdd5d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698923"
---
# <a name="activeconnection-property-ado"></a>Propriedade ActiveConnection (ADO)
Indica para o qual [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) do objeto especificado [comando](../../../ado/reference/ado-api/command-object-ado.md), [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md), ou [registro](../../../ado/reference/ado-api/record-object-ado.md) no momento, o objeto pertence.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **cadeia de caracteres** valor que contém uma definição para uma conexão se a conexão é fechada ou um **Variant** contendo atual **Conexão** objeto se a conexão está aberta. O padrão é uma referência de objeto nulo. Consulte a [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade.  
  
## <a name="remarks"></a>Comentários  
 Use o **ActiveConnection** propriedade para determinar a **Conexão** objeto sobre o qual especificado **comando** objeto executará ou especificado  **Conjunto de registros** será aberta.  
  
## <a name="command"></a>Comando  
 Para **comando** objetos, o **ActiveConnection** propriedade é leitura/gravação.  
  
 Se você tentar chamar o [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) método em um **comando** objeto antes de definir essa propriedade como um aberto **Conexão** objeto ou cadeia de caracteres de conexão válida, ocorrerá um erro.  
  
 Se um **Conexão** objeto é atribuído para o **ActiveConnection** propriedade, o objeto deve ser aberto. Atribuição de um objeto de Conexão fechado causa um erro.  
  
### <a name="note"></a>Observação  
 **Microsoft Visual Basic** configuração o **ActiveConnection** propriedade *nada* desassocia o **comando** objeto atuais **Conexão** e faz com que o provedor liberar quaisquer recursos associados à fonte de dados. Em seguida, você pode associar o **comando** objeto com o mesmo ou outro **Conexão** objeto. Alguns provedores permitem que você altere a configuração da propriedade de um **Conexão** para outra, sem precisar primeiro defina a propriedade como *nada*.  
  
 Se o [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção da **comando** objeto contém os parâmetros fornecidos pelo provedor, a coleção está desmarcada se você definir o **ActiveConnection** propriedade para *nada* ou para outro **Conexão** objeto. Se você criar manualmente [parâmetro](../../../ado/reference/ado-api/parameter-object.md) objetos e usá-los para preencher o **parâmetros** coleção dos **comando** objeto, definindo o **ActiveConnection**  propriedade para *nada* ou em outro **Conexão** objeto deixa o **parâmetros** coleção intacta.  
  
 Fechando a **Conexão** objeto com o qual um **comando** conjuntos associados do objeto é o **ActiveConnection** propriedade *nada*. Definir essa propriedade para um fechado **Conexão** objeto gera um erro.  
  
## <a name="recordset"></a>Conjunto de registros  
 Para abrir **conjunto de registros** objetos ou para **conjunto de registros** objetos cujo [origem](../../../ado/reference/ado-api/source-property-ado-recordset.md) propriedade é definida como válido **comando** objeto, a **ActiveConnection** propriedade é somente leitura. Caso contrário, ele é leitura/gravação.  
  
 Você pode definir essa propriedade platnou **Conexão** objeto ou uma cadeia de caracteres de conexão válida. Nesse caso, o provedor cria uma nova **Conexão** usando esta definição de objeto e abre a conexão. Além disso, o provedor pode definir essa propriedade para o novo **Conexão** objeto para dar a você uma maneira de acessar o **Conexão** para informações sobre erros estendidos ou executar outros comandos do objeto.  
  
 Se você usar o *ActiveConnection* argumento do [abra](../../../ado/reference/ado-api/open-method-ado-recordset.md) método para abrir um **conjunto de registros** objeto, o **ActiveConnection** será de propriedade herde o valor do argumento.  
  
 Se você definir a **fonte** propriedade da **conjunto de registros** objeto a ser válido **comando** variável de objeto, o **ActiveConnection** propriedade de o **conjunto de registros** herda a configuração do **comando** do objeto **ActiveConnection** propriedade.  
  
> [!NOTE]
>  **Uso do serviço de dados remotos** quando usado em um lado do cliente **conjunto de registros** objeto, essa propriedade pode ser definida somente para uma cadeia de caracteres de conexão ou (no Microsoft Visual Basic ou Visual Basic, Scripting Edition) para *nada* .  
  
## <a name="record"></a>Record  
 Essa propriedade é leitura/gravação quando o **registro** objeto está fechado e pode conter uma cadeia de caracteres de conexão ou referência a um aberto **Conexão** objeto. Essa propriedade é somente leitura quando o **registro** objeto está aberto e contém uma referência a um aberto **Conexão** objeto.  
  
 Um **Conexão** objeto é criado implicitamente quando o **registro** objeto está aberto a partir de uma URL. Abra o **registro** com um existente, abra **Conexão** objeto por meio da atribuição a **Conexão** do objeto para essa propriedade, ou usando o **Conexão** objeto como um parâmetro em de [aberto](../../../ado/reference/ado-api/open-method-ado-record.md) chamada de método. Se o **registro** é aberta a partir de um existente **registro** ou [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md), em seguida, ele é automaticamente associado que **registro** ou  **Conjunto de registros** do objeto **Conexão** objeto.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [absoluta e relativa URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se a  
  
||||  
|-|-|-|  
|[Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Consulte também  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Propriedade ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)

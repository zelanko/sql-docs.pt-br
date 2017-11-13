---
title: Propriedade ActiveConnection (ADO) | Microsoft Docs
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
- Command15::ActiveConnection
- Recordset15::get_ActiveConnection
- _Record::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO]
ms.assetid: 52d0a96c-14fb-4ad9-b004-4d821bc0a6db
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 431438fa61750ca2f8eaee3362f94188e5985523
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="activeconnection-property-ado"></a>Propriedade ActiveConnection (ADO)
Indica para qual [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) do objeto especificado [comando](../../../ado/reference/ado-api/command-object-ado.md), [registros](../../../ado/reference/ado-api/recordset-object-ado.md), ou [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto pertence no momento.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **cadeia de caracteres** valor que contém uma definição para uma conexão se a conexão é fechada, ou um **Variant** contendo atual **Conexão** objeto se a conexão está aberta. Padrão é uma referência de objeto nulo. Consulte o [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade.  
  
## <a name="remarks"></a>Comentários  
 Use o **ActiveConnection** propriedade para determinar a **Conexão** objeto sobre o qual especificado **comando** objeto será executado ou especificado  **Conjunto de registros** será aberta.  
  
## <a name="command"></a>Comando  
 Para **comando** objetos, o **ActiveConnection** propriedade é leitura/gravação.  
  
 Se você tentar chamar o [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) método em um **comando** objeto antes de definir essa propriedade como um aberto **Conexão** objeto ou cadeia de caracteres de conexão válido, ocorrerá um erro.  
  
 Se um **Conexão** objeto é atribuído para o **ActiveConnection** propriedade, o objeto deve ser aberto. Atribuição de um objeto de Conexão fechado causa um erro.  
  
### <a name="note"></a>Observação  
 **Microsoft Visual Basic** configuração o **ActiveConnection** propriedade *nada* desassocia o **comando** objeto do atual **Conexão** e faz com que o provedor liberar todos os recursos associados na fonte de dados. Você pode associar o **comando** objeto com o mesmo ou outro **Conexão** objeto. Alguns provedores permitem que você altere a configuração da propriedade de um **Conexão** para outro, sem a necessidade de primeiro definir a propriedade como *nada*.  
  
 Se o [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção do **comando** objeto contém os parâmetros fornecidos pelo provedor, a coleção é desmarcada se você definir o **ActiveConnection** propriedade *nada* ou para outro **Conexão** objeto. Se você criar manualmente [parâmetro](../../../ado/reference/ado-api/parameter-object.md) objetos e usá-los para preencher o **parâmetros** coleção do **comando** objeto, definindo o **ActiveConnection**  propriedade *nada* ou para outro **Conexão** objeto deixa o **parâmetros** coleção intacta.  
  
 Fechando o **Conexão** objeto com o qual um **comando** conjuntos associados do objeto é o **ActiveConnection** propriedade *nada*. A definição dessa propriedade para um fechado **Conexão** objeto gera um erro.  
  
## <a name="recordset"></a>Conjunto de registros  
 Para abrir **registros** objetos ou para **registros** objetos cujo [fonte](../../../ado/reference/ado-api/source-property-ado-recordset.md) está definida como uma opção válida **comando** objeto, o **ActiveConnection** propriedade é somente leitura. Caso contrário, ele é leitura/gravação.  
  
 Você pode definir essa propriedade para um válida **Conexão** objeto ou uma cadeia de caracteres de conexão válido. Nesse caso, o provedor cria um novo **Conexão** usando esta definição de objeto e abre a conexão. Além disso, o provedor pode definir essa propriedade para o novo **Conexão** objeto para dar a você uma maneira de acessar o **Conexão** para obter informações de erro estendidas ou executar outros comandos do objeto.  
  
 Se você usar o *ActiveConnection* argumento do [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) método para abrir um **registros** objeto, o **ActiveConnection** será de propriedade herde o valor do argumento.  
  
 Se você definir o **fonte** propriedade do **registros** objeto válido **comando** variável de objeto, o **ActiveConnection** propriedade de o **registros** herda a configuração do **comando** do objeto **ActiveConnection** propriedade.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** quando usado em um cliente **registros** objeto, essa propriedade pode ser definida somente como uma cadeia de caracteres de conexão ou (no Microsoft Visual Basic ou Visual Basic, Scripting Edition) para *nada* .  
  
## <a name="record"></a>Record  
 Esta propriedade é leitura/gravação quando o **registro** objeto é fechado e pode conter uma cadeia de caracteres de conexão ou referência a um aberto **Conexão** objeto. Essa propriedade é somente leitura quando o **registro** objeto está aberto e contém uma referência a um aberto **Conexão** objeto.  
  
 Um **Conexão** objeto é criado implicitamente quando o **registro** objeto é aberto em uma URL. Abra o **registro** com um existente, abra **Conexão** objeto atribuindo o **Conexão** de objeto para essa propriedade, ou usando o **Conexão** objeto como um parâmetro no [abrir](../../../ado/reference/ado-api/open-method-ado-record.md) chamada de método. Se o **registro** é aberto a partir de um existente **registro** ou [registros](../../../ado/reference/ado-api/recordset-object-ado.md), e em seguida, ele será automaticamente associado que **registro** ou  **Conjunto de registros** do objeto **Conexão** objeto.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [Absolute e URLs relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se a  
  
||||  
|-|-|-|  
|[Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Consulte também  
 [ActiveConnection CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Propriedade ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)


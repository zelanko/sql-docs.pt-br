---
title: Método Append (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _DynaCollection::Append
helpviewer_keywords:
- Append method [ADO]
ms.assetid: f8a9bbed-ba9c-4698-945d-317ad22d2e92
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 17fa0ff30e8dcdbf7ea67080f17c3e066bba8605
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67920669"
---
# <a name="append-method-ado"></a>Método Append (ADO)
Anexa um objeto a uma coleção. Se a coleção for de [campos](../../../ado/reference/ado-api/fields-collection-ado.md), um novo objeto de [campo](../../../ado/reference/ado-api/field-object.md) poderá ser criado antes de ser anexado à coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
collection.Append object  
fields.Append Name, Type, DefinedSize, Attrib, FieldValue  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Cole*  
 Um objeto de coleção.  
  
 *campos*  
 Uma coleção de **campos** .  
  
 *objeto*  
 Uma variável de objeto que representa o objeto a ser anexado.  
  
 *Nome*  
 Um valor de **cadeia de caracteres** que contém o nome do novo objeto de **campo** e não deve ter o mesmo nome de qualquer outro objeto em *campos*.  
  
 *Tipo*  
 Um valor de [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) , cujo valor padrão é **adEmpty**, que especifica o tipo de dados do novo campo. Os seguintes tipos de dados não são suportados pelo ADO e não devem ser usados ao acrescentar novos campos a um [objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md): **adIDispatch**, **adIUnknown**, **adVariant**.  
  
 *DefinedSize*  
 Opcional. Um valor **longo** que representa o tamanho definido, em caracteres ou bytes, do novo campo. O valor padrão para esse parâmetro é derivado do *tipo*. Os campos que têm um *DefinedSize* maior que 255 bytes são tratados como colunas de comprimento variável. O padrão para *DefinedSize* não é especificado.  
  
 *Atributos*  
 Opcional. Um valor de [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md) , cujo valor padrão é **adFldDefault**, que especifica atributos para o novo campo. Se esse valor não for especificado, o campo conterá atributos derivados do *tipo*.  
  
 *FieldValue*  
 Opcional. Uma **variante** que representa o valor do novo campo. Se não for especificado, o campo será anexado com um valor nulo.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="parameters-collection"></a>Coleção Parâmetros  
 Você deve definir a propriedade [Type](../../../ado/reference/ado-api/type-property-ado.md) de um objeto de [parâmetro](../../../ado/reference/ado-api/parameter-object.md) antes de acrescentá-lo à coleção de [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) . Se você selecionar um tipo de dados de comprimento variável, também deverá definir a propriedade [tamanho](../../../ado/reference/ado-api/size-property-ado-parameter.md) como um valor maior que zero.  
  
 Descrever os parâmetros você mesmo minimiza as chamadas para o provedor e, portanto, melhora o desempenho ao usar procedimentos armazenados ou consultas parametrizadas. No entanto, você deve saber as propriedades dos parâmetros associados ao procedimento armazenado ou à consulta parametrizada que você deseja chamar.  
  
 Use o método [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) para criar objetos de **parâmetro** com as configurações de propriedade apropriadas e use o método **Append** para adicioná-los à coleção de [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) . Isso permite que você defina e retorne valores de parâmetro sem precisar chamar o provedor para as informações de parâmetro. Se você estiver gravando em um provedor que não fornece informações de parâmetro, deverá usar esse método para preencher manualmente a coleção de **parâmetros** a fim de usar parâmetros.  
  
## <a name="fields-collection"></a>Coleção Campos  
 O parâmetro *FieldValue* só é válido ao adicionar um objeto de **campo** a um objeto de [registro](../../../ado/reference/ado-api/record-object-ado.md) , não a um objeto **Recordset** . Com um objeto **Record** , você pode acrescentar campos e fornecer valores ao mesmo tempo. Com um objeto **Recordset** , você deve criar campos enquanto o **conjunto de registros** é fechado e, em seguida, abrir o **conjunto de registros** e atribuir valores aos campos.  
  
> [!NOTE]
>  Para novos objetos de **campo** que foram acrescentados à coleção **Fields** de um objeto **Record** , a propriedade [Value](../../../ado/reference/ado-api/value-property-ado.md) deve ser definida antes que qualquer outra propriedade **Field** possa ser especificada. Primeiro, um valor específico para a propriedade **Value** deve ter sido atribuído e [atualizado](../../../ado/reference/ado-api/update-method.md) na coleção **Fields** chamada. Em seguida, outras propriedades, como [tipo](../../../ado/reference/ado-api/type-property-ado.md) ou [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) , podem ser acessadas. Objetos de **campo** dos seguintes tipos de dados **(DataTypeEnum**) não podem ser acrescentados à coleção **Fields** e causarão um erro: **adArray**, **adChapter**, **adEmpty**, **adPropVariant**e **adUserDefined**. Além disso, os seguintes tipos de dados não são suportados pelo ADO: **adIDispatch**, **adIUnknown**e **adIVariant**. Para esses tipos, nenhum erro ocorrerá quando acrescentado, mas o uso poderá produzir resultados imprevisíveis, incluindo vazamentos de memória.  
  
## <a name="recordset"></a>Conjunto de registros  
 Se você não definir a propriedade [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) antes de chamar o método **Append** , **CursorLocation** será definido como **adUseClient** (um valor [CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md) ) automaticamente quando o método [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) do objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) for chamado.  
  
 Ocorrerá um erro em tempo de execução se o método **Append** for chamado na coleção **Fields** de um **conjunto de registros**aberto ou em um conjunto de **registros** em que a propriedade [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) foi definida. Você só pode acrescentar campos a um **conjunto de registros** que não esteja aberto e ainda não tenha sido conectado a uma fonte de dados. Normalmente, esse é o caso quando um objeto **Recordset** é criei com o método [createrecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md) ou atribuído a uma variável de objeto.  
  
## <a name="record"></a>Record  
 Um erro de tempo de execução não ocorrerá se o método **Append** for chamado na coleção **Fields** de um **registro**aberto. O novo campo será adicionado à coleção **Fields** do objeto **Record** . Se o **registro** tiver sido derivado de um **conjunto de registros**, o novo campo não será exibido na coleção **Fields** do objeto **Recordset** .  
  
 Um campo inexistente pode ser criado e acrescentado à coleção **Fields** , atribuindo um valor ao objeto Field como se ele já existisse na coleção. A atribuição irá disparar a criação automática e o acréscimo do objeto **Field** e, em seguida, a atribuição será concluída.  
  
 Depois de acrescentar um **campo** à coleção **Fields** de um objeto **Record** , chame o método **Update** da coleção **Fields** para salvar a alteração.  
  
## <a name="applies-to"></a>Aplica-se A  
  
- [Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
- [Coleção Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos Append e CreateParameter (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Exemplo dos métodos Append e CreateParameter (VC + +)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [Método CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Método Delete (coleção de campos ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Método Delete (coleção de parâmetros ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Método Delete (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Método Update](../../../ado/reference/ado-api/update-method.md)

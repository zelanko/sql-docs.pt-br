---
title: Método append (ADO) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 5e03e29d5c9696efb55ef5ce6ec47fcf28fc0467
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47712365"
---
# <a name="append-method-ado"></a>Método Append (ADO)
Acrescenta um objeto a uma coleção. Se a coleção estiver [campos](../../../ado/reference/ado-api/fields-collection-ado.md), uma nova [campo](../../../ado/reference/ado-api/field-object.md) objeto pode ser criado antes que ele é acrescentado à coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
collection.Append object  
fields.Append Name, Type, DefinedSize, Attrib, FieldValue  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *coleção*  
 Um objeto de coleção.  
  
 *fields*  
 Um **campos** coleção.  
  
 *object*  
 Uma variável de objeto que representa o objeto a ser acrescentado.  
  
 *Nome*  
 Um **cadeia de caracteres** valor que contém o nome do novo **campo** do objeto e não deve ser o mesmo nome como qualquer outro objeto no *campos*.  
  
 *Tipo*  
 Um [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) valor, cujo valor padrão é **adEmpty**, que especifica o tipo de dados do novo campo. Não há suporte para os seguintes tipos de dados, ADO e deve não ser usado quando acrescentar novos campos para um [objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md): **adIDispatch**, **adIUnknown**, **adVariant**.  
  
 *DefinedSize*  
 Opcional. Um **longo** valor que representa o tamanho definido, em caracteres ou bytes, do novo campo. O valor padrão para esse parâmetro é derivado de *tipo*. Os campos que têm uma *DefinedSize* maiores que 255 bytes são tratadas como colunas de comprimento variável. O padrão para *DefinedSize* não está especificado.  
  
 *Attrib*  
 Opcional. Um [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md) valor, cujo valor padrão é **adFldDefault**, que especifica os atributos para o novo campo. Se esse valor não for especificado, o campo conterá atributos derivados de *tipo*.  
  
 *FieldValue*  
 Opcional. Um **Variant** que representa o valor para o novo campo. Se não for especificado, o campo é acrescentado com um valor nulo.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="parameters-collection"></a>Coleção Parâmetros  
 Você deve definir a [tipo](../../../ado/reference/ado-api/type-property-ado.md) propriedade de uma [parâmetro](../../../ado/reference/ado-api/parameter-object.md) objeto antes de acrescentá-lo para o [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção. Se você selecionar um tipo de dados de comprimento variável, você também deve definir a [tamanho](../../../ado/reference/ado-api/size-property-ado-parameter.md) propriedade para um valor maior que zero.  
  
 Descrevendo parâmetros por conta própria minimiza as chamadas para o provedor e, portanto, melhora o desempenho ao usar procedimentos armazenados ou consultas parametrizadas. No entanto, você deve saber as propriedades dos parâmetros associados com o procedimento armazenado ou parametrizado da consulta que você deseja chamar.  
  
 Usar o [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) método para criar **parâmetro** objetos com as configurações de propriedade apropriada e o uso de **Append** método para adicioná-los para o [ Parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção. Isso lhe permite definir e retornar valores de parâmetro sem a necessidade de chamar o provedor para obter as informações de parâmetro. Se você estiver escrevendo um provedor que não fornece informações de parâmetro, você deve usar esse método para preencher manualmente a **parâmetros** coleção para usar parâmetros em todos os.  
  
## <a name="fields-collection"></a>Coleção Campos  
 O *FieldValue* parâmetro só é válido ao adicionar um **campo** do objeto para um [registro](../../../ado/reference/ado-api/record-object-ado.md) do objeto, não para um **Recordset** objeto. Com uma **registro** do objeto, você pode acrescentar campos e fornecer valores ao mesmo tempo. Com uma **conjunto de registros** do objeto, você deve criar campos durante a **conjunto de registros** é fechado e, em seguida, abra o **conjunto de registros** e atribuir valores aos campos.  
  
> [!NOTE]
>  Para o novo **campo** objetos que foram acrescentados para o **campos** coleção de um **registro** objeto, o [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade deve ser definida antes de qualquer outro **campo** propriedades podem ser especificadas. Primeiro, um valor específico para o **valor** propriedade deverá ser atribuída e [atualização](../../../ado/reference/ado-api/update-method.md) sobre o **campos** coleção chamada. Em seguida, outras propriedades, como [tipo](../../../ado/reference/ado-api/type-property-ado.md) ou [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) pode ser acessado. **Campo** objetos dos seguintes tipos de dados (**DataTypeEnum**) não pode ser anexada à **campos** coleção e causará um erro ocorra: **adArray**, **adChapter**, **adEmpty**, **adPropVariant**, e **adUserDefined**. Além disso, os seguintes tipos de dados não têm suporte pelo ADO: **adIDispatch**, **adIUnknown**, e **adIVariant**. Para esses tipos, nenhum erro ocorrerá quando for anexado, mas uso pode produzir resultados imprevisíveis, incluindo vazamentos de memória.  
  
## <a name="recordset"></a>Conjunto de registros  
 Se você não definir a [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade antes de chamar o **Append** método **CursorLocation** será definido como **adUseClient** ( uma [CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md) valor) automaticamente quando o [abra](../../../ado/reference/ado-api/open-method-ado-recordset.md) método da [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto é chamado.  
  
 Um erro de tempo de execução ocorrerá se o **Append** método é chamado na **campos** coleção de um aberto **conjunto de registros**, ou em um **Recordset** em que o [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propriedade foi definida. Você apenas pode acrescentar campos para um **Recordset** que não está aberto e ainda não foi conectado a uma fonte de dados. Normalmente, esse é o caso quando um **conjunto de registros** objeto é gerado com o [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md) método ou atribuídos a uma variável de objeto.  
  
## <a name="record"></a>Record  
 Um erro de tempo de execução não ocorrerá se o **Append** método é chamado na **campos** coleção de um aberto **registro**. O novo campo será adicionado para o **campos** coleção da **registro** objeto. Se o **registro** foi derivado de uma **conjunto de registros**, o novo campo não aparecerá na **campos** coleção do **Recordset** objeto.  
  
 Um campo inexistente pode ser criado e anexado à **campos** coleção atribuindo um valor para o objeto de campo, como se ela já existia na coleção. A atribuição irá disparar a criação automática e o acréscimo do **campo** objeto e, em seguida, a atribuição serão concluída.  
  
 Após a anexação de um **campo** para o **campos** coleção de um **registro** do objeto, chame o **atualização** método do **campos**  coleção para salvar a alteração.  
  
## <a name="applies-to"></a>Aplica-se a  
  
- [Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
- [Coleção Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Acrescente e exemplo dos métodos CreateParameter (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Append e CreateParameter métodos (VC + +)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [Método CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Método Delete (coleção de campos ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Excluir método (coleção de parâmetros ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Excluir método (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Método Update](../../../ado/reference/ado-api/update-method.md)

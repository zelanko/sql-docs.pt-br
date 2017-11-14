---
title: "Método (ADO) append | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _DynaCollection::Append
helpviewer_keywords:
- Append method [ADO]
ms.assetid: f8a9bbed-ba9c-4698-945d-317ad22d2e92
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: db5dc5c8b6d40873ce333aa2987d04c046c222b1
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="append-method-ado"></a>(ADO) do método append
Anexa um objeto para uma coleção. Se a coleção é [campos](../../../ado/reference/ado-api/fields-collection-ado.md), um novo [campo](../../../ado/reference/ado-api/field-object.md) objeto pode ser criado antes que ele é adicionado à coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
collection.Append object  
fields.Append Name, Type, DefinedSize, Attrib, FieldValue  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *coleção*  
 Um objeto de coleção.  
  
 *campos*  
 Um **campos** coleção.  
  
 *objeto*  
 Uma variável de objeto que representa o objeto a ser anexado.  
  
 *Nome*  
 Um **cadeia de caracteres** valor que contém o nome do novo **campo** do objeto e não deve ser o mesmo nome como qualquer outro objeto no *campos*.  
  
 *Tipo*  
 Um [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) valor, cujo valor padrão é **adEmpty**, que especifica o tipo de dados do novo campo. Os seguintes tipos de dados não são suportados pelo ADO e deve não ser usado quando anexar novos campos para um [Recordset Object (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md): **adIDispatch**, **adIUnknown**, **adVariant**.  
  
 *DefinedSize*  
 Opcional. Um **longo** valor que representa o tamanho definido, em caracteres ou bytes, do novo campo. O valor padrão para esse parâmetro é derivado do *tipo*. Os campos que têm um *DefinedSize* maiores que 255 bytes são tratadas como colunas de comprimento variável. O padrão para *DefinedSize* não está especificado.  
  
 *Attrib*  
 Opcional. Um [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md) valor, cujo valor padrão é **adFldDefault**, que especifica os atributos para o novo campo. Se esse valor não for especificado, o campo irá conter atributos derivados de *tipo*.  
  
 *FieldValue*  
 Opcional. Um **Variant** que representa o valor para o novo campo. Se não for especificado, o campo é acrescentado com um valor nulo.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="parameters-collection"></a>Coleção Parâmetros  
 Você deve definir o [tipo](../../../ado/reference/ado-api/type-property-ado.md) propriedade de um [parâmetro](../../../ado/reference/ado-api/parameter-object.md) objeto antes de acrescentá-lo para o [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção. Se você selecionar um tipo de dados de comprimento variável, você também deve definir o [tamanho](../../../ado/reference/ado-api/size-property-ado-parameter.md) propriedade para um valor maior que zero.  
  
 Descrever os parâmetros por conta própria minimiza as chamadas ao provedor e, portanto, melhora o desempenho quando você usar procedimentos armazenados ou consultas parametrizadas. No entanto, você deve saber as propriedades dos parâmetros associados com o procedimento armazenado ou consulta que você deseja chamar parametrizada.  
  
 Use o [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) método para criar **parâmetro** objetos com as configurações de propriedade apropriado e use o **Append** método para adicioná-los para o [ Parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção. Isso permite definir e retornar valores de parâmetro sem a necessidade de chamar o provedor para obter as informações de parâmetro. Se você estiver escrevendo um provedor que não fornece informações de parâmetro, você deve usar esse método para popular manualmente o **parâmetros** coleção para usar parâmetros.  
  
## <a name="fields-collection"></a>Coleção Campos  
 O *FieldValue* parâmetro só é válido ao adicionar um **campo** do objeto para um [registro](../../../ado/reference/ado-api/record-object-ado.md) do objeto, não para um **Recordset** objeto. Com um **registro** do objeto, você pode acrescentar campos e fornecer valores ao mesmo tempo. Com um **Recordset** do objeto, você deve criar campos ao **registros** está fechado e, em seguida, abra o **Recordset** e atribuir valores para os campos.  
  
> [!NOTE]
>  Para o novo **campo** objetos que foram acrescentados ao **campos** coleção de um **registro** objeto, o [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade deve ser definida antes de qualquer outro **campo** propriedades podem ser especificadas. Primeiro, um valor específico para o **valor** propriedade deve ser atribuída e [atualização](../../../ado/reference/ado-api/update-method.md) no **campos** coleção chamada. Em seguida, outras propriedades, como [tipo](../../../ado/reference/ado-api/type-property-ado.md) ou [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) pode ser acessado. **Campo** objetos dos seguintes tipos de dados (**DataTypeEnum**) não é possível anexar o **campos** coleção e causará um erro ocorra: **adArray**, **adChapter**, **adEmpty**, **adPropVariant**, e **adUserDefined**. Além disso, os seguintes tipos de dados não têm suporte pelo ADO: **adIDispatch**, **adIUnknown**, e **adIVariant**. Para esses tipos, nenhum erro ocorrerá quando anexado, mas uso pode produzir resultados imprevisíveis, incluindo vazamentos de memória.  
  
## <a name="recordset"></a>Conjunto de registros  
 Se você não definir a [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade antes de chamar o **Append** método **CursorLocation** será definida como **adUseClient** ( um [CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md) valor) automaticamente quando o [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) método o [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto é chamado.  
  
 Ocorrerá um erro de tempo de execução se o **acrescentar** método é chamado no **campos** coleção de um aberto **registros**, ou em um **Recordset** onde o [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propriedade foi definida. Você só pode incluir campos para um **registros** que não está aberto e ainda não foi conectado a uma fonte de dados. Normalmente, esse é o caso quando um **registros** objeto é gerado com o [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md) método ou atribuído a uma variável de objeto.  
  
## <a name="record"></a>Record  
 Um erro de tempo de execução não ocorrerá se o **Append** método é chamado no **campos** coleção de um aberto **registro**. O novo campo será adicionado para o **campos** coleção do **registro** objeto. Se o **registro** foi derivada de um **registros**, o novo campo não serão exibidos no **campos** coleção do **Recordset** objeto.  
  
 Um campo existente não pode ser criado e anexado ao **campos** coleção atribuindo um valor para o objeto de campo como se ele já existe na coleção. A atribuição irá disparar a criação automática e anexando do **campo** objeto e, em seguida, a atribuição serão concluída.  
  
 Depois de anexar um **campo** para o **campos** coleção de um **registro** de objeto, chame o **atualização** método do **campos**  coleção para salvar a alteração.  
  
## <a name="applies-to"></a>Aplica-se a  
  
- [Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
- [Coleção Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Anexar e exemplo dos métodos CreateParameter (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Anexar e exemplo dos métodos CreateParameter (VC + +)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [Método CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Método Delete (coleção de campos do ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Excluir método (coleção de parâmetros do ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Excluir método (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Método Update](../../../ado/reference/ado-api/update-method.md)


---
title: "Método AddNew (ADO) | Microsoft Docs"
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
- Recordset15::AddNew
- Recordset15::raw_AddNew
helpviewer_keywords:
- AddNew method [ADO]
ms.assetid: a9f54be9-5763-45d0-a6eb-09981b03bc08
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b804e2c2ea92a2f1f10caf98a556de3ff1a8fca4
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="addnew-method-ado"></a>Método AddNew (ADO)
Cria um novo registro para um atualizável [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.AddNew FieldList, Values  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *conjunto de registros*  
 Um **registros** objeto.  
  
 *FieldList*  
 Opcional. Um nome único ou uma matriz de nomes ou posições ordinais dos campos no novo registro.  
  
 *Valores*  
 Opcional. Um único valor ou uma matriz de valores para os campos no novo registro. Se *Fieldlist* é uma matriz, *valores* também deve ser uma matriz com o mesmo número de membros; caso contrário, ocorrerá um erro. A ordem dos nomes de campo deve corresponder à ordem dos valores de campo em cada matriz.  
  
## <a name="remarks"></a>Comentários  
 Use o **AddNew** método para criar e inicializar um novo registro. Use o [dá suporte a](../../../ado/reference/ado-api/supports-method.md) método com **adAddNew** (uma [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md) valor) para verificar se você pode adicionar registros a atual **registros**objeto.  
  
 Depois de chamar o **AddNew** método, o novo registro se tornará o registro atual e permanece atual depois de chamar o [atualização](../../../ado/reference/ado-api/update-method.md) método. Desde que o novo registro é anexado ao **registros**, uma chamada para **MoveNext** após a atualização moverá após o término do **registros**, tornando **EOF ** True. Se o **registros** objeto não oferece suporte a indicadores, você não poderá acessar o novo registro depois que você vai para outro registro. Dependendo de seu tipo de cursor, talvez seja necessário chamar o [Requery](../../../ado/reference/ado-api/requery-method.md) método para disponibilizar o novo registro.  
  
 Se você chamar **AddNew** ao editar o registro atual ou ao adicionar um novo registro, o ADO chama o **atualização** método para salvar quaisquer alterações e, em seguida, cria o novo registro.  
  
 O comportamento do **AddNew** método depende do modo de atualização do **Recordset** objeto e se você passa o *Fieldlist* e *valores*argumentos.  
  
 Em *modo de atualização imediata* (no qual o provedor grava as alterações à fonte de dados subjacente quando você chamar o **atualizar** método), chamar o **AddNew** método sem conjuntos de argumentos de [EditMode](../../../ado/reference/ado-api/editmode-property.md) propriedade **adEditAdd** (uma [EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md) valor). O provedor armazena em cache localmente as alterações de valor de campo. Chamando o **atualização** método posta o novo registro no banco de dados e redefine o **EditMode** propriedade **adEditNone** (uma **EditModeEnum**valor). Se você passar o *Fieldlist* e *valores* argumentos, o ADO envia imediatamente o novo registro no banco de dados (sem **atualização** chamada é necessária); o **EditMode ** não altera o valor da propriedade (**adEditNone**).  
  
 Em *o modo de atualização em lotes* (no qual o provedor armazena em cache várias alterações e grava a fonte de dados somente quando você chamar o [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método), chamar o **AddNew** método sem conjuntos de argumentos de **EditMode** propriedade **adEditAdd**. O provedor armazena em cache localmente as alterações de valor de campo. Chamando o **atualização** método adiciona o novo registro para o atual **registros**, mas o provedor não postar as alterações no banco de dados subjacente ou redefinir o **EditMode** para **adEditNone**, até que você chame o **UpdateBatch** método. Se você passar o *lista de campos* e *valores* argumentos, ADO envia o novo registro para o provedor de armazenamento em um cache e configura o **EditMode** para **adEditAdd **; você precisa chamar o **UpdateBatch** método para lançar o novo registro no banco de dados subjacente.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como usar o método AddNew com a lista de campos e a lista de valores incluídos para ver como incluir a lista de campos e a lista de valores como matrizes.  
  
```  
create table aa1 (intf int, charf char(10))  
insert into aa1 values (2, 'aa')  
  
Dim cn As New adodb.Connection  
Dim rs As New adodb.Recordset  
Dim cmd As New adodb.Command  
  
cn.ConnectionString = "Provider=SQLOLEDB;Data Source=alexverb2;uid=sa;pwd=foo$bar00;"  
  
cn.Open  
rs.Open "select * from xxx..aa1", cn, adOpenKeyset, adLockOptimistic  
  
Dim fieldsArray(1) As Variant  
fieldsArray(0) = "intf"  
fieldsArray(1) = "charf"  
Dim values(1) As Variant  
values(0) = 4  
values(1) = "as"  
rs.AddNew fieldsArray, values  
rs.Update  
```  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método AddNew (VB)](../../../ado/reference/ado-api/addnew-method-example-vb.md)   
 [Exemplo do método AddNew (VBScript)](../../../ado/reference/ado-api/addnew-method-example-vbscript.md)   
 [Exemplo do método AddNew (VC + +)](../../../ado/reference/ado-api/addnew-method-example-vc.md)   
 [Método CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Propriedade EditMode](../../../ado/reference/ado-api/editmode-property.md)   
 [Método Requery](../../../ado/reference/ado-api/requery-method.md)   
 [Oferece suporte ao método](../../../ado/reference/ado-api/supports-method.md)   
 [Método Update](../../../ado/reference/ado-api/update-method.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)


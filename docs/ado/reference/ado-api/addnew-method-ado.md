---
title: Método AddNew (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AddNew
- Recordset15::raw_AddNew
helpviewer_keywords:
- AddNew method [ADO]
ms.assetid: a9f54be9-5763-45d0-a6eb-09981b03bc08
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 911509c62c5ae93bc73ca94469ac776195d2a8b1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63065255"
---
# <a name="addnew-method-ado"></a>Método AddNew (ADO)
Cria um novo registro para um atualizável [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.AddNew FieldList, Values  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *recordset*  
 Um **Recordset** objeto.  
  
 *FieldList*  
 Opcional. Um único nome ou uma matriz de nomes ou as posições ordinais dos campos no novo registro.  
  
 *Valores*  
 Opcional. Um único valor ou uma matriz de valores para os campos no novo registro. Se *Fieldlist* é uma matriz *valores* também deve ser uma matriz com o mesmo número de membros; caso contrário, ocorrerá um erro. A ordem dos nomes de campo deve corresponder à ordem dos valores de campo em cada matriz.  
  
## <a name="remarks"></a>Comentários  
 Use o **AddNew** método para criar e inicializar um novo registro. Use o [dá suporte a](../../../ado/reference/ado-api/supports-method.md) método com **adAddNew** (uma [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md) valor) para verificar se você pode adicionar registros a atual **Recordset**objeto.  
  
 Depois de chamar o **AddNew** método, o novo registro se tornará o registro atual e permanece atual depois de chamar o [atualização](../../../ado/reference/ado-api/update-method.md) método. Uma vez que o novo registro é acrescentado à **conjunto de registros**, uma chamada para **MoveNext** após a atualização moverá após o final do **conjunto de registros**, tornando **EOF**  True. Se o **Recordset** objeto não oferece suporte a indicadores, você não consiga acessar o novo registro, quando você move para outro registro. Dependendo do seu tipo de cursor, você precisa chamar o [Requery](../../../ado/reference/ado-api/requery-method.md) método para disponibilizar o novo registro.  
  
 Se você chamar **AddNew** durante a edição do registro atual ou ao adicionar um novo registro, o ADO chama o **atualização** método para salvar qualquer altera e, em seguida, cria o novo registro.  
  
 O comportamento do **AddNew** método depende do modo de atualização a **conjunto de registros** objeto e se você passa o *Fieldlist* e *valores*argumentos.  
  
 Na *modo de atualização imediata* (no qual o provedor grava as alterações à fonte de dados subjacente depois de chamar o **atualizar** método), chamar o **AddNew** método sem conjuntos de argumentos de [EditMode](../../../ado/reference/ado-api/editmode-property.md) propriedade **adEditAdd** (um [EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md) valor). O provedor armazena em cache localmente as alterações de valor de campo. Chamar o **atualização** método posta o novo registro ao banco de dados e redefine o **EditMode** propriedade a ser **adEditNone** (um **EditModeEnum**valor). Se você passar o *Fieldlist* e *valores* argumentos, o ADO posta imediatamente o novo registro ao banco de dados (sem **atualização** chamada é necessária); o **EditMode**  não altera o valor da propriedade (**adEditNone**).  
  
 Na *modo de atualização em lotes* (em que o provedor armazena em cache várias alterações e os grava em fonte de dados subjacente somente quando você chama o [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método), chamar o **AddNew** método sem argumentos define o **EditMode** propriedade **adEditAdd**. O provedor armazena em cache localmente as alterações de valor de campo. Chamar o **atualização** método adiciona o novo registro atual **conjunto de registros**, mas o provedor não postam as alterações no banco de dados subjacente, ou redefina o **EditMode** para **adEditNone**, até que você chame a **UpdateBatch** método. Se você passar o *Fieldlist* e *valores* argumentos, ADO envia o novo registro para o provedor para o armazenamento em um cache e configura o **EditMode** para **adEditAdd** ; você precisa chamar o **UpdateBatch** método para lançar o novo registro ao banco de dados subjacente.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como usar o método AddNew com a lista de campos e a lista de valores incluídos para ver como incluir a lista de campos e uma lista de valores como matrizes.  
  
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
 [Dá suporte ao método](../../../ado/reference/ado-api/supports-method.md)   
 [Método de atualização](../../../ado/reference/ado-api/update-method.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)

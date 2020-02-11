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
ms.openlocfilehash: a2f9efa8f5042fab603c794edada5aacab001936
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67921321"
---
# <a name="addnew-method-ado"></a>Método AddNew (ADO)
Cria um novo registro para um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) atualizável.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.AddNew FieldList, Values  
```  
  
#### <a name="parameters"></a>parâmetros  
 *registros*  
 Um objeto **Recordset** .  
  
 *FieldList*  
 Opcional. Um único nome ou uma matriz de nomes ou posições ordinais dos campos no novo registro.  
  
 *Valores*  
 Opcional. Um único valor ou uma matriz de valores para os campos no novo registro. Se *FieldList* for uma matriz, *os valores* também deverão ser uma matriz com o mesmo número de membros; caso contrário, ocorrerá um erro. A ordem dos nomes de campo deve corresponder à ordem dos valores de campo em cada matriz.  
  
## <a name="remarks"></a>Comentários  
 Use o método **AddNew** para criar e inicializar um novo registro. Use o método de [suporte](../../../ado/reference/ado-api/supports-method.md) com **adAddNew** (um valor de [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md) ) para verificar se você pode adicionar registros ao objeto **Recordset** atual.  
  
 Depois que você chamar o método **AddNew** , o novo registro se tornará o registro atual e permanecerá atualizado depois que você chamar o método [Update](../../../ado/reference/ado-api/update-method.md) . Como o novo registro é acrescentado ao conjunto de **registros**, uma chamada para **MoveNext** após a atualização será movida após o final do **conjunto de registros**, tornando o **EOF** true. Se o objeto **Recordset** não oferecer suporte a indicadores, talvez você não consiga acessar o novo registro depois de mover para outro registro. Dependendo do tipo de cursor, talvez seja necessário chamar o método [Requery](../../../ado/reference/ado-api/requery-method.md) para tornar o novo registro acessível.  
  
 Se você chamar **AddNew** ao editar o registro atual ou ao adicionar um novo registro, o ADO chamará o método **Update** para salvar as alterações e, em seguida, criará o novo registro.  
  
 O comportamento do método **AddNew** depende do modo de atualização do objeto **Recordset** e se você passa os argumentos *FieldList* e *Values* .  
  
 No *modo de atualização imediata* (no qual o provedor grava as alterações na fonte de dados subjacente depois que você chama o método **Update** ), chamar o método **AddNew** sem argumentos define a propriedade [EditMode](../../../ado/reference/ado-api/editmode-property.md) como **adEditAdd** (um valor [EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md) ). O provedor armazena em cache qualquer valor de campo alterado localmente. Chamar o método **Update** posta o novo registro no banco de dados e redefine a propriedade **EditMode** como **adEditNone** (um valor **EditModeEnum** ). Se você passar os argumentos *FieldList* e *Values* , o ADO imediatamente posta o novo registro no banco de dados (nenhuma chamada de **atualização** é necessária); o valor da propriedade **EditMode** não é alterado (**adEditNone**).  
  
 No *modo de atualização em lotes* (no qual o provedor armazena em cache várias alterações e as grava na fonte de dados subjacente somente quando você chama o método [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) ), chamar o método **AddNew** sem argumentos define a propriedade **EditMode** como **adEditAdd**. O provedor armazena em cache qualquer valor de campo alterado localmente. Chamar o método **Update** adiciona o novo registro ao conjunto de **registros**atual, mas o provedor não publica as alterações no banco de dados subjacente ou redefine o **EditMode** para **adEditNone**, até que você chame o método **UpdateBatch** . Se você passar os argumentos *FieldList* e *Values* , o ADO enviará o novo registro ao provedor para armazenamento em um cache e definirá o **EditMode** como **adEditAdd**; Você precisa chamar o método **UpdateBatch** para postar o novo registro no banco de dados subjacente.  
  
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
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método AddNew (VB)](../../../ado/reference/ado-api/addnew-method-example-vb.md)   
 [Exemplo do método AddNew (VBScript)](../../../ado/reference/ado-api/addnew-method-example-vbscript.md)   
 [Exemplo do método AddNew (VC + +)](../../../ado/reference/ado-api/addnew-method-example-vc.md)   
 [Método CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Propriedade EditMode](../../../ado/reference/ado-api/editmode-property.md)   
 [Método Requery](../../../ado/reference/ado-api/requery-method.md)   
 [Dá suporte ao método](../../../ado/reference/ado-api/supports-method.md)   
 [Método de atualização](../../../ado/reference/ado-api/update-method.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)

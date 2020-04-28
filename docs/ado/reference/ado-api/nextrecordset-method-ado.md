---
title: Método NextRecordset (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- NextRecordset
- Recordset15::NextRecordset
- Recordset15::raw_NextRecordset
helpviewer_keywords:
- NextRecordset method [ADO]
ms.assetid: ab1fa449-a695-4987-b1ee-bc68f89418dd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3c7af4f5d217670ab23e71a3c53ccd5cf7944b0c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932032"
---
# <a name="nextrecordset-method-ado"></a>Método NextRecordset (ADO)
Limpa o objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) atual e retorna o próximo **conjunto de registros** avançando por meio de uma série de comandos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set recordset2 = recordset1.NextRecordset(RecordsAffected )  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um objeto **Recordset** . No modelo de sintaxe, *recordset1* e *recordset2* podem ser o mesmo objeto **Recordset** ou você pode usar objetos separados. Ao usar objetos **Recordset** separados, redefinir a propriedade **ActiveConnection** no **conjunto de registros** original (*recordset1*) depois que **NextRecordset** foi chamado gerará um erro.  
  
#### <a name="parameters"></a>Parâmetros  
 *RecordsAffected*  
 Opcional. Uma variável **longa** para a qual o provedor retorna o número de registros que a operação atual afetou.  
  
> [!NOTE]
>  Esse parâmetro retorna apenas o número de registros afetados por uma operação; Ele não retorna uma contagem de registros de uma instrução SELECT usada para gerar o **conjunto de registros**.  
  
## <a name="remarks"></a>Comentários  
 Use o método **NextRecordset** para retornar os resultados do próximo comando em uma instrução de comando composta ou de um procedimento armazenado que retorna vários resultados. Se você abrir um objeto **Recordset** com base em uma instrução de comando composta (por exemplo, \* "select from Table1; SELECT \* from Table2 ") usando o método [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) em um [comando](../../../ado/reference/ado-api/command-object-ado.md) ou o método [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) em um **conjunto de registros**, o ADO executa apenas o primeiro comando e retorna os resultados para o conjunto de *registros*. Para acessar os resultados dos comandos subsequentes na instrução, chame o método **NextRecordset** .  
  
 Desde que haja resultados adicionais e o conjunto de **registros** que contém as instruções compostas não seja desconectado ou empacotado entre limites de processo, o método **NextRecordset** continuará a retornar objetos **Recordset** . Se um comando de retorno de linha for executado com êxito, mas não retornar registros, o objeto **Recordset** retornado será aberto, mas vazio. Teste para esse caso verificando se as propriedades [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) e [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) são ambas **verdadeiras**. Se um comando sem retorno de linha for executado com êxito, o objeto **Recordset** retornado será fechado, que você poderá verificar testando a propriedade [State](../../../ado/reference/ado-api/state-property-ado.md) no **conjunto de registros**. Quando não houver mais resultados, o *conjunto de registros* será definido como *Nothing*.  
  
 O método **NextRecordset** não está disponível em um objeto **Recordset** desconectado, em que a [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) foi definida como **Nothing** (no Microsoft Visual Basic) ou NULL (em outras linguagens).  
  
 Se uma edição estiver em andamento enquanto estiver no modo de atualização imediata, chamar o método **NextRecordset** gerará um erro; Chame o método [Update](../../../ado/reference/ado-api/update-method.md) ou [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) primeiro.  
  
 Para passar parâmetros para mais de um comando na instrução composta preenchendo a coleção [Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md) ou passando uma matriz com a chamada original **Open** ou **Execute** , os parâmetros devem estar na mesma ordem na coleção ou na matriz como seus respectivos comandos na série de comandos. Você deve concluir a leitura de todos os resultados antes de ler os valores de parâmetro de saída.  
  
 Seu provedor de OLE DB determina quando cada comando em uma instrução composta é executado. O [provedor de OLE DB da Microsoft para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), por exemplo, executa todos os comandos em um lote após receber a instrução composta. Os **conjuntos de registros** resultantes são simplesmente retornados quando você chama **NextRecordset**.  
  
 No entanto, outros provedores podem executar o próximo comando em uma instrução somente depois que NextRecordset é chamado. Para esses provedores, se você fechar explicitamente o objeto **Recordset** antes de percorrer a instrução de comando inteira, o ADO nunca executará os comandos restantes.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método NextRecordset (VB)](../../../ado/reference/ado-api/nextrecordset-method-example-vb.md)   
 [Exemplo do método NextRecordset (VC++)](../../../ado/reference/ado-api/nextrecordset-method-example-vc.md)   

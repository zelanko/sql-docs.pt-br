---
title: "Método NextRecordset (ADO) | Microsoft Docs"
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
- NextRecordset
- Recordset15::NextRecordset
- Recordset15::raw_NextRecordset
helpviewer_keywords:
- NextRecordset method [ADO]
ms.assetid: ab1fa449-a695-4987-b1ee-bc68f89418dd
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e7650cb3516311f3eb93e93304ba9d20ec874466
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="nextrecordset-method-ado"></a>Método NextRecordset (ADO)
Limpa atual [registros](../../../ado/reference/ado-api/recordset-object-ado.md) de objeto e retorna o próximo **registros** pelo adiantamento por meio de uma série de comandos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set recordset2 = recordset1.NextRecordset(RecordsAffected )  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um **registros** objeto. No modelo de sintaxe, *recordset1* e *recordset2* pode ser o mesmo **registros** objeto, ou você pode usar objetos separados. Ao usar separada **registros** objetos, redefinindo o **ActiveConnection** propriedade original **registros** (*recordset1*) Depois de **NextRecordset** foi chamado irá gerar um erro.  
  
#### <a name="parameters"></a>Parâmetros  
 *RecordsAffected*  
 Opcional. Um **longo** variável na qual o provedor retorna o número de registros afetada a operação atual.  
  
> [!NOTE]
>  Este parâmetro retorna somente o número de registros afetados por uma operação; ele não retorna uma contagem de registros de uma instrução select usada para gerar o **registros**.  
  
## <a name="remarks"></a>Comentários  
 Use o **NextRecordset** método para retornar os resultados do próximo comando em uma instrução composta de comando ou de um procedimento armazenado que retorna vários resultados. Se você abrir um **registros** objeto com base em uma instrução composta de comando (por exemplo, "selecionar \* de table1; Selecione \* de table2 ") usando o [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) método em um [comando](../../../ado/reference/ado-api/command-object-ado.md) ou o [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) método em um **Recordset**, ADO executa somente o primeiro comando e retorna os resultados para *registros*. Para acessar os resultados dos comandos subsequentes na instrução, chame o **NextRecordset** método.  
  
 Como há resultados adicionais e o **registros** que contém as declarações compostas é desconectado ou realizar marshaling nos limites de processo, não o **NextRecordset** método continuarão a retornar **registros** objetos. Se um comando de retorno de linha é executado com êxito, mas não retornou nenhum registro retornado **registros** objeto será aberto, mas vazio. Teste para este caso, verificando se o [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) e [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) propriedades estiverem **True**. Se um não??? retorno de linha comando for executado com êxito, retornado **Recordset** objeto será fechado, que você pode verificar Testando o [estado](../../../ado/reference/ado-api/state-property-ado.md) propriedade no **Recordset**. Quando não há mais nenhum resultado *registros* será definida como *nada*.  
  
 O **NextRecordset** método não está disponível em um desconectada **registros** objeto, onde [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) foi definida como **nada**(no Microsoft Visual Basic) ou nulo (em outras linguagens).  
  
 Se uma edição está em andamento no modo de atualização imediata, chamando o **NextRecordset** método gera um erro; chamar o [atualizar](../../../ado/reference/ado-api/update-method.md) ou [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) método primeiro.  
  
 Para passar parâmetros para mais de um comando na instrução composta preenchendo o [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção, ou passando uma matriz com o original **abrir** ou **Execute** chamada, os parâmetros devem ser na mesma ordem na coleção ou matriz de seus respectivos comandos na série de comando. Você deve concluir a leitura de todos os resultados antes de ler os valores de parâmetro de saída.  
  
 O provedor OLE DB determina quando cada comando em uma instrução composta é executado. O [Microsoft OLE DB Provider para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), por exemplo, executa todos os comandos em um lote ao receber a instrução composta. Resultante **conjuntos de registros** simplesmente são retornadas quando você chamar **NextRecordset**.  
  
 No entanto, outros provedores podem executar o próximo comando em uma instrução somente depois NextRecordset é chamado. Para esses provedores, se você fechar explicitamente o **registros** objeto antes de passar por meio da instrução de comando inteira, ADO nunca executa os comandos restantes.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método NextRecordset (VB)](../../../ado/reference/ado-api/nextrecordset-method-example-vb.md)   
 [Exemplo do método NextRecordset (VC++)](../../../ado/reference/ado-api/nextrecordset-method-example-vc.md)   


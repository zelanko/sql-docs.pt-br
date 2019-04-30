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
manager: craigg
ms.openlocfilehash: fba1826dcad9a183bab9b9b0106bb9b45eb29846
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242417"
---
# <a name="nextrecordset-method-ado"></a>Método NextRecordset (ADO)
Limpa o atual [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) do objeto e retorna o próximo **Recordset** por Avançar até uma série de comandos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set recordset2 = recordset1.NextRecordset(RecordsAffected )  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um **Recordset** objeto. No modelo de sintaxe *recordset1* e *recordset2* pode ser o mesmo **Recordset** objeto, ou você pode usar objetos separados. Ao usar separado **conjunto de registros** objetos, redefinindo o **ActiveConnection** propriedade no original **conjunto de registros** (*recordset1*) Depois que **NextRecordset** tiver sido chamado irá gerar um erro.  
  
#### <a name="parameters"></a>Parâmetros  
 *RecordsAffected*  
 Opcional. Um **longo** variável na qual o provedor retorna o número de registros afetada da operação atual.  
  
> [!NOTE]
>  Esse parâmetro só retorna o número de registros afetados por uma operação; ele não retorna uma contagem de registros de uma instrução select usada para gerar o **conjunto de registros**.  
  
## <a name="remarks"></a>Comentários  
 Use o **NextRecordset** método para retornar os resultados do comando próxima em uma instrução composta de comando ou de um procedimento armazenado que retorna vários resultados. Se você abrir um **conjunto de registros** objeto com base em uma instrução composta de comando (por exemplo, "selecionar \* FROM table1; Selecione \* de table2 ") usando o [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) método em um [comando](../../../ado/reference/ado-api/command-object-ado.md) ou o [abertos](../../../ado/reference/ado-api/open-method-ado-recordset.md) método em um **Recordset**, ADO executa apenas o primeiro comando e retorna os resultados para *conjunto de registros*. Para acessar os resultados dos comandos subsequentes na instrução, chame o **NextRecordset** método.  
  
 Como há resultados adicionais e o **conjunto de registros** que contém as instruções compostas não está desconectado ou marshaling entre limites de processo, o **NextRecordset** método continuará a retornar **Recordset** objetos. Se um retorno de linha comando for executado com êxito, mas não retornou nenhum registro retornado **Recordset** objeto será aberto, mas vazio. Teste para esse caso, verificando se o [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) e [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) as propriedades são ambos **verdadeiro**. Se um comando não retornar a linha for executado com êxito, retornado **conjunto de registros** objeto será fechado, que você pode verificar Testando a [estado](../../../ado/reference/ado-api/state-property-ado.md) propriedade no **Recordset**. Quando não houver mais nenhum resultado *conjunto de registros* será definido como *nada*.  
  
 O **NextRecordset** método não está disponível em um desconectado **conjunto de registros** objeto, onde [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) foi definido como **nada**(no Microsoft Visual Basic) ou nulo (em outras linguagens).  
  
 Se uma edição está em andamento enquanto estiver no modo de atualização imediata, chamando o **NextRecordset** método gera um erro; a chamada a [atualizar](../../../ado/reference/ado-api/update-method.md) ou [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) método primeiro.  
  
 Para passar parâmetros para mais de um comando na instrução composta, preenchendo a [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção, ou passando uma matriz com o original **abra** ou **Execute** chamada, os parâmetros devem ser na mesma ordem na coleção ou matriz como seus respectivos comandos da série de comando. Você deve concluir a leitura de todos os resultados antes de ler os valores de parâmetro de saída.  
  
 Seu provedor de OLE DB determina quando cada comando em uma instrução composta é executado. O [Microsoft OLE DB Provider para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), por exemplo, executa todos os comandos em um lote após receber a instrução composta. Resultante **conjuntos de registros** simplesmente são retornadas quando você chama **NextRecordset**.  
  
 No entanto, outros provedores podem executar o próximo comando em uma instrução somente depois NextRecordset é chamado. Para esses provedores, se você fechar explicitamente o **Recordset** objeto antes de passar por meio da instrução de comando inteira, ADO nunca executa os comandos restantes.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método NextRecordset (VB)](../../../ado/reference/ado-api/nextrecordset-method-example-vb.md)   
 [Exemplo do método NextRecordset (VC++)](../../../ado/reference/ado-api/nextrecordset-method-example-vc.md)   

---
title: Executar método (comando ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::Execute
- Command15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: f84a5ff3-0528-4ad7-9bea-9a15103378dd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f9508b85bc73ebbec82ad7d3bea5af5148d7c674
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184802"
---
# <a name="execute-method-ado-command"></a>Método Execute (comando ADO)
Executa a consulta, a instrução SQL ou o procedimento armazenado especificado na [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) ou [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) propriedade do [objeto de comando](../../../ado/reference/ado-api/command-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set recordset = command.Execute( RecordsAffected, Parameters, Options )  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) referência de objeto, um fluxo, ou **nada**.  
  
#### <a name="parameters"></a>Parâmetros  
 *RecordsAffected*  
 Opcional. Um **longo** variável na qual o provedor retorna o número de registros afetada da operação. O *RecordsAffected* parâmetro aplica-se somente para consultas de ação ou procedimentos armazenados. *RecordsAffected* não retorna o número de registros retornados por uma consulta retorna resultados ou um procedimento armazenado. Para obter essas informações, use o [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) propriedade. O **Execute** método não retornará as informações corretas quando usado com **adAsyncExecute**, simplesmente porque quando um comando é executado de forma assíncrona, o número de registros afetados ainda não pode ser conhecido no momento, o método retorna.  
  
 *Parâmetros*  
 Opcional. Um **Variant** matriz de valores de parâmetro usados em conjunto com a cadeia de caracteres de entrada ou o fluxo especificado em **CommandText** ou **CommandStream**. (Parâmetros de saída não retornará os valores corretos quando passados neste argumento.)  
  
 *Opções*  
 Opcional. Um **longo** valor que indica como o provedor deve avaliar o [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) ou o [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) propriedade do [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto. Pode ser feito usando um valor de bitmask [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) e/ou [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valores. Por exemplo, você pode usar **adCmdText** e **adExecuteNoRecords** em combinação, se você quiser ter ADO a avaliar o valor da **CommandText** propriedade como texto, e indica que o comando deve descartar e não retornar os registros que podem ser gerados quando o texto do comando é executado.  
  
> [!NOTE]
>  Use o **ExecuteOptionEnum** valor **adExecuteNoRecords** para melhorar o desempenho, minimizando o processamento interno. Se **adExecuteStream** foi especificado, as opções **adAsyncFetch** e **adAsynchFetchNonBlocking** são ignorados. Não use o **CommandTypeEnum** valores de **adCmdFile** ou **adCmdTableDirect** com **Execute**. Esses valores só podem ser usados como opções com o [aberto](../../../ado/reference/ado-api/open-method-ado-recordset.md) e [Requery](../../../ado/reference/ado-api/requery-method.md) métodos de um **conjunto de registros**.  
  
## <a name="remarks"></a>Comentários  
 Usando o **Execute** método em um **comando** objeto executa a consulta especificada no **CommandText** propriedade ou **CommandStream** propriedade do objeto.  
  
 Os resultados são retornados em uma **Recordset** (por padrão) ou como um fluxo de informações binárias. Para obter um fluxo binário, especifique **adExecuteStream** na *opções*, em seguida, forneça um fluxo, definindo **Command.Properties ("saída Stream")**. ADO **Stream** objeto pode ser especificado para receber os resultados ou outro objeto de fluxo como o objeto de resposta do IIS pode ser especificado. Se nenhum fluxo tiver sido especificado antes de chamar **Execute** com **adExecuteStream**, ocorrerá um erro. A posição do fluxo no retorno de **Execute** é o provedor específico.  
  
 Se o comando não se destina para retornar resultados (por exemplo, uma consulta de atualização do SQL) o provedor retorna **nada** desde que a opção **adExecuteNoRecords** é especificado; caso contrário, Execute retorna um fechado **conjunto de registros**. Alguns idiomas de aplicativo permitem que você ignorar esse valor retornado se nenhum **Recordset** é desejado.  
  
 **Execute** gerará um erro se o usuário Especifica um valor para **CommandStream** quando o **CommandType** é **adCmdStoredProc**,  **adCmdTable**, ou **adCmdTableDirect**.  
  
 Se a consulta tiver parâmetros, valores de atual para o **comando** parâmetros do objeto são usados, a menos que você substituí-las com valores de parâmetro passados com o **Execute** chamar. Você pode substituir um subconjunto dos parâmetros, omitindo os novos valores para alguns dos parâmetros ao chamar o **Execute** método. A ordem em que você especifique os parâmetros é a mesma ordem em que o método passa. Por exemplo, se havia quatro (ou mais) parâmetros e você quiser passar valores novos para apenas os primeiro e o quarto parâmetros, você passaria `Array(var1,,,var4)` como o *parâmetros* argumento.  
  
> [!NOTE]
>  Parâmetros de saída não retornará os valores corretos quando passado a *parâmetros* argumento.  
  
 Uma [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md) evento será emitido quando conclui essa operação.  
  
> [!NOTE]
>  Ao emitir comandos que contêm URLs, aqueles que usam o esquema http invocará automaticamente o [Microsoft OLE DB Provider para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [absoluta e relativa URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Execute, Requery e Clear exemplo dos métodos (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute, Requery e Clear exemplo dos métodos (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute, Requery e Clear exemplo dos métodos (VC + +)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [Propriedade CommandStream (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [Propriedade CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)   
 [Executar método (Conexão ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Evento ExecuteComplete (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)

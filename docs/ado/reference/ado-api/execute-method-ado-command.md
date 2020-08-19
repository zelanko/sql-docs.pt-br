---
description: Método Execute (comando ADO)
title: Método Execute (comando ADO) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b33ada4ce6ac53c1caafbec80c19d1fd31deb6ab
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443888"
---
# <a name="execute-method-ado-command"></a>Método Execute (comando ADO)
Executa a consulta, a instrução SQL ou o procedimento armazenado especificado na propriedade [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) ou [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) do [objeto Command](../../../ado/reference/ado-api/command-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set recordset = command.Execute( RecordsAffected, Parameters, Options )  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna uma referência de objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) , um fluxo ou **nada**.  
  
#### <a name="parameters"></a>Parâmetros  
 *RecordsAffected*  
 Opcional. Uma variável **longa** para a qual o provedor retorna o número de registros afetados pela operação. O parâmetro *RecordsAffected* aplica-se somente a consultas de ação ou procedimentos armazenados. *RecordsAffected* não retorna o número de registros retornados por uma consulta de retorno de resultado ou procedimento armazenado. Para obter essas informações, use a propriedade [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) . O método **Execute** não retornará as informações corretas quando usado com **adAsyncExecute**, simplesmente porque quando um comando é executado de forma assíncrona, o número de registros afetados pode ainda não ser conhecido no momento em que o método retorna.  
  
 *Parâmetros*  
 Opcional. Uma matriz **variante** de valores de parâmetro usada em conjunto com a cadeia de caracteres de entrada ou o fluxo especificado em **CommandText** ou **CommandStream**. (Os parâmetros de saída não retornarão valores corretos quando passados neste argumento).  
  
 *Opções*  
 Opcional. Um valor **longo** que indica como o provedor deve avaliar a propriedade [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) ou [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) do objeto [Command](../../../ado/reference/ado-api/command-object-ado.md) . Pode ser um valor de bitmask feito usando valores [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) e/ou [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) . Por exemplo, você pode usar **adCmdText** e **adExecuteNoRecords** em combinação se quiser que o ADO avalie o valor da propriedade **CommandText** como texto e indique que o comando deve descartar e não retornar nenhum registro que possa ser gerado quando o texto do comando for executado.  
  
> [!NOTE]
>  Use o **ExecuteOptionEnum** valor ExecuteOptionEnum **adExecuteNoRecords** para melhorar o desempenho, minimizando o processamento interno. Se **adExecuteStream** tiver sido especificado, as opções **adAsyncFetch** e **adAsynchFetchNonBlocking** serão ignoradas. Não use os valores de **CommandTypeEnum** de **adCmdFile** ou **adCmdTableDirect** com **Execute**. Esses valores só podem ser usados como opções com os métodos [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) e [Requery](../../../ado/reference/ado-api/requery-method.md) de um **conjunto de registros**.  
  
## <a name="remarks"></a>Comentários  
 O uso do método **Execute** em um objeto **Command** executa a consulta especificada na propriedade **CommandText** ou na propriedade **CommandStream** do objeto.  
  
 Os resultados são retornados em um **conjunto de registros** (por padrão) ou como um fluxo de informações binárias. Para obter um fluxo binário, especifique **adExecuteStream** em *Opções*e, em seguida, forneça um fluxo definindo **Command. Properties ("fluxo de saída")**. Um objeto de **fluxo** ADO pode ser especificado para receber os resultados ou outro objeto de fluxo, como o objeto de resposta do IIS, pode ser especificado. Se nenhum fluxo tiver sido especificado antes de chamar **Execute** with **adExecuteStream**, ocorrerá um erro. A posição do fluxo em retornar da **execução** é específica do provedor.  
  
 Se o comando não se destinar a retornar resultados (por exemplo, uma consulta SQL UPDATE), o provedor não retornará **nada** enquanto a opção **adExecuteNoRecords** for especificada; caso contrário, execute retorna um **conjunto de registros**fechado. Algumas linguagens de aplicativo permitem ignorar esse valor de retorno se nenhum **conjunto de registros** for desejado.  
  
 **Executar** gerará um erro se o usuário especificar um valor **para CommandStream** quando o **CommandType** for **adCmdStoredProc**, **adCmdTable**ou **adCmdTableDirect**.  
  
 Se a consulta tiver parâmetros, os valores atuais para os parâmetros do objeto de **comando** serão usados, a menos que você os substitua por valores de parâmetro passados com a chamada de **execução** . Você pode substituir um subconjunto dos parâmetros omitindo novos valores para alguns dos parâmetros ao chamar o método **Execute** . A ordem na qual você especifica os parâmetros é a mesma ordem na qual o método os passa. Por exemplo, se houvesse quatro (ou mais) parâmetros e você quisesse passar novos valores apenas para o primeiro e o quarto parâmetros, você passaria `Array(var1,,,var4)` como o argumento *Parameters* .  
  
> [!NOTE]
>  Os parâmetros de saída não retornarão valores corretos quando passados no argumento *Parameters* .  
  
 Um evento [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md) será emitido quando esta operação for concluída.  
  
> [!NOTE]
>  Ao emitir comandos que contêm URLs, aqueles que usam o esquema http invocarão automaticamente o [provedor do Microsoft OLE DB para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [URLs absolutas e relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos Execute, Requery e Clear (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Exemplo dos métodos Execute, Requery e Clear (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Exemplo dos métodos Execute, Requery e Clear (VC + +)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [Propriedade CommandStream (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [Propriedade CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)   
 [Método Execute (conexão ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Evento ExecuteComplete (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)

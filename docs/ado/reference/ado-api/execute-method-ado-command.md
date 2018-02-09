---
title: "Executar método (comando ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
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
- Command15::Execute
- Command15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: f84a5ff3-0528-4ad7-9bea-9a15103378dd
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7f16d3c01fb219bdbe7f52bbc39d3c410b5de918
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="execute-method-ado-command"></a>Executar método (comando ADO)
Executa a consulta, a instrução SQL ou o procedimento armazenado especificado no [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) ou [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) propriedade o [o objeto de comando](../../../ado/reference/ado-api/command-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set recordset = command.Execute( RecordsAffected, Parameters, Options )  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) referência de objeto, um fluxo ou **nada**.  
  
#### <a name="parameters"></a>Parâmetros  
 *RecordsAffected*  
 Opcional. Um **longo** variável na qual o provedor retorna o número de registros afetada a operação. O *RecordsAffected* parâmetro aplica-se somente para procedimentos armazenados ou consultas de ação. *RecordsAffected* não retorna o número de registros retornados por uma consulta retorna resultados ou o procedimento armazenado. Para obter essas informações, use o [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) propriedade. O **Execute** método não retornará as informações corretas quando usado com **adAsyncExecute**, simplesmente porque quando um comando é executado de forma assíncrona, o número de registros afetados ainda não pode ser conhecido no momento em que o método retorna.  
  
 *Parâmetros*  
 Opcional. Um **Variant** matriz de valores de parâmetro usados em conjunto com a cadeia de caracteres de entrada ou o fluxo especificado em **CommandText** ou **CommandStream**. (Parâmetros de saída não retornará valores corretos quando esse argumento passado.)  
  
 *Opções*  
 Opcional. Um **longo** valor que indica como o provedor deve avaliar o [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) ou o [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) propriedade o [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto. Pode ser um valor de máscara de bits feito usando [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) e/ou [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valores. Por exemplo, você pode usar **adCmdText** e **adExecuteNoRecords** em combinação, se você quiser ter ADO a avaliar o valor da **CommandText** propriedade como texto, e indica que o comando deve descartar e não retorna registros que podem ser gerados quando o texto do comando é executado.  
  
> [!NOTE]
>  Use o **ExecuteOptionEnum** valor **adExecuteNoRecords** para melhorar o desempenho, reduzindo o processamento interno. Se **adExecuteStream** foi especificado, as opções de **adAsyncFetch** e **adAsynchFetchNonBlocking** são ignorados. Não use o **CommandTypeEnum** valores de **adCmdFile** ou **adCmdTableDirect** com **Execute**. Esses valores podem ser usados apenas como opções com a [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) e [Requery](../../../ado/reference/ado-api/requery-method.md) métodos de um **registros**.  
  
## <a name="remarks"></a>Remarks  
 Usando o **Execute** método em um **comando** objeto executa a consulta especificada no **CommandText** propriedade ou **CommandStream** propriedade do objeto.  
  
 Os resultados são retornados em uma **registros** (por padrão) ou como um fluxo de informações binárias. Para obter um fluxo binário, especifique **adExecuteStream** na *opções*, em seguida, forneça um fluxo definindo **Command.Properties ("fluxo de saída")**. ADO **fluxo** objeto pode ser especificado para receber os resultados ou outro objeto de fluxo, como o objeto de resposta de IIS pode ser especificado. Se nenhum fluxo foi especificado antes de chamar **Execute** com **adExecuteStream**, ocorrerá um erro. A posição do fluxo no retorno de **Execute** é o provedor específico.  
  
 Se o comando não se destina para retornar resultados (por exemplo, uma consulta de atualização do SQL) o provedor retorna **nada** desde que a opção **adExecuteNoRecords** for especificado; caso contrário, Execute retorna um fechado **registros**. Alguns idiomas de aplicativo permitem que você ignorar esse valor de retorno se nenhum **registros** é desejado.  
  
 **Executar** gera um erro se o usuário Especifica um valor para **CommandStream** quando o **CommandType** é **adCmdStoredProc**,  **adCmdTable**, ou **adCmdTableDirect**.  
  
 Se a consulta tiver parâmetros, os valores atuais para o **comando** os parâmetros do objeto são usados a menos que você substitua esses recursos com valores de parâmetro passados com o **Execute** chamar. Você pode substituir um subconjunto dos parâmetros omitindo novos valores para alguns dos parâmetros ao chamar o **Execute** método. A ordem em que você especificar os parâmetros é a mesma ordem em que o método passa. Por exemplo, se houvesse parâmetros quatro (ou mais) e desejar passar os novos valores para apenas os primeiro e o quarto parâmetros, você passaria `Array(var1,,,var4)` como o *parâmetros* argumento.  
  
> [!NOTE]
>  Parâmetros de saída não retornará valores corretos quando passado a *parâmetros* argumento.  
  
 Um [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md) evento será emitido quando conclui a operação.  
  
> [!NOTE]
>  Ao emitir comandos que contêm URLs, aquelas que usam o esquema http automaticamente invocará o [Microsoft OLE DB Provider para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [Absolute e URLs relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Execute, repetir e limpar o exemplo de métodos (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute, repetir e limpar o exemplo de métodos (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute, repetir e limpar o exemplo de métodos (VC + +)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [Propriedade CommandStream (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [Propriedade CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)   
 [Executar método (Conexão ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Evento ExecuteComplete (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)

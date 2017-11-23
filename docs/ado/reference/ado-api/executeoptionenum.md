---
title: ExecuteOptionEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: ExecuteOptionEnum
helpviewer_keywords: ExecuteOptionEnum enumeration [ADO]
ms.assetid: 68bfa83a-5df4-4bef-8736-0f88ae8c29ea
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8357988f5082498114c435f899e898552fca1707
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="executeoptionenum"></a>ExecuteOptionEnum
Especifica como um provedor deve executar um comando.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adAsyncExecute**|0x10|Indica que o comando deve executar de forma assíncrona.<br /><br /> Esse valor não pode ser combinado com o [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) valor **adCmdTableDirect**.|  
|**adAsyncFetch**|0x20|Indica que as demais linhas após a quantidade inicial especificada a [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) propriedade deve ser recuperada de forma assíncrona.|  
|**adAsyncFetchNonBlocking**|0x40|Indica que o thread principal nunca bloqueia durante a recuperação. Se a linha solicitada não foi recuperada, a linha atual se transforma automaticamente ao final do arquivo.<br /><br /> Se você abrir um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) de um [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) contendo armazenado persistentemente **registros**, **adAsyncFetchNonBlocking** não terão um efeito; a operação será síncrona e de bloqueio.<br /><br /> **adAsynchFetchNonBlocking** não tem nenhum efeito quando o [adCmdTableDirect](../../../ado/reference/ado-api/commandtypeenum.md) opção é usada para abrir o **registros**.|  
|**adExecuteNoRecords**|0x80|Indica que o texto do comando é um comando ou procedimento armazenado que não retorna linhas (por exemplo, um comando que insere apenas dados). Se todas as linhas são recuperadas, eles são descartados e não retornados.<br /><br /> **adExecuteNoRecords** só pode ser passado como um parâmetro opcional para o **comando** ou **Conexão executar** método.|  
|**adExecuteStream**|0x400|Indica que os resultados de uma execução de comando devem ser retornados como um fluxo.<br /><br /> **adExecuteStream** só pode ser passado como um parâmetro opcional para o **executar comando** método.|  
|**adExecuteRecord**||Indica que o **CommandText** é um comando ou procedimento armazenado que retorna uma única linha que deve ser retornada como um **registro** objeto.|  
|**Feita**|-1|Indica que o comando não for especificado.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.ExecuteOption.ASYNCEXECUTE|  
|AdoEnums.ExecuteOption.ASYNCFETCH|  
|AdoEnums.ExecuteOption.ASYNCFETCHNONBLOCKING|  
|AdoEnums.ExecuteOption.NORECORDS|  
|AdoEnums.ExecuteOption.UNSPECIFIED|  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Método Execute (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)|[Método Execute (conexão ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|  
|[Método Open (Conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[Método Requery](../../../ado/reference/ado-api/requery-method.md)|

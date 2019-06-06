---
title: ExecuteOptionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ExecuteOptionEnum
helpviewer_keywords:
- ExecuteOptionEnum enumeration [ADO]
ms.assetid: 68bfa83a-5df4-4bef-8736-0f88ae8c29ea
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 589519e7c4a075d5fb06b5f2640d48e5d4ed898d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695266"
---
# <a name="executeoptionenum"></a>ExecuteOptionEnum
Especifica como um provedor deve executar um comando.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adAsyncExecute**|0x10|Indica que o comando deve executar de forma assíncrona.<br /><br /> Esse valor não pode ser combinado com o [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) valor **adCmdTableDirect**.|  
|**adAsyncFetch**|0x20|Indica que o restante linhas após a quantidade inicial especificada do [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) propriedade deve ser recuperada de maneira assíncrona.|  
|**adAsyncFetchNonBlocking**|0x40|Indica que o thread principal nunca for bloqueado durante a recuperação. Se a linha solicitada não foi recuperada, a linha atual se move automaticamente até o final do arquivo.<br /><br /> Se você abrir um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) de uma [Stream](../../../ado/reference/ado-api/stream-object-ado.md) que contém um persistentemente armazenado **conjunto de registros**, **adAsyncFetchNonBlocking** não terão um efeito; a operação será síncrona e bloqueio.<br /><br /> **adAsynchFetchNonBlocking** não tem nenhum efeito quando o [adCmdTableDirect](../../../ado/reference/ado-api/commandtypeenum.md) opção é usada para abrir o **conjunto de registros**.|  
|**adExecuteNoRecords**|0x80|Indica que o texto do comando é um comando ou procedimento armazenado que não retorna linhas (por exemplo, um comando que insere apenas dados). Se todas as linhas são recuperadas, elas são descartadas e não retornadas.<br /><br /> **adExecuteNoRecords** só pode ser passado como um parâmetro opcional para o **comando** ou **Conexão executar** método.|  
|**adExecuteStream**|0x400|Indica que os resultados de uma execução de comando devem ser retornados como um fluxo.<br /><br /> **adExecuteStream** só pode ser passado como um parâmetro opcional para o **Command Execute** método.|  
|**adExecuteRecord**||Indica que o **CommandText** é um comando ou procedimento armazenado que retorna uma única linha que deve ser retornada como um **registro** objeto.|  
|**adOptionUnspecified**|-1|Indica que o comando é especificado.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Package: **com.ms.wfc.data**  
  
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

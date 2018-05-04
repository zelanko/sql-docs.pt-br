---
title: Propriedade FetchOptions (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FetchOptions property [ADO]
ms.assetid: 7b2e254a-9354-4541-bc98-bb185276388f
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe754d9fe91818e0f80a4b027e3bf74aae11bfeb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="fetchoptions-property-rds"></a>Propriedade FetchOptions (RDS)
Indica o tipo de busca de maneira assíncrona.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="setting-and-return-values"></a>Configuração e valores de retorno  
 Define ou retorna um dos valores a seguir.  
  
|Constante|Description|  
|--------------|-----------------|  
|**adcFetchUpFront**|Todos os registros da [registros](../../../ado/reference/ado-api/recordset-object-ado.md) são buscadas antes do controle é retornado para o aplicativo. Completo **registros** é buscada antes do aplicativo tem permissão para fazer qualquer coisa com ele.|  
|**adcFetchBackground**|Controle pode retornar para o aplicativo assim que o primeiro lote de registros foi buscado. Ler um subsequentes do **registros** que tenta acessar um registro não buscado no primeiro lote será atrasada até que o registro procurado na verdade é obtido, momento em que o controle retorna para o aplicativo.|  
|**adcFetchAsync**|Padrão. O controle retorna imediatamente para o aplicativo enquanto os registros são buscados em segundo plano. Se o aplicativo tenta ler um registro que ainda não tenha sido buscado, lerá o registro mais próximo para o registro pesquisado e controle retornará imediatamente, indicando que o final atual do **Recordset** foi atingido. Por exemplo, uma chamada para [MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) moverá a posição atual do registro para o último registro realmente buscado, mesmo que mais registros continuará preencher o **registros**.|  
  
> [!NOTE]
>  Cada arquivo executável do lado do cliente que usa constantes deve fornecer declarações para eles. Você pode recortar e colar as declarações de constantes desejado do arquivo Adcvbs.inc, localizado na pasta de instalação padrão para a biblioteca RDS.  
  
## <a name="remarks"></a>Remarks  
 Em um aplicativo Web, você normalmente deve usar **adcFetchAsync** (o valor padrão), porque ele fornece um melhor desempenho. Em um aplicativo cliente compilado, você normalmente deve usar **adcFetchBackground**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedades de FetchOptions (VBScript) e ExecuteOptions](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Método Cancel (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)



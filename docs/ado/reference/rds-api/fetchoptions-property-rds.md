---
title: Propriedade FetchOptions (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FetchOptions property [ADO]
ms.assetid: 7b2e254a-9354-4541-bc98-bb185276388f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4e4e0943a675ef7cf3684ccddd2699fba02dac9e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67964123"
---
# <a name="fetchoptions-property-rds"></a>Propriedade FetchOptions (RDS)
Indica o tipo de busca assíncrona.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="setting-and-return-values"></a>Valores de configuração e retorno  
 Define ou retorna um dos valores a seguir.  
  
|Constante|Descrição|  
|--------------|-----------------|  
|**adcFetchUpFront**|Todos os registros do [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) são buscados antes do controle ser retornado para o aplicativo. O **conjunto de registros** completo é buscado antes que o aplicativo tenha permissão para fazer qualquer coisa com ele.|  
|**adcFetchBackground**|O controle pode retornar ao aplicativo assim que o primeiro lote de registros for obtido. Uma leitura subsequente do **conjunto de registros** que tenta acessar um registro não buscado no primeiro lote será atrasada até que o registro procurado seja realmente buscado, quando o controle de tempo retornar ao aplicativo.|  
|**adcFetchAsync**|Padrão. O controle retorna imediatamente para o aplicativo enquanto os registros são buscados em segundo plano. Se o aplicativo tentar ler um registro que ainda não foi buscado, o registro mais próximo do registro procurado será lido e o controle retornará imediatamente, indicando que a extremidade atual do **conjunto de registros** foi atingida. Por exemplo, uma chamada para [MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) moverá a posição do registro atual para o último registro realmente buscado, embora mais registros continuem a preencher o **conjunto de registros**.|  
  
> [!NOTE]
>  Cada arquivo executável do lado do cliente que usa essas constantes deve fornecer declarações para eles. Você pode recortar e colar as declarações de constante desejadas do arquivo Adcvbs. Inc, localizadas na pasta de instalação padrão da biblioteca do RDS.  
  
## <a name="remarks"></a>Comentários  
 Em um aplicativo Web, geralmente você desejará usar **adcFetchAsync** (o valor padrão), pois ele fornece um melhor desempenho. Em um aplicativo cliente compilado, geralmente você desejará usar o **adcFetchBackground**.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades executeoptions e FetchOptions (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Método Cancel (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)



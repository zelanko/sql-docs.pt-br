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
manager: jroth
ms.openlocfilehash: a85f6938ec0f97ff69eab1782c0a24b78a5a6e8b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712685"
---
# <a name="fetchoptions-property-rds"></a>Propriedade FetchOptions (RDS)
Indica o tipo de busca de maneira assíncrona.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="setting-and-return-values"></a>Configuração e valores de retorno  
 Define ou retorna um dos valores a seguir.  
  
|Constante|Descrição|  
|--------------|-----------------|  
|**adcFetchUpFront**|Todos os registros da [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) são buscadas antes que o controle é retornado ao aplicativo. A conclusão **Recordset** é buscado antes que o aplicativo tem permissão para fazer algo com ele.|  
|**adcFetchBackground**|Controle pode retornar para o aplicativo assim que o primeiro lote de registros foi buscado. Uma leitura subsequente do **Recordset** que tenta acessar um registro não buscado no primeiro lote será adiada até o registro procurado, na verdade, é obtido, momento em que o controle retorna para o aplicativo.|  
|**adcFetchAsync**|Padrão. Controle retorna imediatamente para o aplicativo enquanto os registros são buscados em segundo plano. Se o aplicativo tenta ler um registro que ainda não tiver sido buscado, lerá o registro mais próximo para o registro procurado e o controle retornará imediatamente, indicando que o final do **Recordset** foi atingido. Por exemplo, uma chamada para [MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) moverá a posição atual do registro para o último registro efetivamente buscado, mesmo que continuarão mais registros preencher o **conjunto de registros**.|  
  
> [!NOTE]
>  Cada arquivo executável do lado do cliente que usa constantes deve fornecer declarações para eles. Você pode recortar e colar as declarações de constante desejada do arquivo Adcvbs.inc, localizado na pasta de instalação padrão para a biblioteca RDS.  
  
## <a name="remarks"></a>Comentários  
 Em um aplicativo Web, você geralmente desejará usar **adcFetchAsync** (o valor padrão), pois ele fornece um melhor desempenho. Em um aplicativo cliente compilado, você geralmente desejará usar **adcFetchBackground**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte também  
 [ExecuteOptions e FetchOptions exemplo das propriedades (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Método Cancel (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)



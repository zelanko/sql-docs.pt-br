---
title: "Estado de prontidão é de propriedade (RDS) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: ReadyState property [ADO]
ms.assetid: 5be75bc7-1171-4440-a37e-c8cc6b5cd865
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0d5533fd471b6aee697825d2251c84adbcdfccfa
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="readystate-property-rds"></a>Estado de prontidão é de propriedade (RDS)
Indica o progresso de uma [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) do objeto que recupera dados em seu [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um dos valores a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|**adcReadyStateLoaded**|A consulta atual ainda está em execução e nenhuma linha foi buscada. O **DataControl** do objeto **registros** não está disponível para uso.|  
|**adcReadyStateInteractive**|Um conjunto inicial de linhas recuperadas pela consulta atual foi armazenado no **DataControl** do objeto **registros** e estão disponíveis para uso. As linhas restantes ainda estão sendo buscadas.|  
|**adcReadyStateComplete**|Todas as linhas recuperadas pela consulta atual foram armazenadas na **DataControl** do objeto **registros** e estão disponíveis para uso.<br /><br /> Esse estado também existirá se uma operação anulada devido a um erro ou se o **registros** objeto não foi inicializado.|  
  
> [!NOTE]
>  Cada arquivo executável do lado do cliente que usa constantes deve fornecer declarações para eles. Você pode recortar e colar as declarações de constantes desejado do arquivo Adcvbs.inc, localizado na pasta de instalação padrão para a biblioteca RDS.  
  
## <a name="remarks"></a>Comentários  
 Use o [onReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md) evento para monitorar as alterações no **estado de prontidão é** propriedade durante uma operação de consulta assíncrona. Isso é mais eficiente do que verificar periodicamente o valor da propriedade.  
  
 Se ocorrer um erro durante uma operação assíncrona, o **estado de prontidão é** alteração na propriedade **adcReadyStateComplete**, o [estado](../../../ado/reference/ado-api/state-property-ado.md) propriedade muda de **adStateExecuting** para **adStateClosed**e o **registros** objeto [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade permanece *nada* .  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de estado de prontidão é de propriedade (VBScript)](../../../ado/reference/rds-api/readystate-property-example-vbscript.md)   
 [Método Cancel (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [Propriedade ExecuteOptions (RDS)](../../../ado/reference/rds-api/executeoptions-property-rds.md)



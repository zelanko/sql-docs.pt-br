---
title: Propriedade ReadyState (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ReadyState property [ADO]
ms.assetid: 5be75bc7-1171-4440-a37e-c8cc6b5cd865
author: rothja
ms.author: jroth
ms.openlocfilehash: c5e1eb89c0e4c7dcbef736d2968a4ffd97a37b93
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82751215"
---
# <a name="readystate-property-rds"></a>Propriedade ReadyState (RDS)
Indica o progresso de um objeto [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) à medida que ele recupera dados em seu objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**adcReadyStateLoaded**|A consulta atual ainda está em execução e nenhuma linha foi buscada. O **conjunto de registros** do objeto **DataControl** não está disponível para uso.|  
|**adcReadyStateInteractive**|Um conjunto inicial de linhas recuperadas pela consulta atual foi armazenado no **conjunto de registros** do objeto **DataControl** e está disponível para uso. As linhas restantes ainda estão sendo buscadas.|  
|**adcReadyStateComplete**|Todas as linhas recuperadas pela consulta atual foram armazenadas no **conjunto de registros** do objeto **DataControl** e estão disponíveis para uso.<br /><br /> Esse estado também existirá se uma operação for anulada devido a um erro ou se o objeto **Recordset** não for inicializado.|  
  
> [!NOTE]
>  Cada arquivo executável do lado do cliente que usa essas constantes deve fornecer declarações para eles. Você pode recortar e colar as declarações de constante desejadas do arquivo Adcvbs. Inc, localizadas na pasta de instalação padrão da biblioteca do RDS.  
  
## <a name="remarks"></a>Comentários  
 Use o evento [onReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md) para monitorar as alterações na propriedade **ReadyState** durante uma operação de consulta assíncrona. Isso é mais eficiente do que verificar periodicamente o valor da propriedade.  
  
 Se ocorrer um erro durante uma operação assíncrona, a propriedade **readyly** será alterada para **adcReadyStateComplete**, a propriedade [State](../../../ado/reference/ado-api/state-property-ado.md) mudará de **adStateExecuting** para **adStateClosed**e a propriedade [Value](../../../ado/reference/ado-api/value-property-ado.md) do objeto **Recordset** permanecerá *Nothing*.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade ReadyState (VBScript)](../../../ado/reference/rds-api/readystate-property-example-vbscript.md)   
 [Método Cancel (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [Propriedade ExecuteOptions (RDS)](../../../ado/reference/rds-api/executeoptions-property-rds.md)



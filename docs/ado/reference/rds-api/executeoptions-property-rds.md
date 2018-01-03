---
title: Propriedade ExecuteOptions (RDS) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: ExecuteOptions property [ADO], VBScript example
ms.assetid: 62a4fd88-afc3-4f1f-b978-40710a30c4e9
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 76876c9182ccba3eab0fa8f16171a3dceabd0876
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="executeoptions-property-rds"></a>Propriedade ExecuteOptions (RDS)
Indica se a execução assíncrona está habilitada.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um dos valores a seguir.  
  
|Constante|Description|  
|--------------|-----------------|  
|**adcExecSync**|Executa a próxima atualização da [registros](../../../ado/reference/ado-api/recordset-object-ado.md) sincronicamente.|  
|**adcExecAsync**|Padrão. Executa a próxima atualização da **registros** assincronamente.|  
  
> [!NOTE]
>  Cada arquivo executável que usa constantes deve fornecer declarações para eles. Você pode recortar e colar as declarações de constantes que deseja para o arquivo Adcvbs.inc, localizado na pasta de instalação padrão para a biblioteca RDS.  
  
## <a name="remarks"></a>Remarks  
 Se **ExecuteOptions** é definido como **adcExecAsync**, e isso executa de forma assíncrona o próximo **atualizar** ligar o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) do objeto **registros**.  
  
 Se você tentar chamar [redefinir](../../../ado/reference/rds-api/reset-method-rds.md), [atualizar](../../../ado/reference/rds-api/refresh-method-rds.md), [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md), [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md), ou [registros](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) enquanto outra operação assíncrona que pode alterar o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) do objeto **registros** está em execução, ocorrerá um erro.  
  
 Se ocorrer um erro durante uma operação assíncrona, o **RDS. DataControl** do objeto [estado de prontidão é](../../../ado/reference/rds-api/readystate-property-rds.md) valor muda de **adcReadyStateLoaded** para **adcReadyStateComplete**e o  **Conjunto de registros** o valor da propriedade permanece *nada*.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de propriedades de FetchOptions (VBScript) e ExecuteOptions](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Método Cancel (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)



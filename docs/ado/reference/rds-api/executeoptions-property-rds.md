---
title: Propriedade ExecuteOptions (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ExecuteOptions property [ADO], VBScript example
ms.assetid: 62a4fd88-afc3-4f1f-b978-40710a30c4e9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6ac7ee6c1f996294c1f8aa353719deb11d698e47
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51603316"
---
# <a name="executeoptions-property-rds"></a>Propriedade ExecuteOptions (RDS)
Indica se a execução assíncrona está habilitada.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um dos valores a seguir.  
  
|Constante|Description|  
|--------------|-----------------|  
|**adcExecSync**|Executa a próxima atualização do [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) forma síncrona.|  
|**adcExecAsync**|Padrão. Executa a próxima atualização do **Recordset** assincronamente.|  
  
> [!NOTE]
>  Cada arquivo executável que usa constantes deve fornecer declarações para eles. Você pode recortar e colar as declarações de constante que você deseja do arquivo Adcvbs.inc, localizado na pasta de instalação padrão para a biblioteca RDS.  
  
## <a name="remarks"></a>Comentários  
 Se **ExecuteOptions** é definido como **adcExecAsync**, então isso executa de forma assíncrona a próxima **atualizar** chamar o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) do objeto **conjunto de registros**.  
  
 Se você tentar chamar [redefina](../../../ado/reference/rds-api/reset-method-rds.md), [atualize](../../../ado/reference/rds-api/refresh-method-rds.md), [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md), [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md), ou [Recordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) enquanto outra operação assíncrona que pode ser alterado a [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) do objeto **Recordset** está em execução, ocorrerá um erro.  
  
 Se ocorrer um erro durante uma operação assíncrona, o **RDS. DataControl** do objeto [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) muda de valor de **adcReadyStateLoaded** para **adcReadyStateComplete**e o  **Conjunto de registros** valor da propriedade permanece *nada*.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte também  
 [ExecuteOptions e FetchOptions exemplo das propriedades (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Método Cancel (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)



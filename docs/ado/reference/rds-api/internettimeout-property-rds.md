---
description: Propriedade InternetTimeout (RDS)
title: Propriedade InternetTimeout (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- InternetTimeout property [ADO]
ms.assetid: 4d1c8892-4bbc-4e71-bf4b-ba52c0ea9549
author: rothja
ms.author: jroth
ms.openlocfilehash: f69b6909630f2930939bc7757c9a4d9d1f1dd943
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88981977"
---
# <a name="internettimeout-property-rds"></a>Propriedade InternetTimeout (RDS)
Indica o número de milissegundos a aguardar antes que uma solicitação expire.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor **longo** que representa o número de milissegundos antes que uma solicitação expire.  
  
## <a name="remarks"></a>Comentários  
 Essa propriedade só se aplica a solicitações enviadas com os protocolos HTTP ou HTTPS.  
  
 As solicitações em um ambiente de três camadas podem levar vários minutos para serem executadas. Use essa propriedade para especificar o tempo adicional para solicitações de execução longa.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto DataControl (RDS)](./datacontrol-object-rds.md)  
    :::column-end:::
    :::column:::
        [Objeto DataSpace (RDS)](./dataspace-object-rds.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade InternetTimeout (VB)](./internettimeout-property-example-vb.md)   
 [Exemplo da propriedade InternetTimeout (VC++)](./internettimeout-property-example-vc.md)   

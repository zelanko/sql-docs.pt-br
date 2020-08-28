---
description: Propriedade Connect (RDS)
title: Propriedade Connect (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Connect property [ADO]
ms.assetid: dbad5e77-b213-4eb8-aecf-d60f203fdb59
author: rothja
ms.author: jroth
ms.openlocfilehash: e956a86333479320fe18114705148bad77ea0440
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88982667"
---
# <a name="connect-property-rds"></a>Propriedade Connect (RDS)
Indica o nome do banco de dados do qual as operações de consulta e atualização são executadas.  
  
 Você pode definir a propriedade **conectar** em tempo de design no [RDS. ](./datacontrol-object-rds.md) Marcas de objeto do objeto DataControl ou em tempo de execução no código de script (por exemplo, VBScript).  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Design time: <PARAM NAME="Connect" VALUE="ConnectionString">  
Run time: DataControl.Connect = "ConnectionString"  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ConnectionString*  
 Uma cadeia de conexão válida. Para obter mais informações gerais sobre cadeias de conexão, consulte a propriedade [ConnectionString](../ado-api/connectionstring-property-ado.md) ou a documentação do provedor.  
  
> [!NOTE]
>  Especificando o MS Remote como o provedor para o **RDS. O DataControl** criaria um cenário de quatro camadas. Cenários maiores que três camadas não foram testados e não devem ser necessários.  
  
 *DataControl*  
 Uma variável de objeto que representa um **RDS. Objeto DataControl** .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataControl (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade Connect (VBScript)](./connect-property-example-vbscript.md)   
 [Método de consulta (RDS)](./query-method-rds.md)   
 [Método de atualização (RDS)](./refresh-method-rds.md)   
 [Método SubmitChanges (RDS)](./submitchanges-method-rds.md)
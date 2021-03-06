---
description: Objetos RDS
title: Objetos RDS | Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
helpviewer_keywords:
- objects [ADO], RDS
- RDS objects [ADO]
ms.assetid: f2ac8b3b-f968-41c4-a504-7aee3538b7c7
author: rothja
ms.author: jroth
ms.openlocfilehash: fa9329b1da84643f75a83ee1487f8c1be47601b1
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724337"
---
# <a name="rds-objects"></a>Objetos RDS
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
|Objeto|Descrição|  
|-|-|  
|[Controle de origem (RDS)](./datacontrol-object-rds.md)|Associa um **conjunto de registros** de consulta de dados a um ou mais controles (por exemplo, uma caixa de texto, controle de grade ou caixa de combinação) para exibir os dados do **conjunto de registros** em uma página da Web.<br /><br /> O objeto **DataControl** é seguro para scripts.|  
|[Datafactory (RDSServer)](./datafactory-object-rdsserver.md)|Implementa métodos que fornecem acesso de dados de leitura/gravação a fontes de dados especificadas para aplicativos do lado do cliente.<br /><br /> O objeto **DataFactory** não é seguro para scripts.|  
|[DataSpace (RDS)](./dataspace-object-rds.md)|Cria proxies do lado do cliente para objetos comerciais personalizados localizados na camada intermediária.<br /><br /> O objeto **DataSpace** é seguro para scripts.|  
|[Interface IRDSService (RDS)](./irdsservice-interface-rds.md)|Expõe o método [InvokeService (RDS)](./invokeservice-rds.md) , que é usado para retornar um ponteiro para a interface solicitada em uma versão mais compatível do objeto.|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de API RDS](./rds-api-reference.md)
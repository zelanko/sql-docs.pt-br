---
description: Propriedades RDS
title: Propriedades de RDS | Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
helpviewer_keywords:
- RDS properties [ADO]
- properties [ADO], RDS
ms.assetid: e4e04cbd-21fc-44a1-9f21-49aa68746934
author: rothja
ms.author: jroth
ms.openlocfilehash: 75124c0fc8d7a0c3c0bb0ea491c84c3673339108
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724347"
---
# <a name="rds-properties"></a>Propriedades RDS
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
|Propriedade|Descrição|  
|-|-|  
|[Conectar (RDS)](./connect-property-rds.md)|Indica o nome do banco de dados do qual as operações de consulta e atualização são executadas.|  
|[Executeoptions (RDS)](./executeoptions-property-rds.md)|Indica se a execução assíncrona está habilitada.|  
|[FetchOptions (RDS)](./fetchoptions-property-rds.md)|Indica o tipo de busca assíncrona.|  
|[FilterColumn (RDS)](./filtercolumn-property-rds.md)|Indica a coluna na qual os critérios de filtro são avaliados.|  
|[FilterCriterion (RDS)](./filtercriterion-property-rds.md)|Indica o operador de avaliação a ser usado no valor do filtro.|  
|[FilterValue (RDS)](./filtervalue-property-rds.md)|Indica o valor para filtrar os registros.|  
|[Handler (RDS)](./handler-property-rds.md)|Indica o nome de um programa de personalização do lado do servidor (*manipulador*) que estende a funcionalidade do **RDSServer. datafactory**e quaisquer parâmetros usados pelo *manipulador*.|  
|[InternetTimeout (RDS)](./internettimeout-property-rds.md)|Indica o número de milissegundos a aguardar antes que uma solicitação expire.|  
|[ReadyState (RDS)](./readystate-property-rds.md)|Indica o progresso de um objeto **DataControl** , pois ele busca dados em seu objeto **Recordset** .|  
|[Conjunto de registros e SourceRecordset (RDS)](./recordset-sourcerecordset-properties-rds.md)|Indica o objeto **Recordset** retornado de um objeto comercial personalizado.|  
|[Servidor (RDS)](./server-property-rds.md)|Indica o nome do Serviços de Informações da Internet (IIS) e o protocolo de comunicação.|  
|[SortColumn (RDS)](./sortcolumn-property-rds.md)|Indica por qual coluna classificar os registros.|  
|[SortDirection (RDS)](./sortdirection-property-rds.md)|Indica se uma ordem de classificação é crescente ou decrescente.|  
|[SQL (RDS)](./sql-property.md)|Indica a cadeia de caracteres de consulta usada para recuperar o **conjunto de registros**.|  
|[URL (RDS)](./url-property-rds.md)|Indica uma cadeia de caracteres que contém uma URL relativa ou absoluta.|
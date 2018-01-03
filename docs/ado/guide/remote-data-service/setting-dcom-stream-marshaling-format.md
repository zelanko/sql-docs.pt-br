---
title: Definir o formato de empacotamento de fluxo DCOM | Microsoft Docs
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
helpviewer_keywords: dcom stream marshaling format in rds [ADO]
ms.assetid: 46664ac5-d6e6-4457-8bae-3a98300f2a41
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 370958ce7f66aa7a87296f47884b62a08935fae0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="setting-dcom-stream-marshaling-format"></a>Definir o formato de empacotamento de fluxo DCOM
Um computador cliente usando componentes de RDS 1.5 ou anterior não é compatível com um servidor usando componentes de RDS 2.0 ou posterior. Ao usar DCOM como protocolo subjacente, o suporte para RDS 2.0 ou posterior é mais eficiente no transporte [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objetos. Se o cliente estiver executando os componentes de RDS 1.5 ou anterior, você pode definir seu servidor para trabalhar com o suporte RDS anterior (chamado RDS 1.0) ou o suporte mais recente do RDS (chamado RDS 2.0 ou posterior). Defina qualquer uma das entradas do registro a seguir:  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
```  
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS10"  
```  
  
 -ou-  
  
```  
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS20"  
```



---
title: Definindo o formato de marshaling de fluxo DCOM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dcom stream marshaling format in rds [ADO]
ms.assetid: 46664ac5-d6e6-4457-8bae-3a98300f2a41
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 29bf8d19b9e3c9ec9b4072edd9575add9947c8f3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922213"
---
# <a name="setting-dcom-stream-marshaling-format"></a>Configurar o formato de marshaling de fluxo DCOM
Um computador cliente que usa componentes do RDS 1,5 ou anterior não é compatível com um servidor usando componentes do RDS 2,0 ou posterior. Ao usar o DCOM como o protocolo subjacente, o suporte para o RDS 2,0 ou posterior é mais eficiente no transporte de objetos [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) . Se o cliente estiver executando componentes do RDS 1,5 ou anterior, você poderá definir seu servidor para trabalhar com o suporte RDS anterior (chamado RDS 1,0) ou com o suporte RDS mais recente (chamado RDS 2,0 ou posterior). Defina uma das seguintes entradas do registro:  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
```console
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS10"  
```  
  
 -ou-  
  
```console
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS20"  
```



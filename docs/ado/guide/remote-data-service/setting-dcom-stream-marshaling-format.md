---
title: Definindo o formato de Marshaling de Stream DCOM | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: adec8a50e6bcf0af25227e2e456f3f76692f6d67
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704186"
---
# <a name="setting-dcom-stream-marshaling-format"></a>Configurar o formato de marshaling de fluxo DCOM
Um computador cliente usando os componentes do RDS 1.5 ou anterior não é compatível com um servidor usando componentes de RDS 2.0 ou posterior. Ao usar DCOM como protocolo subjacente, o suporte para o RDS 2.0 ou posterior é mais eficiente para transportar [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos. Se seu cliente estiver executando componentes do RDS 1.5 ou anterior, você pode definir seu servidor para trabalhar com o suporte RDS anterior (chamado RDS 1.0) ou o suporte mais recente do RDS (chamado RDS 2.0 ou posterior). Defina qualquer uma das entradas do registro a seguir:  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
```console
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS10"  
```  
  
 -ou-  
  
```console
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS20"  
```



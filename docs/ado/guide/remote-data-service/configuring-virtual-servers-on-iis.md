---
description: Configurar servidores virtuais no IIS
title: Configurando servidores virtuais no IIS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- virtual servers in RDS [ADO]
ms.assetid: 2b4786c6-40c4-4ce1-9ad4-03df436e0aff
author: rothja
ms.author: jroth
ms.openlocfilehash: f4e09c5775d87d3339a4965b587828c613ed89fa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452268"
---
# <a name="configuring-virtual-servers-on-iis"></a>Configurar servidores virtuais no IIS
Ao criar servidores virtuais no Serviços de Informações da Internet 4,0, as duas etapas adicionais a seguir são necessárias para configurar o servidor virtual para trabalhar com o RDS:  
  
1.  Ao configurar o servidor, marque "permitir acesso de execução".  
  
2.  Mova msadcs.dll para o *vroot*\msadc, em que o *vroot* é o diretório base do seu servidor virtual.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)



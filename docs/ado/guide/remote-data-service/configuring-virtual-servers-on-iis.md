---
description: Configurar servidores virtuais no IIS
title: Configurando servidores virtuais no IIS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- virtual servers in RDS [ADO]
ms.assetid: 2b4786c6-40c4-4ce1-9ad4-03df436e0aff
author: rothja
ms.author: jroth
ms.openlocfilehash: 53d22155f8e7af894419a28ddf01bf3fe80e34f3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978277"
---
# <a name="configuring-virtual-servers-on-iis"></a>Configurar servidores virtuais no IIS
Ao criar servidores virtuais no Serviços de Informações da Internet 4,0, as duas etapas adicionais a seguir são necessárias para configurar o servidor virtual para trabalhar com o RDS:  
  
1.  Ao configurar o servidor, marque "permitir acesso de execução".  
  
2.  Mova msadcs.dll para o *vroot*\msadc, em que o *vroot* é o diretório base do seu servidor virtual.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos básicos do RDS](./rds-fundamentals.md)
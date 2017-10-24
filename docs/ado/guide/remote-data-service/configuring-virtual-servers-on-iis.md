---
title: Configurando servidores virtuais no IIS | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- virtual servers in RDS [ADO]
ms.assetid: 2b4786c6-40c4-4ce1-9ad4-03df436e0aff
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 10edd98f77c0aaeae05d25e76ad76a15b99bc1ed
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="configuring-virtual-servers-on-iis"></a>Configurando servidores virtuais no IIS
Ao criar servidores virtuais no Internet Information Services 4.0, duas etapas adicionais a seguir são necessárias para configurar o servidor virtual para funcionar com RDS:  
  
1.  Ao configurar o servidor, marque "Permitir acesso de execução".  
  
2.  Mover Msadcs para *vroot*\msadc, onde *vroot* é o diretório base do servidor virtual.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)




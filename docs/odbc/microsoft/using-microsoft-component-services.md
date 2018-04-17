---
title: Usando serviços de componentes da Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], component services
- component services [ODBC]
ms.assetid: 06450562-d8f3-4987-b7bd-4a70223ff937
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 99ef6529d40d626a5f7c2bab97120f4173c8d5d7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="using-microsoft-component-services"></a>Usando serviços de componentes da Microsoft
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Você pode habilitar um banco de dados Oracle trabalhar com serviços de componentes transacionais (ou MTS, se você estiver usando o Windows NT) no Microsoft Windows NT/Windows 2000 e Microsoft Windows 95/98. Para habilitar um banco de dados Oracle trabalhar com serviços de componentes que dão suporte a transações, os administradores do sistema devem criar uma exibição nomeada V$ XATRANS$. Para criar esse script, você deve executar um script fornecido pela Oracle. Para obter mais informações, consulte a Ajuda de serviços de componente ou a documentação do Oracle.

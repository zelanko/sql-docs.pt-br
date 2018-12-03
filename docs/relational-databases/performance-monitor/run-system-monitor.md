---
title: Executar o Monitor do Sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
s.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- System Monitor [SQL Server], running
- Windows System Monitor [SQL Server], running
- remote procedure calls [SQL Server]
- starting Windows NT System Monitor
- RPC
ms.assetid: 05297984-bc8d-43df-829c-032387f7ea61
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9ceac8451a8c1043876efa7025d41d7420ce150d
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52158764"
---
# <a name="run-system-monitor"></a>Executar o Monitor do Sistema
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O Monitor do Sistema usa RPCs (chamadas de procedimento remotas) para coletar informações do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Qualquer usuário com permissões do Microsoft Windows para executar o Monitor do Sistema pode utilizá-lo para monitorar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Ao usar o Monitor do Sistema ou o Monitor de Desempenho, não é possível se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que seja executada em Windows 98.  
  
 Assim como ocorre com toda ferramenta de monitoramento de desempenho, é de se esperar alguma sobrecarga quando se usa o Monitor do Sistema para monitorar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A sobrecarga real em instâncias específicas depende da plataforma de hardware, do número de contadores e do intervalo de atualização selecionado. No entanto, a integração do Monitor do Sistema com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi projetada para minimizar qualquer redução no desempenho.  
  
> [!NOTE]  
>  Se tiver selecionado contadores de desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para monitoramento no snap-in do Monitor do Sistema, você verá os contadores mesmo que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não esteja em execução.  
  
 Para obter informações sobre como iniciar o Monitor do Sistema, consulte [Iniciar o Monitor do Sistema &#40;Windows&#41;](../../relational-databases/performance/start-system-monitor-windows.md).  
  
  

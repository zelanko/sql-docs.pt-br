---
title: Configurar logs de erros do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.configurelogs.configureerrorlogs.f1
ms.assetid: 03f0d463-9b0b-4af9-a853-da936d75e5af
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a4da039e1fcc41570fcead275bbe4b2cb0be5797
ms.sourcegitcommit: 0d89bcaebdf87db3bd26db2ca263be9c671b0220
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2019
ms.locfileid: "68731094"
---
# <a name="scm-services---configure-sql-server-error-logs"></a>Serviços SCM – configurar logs de erros do SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como exibir ou modificar o modo como logs de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são reciclados.  

## <a name="to-open-the-configure-sql-server-error-logs-dialog-box"></a>Para abrir a caixa de diálogo Configurar Logs de Erros do SQL Server  

1. No Pesquisador de Objetos, expanda a instância do SQL Server, expanda **Gerenciamento**, clique com o botão direito do mouse em **Logs do SQL Server**e clique em **Configurar**.

2. Na caixa de diálogo **Configurar Logs de Erros do SQL Server** , escolha uma das opções a seguir.

    A. Contagem de arquivos de log

      **Limite o número dos arquivos de log de erros antes que eles sejam reciclados**

      Verifique e limite o número de logs de erros criados antes que eles sejam reciclados. Um novo log de erros é criado a cada vez que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciada. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retém backups dos seis últimos logs, a não ser que essa opção seja marcada um número máximo diferente de arquivos de log de erros seja especificado, logo abaixo.  
  
      **Número máximo de arquivos de log de erros**

      Especifique o número máximo de arquivos de log de erros criados, antes que eles sejam reciclados. O padrão é 6, que é o número de logs de backup anteriores que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , retém antes de reciclá-los.

    B. Tamanho do arquivo de log

      **Tamanho máximo do arquivo de log de erros em KB**

      Você pode definir o tamanho de cada arquivo em KB. Se você deixar o valor como 0, o tamanho do log será ilimitado.

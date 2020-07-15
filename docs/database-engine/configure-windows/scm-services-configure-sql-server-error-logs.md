---
title: Configurar logs de erros do SQL Server | Microsoft Docs
description: Saiba mais sobre a reciclagem de logs de erros. Confira como definir o tamanho máximo do arquivo de log e como definir o número de arquivos de log anteriores dos quais o SQL Server faz backup e que arquiva.
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 060b3828c772a030ab095ae1bea857dc8eaa3b5a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85651377"
---
# <a name="scm-services---configure-sql-server-error-logs"></a>Serviços SCM – configurar logs de erros do SQL Server

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como exibir ou modificar o modo como logs de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são reciclados.  

## <a name="to-open-the-configure-sql-server-error-logs-dialog-box"></a>Para abrir a caixa de diálogo Configurar Logs de Erros do SQL Server  

1. No Pesquisador de Objetos, expanda a instância do SQL Server, expanda **Gerenciamento**, clique com o botão direito do mouse em **Logs do SQL Server**e clique em **Configurar**.

2. Na caixa de diálogo **Configurar Logs de Erros do SQL Server** , escolha uma das opções a seguir.

    a. Contagem de arquivos de log

      **Limite o número dos arquivos de log de erros antes que eles sejam reciclados**

      Verifique e limite o número de logs de erros criados antes que eles sejam reciclados. Um novo log de erros é criado a cada vez que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciada. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retém backups dos seis últimos logs, a não ser que essa opção seja marcada um número máximo diferente de arquivos de log de erros seja especificado, logo abaixo.  
  
      **Número máximo de arquivos de log de erros**

      Especifique o número máximo de arquivos de log de erros arquivados criados antes de serem reciclados. O padrão é 6, não incluindo o atual. Esse valor determina o número de logs de backup anteriores que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retém antes de reciclá-los.

    b. Tamanho do arquivo de log

      **Tamanho máximo do arquivo de log de erros em KB**

      Você pode definir o tamanho de cada arquivo em KB. Se você deixar o valor como 0, o tamanho do log será ilimitado.

---
title: Validar uma instalação do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- validating installations [SQL Server]
ms.assetid: 1689af50-d2b8-4aa6-8f27-cc7127157fc8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e2a71d127ad565690f78dbbbf8eeffaa13194b2a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178556"
---
# <a name="validate-a-sql-server-installation"></a>Validar uma instalação do SQL Server
  O relatório de descoberta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser usado para verificar a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalados no computador. O **Installed [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relatório de descoberta de recursos** exibe um relatório de todos os [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], e [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] produtos e os recursos são instalados no servidor local. O relatório de descoberta de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está disponível na página **Ferramentas** na Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Para executar o relatório de descoberta de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :**  
  
 Inicie a Central de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o menu **Iniciar**, aponte para **Todos os Programas**, aponte para **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \<Version Name>**, aponte para **Ferramentas de Configuração** e clique em **Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**. Para executar o relatório de descoberta de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], clique em **Ferramentas** na área de navegação esquerda da **Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** e clique em **Relatório de descoberta de recursos instalados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relatório de descoberta é salvo em % ProgramFiles %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< last Setup Session\>.  
  
 Você também pode gerar o relatório de descoberta através da linha de comando. Execute "Setup.exe /Action = RunDiscovery" em um prompt de comando, se você adicionar "/ q" à linha de comando acima nenhuma interface do usuário será mostrada, mas o relatório ainda será criado em % ProgramFiles %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< last Setup Session\>.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e ler arquivos de log da Instalação do SQL Server](view-and-read-sql-server-setup-log-files.md)  
  
  

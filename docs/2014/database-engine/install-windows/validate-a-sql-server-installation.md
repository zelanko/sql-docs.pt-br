---
title: Validar uma instalação do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- validating installations [SQL Server]
ms.assetid: 1689af50-d2b8-4aa6-8f27-cc7127157fc8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8dd4e6ce7800c3a0a9db51f6c1a4bddfe7a188c3
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84931687"
---
# <a name="validate-a-sql-server-installation"></a>Validar uma instalação do SQL Server
  O relatório de descoberta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser usado para verificar a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalados no computador. O ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relatório de descoberta de recursos instalados** exibe um relatório de todos os produtos,,, [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] , e e [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] recursos que estão instalados no servidor local. O relatório de descoberta de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está disponível na página **Ferramentas** na Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Para executar o relatório de descoberta de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :**  
  
 Inicie a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] central de instalação, usando o menu **Iniciar** , aponte para **todos os programas**, ** [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \<Version Name> **aponte para, aponte para **ferramentas de configuração**e clique em ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] centro de instalação**. Para executar o relatório de descoberta de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], clique em **Ferramentas** na área de navegação esquerda da **Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** e clique em **Relatório de descoberta de recursos instalados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** .  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relatório de descoberta é salvo em% ProgramFiles% \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \120\Setup Bootstrap\Log \\<última sessão de instalação \> .  
  
 Você também pode gerar o relatório de descoberta através da linha de comando. Execute "Setup.exe/Action = RunDiscovery" em um prompt de comando se você adicionar "/q" à linha de comando acima, nenhuma interface do usuário será mostrada, mas o relatório ainda será criado em% ProgramFiles% \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \120\Setup Bootstrap\Log \\<última sessão de instalação \> .  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e ler arquivos de log da Instalação do SQL Server](view-and-read-sql-server-setup-log-files.md)  
  
  

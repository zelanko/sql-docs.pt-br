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
manager: craigg
ms.openlocfilehash: 34e4c29cb28f76c930f1f04152528ca1a8a89dfc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62775229"
---
# <a name="validate-a-sql-server-installation"></a>Validar uma instalação do SQL Server
  O relatório de descoberta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser usado para verificar a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalados no computador. O **relatório [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de descoberta de recursos instalados** exibe um relatório de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]todos [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]os [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]produtos [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)],, [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ,, e e recursos que estão instalados no servidor local. O relatório de descoberta de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está disponível na página **Ferramentas** na Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Para executar o relatório de descoberta de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :**  
  
 Inicie a Central de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o menu **Iniciar**, aponte para **Todos os Programas**, aponte para **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \<Nome da Versão>** , aponte para **Ferramentas de Configuração** e clique em **Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** . Para executar o relatório de descoberta de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], clique em **Ferramentas** na área de navegação esquerda da **Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** e clique em **Relatório de descoberta de recursos instalados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** .  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relatório de descoberta é salvo em\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]% ProgramFiles%\\ \120\Setup Bootstrap\Log<última\>sessão de instalação.  
  
 Você também pode gerar o relatório de descoberta através da linha de comando. Execute "setup. exe/Action = RunDiscovery" em um prompt de comando se você adicionar "/q" à linha de comando acima, nenhuma interface do usuário será mostrada, mas o relatório ainda será criado em\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]% ProgramFiles% \120\Setup\\ Bootstrap\Log\><última sessão de instalação.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e ler arquivos de log da Instalação do SQL Server](view-and-read-sql-server-setup-log-files.md)  
  
  

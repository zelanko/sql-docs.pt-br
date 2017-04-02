---
title: "Validar uma instala&#231;&#227;o do SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "validando instalações [SQL Server]"
ms.assetid: 1689af50-d2b8-4aa6-8f27-cc7127157fc8
caps.latest.revision: 31
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 31
---
# Validar uma instala&#231;&#227;o do SQL Server
  O relatório de descoberta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser usado para verificar a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalados no computador. O **Relatório de descoberta de recursos instalados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** exibe um relatório de todos os produtos e recursos do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] que estão instalados no servidor local. O relatório de descoberta de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está disponível na página **Ferramentas** na Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Para executar o relatório de descoberta de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:**  
  
 Inicie a Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], usando o menu **Iniciar**, aponte para **Todos os Programas**, **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \<Nome da Versão>**, **Ferramentas de Configuração** e clique em **Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**. Para executar o relatório de descoberta de recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], clique em **Ferramentas** na área de navegação esquerda da **Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** e clique em **Relatório de descoberta de recursos instalados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**.  
  
 O relatório de descoberta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é salvo em %ProgramFiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<Última Sessão de Instalação\>.  
  
 Você também pode gerar o relatório de descoberta através da linha de comando. Execute“Setup.exe /Action=RunDiscovery” em um prompt de comando. Se você adicionar "/q" à linha de comando acima, nenhuma interface do usuário será mostrada, mas o relatório ainda será criado em %ProgramFiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<Última Sessão de Instalação\>.  
  
## Consulte também  
 [Exibir e ler arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
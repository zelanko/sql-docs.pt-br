---
title: "Instalar atualiza&#231;&#245;es de servi&#231;o do SQL Server 2016 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7d6c962b-c8d0-49f7-a2ac-00ad8dca930a
caps.latest.revision: 13
ms.author: "mikeray"
manager: "jhubbard"
---
# Instalar atualiza&#231;&#245;es de servi&#231;o do SQL Server 2016
  Este tópico fornece informações sobre como instalar atualizações para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Esta seção fornece informações sobre o seguinte:  
  
-   Instalando atualizações para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] durante uma nova instalação  
  
-   Instalando atualizações para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] depois que já tiver sido instalado.  
  
 Nós recomendamos que os clientes avaliem e instalem as atualizações mais recentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o mais rápido possível para ter certeza de que os sistemas estejam atualizados com as atualizações de segurança mais recentes.  
  
## Instalando atualizações para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] durante uma nova instalação  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integra as últimas atualizações de produto com a instalação principal de produto, de forma que o produto principal e suas atualizações aplicáveis sejam instalados ao mesmo tempo. A atualização de produto pode pesquisar as atualizações aplicáveis de:  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update (atualizar)  
  
-   Windows Server Update Services (WSUS)  
  
-   Uma pasta local  
  
-   Um compartilhamento de rede  
  
 Depois que a Instalação localizar as versões mais recentes das atualizações aplicáveis, ela baixará e integrará essas atualizações com o processo de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atual. A Atualização de Produto pode incluir uma atualização cumulativa, service pack ou service pack mais atualização cumulativa.  
  
## Instalando atualizações para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] depois que já tiver sido instalado  
 Em uma instância instalada do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], recomendamos que você aplique as últimas atualizações de segurança e atualizações críticas, incluindo GDRs (versões de distribuição geral), SPs (service packs) e CUs (atualizações cumulativas). Para obter mais informações, consulte o [Comunicado de março de 2016 sobre o ISM (Modelo de Serviços Incremental) do SQL Server](http://blogs.msdn.microsoft.com/sqlreleaseservices/announcing-updates-to-the-sql-server-incremental-servicing-model-ism/). 
  
 As atualizações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão disponíveis com a atualização do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update (MU), o Windows Server Update Services (WSUS) e o Centro de Download da Microsoft. As atualizações de segurança e atualizações críticas para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão disponíveis pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update e, para ver estas atualizações, você precisará optar pelo MU por meio do applet do Windows Update no Painel de Controle.  
  
 Quando você receber uma atualização por meio do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, atualizará todos os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a versão mais recente em um modo autônomo. Se precisar de mais flexibilidade ou não tiver Internet ou acesso WSUS, você precisará obter as atualizações no Centro de Download da [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
## Consulte também  
 [Instalar o SQL Server 2016 por meio do Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md)   
 [Adicionar recursos a uma instância do SQL Server 2016 &#40;instalação&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)   
 [Reparar uma instalação com falha do SQL Server 2016](../../database-engine/install-windows/repair-a-failed-sql-server-2016-installation.md)  
  
  
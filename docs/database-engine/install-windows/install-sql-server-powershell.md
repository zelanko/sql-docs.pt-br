---
title: "Instalar o SQL Server PowerShell | Microsoft Docs"
ms.custom: ""
ms.date: "02/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 854c0b2f-02d2-46a4-a8cc-6b7a5d191cf8
caps.latest.revision: 9
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 9
---
# Instalar o SQL Server PowerShell
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A instalação configura automaticamente os componentes do PowerShell.  
  
## Instalando o suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell  
 Você instala o software que oferece suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao Windows PowerShell usando o programa de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ao selecionar quaisquer recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que exigem suporte do PowerShell, a Instalação instala os seguintes componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell:  
  
-   Snap-ins do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell. Os snap-ins são arquivos dll que implementam dois tipos de suporte do Windows PowerShell ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    -   Conjunto de cmdlets do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os cmdlets são comandos que implementam uma ação específica. Por exemplo, **Invoke-Sqlcmd** executa um script [!INCLUDE[tsql](../../includes/tsql-md.md)] ou XQuery que também pode ser executado usando o utilitário **sqlcmd**, e **Invoke-PolicyEvaluation** relata se os objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cumprem as políticas de gerenciamento baseadas em políticas.  
  
    -   Um provedor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O provedor permite navegar pela hierarquia dos objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um caminho semelhante a um caminho de sistema de arquivos. Cada objeto é associado a uma classe de modelos de objeto de gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Você pode usar os métodos e as propriedades da classe para realizar trabalhos nos objetos. Por exemplo, se você usar cd para um objeto do banco de dados em um caminho, poderá usar os métodos e as propriedades da classe Microsoft.SqlServer.Managment.SMO.Database para gerenciar o banco de dados.  
  
-   O módulo **sqlps**, que é importado para as sessões do Windows PowerShell a fim de carregar os snap-ins do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] dá suporte à inicialização das sessões do Windows PowerShell por meio da árvore do Pesquisador de Objetos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent dá suporte às etapas de trabalho do Windows PowerShell.  
  
 O Windows Server 2012 e posterior e o Windows 8 e posterior são fornecidos com o PowerShell instalado e configurado. Para obter informações sobre como instalar o Windows PowerShell, confira a página [Instalando o Windows PowerShell](http://msdn.microsoft.com/library/hh847837.aspx).  
  
## Consulte também  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
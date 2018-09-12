---
title: Administrar servidores com o SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], servers
- servers [SQL Server], administering
ms.assetid: 938bb035-e07a-4082-9f93-229d9feb6b06
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 883d5b032739c0eafa6f6d68e1e22896ac3720e4
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43819982"
---
# <a name="administer-servers-with-sql-server-management-studio"></a>Gerenciar servidores com o SQL Server Management Studio
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] é um cliente administrativo rico e integrado, projetado para atender a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] requisitos de gerenciamento de servidor do administrador. No [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], as tarefas administrativas são realizadas com o Pesquisador de Objetos, que permite conectar-se a qualquer servidor da família [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e procurar conteúdo de forma gráfica. Um servidor pode ser uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)], do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 Os componentes de ferramentas do [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] incluem os Servidores Registrados, o Pesquisador de Objetos, o Gerenciador de Soluções, o Explorador de Modelos, a página Detalhes do Pesquisador de Objetos e a janela de documentos. Para exibir uma ferramenta, no menu **Exibir** , clique no nome da ferramenta. Para exibir a ferramenta Editor de Consultas, clique no botão **Nova Consulta** na barra de ferramentas.  
  
> [!IMPORTANT]  
>  O tráfego de rede entre o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] e o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não é criptografado por padrão. Não trabalhe com dados confidenciais (inclusive senhas) no [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] a menos que você tenha definido uma conexão criptografada. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 Use o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] para:  
  
-   Servidores registrados.  
  
-   Conectar-se a uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)], do [!INCLUDE[ssAS](../includes/ssas-md.md)], do [!INCLUDE[ssRS](../includes/ssrs.md)] ou do [!INCLUDE[ssIS](../includes/ssis-md.md)].  
  
-   Configurar propriedades de servidor.  
  
-   Gerenciar banco de dados e objetos [!INCLUDE[ssAS](../includes/ssas-md.md)] , como cubos, dimensões e assemblies.  
  
-   Criar objetos, como bancos de dados, tabelas, cubos, usuários de banco de dados e logons.  
  
-   Administrar arquivos e grupos de arquivos.  
  
-   Anexar ou desanexar bancos de dados.  
  
-   Iniciar ferramentas de script.  
  
-   Administrar segurança.  
  
-   Exibir logs do sistema.  
  
-   Monitorar a atividade atual.  
  
-   Configurar replicação.  
  
-   Administrar índices de texto completo.  
  
 Para iniciar e parar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent, use o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager.  
  
## <a name="see-also"></a>Consulte também  
 [Usar o SQL Server Management Studio](../database-engine/use-sql-server-management-studio.md)   
 [Exibir ou alterar as propriedades de servidor &#40;SQL Server&#41;](../database-engine/configure-windows/view-or-change-server-properties-sql-server.md)  
  
  

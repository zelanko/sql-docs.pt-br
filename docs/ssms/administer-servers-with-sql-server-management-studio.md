---
description: Gerenciar servidores com o SQL Server Management Studio
title: Gerenciar servidores com o SQL Server Management Studio
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], servers
- servers [SQL Server], administering
ms.assetid: 938bb035-e07a-4082-9f93-229d9feb6b06
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e22004ab339442cce1e6f09f739ba9f27b867213
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036679"
---
# <a name="administer-servers-with-sql-server-management-studio"></a>Gerenciar servidores com o SQL Server Management Studio
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
O [!INCLUDE[msCoName](../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] é um cliente administrativo avançado e integrado, projetado para cumprir os requisitos de gerenciamento de servidor do administrador do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e do Banco de Dados SQL do Azure. No [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], as tarefas administrativas são realizadas com o Pesquisador de Objetos, que permite conectar-se a qualquer servidor da família [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e procurar conteúdo de forma gráfica. Um servidor pode ser uma instância do [!INCLUDE[ssDE](../includes/ssde_md.md)], do [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)], do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ou do Banco de Dados SQL do Azure.  
  
Os componentes de ferramentas do [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] incluem os Servidores Registrados, o Pesquisador de Objetos, o Gerenciador de Soluções, o Explorador de Modelos, a página Detalhes do Pesquisador de Objetos e a janela de documentos. Para exibir uma ferramenta, no menu **Exibir** , clique no nome da ferramenta. Para exibir a ferramenta Editor de Consultas, clique no botão **Nova Consulta** na barra de ferramentas.  
  
> [!IMPORTANT]  
> O tráfego de rede entre o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] e o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não é criptografado por padrão. Não trabalhe com dados confidenciais (inclusive senhas) no [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] a menos que você tenha definido uma conexão criptografada. Para obter mais informações, veja [Como habilitar conexões criptografadas no Mecanismo de Banco de Dados (SQL Server Configuration Manager)](../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
Use o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] para:  
  
-   Servidores registrados.  
  
-   Conecte-se a uma instância do [!INCLUDE[ssDE](../includes/ssde_md.md)], do SSAS, do [!INCLUDE[ssRS](../includes/ssrs.md)], do [!INCLUDE[ssIS](../includes/ssis_md.md)] ou do Banco de Dados SQL do Azure.  
  
-   Configurar propriedades de servidor.  
  
-   Gerenciar banco de dados e objetos do SAAS, como cubos, dimensões e assemblies.  
  
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
  
## <a name="see-also"></a>Consulte Também  
[Usar o SQL Server Management Studio](./sql-server-management-studio-ssms.md)  
[Como exibir propriedades do servidor (SQL Server Management Studio)](../database-engine/configure-windows/view-or-change-server-properties-sql-server.md)  

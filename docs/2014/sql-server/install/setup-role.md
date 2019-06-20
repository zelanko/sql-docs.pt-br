---
title: Função de instalação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c7e9db15-89f2-4d4d-8860-1e64c5821c4d
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: b1cf8c6f8442fc69669c10106f671040733e48ef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092229"
---
# <a name="setup-role"></a>Função de instalação
  Use esta página para especificar se deseja usar a página de Seleção de Recursos para selecionar recursos individuais ou se deseja instalar usando uma função de instalação.  
  
 Uma `setup role` é uma seleção fixa de todos os recursos e componentes compartilhados que são necessários para implementar uma configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predefinida.  
  
## <a name="options"></a>Opções  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instalação de recurso**  
 Escolha esta opção para selecionar recursos individuais e componentes compartilhados. Os recursos de instância incluem os Serviços de Mecanismo de Banco de Dados, o Analysis Services (modo nativo) e o Reporting Services.  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerPivot para SharePoint**  
 Escolha esta opção para instalar componentes do servidor do Analysis Services em um farm do SharePoint 2010. Esta opção implanta o Serviço de Sistema do PowerPivot e o servidor do Analysis Server em um farm, habilitando o processamento de consultas e dados para pastas de trabalho do Excel publicadas que contenham dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] inseridos.  
  
 Opcionalmente, você poderá adicionar uma instância do mecanismo de banco de dados relacional à sua instalação se precisar hospedar bancos de dados em um farm do SharePoint. Se o farm já estiver configurado, essa opção poderá ser ignorada.  
  
 Após a conclusão da instalação, você deve configurar o software usando uma das seguintes abordagens: Ferramenta de configuração do PowerPivot, cmdlets do PowerShell ou Administração Central do SharePoint 2010. Ao contrário do que acontecia nas versões anteriores, a Instalação não executa mais nenhuma tarefa de configuração para uma instalação do PowerPivot.  
  
 Uma instalação baseada em função não inclui o aplicativo cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerPivot para Excel. O aplicativo cliente é instalado separadamente.  
  
 **Todos os recursos com padrões**  
 Escolha esta função de instalação para instalar todos os recursos que estão disponíveis para esta versão. Observe que o PowerPivot para SharePoint está excluído dessa função. Você deve usar a função de instalação do PowerPivot para SharePoint para instalar esse recurso.  
  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] é configurado para iniciar usando a conta **NT AUTHORITY\NETWORK SERVICE**. O usuário atual será provisionado como membro da função **sysadmin** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os valores definidos por esta opção podem ser substituídos especificando-se parâmetros de linha de comando adicionais.  
  
 Quando o sistema operacional não for um controlador de domínio, por padrão o Mecanismo de Banco de Dados e o Reporting Services usarão a conta NTAUTHORITY\NETWORK SERVICE, o Integration Services usará a conta NTAUTHORITY\NETWORK SERVICE e o Iniciador do Daemon de Filtro de Texto Completo do SQL usará a conta NTAUTHORITY\LOCAL SERVICE.  
  
## <a name="see-also"></a>Consulte também  
 [Instalando o PowerPivot para SharePoint](https://go.microsoft.com/fwlink/?LinkId=206906)   
 [Requisitos de hardware e Software (PowerPivot para SharePoint](https://go.microsoft.com/fwlink/?LinkId=216823)   
 [Seleção de recursos](../../../2014/sql-server/install/feature-selection.md)  
  
  

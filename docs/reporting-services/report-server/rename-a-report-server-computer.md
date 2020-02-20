---
title: Renomear um computador do servidor de relatório | Microsoft Docs
ms.date: 06/19/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- renaming report servers
ms.assetid: 82fc4ba2-291a-4939-a025-271b8d687c54
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b3fe381daf1b89d76d9282f2c1a54c3940a3ffbe
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67314051"
---
# <a name="rename-a-report-server-computer"></a>Renomear um computador de servidor de relatório
  A renomeação de um computador provoca uma alteração de nome correspondente para o servidor Web e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (se estiver no mesmo computador). Em alguns casos, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] talvez não possa ser acessado após uma alteração de nome do computador. Use as etapas fornecidas neste artigo para reconfigurar um servidor de relatório depois de uma alteração de nome do computador.  
  
## <a name="renaming-a-sql-server-database-engine"></a>Renomeando um Mecanismo de Banco de Dados do SQL Server  
 Se você renomear a instância do  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que executa o banco de dados do servidor de relatório, faça o seguinte:  
  
1.  Inicie a ferramenta Configuração do Reporting Services e conecte-se ao servidor de relatório que usa o banco de dados do servidor de relatório no servidor renomeado.  
  
2.  Abra a página Configuração do Banco de Dados.  
  
3.  Em **Nome do Servidor**, digite ou selecione o nome do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, em seguida, clique em **Conectar**.  
  
4.  Clique em **Aplicar**.  
  
 Se o servidor de relatório estiver usando uma instância local do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , use *(local)* ou *(local)\nomedainstância* para especificar o servidor. Se você usar *(local)* para fazer referência ao servidor, poderá renomear o servidor e as conexões continuarão funcionando. Caso esteja usando um servidor remoto ou o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] seja configurado com o nome do servidor, atualize as informações de conexão do banco de dados sempre que o nome do servidor for alterado.  
  
## <a name="renaming-a-report-server-computer"></a>Renomeando um computador de servidor de relatório  
 Se você renomear um computador que executa um servidor de relatório, faça o seguinte:  
  
1.  Abra RSReportServer.config em um editor de texto e modifique a configuração **UrlRoot** para refletir o novo nome do servidor. A configuração **UrlRoot** é usada pelas extensões de entrega para compor o URL usado para acessar itens armazenados no servidor de relatório. A alteração do endereço URL do servidor de relatório requer a atualização da configuração **UrlRoot** para que as assinaturas continuem a entregar os relatórios conforme o esperado.  
  
2.  No mesmo arquivo, se estiver definida, modifique a configuração **ReportServerUrl** para refletir o novo nome do servidor. Esta configuração não é usada em todas as instalações. Se estiver vazio, não faça nada.  
  
    > [!NOTE]  
    >  Se você estiver usando o WINS (Serviço de Cadastramento na Internet do Windows) na rede corporativa, o servidor de relatório e o portal da Web podem continuar disponíveis com o nome anterior por um período de tempo. O WINS mapeia um endereço IP para cada computador ao qual oferece suporte. Quando o WINS atualiza o endereço IP do computador renomeado, o nome antigo do computador não pode ser mais usado para acessar o servidor de relatório ou o portal da Web.  
  
## <a name="see-also"></a>Confira também  
 [Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Servidor de relatório do Reporting Services &#40;Modo Nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Iniciar e parar o serviço Servidor de Relatório](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)   
 [Utilitário rsconfig &#40;SSRS&#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md)  
  
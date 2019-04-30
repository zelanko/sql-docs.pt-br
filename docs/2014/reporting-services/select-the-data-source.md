---
title: Selecione a fonte de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptwizard.selectdatasource.f1
ms.assetid: cdd84ad8-7c6a-41ac-bf51-1b0973434829
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d2823ad2eefd8855ba5e6ebd706e99271d30da0a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63223305"
---
# <a name="select-the-data-source"></a>Selecionar a fonte de dados
  Use esta página do Assistente de Relatório para definir uma fonte de dados para o relatório.  
  
## <a name="options"></a>Opções  
 **fonte de dados compartilhada**  
 Selecione **Fonte de Dados Compartilhada** para usar uma fonte de dados compartilhada predefinida que já tenha as informações de conexão da fonte de dados que você deseja usar. A lista contém todas as fontes de dados compartilhadas incluídas no projeto.  
  
 **Nova fonte de dados**  
 Selecione **Nova fonte de dados** para definir uma nova fonte de dados. A informações da fonte de dados só será usada com o relatório atual.  
  
 **Nome**  
 Digite um nome para a conexão à fonte de dados. O nome da fonte de dados deve ser exclusivo no relatório.  
  
 **Tipo**  
 Selecione o tipo de fonte de dados que você está usando (por exemplo, se você estiver usando um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , escolha [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]).  
  
 **Cadeia de conexão**  
 Digite uma cadeia de conexão para a fonte de dados. Para obter mais informações sobre cadeias de caracteres de conexão, consulte [conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 Clique em **Editar** para especificar o servidor da fonte de dados na caixa de diálogo **Propriedades de Conexão** . Você pode especificar uma fonte de dados locais ou remotos.  
  
 Clique em **Credenciais** para fornecer credenciais de banco de dados. A um mínimo, os credenciais que você especifica devem ser suficientes para você se conectar à fonte de dados para propósitos de design de relatório. Quando o relatório é implantado em um servidor de relatório, os credenciais de banco de dados devem acomodar todos os usuários do relatório. Por exemplo, se você desejar que todos os usuários de relatório se conectem à fonte de dados usando seus credenciais, escolha **Usar Autenticação do Windows (Segurança Integrada)**. Os credenciais que você especifica devem ser válidos para a fonte de dados; portanto, se você escolher Autenticação do Windows, verifique se a fonte de dados aceita conexões de todas as contas de usuário que executarão o relatório. Os credenciais de bancos de dados podem ser gerenciados separadamente do relatório. Para obter mais informações, consulte [Gerenciar uma fonte de dados de relatório](report-data/manage-report-data-sources.md).  
  
 **Tornar esta fonte de dados compartilhados**  
 Selecione esta opção para armazenar a fonte de dados no projeto como uma fonte de dados compartilhada, em vez de armazenar no relatório. Dessa maneira, você pode usá-la como a fonte de dados para outros relatórios no projeto.  
  
## <a name="see-also"></a>Consulte também  
 [Conexões de dados ou fontes de dados inseridas e compartilhadas &#40;Construtor de Relatórios e SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [Especificar informações de credenciais e de conexão para fontes de dados de relatório](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Servidor de Relatório do Reporting Services](../../2014/reporting-services/reporting-services-report-server.md)   
 [Arquivo de configuração RSReportDesigner](report-server/rsreportdesigner-configuration-file.md)   
 [Conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Ajuda do Assistente de Relatório](../../2014/reporting-services/report-wizard-help.md)  
  
  

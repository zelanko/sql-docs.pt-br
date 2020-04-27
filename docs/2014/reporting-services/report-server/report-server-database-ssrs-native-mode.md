---
title: Banco de dados do servidor de relatório (modo nativo do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- databases [Reporting Services]
- report servers [Reporting Services], databases
- temporary databases [Reporting Services]
- report server database
- reportservertempdb
- reportserver database
ms.assetid: 0fc5c033-3fe1-4cea-86c7-66ea5e424d65
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5e5f5225ef696a5477ef9d0aa4a67749bc5e4a88
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66103450"
---
# <a name="report-server-database-ssrs-native-mode"></a>Banco de dados do servidor relatório (modo nativo do SSRS)
  Um servidor de relatório é um servidor sem estado que usa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] para armazenar definições de objeto e metadados. Uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo nativo usa dois bancos de dados para separar os requisitos de armazenamento de dados persistente do armazenamento de dados temporário. Os bancos de dados são criados juntamente e associados por nome. Por padrão, os nomes do banco de dados são **reportserver** e **reportservertempdb**, respectivamente.  
  
 Uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint também criará um banco de dados para obter os recursos de alerta de dados. Os três bancos de dados no modo do SharePoint estão associados a aplicativos de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, veja [Gerenciar um aplicativo de serviço SharePoint do Reporting Services](../manage-a-reporting-services-sharepoint-service-application.md)  
  
 Os bancos de dados podem ser executados em uma instância local ou remota do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . A instância local será útil se você tiver recursos de sistema suficientes ou se desejar manter as licenças de software, mas a execução dos bancos de dados em um computador remoto pode melhorar o desempenho.  
  
 Você pode optar por uma porta ou reutilizar um banco de dados do servidor de relatórios existente da instalação anterior ou uma instância diferente com outra instância do servidor de relatórios. O esquema do banco de dados do servidor de relatórios deve ser compatível com a instância do servidor de relatórios. Se o banco de dados estiver em um formato anterior, será solicitada a atualização para o formato atual. Não é possível executar o downgrade das versões mais novas para uma versão mais antiga. Se você tiver um banco de dados do servidor de relatórios, não poderá usá-lo com uma versão anterior de instâncias do servidor de relatórios. Para obter mais informações sobre os bancos de dados do servidor de relatório são atualizados para formatos mais novos, consulte [Atualizar um banco de dados do servidor de relatório](../install-windows/upgrade-a-report-server-database.md).  
  
> [!IMPORTANT]  
>  A estrutura de tabelas dos bancos de dados é otimizada para operações de servidor e não deve ser modificada ou ajustada. [!INCLUDE[msCoName](../../includes/msconame-md.md)] pode alterar a estrutura da tabela de uma versão para a próxima. Se você modificar ou estender o banco de dados, poderá limitar ou impedir a capacidade de desenvolvimento de futuras atualizações ou aplicar service packs. Você também corre o risco de fazer alterações que prejudiquem as operações do servidor de relatórios. Por exemplo, se você ativar o READ_COMMITTED_SNAPSHOT no banco de dados do ReportServer, quebrará o recurso de classificação interativo.  
  
 Todos os acessos a um banco de dados do servidor de relatórios devem ser controlados pelo servidor de relatórios. Para acessar o conteúdo em um banco de dados do servidor de relatório, você pode usar as ferramentas de gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]servidor de relatório (como Report Manager e) ou interfaces programáticas, como acesso à URL, serviço Web do servidor de relatório ou o provedor de instrumentação de gerenciamento do Windows (WMI).  
  
 A conexão com o banco de dados do servidor de relatório normalmente é definida por meio da ferramenta Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Entretanto, ela poderá ser definida durante a instalação se você escolher instalar a configuração padrão. Para obter mais informações sobre a conexão do servidor de relatório ao banco de dados, consulte [Configurar uma conexão de banco de dados do servidor de relatório &#40;Gerenciador de Configurações do SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
## <a name="report-server-database"></a>banco de dados do servidor de relatório  
 O banco de dados do servidor de relatório é um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que armazena o seguinte conteúdo:  
  
-   Itens gerenciados por um servidor de relatório (.. /Reports e relatórios vinculados, fontes de dados compartilhadas, modelos de relatório, pastas, recursos) e todas as propriedades e configurações de segurança associadas a esses itens.  
  
-   Assinatura e definições de agendamento.  
  
-   Instantâneos (que incluem resultados de consulta) e históricos de relatórios.  
  
-   Propriedades do sistema e configurações de segurança no nível de sistema.  
  
-   Dados do log de execução do relatório.  
  
-   Chaves simétricas e conexão criptografada e credenciais para fontes de dados de relatório.  
  
 Como o servidor de relatórios armazena dados persistentes e o estado do aplicativo, é preciso criar um agendamento de backup do banco de dados para evitar a perda de dados. Para obter recomendações e instruções sobre como fazer backup do banco de dados, consulte [Movendo os bancos de dados do Servidor de Relatório para outro computador &#40;modo nativo do SSRS&#41;](moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
## <a name="report-server-temporary-database"></a>Banco de dados temporário do servidor de relatórios  
 Todo banco de dados do servidor de relatórios usa um banco de dados temporário relacionado para armazenar dados de execução e sessão, relatórios em cache e tabelas de trabalho gerados pelo servidor de relatórios. Processos do servidor em segundo plano removerão periodicamente itens mais antigos e não usados das tabelas do banco de dados temporário.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não recria o banco de dados temporário se ele está ausente nem repara tabelas ausentes ou modificadas. Embora o banco de dados temporário não contenha dados persistentes, ainda assim é preciso fazer backup do banco de dados para evitar a necessidade de recriá-lo como parte de uma operação de recuperação de falha.  
  
 Se você fizer backup do banco de dados temporário e, em seguida, restaurá-lo, será preciso excluir o conteúdo. Geralmente, a exclusão do conteúdo do banco de dados temporário é segura e pode ser feita a qualquer momento. Entretanto, é preciso reiniciar o serviço Servidor de Relatórios do Windows após a exclusão do conteúdo.  
  
## <a name="see-also"></a>Consulte Também  
 [Hospedar um banco de dados do servidor de relatório em um cluster de failover do SQL Server](../install-windows/host-a-report-server-database-in-a-sql-server-failover-cluster.md)   
 [Armazenar dados criptografados do servidor de relatório &#40;Configuration Manager do SSRS&#41;](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Servidor de Relatório do Reporting Services](../reporting-services-report-server.md)   
 [Administrar um banco de dados do Servidor de Relatório &#40;modo nativo do SSRS&#41;](report-server-database-ssrs-native-mode.md)   
 [Criar um banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)   
 [Operações de backup e restauração para o Reporting Services](../install-windows/backup-and-restore-operations-for-reporting-services.md)  
  
  

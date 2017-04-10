---
title: "Recursos do Reporting Services com suporte nas edi&#231;&#245;es do SQL Server 2016 | Microsoft Docs"
ms.custom: ""
ms.date: "09/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
  - "reporting-services-sharepoint"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: 39f03d2d-6e48-4b34-a9d3-07f86313b937
caps.latest.revision: 3
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 3
---
# Recursos do Reporting Services com suporte nas edi&#231;&#245;es do SQL Server 2016
Esse tópico fornece detalhes dos recursos que têm suporte na diferentes edições do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
 A edição Evaluation do SQL Server está disponível por um período de avaliação de 180 dias.  
  
 Para obter as notas de versão mais recentes, confira [SQL Server 2016 Release Notes](../sql-server/sql-server-2016-release-notes.md). Para obter as últimas informações sobre as novidades, consulte [Novidades no SSRS (Reporting Services)](What's%20New%20in%20Reporting%20Services%20\(SSRS\).md).
    
 **Experimente o SQL Server 2016!**    
    
 > [![Baixar no Centro de Avaliação](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[Baixar o SQL Server 2016 no Centro de Avaliação](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![A máquina virtual pequena do Azure](../analysis-services/media/azure-virtual-machine-small.png) **[Criar uma máquina virtual com o SQL Server 2016 já instalado](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)**    

Para saber quais recursos têm suporte nas edições Evaluation e Developer, consulte SQL Server Enterprise Edition.

Para navegar até a tabela de uma tecnologia do SQL Server, clique no respectivo link:  

-   [Reporting Services](#SSRS)  
  
-   [Clientes de Business Intelligence](#BIC)  

##  <a name="SSRS"></a> Reporting Services  
  
|Nome do recurso|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Desenvolvedor|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Relatórios móveis e KPIs|Sim||||||Sim|  
|Banco de dados de catálogo com suporte - [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] edition|Standard ou superior|Standard ou superior|Web|Express|||Standard ou superior|  
|Fonte de dados com suporte - [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] edition|Todas as edições do   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Web|Express|||Todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|  
|Servidor de relatório|Sim|Sim|Sim|Sim|||Sim|  
|Designer de Relatórios|Sim|Sim|Sim|Sim|||Sim|  
|Portal da Web do Designer de Relatórios|Sim|Sim|Sim|Sim|||Sim|  
|Segurança baseada em função|Sim|Sim|Sim|Sim|||Sim|  
|Exportar para Excel, Power Point, Word, PDF e imagens|Sim|Sim|Sim|Sim|||Sim|  
|Gráficos e medidores aprimorados|Sim|Sim|Sim|Sim|||Sim|  
|Fixar itens de relatório em [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]painéis|Sim|Sim|Sim|Sim|||Sim|  
|Autenticação personalizada|Sim|Sim|Sim|Sim|||Sim|  
|Relatar como feeds de dados|Sim|Sim|Sim|Sim|||Sim|  
|Suporte a modelo|Sim|Sim|Sim||||Sim|  
|Criar funções personalizadas para segurança baseada em função|Sim|Sim|||||Sim|  
|Segurança de item de modelo|Sim|Sim|||||Sim|  
|Clickthrough infinito|Sim|Sim|||||Sim|  
|Biblioteca de componentes compartilhados|Sim|Sim|||||Sim|  
|Agendamento e assinaturas de email e compartilhamento de arquivos|Sim|Sim|||||Sim|  
|Histórico de relatórios, execução de instantâneos e armazenamento em cache|Sim|Sim|||||Sim|  
|Integração do SharePoint|Sim|Sim|||||Sim|  
|Suporte de fonte de dados remota e não SQL<sup>1</sup>|Sim|Sim|||||Sim|  
|Extensibilidade RDCE de fonte de dados, entrega e renderização|Sim|Sim|||||Sim|  
|Identidade visual personalizada|Sim||||||Sim|  
|Assinatura de relatórios controladas por dados|Sim||||||Sim|  
|Implantação em expansão (Web farms)|Sim||||||Sim|  
|Alerta<sup>2</sup>|Sim||||||Sim|  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] <sup>2</sup>|Sim||||||Sim|  
  
 <sup>1</sup> Para obter mais informações sobre as fontes de dados com suporte no SSRS (SQL Server 2016 Reporting Services), consulte [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
 <sup>2</sup> Exige o Reporting Services no modo do SharePoint. Para obter mais informações, veja [Instalar o Reporting Services no modo do SharePoint](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).  
  
## Requisitos das edições do servidor de banco de dados do servidor de relatório  
 Na criação de um banco de dados de servidor de relatório, nem todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] podem ser usadas para hospedar o banco de dados. A tabela a seguir mostra quais edições do [!INCLUDE[ssDE](../includes/ssde-md.md)] podem ser usadas para edições específicas do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
|Para esta edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services|Use esta edição da instância do Mecanismo de Banco de Dados para hospedar o banco de dados|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|Edições Enterprise ou Standard (local ou remota)|  
|Standard|Edições Enterprise ou Standard (local ou remota)|  
|Web|Web Edition (apenas localmente)|  
|Express with Advanced Services|Express with Advanced Services (apenas local).|  
|Evaluation|Evaluation|  
  
##  <a name="BIC"></a> Clientes de Business Intelligence  
 Os aplicativos cliente de software a seguir estão disponíveis no Centro de Download da Microsoft e são fornecidos para ajudar a criar documentos de Business Intelligence executados em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Quando esses documentos forem hospedados em um ambiente de servidor, use uma edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que dê suporte para esse tipo de documento. A tabela a seguir identifica qual edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] contém os recursos de servidor necessários para hospedar os documentos criados nesses aplicativos cliente.  
  
|Nome da ferramenta|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Desenvolvedor|  
|---------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion-md.md)] (.rdl e .rds)|Sim|Sim|||||Sim|  
|[!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long-md.md)] (.rsmobile)|Sim||||||Sim|  
|Aplicativos do Power BI para dispositivos móveis (iOS, Windows 10, Android) (.rsmobile)|Sim||||||Sim|  
  
> [!NOTE]  
> 1.  A tabela acima identifica as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] necessárias para habilitar essas ferramentas cliente; no entanto, essas ferramentas podem acessar os dados hospedados em qualquer edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
> 2.  [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long-md.md)] é o único ponto de criação de relatórios móveis. Conecte-se a um servidor do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para acessar fontes de dados e criar relatórios. Em seguida, publique-os no servidor do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para que outras pessoas da organização possam acessá-los, no servidor ou em dispositivos móveis. Você também pode usar o [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long-md.md)] autônomo com fontes de dados locais  
> 3.  Se estiver usando o [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] local, o [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] na nuvem ou ambos como sua solução de entrega de relatórios, você precisará apenas de um aplicativo móvel para acessar painéis e relatórios móveis em dispositivos móveis. Os aplicativos [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] estão disponíveis para download nas lojas de aplicativos do Windows, iOS ou Android.  

## Consulte também  
 [Recursos com suporte nas edições do SQL Server 2016](Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
 [Especificações do produto para SQL Server 2016](../Topic/Product%20Specifications%20for%20SQL%20Server%202016.md)   
 [Instalação do SQL Server 2016](../database-engine/install-windows/installation-for-sql-server-2016.md) 
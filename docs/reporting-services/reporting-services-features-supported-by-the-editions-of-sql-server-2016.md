---
title: Recursos compatíveis com diferentes edições – SQL Server Reporting Services | Microsoft Docs
description: Esse tópico explica os recursos do SQL Server Reporting Services (SSRS) que têm suporte nas diferentes edições do SQL Server. A edição Evaluation do SQL Server está disponível por um período de avaliação de 180 dias.
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.date: 12/16/2019
ms.openlocfilehash: 96fe1480deed7dad420687b5b3b08a3ea8da2ffd
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "76516597"
---
# <a name="sql-server-reporting-services-features-supported-by-editions"></a>Recursos do SQL Server Reporting Services compatíveis com as edições

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Esse tópico explica os recursos do SQL Server Reporting Services (SSRS) que têm suporte nas diferentes edições do SQL Server. A edição Evaluation do SQL Server está disponível por um período de avaliação de 180 dias.  

## <a name="related-links"></a>Links relacionados
  
 - [Notas sobre a versão do SSRS (SQL Server Reporting Services)](release-notes-reporting-services.md). 
 - [Novidades do SSRS (SQL Server Reporting Services)](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md).
 - [Recursos compatíveis com as edições do SQL Server](~/sql-server/editions-and-components-of-sql-server-version-15.md)

##  <a name="SSRS"></a> SQL Server Reporting Services  

Para saber quais recursos têm suporte nas edições Evaluation e Developer, confira a coluna SQL Server Enterprise Edition na tabela a seguir.

|Nome do recurso|Enterprise|Standard|Web|Express with Advanced Services|Desenvolvedor|  
|------|---------|---------------|-----------|-------|---------|  
| Relatórios do Power BI e pastas de trabalho do Excel | Sim, com o Software Assurance | | | | Sim |
|Relatórios móveis e análises|Sim||||Sim|  
|Edição [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] do banco de dados de catálogo com suporte|Standard ou superior|Standard ou superior|Web|Express|Standard ou superior|  
|Fonte de dados com suporte - [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] edition|Todas as edições do   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Web|Express|Todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|  
|Servidor de relatório|Sim|Sim|Sim|Sim|Sim|  
|Designer de Relatórios|Sim|Sim|Sim|Sim|Sim|  
|Portal da Web do Designer de Relatórios|Sim|Sim|Sim|Sim|Sim|  
|Segurança baseada em função|Sim|Sim|Sim|Sim|Sim|  
|Exportar para Excel, Power Point, Word, PDF e imagens|Sim|Sim|Sim|Sim|Sim|  
|Gráficos e medidores aprimorados|Sim|Sim|Sim|Sim|Sim|  
|Fixar itens de relatório a painéis [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]|Sim|Sim|Sim|Sim|Sim|  
|Autenticação personalizada|Sim|Sim|Sim||Sim|  
|Relatar como feeds de dados|Sim|Sim|Sim|Sim|Sim|  
|Suporte a modelo|Sim|Sim|Sim||Sim|  
|Criar funções personalizadas para segurança baseada em função|Sim|Sim|||Sim|  
|Segurança de item de modelo|Sim|Sim|||Sim|  
|Clickthrough infinito|Sim|Sim|||Sim|  
|Biblioteca de componentes compartilhados|Sim|Sim|||Sim|  
|Agendamento e assinaturas de email e compartilhamento de arquivos|Sim|Sim|||Sim|  
|Histórico de relatórios, instantâneos de execução e armazenamento em cache|Sim|Sim|||Sim|  
|Integração do SharePoint<sup>2</sup>|Sim|Sim|||Sim|  
|Suporte de fonte de dados remota e não SQL<sup>1</sup>|Sim|Sim|||Sim|  
|Extensibilidade de RDCE e fonte de dados, entrega e renderização|Sim|Sim|||Sim|  
|Identidade visual personalizada|Sim||||Sim|  
|Inscrição no relatório orientada por dados|Sim||||Sim|  
|Implantação escalável (web farms)|Sim||||Sim|  
|Alerta<sup>2</sup> (SSRS 2016) |Sim||||Sim|  
|Power View<sup>2</sup> (SSRS 2016) |Sim||||Sim| 
|Comentários<sup>3</sup> |Sim|Sim|Sim|Sim|Sim|  

 <sup>1</sup> Confira mais informações sobre as fontes de dados com suporte no SSRS (SQL Server Reporting Services) em [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
 <sup>2</sup> Exige o Reporting Services do SQL Server 2016 no modo do SharePoint. Confira mais informações em [Instalar o SQL Server Reporting Services no modo do SharePoint](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md). A integração do Reporting Services ao SharePoint não está mais disponível a partir do SQL Server 2017. 

<sup>3</sup> Apenas no Servidor de Relatórios do Power BI e no Reporting Services do SQL Server 2017 e posterior.

> [!NOTE]
> SQL Server Express com Tools e SQL Server Express não dão suporte a SQL Server Reporting Services.
  
## <a name="edition-requirements-for-the-report-server-database"></a>Requisitos de edição do banco de dados do servidor de relatório
 Quando você cria um banco de dados de servidor de relatório, nem todas as edições do SQL Server [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] podem ser usadas para hospedar o banco de dados. A tabela a seguir mostra quais edições do [!INCLUDE[ssDE](../includes/ssde-md.md)] podem ser usadas para edições específicas do SQL Server [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
|Para esta edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services,|use esta edição da instância do Mecanismo de Banco de Dados para hospedar o banco de dados.|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|Edições Enterprise ou Standard (local ou remota)|  
|Standard|Edições Enterprise ou Standard (local ou remota)|  
|Web|Web Edition (apenas localmente)|  
|Express with Advanced Services|Express with Advanced Services (apenas local)|  
|Avaliação|Avaliação|  
  
##  <a name="BIC"></a> Clientes de business intelligence  
Os seguintes aplicativos cliente de software estão disponíveis no Microsoft Download Center. Eles ajudam a criar documentos de business intelligence que são executados em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Quando esses documentos forem hospedados em um ambiente de servidor, use uma edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que dê suporte para esse tipo de documento. A tabela a seguir identifica qual edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] contém os recursos de servidor necessários para hospedar os documentos criados nesses aplicativos cliente.  
  
|Nome da ferramenta|Enterprise|Standard|Web|Express with Advanced Services|Desenvolvedor|  
|---------------|----------------|--------------|------------------------|-------------|---------------| 
| Power BI Desktop otimizado para o Servidor de Relatórios do Power BI, **.pbix** | Sim, com o Software Assurance | | | | Sim |
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)], **.rdl** e **.rds**|Sim|Sim|Sim|Sim|Sim|  
|[!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)], **.rsmobile**|Sim||||Sim|  
|Aplicativos do Power BI para dispositivos móveis (iOS, Windows 10 e Android), **.rsmobile**|Sim||||Sim|  
  
> [!NOTE]  
> * A tabela anterior identifica as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que são necessárias para habilitar essas ferramentas de cliente. No entanto, essas ferramentas podem acessar os dados hospedados em qualquer edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
> * [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] é o único ponto de criação de relatórios móveis. Conecte-se a um servidor do SSRS para acessar fontes de dados e criar relatórios. Em seguida, publique-os no servidor do SSRS para que outras pessoas da organização possam acessá-los, no servidor ou em dispositivos móveis. Você também pode usar o [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] autônomo com fontes de dados locais.  
> * Se você usar o [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] local, o [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] na nuvem ou ambos como sua solução de entrega de relatórios, você precisará apenas de um aplicativo móvel para acessar painéis e relatórios móveis em dispositivos móveis. Os aplicativos [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] estão disponíveis para download nas lojas de aplicativos do Windows, iOS ou Android.  

## <a name="next-steps"></a>Próximas etapas

* Leia sobre os [Recursos compatíveis com as edições do SQL Server 2017](~/sql-server/editions-and-components-of-sql-server-2017.md). 

* [Planejar uma instalação do SQL Server](../sql-server/install/planning-a-sql-server-installation.md).

* Mais perguntas? Faça uma pergunta no [Fórum do SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).

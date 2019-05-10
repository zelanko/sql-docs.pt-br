---
title: Introdução ao Data Quality Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
helpviewer_keywords:
- Domains
ms.assetid: 5350214c-7333-41d0-ae83-1b7d8454ebec
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3c5898910a5280e797080c99fde978bb3da1c3c6
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65484211"
---
# <a name="introduction-to-data-quality-services"></a>Introdução ao Data Quality Services
  A solução de qualidade de dados fornecida pelo [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) permite que um administrador de dados ou profissional de TI mantenha a qualidade de seus dados e assegure que os dados sejam adequados para uso comercial. O DQS é uma solução controlada por conhecimento que fornece maneiras assistidas por computador e interativas para gerenciar a integridade e a qualidade de suas fontes de dados. O DQS permite descobrir, compilar e gerenciar conhecimento sobre seus dados. Você pode usar esse conhecimento para executar a limpeza, a correspondência e a criação de perfil de dados. Você também pode aproveitar os serviços baseados em nuvem de provedores de dados de referência em um projeto de qualidade de dados do DQS.  
  
##  <a name="BusinessNeed"></a> A necessidade comercial do DQS  
 Dados incorretos podem resultar de erros de entrada de usuário, dano durante a transmissão ou armazenamento, definições incompatíveis de dicionários de dados e outros problemas de qualidade de dados e processos. Agregar dados de origens diferentes que usam padrões de dados diferentes pode resultar em dados inconsistentes, pois pode aplicar uma regra arbitrária ou sobrescrever dados históricos. Dados incorretos afetam a capacidade de uma empresa de executar suas funções comerciais e de fornecer serviços aos seus clientes, o que resulta em perda de credibilidade e receita, insatisfação de clientes e problemas de conformidade. Geralmente, os sistemas automatizados não funcionam com dados incorretos, que desperdiçam tempo e energia das pessoas que executam processos manuais. Dados incorretos podem causar confusão com análise de dados, relatórios, mineração de dados e armazenamento.  
  
 Dados de alta qualidade são imprescindíveis para a eficiência de empresas e instituições. Uma organização de qualquer porte pode usar o DQS para aumentar o valor de informações de seus dados, tornando-os mais adequados para sua finalidade. Uma solução de qualidade de dados pode tornar os dados mais confiáveis, acessíveis e reutilizáveis. Pode melhorar a perfeição, exatidão, conformidade e consistência de seus dados, resolvendo problemas causados por dados incorretos em cargas de trabalho de business intelligence ou de data warehouse, bem como em sistemas OLTP operacionais.  
  
 O DQS permite que o usuário de uma empresa, um profissional da informação ou de TI, que não seja um especialista em banco de dados nem um programador, crie, mantenha e execute as operações de qualidade de dados de suas organizações com tempo mínimo de instalação e preparação.  
  
##  <a name="Answer"></a> Atendendo à necessidade com o DQS  
 A qualidade de dados não é definida em termos absolutos. Ela depende de os dados serem adequados ou não à sua finalidade. O DQS identifica dados possivelmente incorretos e fornece uma avaliação da probabilidade de os dados estarem de fato incorretos. O DQS fornece uma noção semântica dos dados para que você possa decidir sua adequação. O DQS permite resolver problemas que envolvem incompletude, falta de conformidade, inconsistência, imprecisão, invalidade e duplicação de dados.  
  
 O DQS fornece os recursos a seguir para resolver problemas de qualidade de dados.  
  
-   **Limpeza de Dados:** modificação, remoção ou enriquecimento de dados incorretos ou incompletos, usando processos auxiliados por computador e interativos. Para obter mais informações, consulte [Data Cleansing](../../2014/data-quality-services/data-cleansing.md).  
  
-   **Correspondência:** a identificação de duplicatas semânticas em um processo baseado em regras que lhe permite determinar o que constitui uma correspondência e eliminar a duplicação. Para obter mais informações, consulte [Data Matching](../../2014/data-quality-services/data-matching.md).  
  
-   **Serviços de Dados de Referência :** verificação da qualidade de seus dados usando os serviços de um provedor de dados de referência. Você pode usar os serviços de dados de referência do Windows Azure Marketplace DataMarket para limpar, validar, corresponder e enriquecer dados facilmente. Para obter mais informações, consulte [Reference Data Services in DQS](../../2014/data-quality-services/reference-data-services-in-dqs.md).  
  
-   **Criação de Perfil:** análise de uma fonte de dados para fornecer uma perspectiva da qualidade dos dados em todas as fases da descoberta de conhecimento, do gerenciamento de domínio, da correspondência e dos processos de limpeza de dados. Criação de Perfil é uma ferramenta avançada de uma solução de qualidade de dados do DQS. Você pode criar uma solução de qualidade de dados em que a criação de perfil seja tão importante quanto o gerenciamento de conhecimento, a correspondência ou a limpeza de dados. Para obter mais informações, consulte [Data Profiling and Notifications in DQS](../../2014/data-quality-services/data-profiling-and-notifications-in-dqs.md).  
  
-   **Monitoramento:** acompanhamento e determinação do estado de atividades de qualidade de dados. O monitorando permite verificar se sua solução de qualidade de dados está se comportando conforme o esperado. Para obter mais informações, consulte [DQS Administration](../../2014/data-quality-services/dqs-administration.md).  
  
-   **Base de Dados de Conhecimento:** o Data Quality Services é uma solução controlada por conhecimento que analisa dados com base no conhecimento criado com o DQS. Isso permite criar processos de qualidade de dados que aprimoram continuamente o conhecimento sobre seus dados e, consequentemente, aprimoram continuamente a qualidade de seus dados.  
  
 A ilustração a seguir mostra o processo do DQS:  
  
 ![Processo do DQS](../../2014/data-quality-services/media/dqs-process.gif "DQS Process")  
  
##  <a name="KnowledgeDrivenSolution"></a> Uma solução controlada por conhecimento  
 A base de dados de conhecimento do DQS é um repositório de três tipos de conhecimento: conhecimento pronto para uso, conhecimento gerado pelo [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]e conhecimento gerado pelo usuário. O DQS permite armazenar conhecimento sobre seus dados na base de dados de conhecimento, adicionar regras de negócio e modificar o conhecimento conforme você considerar adequado e, depois, aplicá-lo para testar a integridade e a exatidão dos dados. Depois de compilar a base de dados de conhecimento, você pode melhorá-la continuamente e reutilizá-la em vários processos de melhoria da qualidade de dados.  
  
 O conhecimento em uma base de dados de conhecimento identifica dados potencialmente incorretos e propõe alterações nos dados. Com isso, é possível localizar correspondências de dados, permitindo eliminar a duplicação de dados. É possível comparar os dados de origem com os dados de referência baseados em nuvem mantidos e garantidos por provedores de qualidade de dados. O administrador de dados ou o profissional de TI verifica o conhecimento na base de dados de conhecimento e as alterações a serem feitas nos dados, e executa a limpeza, a remoção de duplicação e serviços de dados de referência.  
  
 Uma base de dados de conhecimento armazena todo o conhecimento relacionado a um tipo específico de fonte de dados. Por exemplo, você poderia manter uma base de dados de conhecimento para um banco de dados de clientes e outra base de dados de conhecimento para um banco de dados de funcionários. O conhecimento é contido em um ou mais domínios de dados, e cada um deles é uma representação semântica de um tipo de dados em um campo de dados. Uma base de dados de conhecimento para um banco de dados de clientes pode conter domínios para nomes de empresas, endereços, contatos, informações de contato e assim por diante. Um domínio contém uma lista de valores confiáveis, valores inválidos e dados errôneos. O conhecimento de domínio inclui associações de sinônimos, relações de termos, regras de negócio e validação e políticas de correspondência. De posse desse conhecimento, o administrador de dados pode tomar uma decisão informada sobre se deve corrigir instâncias específicas dos valores em um domínio.  
  
 O DQS permite executar operações de importação e exportação com uma base de dados de conhecimento. Você pode importar ou exportar domínios ou bases de dados de conhecimento usando um arquivo DQS. Você pode importar valores ou domínios de um arquivo do Excel. Você também pode importar valores encontrados por um processo de limpeza fundamentado na base de dados de conhecimento para um domínio. Essas operações permitem melhorar uma base de dados de conhecimento continuamente, garantindo que esse conhecimento adquirido por decisões e descobertas seja retornado à base de dados de conhecimento.  
  
 A solução controlada por conhecimento do DQS usa duas etapas fundamentais para limpar dados:  
  
-   Um processo de **gerenciamento do conhecimento** que cria a base de conhecimento  
  
-   Um **projeto de qualidade de dados** que propõe alterações na fonte de dados com base no conhecimento da base de dados de conhecimento.  
  
 Para obter mais informações, consulte [Bases de dados de conhecimento e domínios do DQS](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md) e [Projetos de qualidade de dados &#40;DQS&#41;](../../2014/data-quality-services/data-quality-projects-dqs.md).  
  
##  <a name="Components"></a> Componentes do DQS  
 O Data Quality Services consiste no [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] e no [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Esses componentes permitem executar o Data Quality Services separadamente de outras operações do SQL Server. Os dois são instalados no programa de instalação do SQL Server.  
  
 O[!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] é implementado como três catálogos do SQL Server que você pode gerenciar e monitorar no SQL Server Management Studio (DQS_MAIN, DQS_PROJECTS e DQS_STAGING_DATA). O DQS_MAIN inclui procedimentos armazenados do DQS, o mecanismo do DQS e bases de dados de conhecimento publicadas. O DQS_PROJECTS inclui dados que são necessários para o gerenciamento da base de dados de conhecimento e de atividades de projeto do DQS. O DQS_STAGING_DATA fornece um banco de dados de preparo intermediário onde você pode copiar seus dados de origem para executar operações do DQS e, depois, exportar os dados processados.  
  
 O[!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] é um aplicativo autônomo que permite executar o gerenciamento de conhecimento, projetos de qualidade de dados e a administração em uma interface do usuário. O aplicativo foi desenvolvido para administradores de dados e administradores do DQS. É um arquivo executável autônomo que executa a descoberta da base de dados de conhecimento, o gerenciamento de domínio, a criação de políticas de correspondência, a limpeza de dados, a correspondência, a criação de perfil, o monitoramento e a administração de servidor. O[!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] pode ser instalado e executado no mesmo computador que o [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] ou remotamente em um computador separado. Muitas operações no [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] são controladas por assistente para facilitar o uso.  
  
##  <a name="Processes"></a> Funcionalidade de qualidade de dados no Integration Services e no Master Data Services  
 A funcionalidade de qualidade de dados fornecida pelo Data Quality Services é integrada a um componente do SSIS (SQL Server Integration Services) e a recursos do MDS (Master Data Services) para permitir que você execute processos de qualidade de dados nesses serviços.  
  
 **[!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)]**  
  
 O [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)] permite executar a limpeza de dados como parte de um pacote do Integration Services. Quando o pacote é executado, a limpeza de dados é executada como um arquivo em lote. Essa é uma alternativa para executar um projeto de limpeza no aplicativo [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Você pode assegurar a qualidade de seus dados automaticamente. Você não tem de executar as etapas interativas de um projeto de limpeza de dados no aplicativo [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Você pode incluir o processo de limpeza de dados em um fluxo de dados que contém outros componentes do Integration Services. Para obter mais informações, consulte [Transformação de Limpeza DQS](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md).  
  
 **Processos de qualidade de dados no Master Data Services**  
  
 A funcionalidade Data Quality Services foi integrada ao MDS (Master Data Services) para que você possa eliminar a duplicação nos dados de origem e nos dados mestre nos fluxos de trabalho do MDS dentro do Suplemento Master Data Services do Microsoft SQL Server 2014 para Microsoft Excel. Para executar correspondência, carregue os dados gerenciados por MDS em uma planilha do Excel, combine-os com dados não gerenciados por MDS e, em seguida, execute a correspondência dentro do Excel. Os componentes do [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] devem ser instalados com o MDS. Para obter mais informações, consulte  [Correspondência de qualidade de dados no Suplemento do MDS para Excel](../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md).  
  
## <a name="see-also"></a>Consulte também  
 [Recursos com suporte nas edições do SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
  

---
title: Conceitos do Data Quality Services
ms.date: 01/01/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 837c71ee-48fa-4044-8744-2be9119aaa04
author: swinarko
ms.author: sawinark
ms.openlocfilehash: fe7f6c957bb1781528c0bad06de41063c41ca3cc
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85887954"
---
# <a name="data-quality-services-concepts"></a>Conceitos do Data Quality Services

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  Este tópico fornece um resumo breve de conceitos do [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) em gerenciamento de conhecimento, projetos de qualidade de dados e administração de qualidade de dados.  
  
##  <a name="knowledge-management-concepts"></a><a name="Knowledge"></a> Conceitos de gerenciamento de conhecimento  
 A base de dados de conhecimento do DQS é um repositório de metadados que são criados pelo administrador de dados ou pelo profissional de TI a fim de melhorar a qualidade de dados através da limpeza e da correspondência de dados. O gerenciamento de conhecimento do DQS inclui os processos usados para criar e gerenciar a base de conhecimento, de forma assistida por computador e interativamente.  
  
 **Descoberta da Base de Dados de Conhecimento**  
  
 A descoberta de conhecimento é um processo assistido por computador que analisa exemplos dos dados de sua organização para criar conhecimento sobre os dados. Quando você tem os resultados da análise, pode validar e aprimorar o conhecimento e, depois, aplicá-lo à execução de limpeza, correspondência e criação de perfil de dados. Para obter mais informações, consulte [DQS Knowledge Bases and Domains](../data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
 **Gerenciamento de domínio**  
  
 O processo de gerenciamento de domínio lhe permite alterar ou aumentar o conhecimento gerado pelo processo de descoberta de conhecimento. Você pode editar, atualizar e revisar interativamente o conhecimento em uma base de dados de conhecimento. Uma base de dados de conhecimento consiste em domínios de dados que contêm valores de domínio e seu status, regras de domínio, relações baseadas em termos e dados de referência. No gerenciamento de domínio, você pode alterar propriedades de domínio, anexar dados de referência a um domínio, gerenciar regras de domínio, gerenciar valores de domínio e inserir relações de dados, além de criar, excluir, importar ou exportar domínios. Você também pode usar domínios compostos que agregam mais de um domínio único. Para obter mais informações, consulte [DQS Knowledge Bases and Domains](../data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
 **Política de Correspondência**  
  
 Uma política de correspondência contém as regras de correspondência usadas para executar a eliminação de duplicação de dados. O processo de política de correspondência permite a você criar regras de correspondência, ajustá-las com base nos resultados correspondentes e na criação de perfis de dados, além de adicionar a política à base de dados de conhecimento. Para obter mais informações, consulte [Data Matching](../data-quality-services/data-matching.md).  
  
 **Serviços de Dados de Referência**  
  
 Você pode usar dados de referência para validar, corrigir e enriquecer seus dados, aproveitando os serviços de empresas que garantem a qualidade dos seus dados de referência. Você pode usar os serviços do Azure Marketplace para se conectar a provedores de dados de referência ou pode usar uma conexão direta com um provedor. Para obter mais informações, consulte [Reference Data Services in DQS](../data-quality-services/reference-data-services-in-dqs.md).  
  
 Para obter mais informações sobre o gerenciamento de conhecimento no DQS, consulte [DQS Knowledge Bases and Domains](../data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
##  <a name="data-quality-project-concepts"></a><a name="Projects"></a> Conceitos de projeto de qualidade de dados  
 O administrador de dados executa operações de qualidade de dados (limpeza e correspondência) usando um projeto de qualidade de dados no aplicativo do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] .  
  
 **Data Cleansing**  
  
 A limpeza de dados no DQS é feita com base no conhecimento em uma base de dados de conhecimento do DQS. A limpeza de dados no DQS é um processo de duas etapas:  
  
-   **Limpeza auxiliada por computador**: o DQS usa o conhecimento na base de dados de conhecimento selecionada para o projeto de limpeza para propor correções/sugestões aos valores em uma fonte de dados.  
  
-   **Limpeza interativa**: o administrador de dados pode executar o processo de limpeza interativo para alterar ou aumentar correções de dados que foram propostas pelo processo de limpeza de dados assistida por computador. O administrador de dados faz isso usando níveis de confiança e estatísticas identificadas pelo processo de limpeza de dados, ou inserindo manualmente suas próprias alterações no projeto.  
  
 Depois de limpar dados, o administrador de dados pode exportar os dados processados para um banco de dados do SQL Server, .csv ou um arquivo do Excel. Para obter mais informações, consulte [Data Cleansing](../data-quality-services/data-cleansing.md).  
  
 **Correspondência de dados**  
  
 O processo de correspondência permite ao administrador de dados comparar dados de forma que dados semelhantes, mas com ligeiras diferenças, possam ser alinhados através de um processo de eliminação de duplicação. O DQS executa a eliminação de duplicação com base em regras de correspondência contidas na base de dados de conhecimento; o administrador de dados especifica parâmetros para o processo de correspondência dentro de um projeto de qualidade de dados. Para obter mais informações, consulte [Data Matching](../data-quality-services/data-matching.md).  
  
 **Criação de perfis e notificações**  
  
 A criação de perfil de dados fornece aos administradores de dados estatísticas em tempo real e informações sobre os dados que estão sendo processados pelo DQS para as atividades de limpeza e correspondência enquanto executa um projeto de qualidade de dados. A criação de perfil de dados ajuda a avaliar a efetividade das atividades de limpeza e correspondência em um projeto de qualidade de dados, e as notificações ajudam o usuário com ações que podem ser realizadas para aprimorar as atividades de limpeza de dados e correspondência de dados. Para obter mais informações, consulte [Data Profiling and Notifications in DQS](../data-quality-services/data-profiling-and-notifications-in-dqs.md).  
  
 Para obter mais informações sobre projetos de qualidade de dados no DQS, consulte [Projetos de qualidade de dados &#40;DQS&#41;](../data-quality-services/data-quality-projects-dqs.md).  
  
##  <a name="data-quality-administration-concepts"></a><a name="Admin"></a> Conceitos de administração do Data Quality  
 Um administrador de DQS pode executar a variedade de tarefas administrativas usando o aplicativo [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] .  
  
 **Monitoramento de Atividades**  
  
 O monitoramento de atividades exibe o status e o estado de cada atividade executada em um intervalo de dados, fornece dados para cada atividade e permite que os administradores do DQS controlem uma atividade. Para obter mais informações, consulte [Monitor DQS Activities](../data-quality-services/monitor-dqs-activities.md).  
  
 **Configuration**  
  
 A opção de Configuração permite que você:  
  
-   Defina configurações de serviço de dados de referência. Para obter mais informações, consulte [Configure DQS to Use Reference Data](../data-quality-services/configure-dqs-to-use-reference-data.md).  
  
-   Defina os valores de limites para atividades de limpeza e correspondência. Para obter mais informações, consulte [Configurar valores de limite para limpeza e correspondência](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md).  
  
-   Habilitar/desabilitar notificações de criação de perfil. Para obter mais informações, consulte [Habilitar ou desabilitar notificações de criação de perfil no DQS](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md).  
  
-   Configure níveis de severidade para os arquivos de log do DQS no nível baseado em atividade ou no nível mais avançado baseado em módulo. Para obter mais informações, consulte [Configure Severity Levels for DQS Log Files](../data-quality-services/configure-severity-levels-for-dqs-log-files.md).  
  
 **Segurança do DQS**  
  
 Você usa funções do mecanismo de segurança do SQL Server para tornar o DQS seguro. Há três funções de DQS que determinam o nível de acesso para um usuário no aplicativo [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] : dqs_administrator, dqs_kb_editor e dqs_kb_operator. Você não pode conceder funções aos usuários usando o aplicativo [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] ; isso é feito usando o SQL Server Management Studio. Para obter mais informações, consulte [DQS Security](../data-quality-services/dqs-security.md).  
  
 Para obter mais informações sobre a administração do DQS, consulte [DQS Administration](../data-quality-services/dqs-administration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Data Quality Services](../data-quality-services/data-quality-services.md)  
  
  

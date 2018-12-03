---
title: Projetos de qualidade de dados (DQS) | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a43fc9c0-19b6-414a-8661-4c7c55e0c03e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 37ef3f8bb8f1a39a9d1af06a8ee71735bf0cccbf
ms.sourcegitcommit: c19696d3d67161ce78aaa5340964da3256bf602d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/29/2018
ms.locfileid: "52617906"
---
# <a name="data-quality-projects-dqs"></a>Projetos de qualidade de dados (DQS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Um projeto de qualidade de dados no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) é uma forma de usar uma base de dados de conhecimento para melhorar a qualidade dos dados de origem, executando atividades de *limpeza de dados* e *correspondência de dados* e, depois, exportando os dados resultantes para um banco de dados do SQL Server ou um arquivo .csv. Você pode criar um projeto de qualidade de dados como um projeto de limpeza ou um projeto de correspondência para executar as respectivas atividades. Os projetos de limpeza e correspondência podem ser executados usando a mesma base de dados de conhecimento, pois o conhecimento para limpeza e correspondência de dados pode ser criado na mesma base de conhecimento.  
  
 Um projeto de qualidade de dados tem os seguintes benefícios:  
  
-   Habilita-o a executar a limpeza de dados em seus dados de origem usando o conhecimento em uma base de dados de conhecimento do DQS.  
  
-   Habilita-o a executar a correspondência de dados em seus dados de origem usando a política de correspondência em uma base de dados de conhecimento.  
  
-   Fornece um assistente para orientá-lo nas atividades de limpeza e correspondência, e na exportação dos dados de acordo com sua seleção para um banco de dados do SQL Server ou para um arquivo .csv. O administrador de dados pode usar o projeto de qualidade de dados para executar e controlar as etapas assistidas por computador/interativas de limpeza e correspondência de dados.  
  
##  <a name="Cleansing"></a> Projeto de qualidade de dados: atividade de limpeza  
 Um projeto de qualidade de dados de limpeza permite que você limpe os dados de origem com base em uma base de dados de conhecimento. A atividade de limpeza de dados no DQS é um processo de duas etapas:  
  
1.  Um processo de limpeza de dados *assistido por computador* que analisa dados de origem em relação ao conhecimento da base de dados de conhecimento e propõe alterações. Os dados processados são categorizados (sugerido, novo, inválido, corrigido) pelo DQS e exibidos para o usuário para processamento adicional.  
  
2.  Um processo de limpeza *interativo* que permite ao administrador de dados aprovar, rejeitar ou modificar os dados propostos pelo processo de limpeza de dados assistido por computador.  
  
 Para obter informações detalhadas sobre a atividade de limpeza em um projeto de qualidade de dados, consulte [Data Cleansing](../data-quality-services/data-cleansing.md).  
  
##  <a name="Matching"></a> Projeto de qualidade de dados: atividade de correspondência  
 Um projeto de qualidade de dados de correspondência lhe permite executar atividades de correspondência com base na política de correspondência em uma base de dados de conhecimento para impedir a duplicação de dados, identificando correspondências exatas e aproximadas e, assim, permitindo a remoção de dados duplicados. É recomendável limpar seus dados antes de executar a correspondência neles. Para fazer isso:  
  
1.  Crie um projeto de qualidade de dados, selecione a atividade de **Limpeza** , conclua a atividade de limpeza de dados nos dados de origem e exporte-os para uma tabela em um banco de dados do SQL Server.  
  
2.  Crie outro projeto de qualidade de dados usando uma base de dados de conhecimento que contém uma política de correspondência, selecione a atividade de **Correspondência** e, depois, na página **Mapear** , selecione o banco de dados e a tabela para onde você exportou os dados limpos na etapa 1.  
  
3.  Conclua a atividade de correspondência nos dados limpos.  
  
 Para obter informações detalhadas sobre a atividade de correspondência em um projeto de qualidade de dados, consulte [Data Matching](../data-quality-services/data-matching.md).  
  
##  <a name="ProfilingNotification"></a> Perfil de dados e notificações  
 Ao executar as atividades de limpeza e correspondência em um projeto de qualidade de dados, você encontra estatísticas em tempo real e informações sobre os dados que estão sendo processados pelo DQS. A criação de perfil de dados o ajuda a avaliar a eficácia dos processos de limpeza e correspondência, e a potencialmente determinar até que ponto a limpeza ou a correspondência de dados ajudaram a melhorar a qualidade dos dados. A criação de perfil do DQS fornece duas dimensões de qualidade de dados: *integridade* (até que ponto os dados estão presentes) e *exatidão* (até que ponto os dados podem ser empregados para o uso pretendido). Além disso, com base nas informações de criação de perfil de dados, notificações são exibidas para o usuário nas ações que podem ser adotadas para aprimorar as operações de limpeza e correspondência de dados. Para obter informações detalhadas sobre a criação de perfil de dados e notificações, consulte [Data Profiling and Notifications in DQS](../data-quality-services/data-profiling-and-notifications-in-dqs.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como criar um projeto de qualidade de dados.|[Criar um projeto de qualidade de dados](../data-quality-services/create-a-data-quality-project.md)|  
|Descreve como abrir, desbloquear, renomear e excluir um projeto de qualidade de dados.|[Abrir, desbloquear, renomear e excluir um projeto do Data Quality](open-unlock-rename-and-delete-a-data-quality-project.md)|  
|Descreve como abrir um projeto do Integration Services no [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].|[Abrir projetos do Integration Services no Data Quality Client](../data-quality-services/open-integration-services-projects-in-data-quality-client.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Bases de Dados de Conhecimento DQS e domínios](../data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  

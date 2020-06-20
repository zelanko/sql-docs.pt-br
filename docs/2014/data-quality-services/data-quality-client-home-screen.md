---
title: Tela inicial do Data Quality Client | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.clienthome.f1
ms.assetid: 7c6ec469-bc7d-4d19-8e21-11dcf8ade108
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: edb0a9e0384804b733441d7fe256d11a150469d7
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937817"
---
# <a name="data-quality-client-home-screen"></a>Tela inicial do Cliente Data Quality
  Use esta tela para obter acesso às interfaces do usuário de cada um dos três grupos de tarefas do DQS ( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] ): gerenciamento da base de dados de conhecimento, projetos de qualidade de dados e administração.  
  
## <a name="options"></a>Opções  
  
### <a name="knowledge-base-management"></a>Gerenciamento da base de dados de conhecimento  
 Uma base de conhecimento do DQS é um repositório de metadados usado pelo DQS para melhorar a qualidade dos dados. Estes metadados são criados pela plataforma do DQS em um processo de descoberta da base de dados de conhecimento assistido por computador e pelo administrador de dados em um processo de gerenciamento de domínio interativo.  
  
 **Nova base de conhecimento**  
 Inicie o processo de criação de uma base de conhecimento a partir do zero ou baseado nos metadados de uma base de conhecimento existente. Este comando abre uma página na qual você pode identificar a base de dados de conhecimento, baseá-la em uma base de dados de conhecimento existente, selecionar a atividade de base de dados de conhecimento desejada e, em seguida, criar a base de dados de conhecimento.  
  
 **Abrir Base de Dados de Conhecimento**  
 Abrir uma base de dados de conhecimento para que você possa gerenciar seus domínios, executar a descoberta da base de dados de conhecimento ou criar uma política de correspondência. Clicar no botão **Abrir Base de Dados de Conhecimento** exibe a página **Abrir Base de Dados de Conhecimento** , que mostra uma lista de bases de dados de conhecimento existentes com suas propriedades, estado atual, base de dados de conhecimento e detalhes de seus domínios. Selecione uma base de dados de conhecimento e abra-a em **Abrir Base de Dados de Conhecimento**.  
  
 **Base de dados de conhecimento recente**  
 Da lista na tela, abra uma base de dados de conhecimento que já foi criada. Se não estiver bloqueada, clique na seta para a direita e selecione a atividade na qual você deseja iniciar a base de dados de conhecimento (Gerenciamento de Domínio, Descoberta da Base de Dados de Conhecimento ou Política de Correspondência).  
  
 Você pode abrir uma base de dados de conhecimento bloqueada e editá-la somente se você a bloqueou. Nesse caso, a base de dados de conhecimento será aberta no estado em que estava quando foi fechada, indicado em parênteses. Se uma base de conhecimento estiver bloqueada, e você não a tiver bloqueado, você só poderá abri-la como somente leitura.  
  
### <a name="data-quality-projects"></a>Projetos de qualidade de dados  
 Um projeto de qualidade de dados é o processo no qual o DQS executa a limpeza de dados ou correspondência de dados, por meio de correção de dados assistida por computador e limpeza de dados interativa.  
  
 **Novo projeto de qualidade de dados**  
 Inicie o projeto de criar um novo projeto. Este comando abre uma página na qual você pode identificar o projeto, associá-lo com uma base de dados de conhecimento, exibir detalhes da base de conhecimento, selecionar a atividade de projeto desejada e, em seguida, criar o projeto.  
  
 **Abrir projeto de qualidade de dados**  
 Abra um projeto para que você possa executar limpeza de dados ou correspondência de dados. Clicar no botão **Abrir projeto de qualidade de dados** exibe a página **Abrir projeto de qualidade de dados** , que mostra uma lista de projetos existentes com suas propriedades, estado atual, base de dados de conhecimento e detalhes de seus domínios e regras de política de correspondência. Selecione um projeto e abra-o em **Abrir projeto de qualidade de dados**.  
  
 **Projeto de qualidade de dados recente**  
 Da lista na tela, selecione um projeto que já foi criado. Você poderá abrir um projeto bloqueado somente se o tiver bloqueado. Nesse caso, o projeto será aberto no estado em que estava quando foi fechado, indicado em parênteses. Se o projeto tiver sido concluído, ele será aberto na etapa de Exportação da atividade.  
  
### <a name="administration"></a>Administração  
 A administração do DQS permite monitorar, configurar e manter o DQS.  
  
 **Monitoramento de Atividades**  
 Exibe o status de todas as atividades (atuais e históricas) que estão relacionadas ao servidor do [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]conectado. Os tipos de atividades monitoradas incluem Gerenciamento de Conhecimento, um Projeto de Qualidade de Dados e uma correção de dados baseada no SSIS.  
  
 **Configuration**  
 Exibe as propriedades de configuração para contas de serviço de dados de referência (tanto por meio do Azure Marketplace quanto diretamente para serviços de dados de referência), configurações gerais (limpeza interativa, correspondência e criação de perfil) e configurações de severidade de log.  
  
## <a name="see-also"></a>Consulte Também  
 [Bases de dados de conhecimento e domínios do DQS](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)   
 [Projetos de qualidade de dados &#40;o DQS&#41;](../../2014/data-quality-services/data-quality-projects-dqs.md)   
 [administração do dqs](../../2014/data-quality-services/dqs-administration.md)  
  
  

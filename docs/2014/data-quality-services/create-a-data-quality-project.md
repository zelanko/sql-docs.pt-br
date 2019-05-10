---
title: Criar um projeto de qualidade de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dqproject.newdqproject.f1
helpviewer_keywords:
- create,data quality project
- data quality project,create
ms.assetid: 19c52d2b-d28e-4449-ab59-5fe0dc326cd9
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: f341d13995cd7a13a06e0ad7b9b380ebd0184f7d
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65480948"
---
# <a name="create-a-data-quality-project"></a>Criar um projeto de qualidade de dados
  Este tópico descreve como criar um projeto de qualidade de dados usando o [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Um projeto de qualidade de dados é usado para executar a atividade de limpeza ou correspondência no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS).  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Você deve ter uma base de dados de conhecimento relevante para usar no projeto de qualidade de dados para a atividade de limpeza ou correspondência.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_kb_operator no banco de dados DQS_MAIN para criar um projeto de qualidade de dados.  
  
##  <a name="Create"></a> Criar um projeto de qualidade de dados  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Novo projeto de qualidade de dados**.  
  
3.  Na tela **Novo Projeto de Qualidade de Dados** :  
  
    1.  Na caixa **Nome** , digite um nome para o novo projeto de qualidade de dados.  
  
    2.  (Opcional) Na caixa **Descrição** , digite uma descrição para o novo projeto de qualidade de dados.  
  
    3.  Na lista **Usar base de dados de conhecimento** , clique para selecionar uma base de dados de conhecimento a ser usada no projeto de qualidade de dados. A área **Detalhes da base de dados de conhecimento: <Knowledge_Base_Name>** do lado direito exibe os nomes de domínio disponíveis na base de dados de conhecimento selecionada.  
  
    4.  Na área **Selecionar Atividade** , clique em uma atividade que você deseja executar usando este projeto de qualidade de dados:  
  
        -   **Limpeza**: selecione esta atividade para limpar os dados de origem.  
  
        -   **Correspondência**: selecione esta atividade para fazer a correspondência. Esta atividade só estará disponível se a base de dados de conhecimento selecionada para o projeto de qualidade de dados contiver uma política de correspondência.  
  
4.  Clique em **Criar** para criar um projeto de qualidade de dados.  
  
##  <a name="FollowUp"></a> Acompanhamento: Após criar um projeto de qualidade de dados  
 Depois que você criar um projeto de qualidade de dados, verá um assistente que deverá ser usado para executar a atividade selecionada: limpeza ou correspondência. Para obter mais informações sobre a limpeza e correspondência de atividades, consulte [Limpeza de dados](../../2014/data-quality-services/data-cleansing.md) e [Correspondência de dados](../../2014/data-quality-services/data-matching.md).  
  
  

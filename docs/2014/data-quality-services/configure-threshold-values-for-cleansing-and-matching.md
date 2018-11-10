---
title: Configurar valores de limite para limpeza e correspondência | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.admin.config.general.f1
helpviewer_keywords:
- cleansing,threshold value
- cleansing threshold values
- matching,threshold value
ms.assetid: d2305409-7115-45a4-8f60-1213c0a47368
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8a76f3fc589e3be0ae6b35e2cc4fc577eeb284cb
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51031773"
---
# <a name="configure-threshold-values-for-cleansing-and-matching"></a>Configurar valores de limite para limpeza e correspondência
  Este tópico descreve como configurar valores de limite que serão usados durante a limpeza auxiliada por computador e as atividades correspondentes no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS).  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 É necessário ter a função dqs_administrator no banco de dados DQS_MAIN para configurar esses valores de limite.  
  
##  <a name="Configure"></a> Configurando os valores de limite  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Configuração**.  
  
3.  Em seguida, clique na guia **Configurações Gerais** . Essa guia permite a você especificar os valores de limite para a limpeza, bem como as atividades de correspondência.  
  
4.  Para especificar valores de limote para a atividade de limpeza, especifique os valores apropriados nas seguintes caixas na área **Limpeza Interativa** :  
  
    -   **Pontuação mínima para sugestões**: a pontuação mínima ou o nível de confiança que será usado pelo DQS para sugerir substitutos para um valor durante o processo de limpeza auxiliada por computador. Insira um valor na notação decimal do valor percentual correspondente. Por exemplo, digite 0,75 para 75%. Esse valor deve ser inferior ou igual ao valor especificado na caixa **Pontuação mínima para correções automáticas** . O valor padrão é 0,7.  
  
    -   **Pontuação mínima para correções automáticas**: a pontuação mínima ou o nível de confiança que será usado pelo DQS para corrigir automaticamente um valor durante o processo de limpeza auxiliada por computador. Insira um valor na notação decimal do valor percentual correspondente. Por exemplo, insira 0,9 para 90%. O valor padrão é 0,8.  
  
5.  Para especificar um valor de limite para a atividade de correspondência, especifique um valor na caixa **Pontuação mínima de registro** na área **Correspondência** . Esse valor significa a pontuação mínima para um registro a ser considerado como uma correspondência para outro registro. O valor padrão é 80%.  
  
6.  Clique em **Fechar**.  
  
  

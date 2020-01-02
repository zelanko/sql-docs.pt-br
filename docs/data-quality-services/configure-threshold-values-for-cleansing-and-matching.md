---
title: Configurar valores de limite para limpeza e correspondência
description: Saiba como configurar valores de limite que serão usados durante a limpeza auxiliada por computador e atividades correspondentes no SQL Server Data Quality Services (DQS).
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.admin.config.general.f1
helpviewer_keywords:
- cleansing,threshold value
- cleansing threshold values
- matching,threshold value
ms.assetid: d2305409-7115-45a4-8f60-1213c0a47368
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 4fcbc8e4e6d6a9c1df07d8e1b1aa68c08c162817
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75557887"
---
# <a name="configure-threshold-values-for-cleansing-and-matching---data-quality-services-dqs"></a>Configurar valores de limite para limpeza e correspondência de serviços de qualidade de dados (DQS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Este tópico descreve como configurar valores de limite que serão usados durante a limpeza auxiliada por computador e as atividades correspondentes no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS).  
  
##  <a name="BeforeYouBegin"></a>Antes de começar  
  
###  <a name="Security"></a>Segurança  
  
####  <a name="Permissions"></a>Permissões  
 É necessário ter a função dqs_administrator no banco de dados DQS_MAIN para configurar esses valores de limite.  
  
##  <a name="Configure"></a>Configurando os valores de limite  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Execute o aplicativo Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Configuração**.  
  
3.  Em seguida, clique na guia **configurações gerais** . Esta guia permite que você especifique valores de limite para limpeza, bem como atividades correspondentes.  
  
4.  Para especificar valores de limote para a atividade de limpeza, especifique os valores apropriados nas seguintes caixas na área **Limpeza Interativa** :  
  
    -   **Pontuação mínima para sugestões**: a pontuação mínima ou o nível de confiança que será usado pelo DQS para sugerir substituições para um valor durante o processo de limpeza auxiliado por computador. Insira um valor na notação decimal do valor percentual correspondente. Por exemplo, digite 0,75 para 75%. Esse valor deve ser inferior ou igual ao valor especificado na caixa **Pontuação mínima para correções automáticas** . O valor padrão é 0,7.  
  
    -   **Pontuação mínima para correções automáticas**: a pontuação mínima ou o nível de confiança que será usado pelo DQS para corrigir automaticamente um valor durante o processo de limpeza auxiliado por computador. Insira um valor na notação decimal do valor percentual correspondente. Por exemplo, insira 0,9 para 90%. O valor padrão é 0,8.  
  
5.  Para especificar um valor de limite para a atividade de correspondência, especifique um valor na caixa **Pontuação mínima de registro** na área **Correspondência** . Esse valor significa a pontuação mínima para um registro a ser considerado como uma correspondência para outro registro. O valor padrão é 80%.  
  
6.  Clique em **Fechar**.  
  
  

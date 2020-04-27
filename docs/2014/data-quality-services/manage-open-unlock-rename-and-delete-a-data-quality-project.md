---
title: Gerenciar (abrir, desbloquear, renomear e excluir) um projeto de qualidade de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dqproject.opendqproject.f1
helpviewer_keywords:
- data quality project,delete
- data quality project,rename
- data quality project,unlock
- data quality project,open
ms.assetid: de8a2b04-4673-4beb-b4cf-96a28cdf3a93
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d5e3ec1fc7c3c811b588aaf4145aa286d9aa078e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65484150"
---
# <a name="manage-open-unlock-rename-and-delete-a-data-quality-project"></a>Gerenciar (abrir, desbloquear, renomear e excluir) um projeto de qualidade de dados
  Este tópico descreve como gerenciar um projeto de qualidade de dados usando o [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , por exemplo, como abrir, desbloquear, renomear e excluir um projeto de qualidade de dados.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> Limitações e restrições  
  
-   Você não pode abrir um projeto bloqueado criado por outro usuário.  
  
-   Você não pode desbloquear, renomear ou excluir um projeto de qualidade de dados criado por outro usuário.  
  
-   Você não pode excluir um projeto de qualidade de dados bloqueado. Primeiro você deve desbloqueá-lo para excluir.  
  
-   Você somente pode desbloquear um projeto de qualidade de dados criado por você.  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
 Você deve ter pelo menos um projeto de qualidade de dados para gerenciar.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_kb_operator no banco de dados DQS_MAIN para gerenciar um projeto de qualidade de dados.  
  
##  <a name="open-a-data-quality-project"></a><a name="Open"></a> Abrir um projeto de qualidade de dados  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Execute o aplicativo Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Abrir projeto de qualidade de dados**. A tela **Abrir projeto** é aberta.  
  
     Alternativamente, você pode abrir, de modo direto, um projeto de qualidade de dados listado em **Projeto de qualidade de dados recente** clicando nele.  
  
3.  Na tela **Abrir projeto** , clique para selecionar o projeto de qualidade de dados que você deseja abrir e clique em **Avançar**.  
  
4.  O projeto de qualidade de dados é aberto no mesmo estado da atividade quando foi fechado pela última vez. Um projeto de qualidade de dados tem os seguintes estados:  
  
    -   Para a atividade de **limpeza** , um projeto de qualidade de dados pode ter os seguintes Estados: **limpeza-mapa**, **limpeza-limpeza**, **limpeza-gerenciar e exibir resultados**e **limpeza-exportar**.  
  
    -   Para a atividade de **correspondência** , um projeto de qualidade de dados pode ter os seguintes Estados: **correspondência-mapa**, correspondência **de**correspondência, **correspondência-sobrevivência**e **exportação de correspondência**.  
  
##  <a name="unlock-a-data-quality-project"></a><a name="Unlock"></a> Desbloquear um projeto de qualidade de dados  
 Quando você cria um projeto de qualidade de dados, ele permanece em estado bloqueado para impedir seu uso ou modificação por outros usuários. Você deverá desbloquear o projeto de qualidade de dados depois de concluir seu trabalho se quiser que outros usuários trabalhem no seu projeto de qualidade de dados. Um símbolo de bloqueio é exibido para projetos que estão bloqueados.  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Execute o aplicativo Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Abrir projeto de qualidade de dados**. A tela **Abrir projeto** é aberta.  
  
3.  Na tela **Abrir projeto** , clique com o botão direito do mouse no projeto de qualidade de dados bloqueado criado por você e clique em **Desbloquear** no menu de atalho. Uma marca de seleção verde é exibida para o projeto, indicando que ele está desbloqueado.  
  
##  <a name="rename-a-data-quality-project"></a><a name="Rename"></a> Renomear um projeto de qualidade de dados  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Execute o aplicativo Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Abrir projeto de qualidade de dados**. A tela **Abrir projeto** é aberta.  
  
3.  Na tela **Abrir projeto** , clique com o botão direito do mouse no projeto de qualidade de dados criado por você e clique em **Renomear** no menu de atalho.  
  
4.  O nome de projeto de qualidade de dados fica editável na coluna **Nome** . Digite um novo nome e pressione Enter.  
  
##  <a name="delete-a-data-quality-project"></a><a name="Delete"></a> Excluir um projeto de qualidade de dados  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Execute o aplicativo Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Abrir projeto de qualidade de dados**. A tela **Abrir projeto** é aberta.  
  
3.  Na tela **Abrir projeto** , clique com o botão direito do mouse em um projeto de qualidade de dados desbloqueado criado por você e clique em **Excluir** no menu de atalho.  
  
4.  Será exibida uma mensagem de confirmação. Clique em **Sim**.  
  
  

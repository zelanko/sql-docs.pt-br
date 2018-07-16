---
title: Assistente de projeto de importação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ssis.importprojectwizard.f1
ms.assetid: 9247ad6c-4bd1-43ab-b347-583181cb9917
caps.latest.revision: 9
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2e25fd5e0d0142d7e29f14fc1691c979bac24149
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37314136"
---
# <a name="import-project-wizard"></a>Assistente para Importação de Projeto
  Use o Assistente de Projeto de Importação do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para criar um novo projeto do Integration Services baseado em um existente. Importe os projetos que já foram implantados para o catálogo do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ou importe projetos de um arquivo de implantação de projeto (extensão .ispac).  
  
### <a name="to-create-a-project-based-on-a-project-in-ispac-file-or-in-catalog"></a>Para criar um projeto com base em um projeto em arquivo .ispac ou em catálogo  
  
1.  Clique em **Arquivo**, aponte para **Novo**e clique em Projeto.  
  
2.  Expanda **Business Intelligence**e clique em **Integration Services**.  
  
3.  Selecione **Assistente de Importação do Integration Services** no painel central, digite um **nome** para a solução, projeto, especifique a **pasta** para o projeto e clique em **OK**.  
  
     Você deverá ver o **Assistente de Importação de Projeto do Integration Services**. Esse assistente cria um novo projeto do Integration Services com base em um projeto existente.  
  
4.  Clique em **Avançar** na página **Introdução** para ver a página **Selecionar Origem** .  
  
5.  Especifique se você deseja importar o projeto de um arquivo .ispac ou de um catálogo.  
  
    -   Se você selecionar a opção **Arquivo de implantação de projeto** , especifique o caminho do arquivo .ispac.  
  
    -   Se você selecionar a opção **Catálogo do Integration Services** , especifique o nome de instância do servidor de banco de dados na qual o catálogo existe e o caminho para o projeto no catálogo.  
  
6.  Clique em **Avançar** na página **Selecionar Origem** para ver a página **Revisão** . Revise as informações exibidas na página sobre a operação de importação que o assistente irá executar.  
  
7.  Clique em **Importar** para criar um novo projeto do Integration Services baseado naquele que você selecionou.  
  
8.  A página **Resultados** deverá exibir os resultados da operação de importação que o assistente executou. Clique em **Salvar Relatório** para salvar o relatório em um arquivo XML.  
  
9. Clique em **Fechar** para fechar o assistente.  
  
  

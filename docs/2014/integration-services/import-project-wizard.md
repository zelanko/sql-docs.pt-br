---
title: Assistente de importação de projeto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.importprojectwizard.f1
ms.assetid: 9247ad6c-4bd1-43ab-b347-583181cb9917
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ec71ccf6434cd892be7c44fd4957099965dff6de
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965476"
---
# <a name="import-project-wizard"></a>Assistente para Importação de Projeto
  Use o Assistente de Projeto de Importação do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para criar um novo projeto do Integration Services baseado em um existente. Importe os projetos que já foram implantados para o catálogo do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ou importe projetos de um arquivo de implantação de projeto (extensão .ispac).  
  
### <a name="to-create-a-project-based-on-a-project-in-ispac-file-or-in-catalog"></a>Para criar um projeto com base em um projeto em arquivo .ispac ou em catálogo  
  
1.  Clique em **arquivo**, aponte para **novo**e clique em projeto.  
  
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
  
  

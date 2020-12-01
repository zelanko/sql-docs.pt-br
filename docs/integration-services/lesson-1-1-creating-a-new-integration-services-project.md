---
description: 'Lição 1-1: Criar um novo projeto do Integration Services'
title: 'Etapa 1: Criar um novo projeto do Integration Services | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: f14521b5-941e-443b-8f5e-385f98e37fbf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 575353cd2cf770ed42d439fd31647ccaef3e01bd
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88449739"
---
# <a name="lesson-1-1-create-a-new-integration-services-project"></a>Lição 1-1: Criar um novo projeto do Integration Services

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



A primeira etapa na criação de um pacote em [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] é criar um projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Esse projeto de exemplo inclui modelos para fontes de dados, exibições de fontes de dados e pacotes que compõem uma solução de transformação de dados.  
  
Os pacotes que você criará neste tutorial do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] interpretam os valores de dados com distinção de localidade. Se o seu computador não estiver configurado para usar a opção regional **Inglês (Estados Unidos)**, será preciso definir propriedades adicionais no pacote. 

Os pacotes que você usará nas lições de 2 a 6 serão copiados dos pacotes que você criar nesta lição.  
  
> [!NOTE]  
> Se você ainda não fez isso, confira os [Pré-requisitos da Lição 1](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites).

## <a name="create-a-new-integration-services-project"></a>Criar um novo projeto do Integration Services  
  
1.  No menu **Iniciar** do Windows, pesquise e selecione **Visual Studio (SSDT)**.  
  
2.  No Visual Studio, selecione **Arquivo** > **Novo** > **Projeto** para criar um novo projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
3.  Na caixa de diálogo **Novo Projeto**, expanda o nó **Business Intelligence** em **Instalados** e selecione **Projeto do Integration Services** no painel **Modelos**.  
  
4.  Na caixa **Nome** , altere o nome padrão para **Tutorial SSIS**. Para usar uma pasta que já existe, desmarque a caixa de seleção **Criar diretório para solução**.  
  
5.  Aceite o local padrão ou selecione **Procurar** para procurar a pasta que deseja usar. Na caixa de diálogo **Local do Projeto**, selecione a pasta e **Selecionar Pasta**.  
  
6.  Selecione **OK**.  
  
    Por padrão, um pacote vazio chamado **Package.dtsx** é criado e adicionado ao projeto nos **Pacotes do SSIS**.  
  
7.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Package.dtsx**, selecione **Renomear** e renomeie o pacote padrão como **Lesson 1.dtsx**.  
  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa
[Etapa 2: Adicionar e configurar um gerenciador de conexões de Arquivo Simples](../integration-services/lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  

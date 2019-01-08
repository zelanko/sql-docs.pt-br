---
title: 'Etapa 1: Criando uma nova integração dos serviços de projeto | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f14521b5-941e-443b-8f5e-385f98e37fbf
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: eff00a91c6fff1caee5e5fc41dd6d59f8635f78f
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53377399"
---
# <a name="step-1-creating-a-new-integration-services-project"></a>Etapa 1: Criando um novo projeto do Integration Services
  A primeira etapa na criação de um pacote em [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] é criar um projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Esse projeto inclui modelos para objetos – fontes de dados, exibições de fontes de dados e pacotes – usados em uma solução de transformação.  
  
 Os pacotes que serão criados neste tutorial do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] interpretam os valores de dados com distinção de localidade. Se o seu computador não estiver configurado para usar a opção regional Inglês (Estados Unidos), será preciso definir propriedades adicionais no pacote. Os pacotes usados nas lições 2 a 5 serão copiados a partir do pacote criado na lição 1 e não será preciso atualizar as propriedades que fazem distinção de localidade nos pacotes copiados.  
  
> [!NOTE]  
>  Este tutorial requer o Microsoft SQL Server Data Tools.  
>   
>  Para obter mais informações sobre como instalar o SQL Server Data Tools, consulte [Download do SQL Server Data Tools](https://msdn.microsoft.com/data/hh297027).  
  
### <a name="to-create-a-new-integration-services-project"></a>Para criar um novo projeto Integration Services  
  
1.  Clique no menu **Iniciar** , aponte para **Todos os Programas**, aponte para **Microsoft SQL Server**e clique em **SQL Server Data Tools**.  
  
2.  No menu **Arquivo** , aponte para **Novo**e clique em **Projeto** para criar um novo projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
3.  Na caixa de diálogo **Novo Projeto** , expanda o nó **Business Intelligence** em **Modelos Instalados**e selecione **Projeto do Integration Services** no painel **Modelos** .  
  
4.  Na caixa **Nome** , altere o nome padrão para **Tutorial SSIS**. Opcionalmente, desmarque a caixa de seleção **Criar diretório para a solução** .  
  
5.  Aceite o local padrão ou clique em **Procurar** para procurar a pasta que deseja usar. Na caixa de diálogo **Local do Projeto** , clique na pasta e clique em **Selecionar Pasta**.  
  
6.  Clique em **OK**.  
  
     Por padrão, um pacote vazio chamado **Package.dtsx**será criado e adicionado ao projeto nos Pacotes do SSIS.  
  
7.  Na barra de ferramentas do **Gerenciador de Soluções** , clique com o botão direito do mouse em **Package.dtsx**, clique em **Renomear**e renomeie o pacote padrão como **Lesson 1.dtsx**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Etapa 2: Adicionando e configurando um Gerenciador de Conexão de arquivo simples](lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
  

---
title: "Conceder permiss&#245;es em estruturas e modelos de minera&#231;&#227;o de dados (Analysis Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.roledesignerdialog.miningmodels.f1"
helpviewer_keywords: 
  - "mineração de dados [Analysis Services], segurança"
  - "permissões [Analysis Services], modelos de mineração"
  - "modelos de mineração [Analysis Services], segurança"
  - "estruturas de mineração [Analysis Services], segurança"
  - "permissões [Analysis Services], estruturas de mineração"
  - "direitos de acesso do usuário [Analysis Services], estruturas de mineração"
  - "direitos de acesso do usuário [Analysis Services], modelos de mineração"
ms.assetid: a0008004-e2b7-47db-acad-5fe7e12b130f
caps.latest.revision: 37
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 37
---
# Conceder permiss&#245;es em estruturas e modelos de minera&#231;&#227;o de dados (Analysis Services)
  Por padrão, apenas um administrador do servidor do Analysis Services tem permissões para exibir estruturas ou modelos de mineração no banco de dados. Siga as instruções abaixo para conceder permissões a usuários não administradores.  
  
## Definir permissões para acessar uma estrutura de mineração  
  
1.  No SSMS, conecte-se ao Analysis Services. Consulte [Conectar-se de aplicativos cliente &#40;Analysis Services&#41;](../../analysis-services/instances/connect-from-client-applications-analysis-services.md) se precisar de ajuda com as etapas.  
  
2.  Abra a pasta **Bancos de Dados** e escolha um banco de dados no Pesquisador de Objetos.  
  
3.  Clique com o botão direito do mouse em **Funções** e escolha **Nova Função**.  
  
4.  Na página Geral, insira um nome e, opcionalmente, uma descrição. Essa página também contém várias permissões de banco de dados, tais como Controle Total, Processar Banco de Dados e Ler Definição. Nenhuma dessas permissões é necessária para acesso aos dados de mineração. Consulte [Conceder permissões de banco de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md) para obter mais informações sobre as permissões do banco de dados.  
  
5.  No painel **Estrutura de Mineração**, escolha **Leitura** ou **Leitura/Gravação** para cada estrutura de mineração de dados.  
  
6.  No painel **Associação**, insira as contas de usuário e de grupo do Windows que se conectam ao Analysis Services usando essa função.  
  
7.  Clique em **OK** para concluir a criação da função.  
  
## Definir permissões para acessar um modelo de mineração  
 Para um modelo de mineração de dados, uma função pode ter permissões de **Leitura** ou **Leitura/Gravação**, bem como permissões de **Detalhamento** e **Ler Definição** que permitem exibir e procurar dados subjacentes.  
  
 **Observação** Se você habilitar detalhamento na estrutura de mineração e no modelo de mineração, qualquer usuário que for membro de uma função que tenha permissões de detalhamento no modelo de mineração e na estrutura de mineração também poderá exibir colunas na estrutura de mineração, até mesmo se essas colunas não estiverem incluídas no modelo de mineração. Portanto, para proteger informações confidenciais, você deveria configurar a exibição da fonte de dados para mascarar informações pessoais e só permitir acesso de detalhamento na estrutura de mineração quando necessário.  
  
 Para conceder a um usuário permissões de leitura ou de leitura/gravação a uma função do banco de dados, o usuário deve ser membro da função de servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou membro de uma função de banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] com permissões de Controle total (Administrador).  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], expanda **Funções** para o banco de dados adequado no Pesquisador de Objetos e clique em uma função de banco de dados (ou crie uma nova função de banco de dados).  
  
2.  Clique no painel **Estrutura de Mineração**, localize o modelo de mineração na lista **Modelo de Mineração** e selecione **Leitura**, **Leitura/Gravação**, **Detalhamento** ou **Procurar** para o modelo de mineração.  
  
3.  No painel **Associação**, insira as contas de usuário e de grupo do Windows que se conectam ao Analysis Services usando essa função.  
  
4.  Clique em **OK** para concluir a criação da função.  
  
 Para usar uma fonte de dados em uma consulta de detalhamento que usa a cláusula DMX (extensões DMX) OPENQUERY, a função de banco de dados precisa também de permissão de leitura/gravação no objeto de fonte de dados adequado. Para obter mais informações, consulte [Conceder permissões em um objeto de fonte de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md) e [OPENQUERY &#40;DMX&#41;](../Topic/OPENQUERY%20\(DMX\).md).  
  
> [!NOTE]  
>  Por padrão, o envio de consultas de DMX usando OPENROWSET está desabilitado.  
  
## Consulte também  
 [Conceder direitos de administração de servidor a uma instância do Analysis Services](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [Conceder permissões de cubo ou modelo &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)   
 [Conceder acesso personalizado a dados da dimensão &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)   
 [Conceder acesso personalizado a dados de célula &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)  
  
  
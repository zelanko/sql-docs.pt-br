---
title: Conceder permissões de banco de dados (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f799b086833f0be7b08786aff08e65d202f29674
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="grant-database-permissions-analysis-services"></a>Conceder permissões de banco de dados (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Se você estiver acessando a administração de banco de dados do Analysis Services com experiência em bancos de dados relacionais, a primeira coisa que você precisa entender é que, em termos de acesso a dados, o banco de dados não é o principal objeto protegível no Analysis Services.  
  
 A estrutura de consulta primária no Analysis Services é um cubo (ou um modelo de tabela), com permissões de usuário definidas nesses objetos particulares. Contrastando com o mecanismo de banco de dados relacional ─ em que os logons do banco de dados e as permissões de usuário (normalmente **db_datareader**) são definidas no próprio banco de dados ─ um banco de dados do Analysis Services é principalmente um contêiner dos principais objetos de consulta em um modelo de dados. Se o objetivo imediato é permitir o acesso a dados para um modelo de cubo ou de tabela, você pode ignorar as permissões de banco de dados agora e ir direto para este tópico: [Conceder permissões de cubo ou modelo &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md).  
  
 As permissões de banco de dados no Analysis Services habilitam funções administrativas. Em um contexto mais amplo, como é o caso da permissão Controle Total do banco de dados ou de natureza mais granular se você estiver delegando operações de processamento. Os níveis de permissão para um banco de dados do Analysis Services são especificados no painel **Geral** da caixa de diálogo **Criar Função** , exibidos na ilustração a seguir e descritos abaixo.  
  
 Não há logons no Analysis Services. Basta criar funções e atribuir contas do Windows no painel **Associação** . Todos os usuários, inclusive os administradores, conectam-se ao Analysis Services usando uma conta do Windows.  
  
 ![Função diálogo mostrando as permissões Create database](../../analysis-services/multidimensional-models/media/ssas-permsdbrole.png "função diálogo mostrando as permissões Create database")  
  
 Há três tipos de permissões especificadas em nível de banco de dados.  
  
 **Controle Total (Administrador)** ─ Controle Total é uma permissão abrangente que transmite amplos poderes sobre um banco de dados do Analysis Services, tais como a capacidade de consultar ou processar qualquer objeto dentro do banco de dados e gerenciar a segurança das funções. Controle Total é sinônimo de status de administrador de banco de dados. Quando você seleciona **Controle Total**, as permissões **Processar Banco de Dados** e **Ler Definição** também são selecionadas e não podem ser removidas.  
  
> [!NOTE]  
>  Os administradores do servidor (membros da função de Administrador do Servidor) também têm Controle Total implícito sobre cada banco de dados no servidor.  
  
 **Processar Banco de Dados** ─ Esta permissão é usada para delegar o processamento em nível do banco de dados. Como administrador, você pode descarregar essa tarefa criando uma função que permita que outra pessoa ou serviço invoque as operações para qualquer objeto no banco de dados. Como alternativa, você também pode criar funções que permitam o processamento de objetos específicos. Consulte [Conceder permissões de processo &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md) para obter mais informações.  
  
 **Ler Definição** ─ Esta permissão concede a capacidade de ler metadados de objetos, menos a capacidade de exibir os dados associados. Normalmente, essa permissão é usada em funções criados para processamento dedicado, adicionando a capacidade de usar ferramentas como [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ou [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para processar um banco de dados de forma interativa. Sem **Ler Definição**, a permissão **Processar Banco de Dados** só é eficaz em cenários de script. Se você pretende automatizar o processamento, talvez por meio do SSIS ou outro agendador, provavelmente vai querer criar uma função que tenha **Processar Banco de Dados** sem **Ler Definição**. Caso contrário, considere a combinação das duas propriedades na mesma função para dar suporte tanto para processamento autônomo quanto interativo com as ferramentas do SQL Server que visualizam o modelo de dados em uma interface de usuário.  
  
## <a name="full-control-administrator-permissions"></a>Permissões de Controle Total (Administrador)  
 Em [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], um administrador de banco de dados consiste em qualquer identidade de usuário do Windows atribuída a uma função que inclua permissões de Controle Total (Administrador). Um administrador de banco de dados pode executar qualquer tarefa dentro do banco de dados, incluindo:  
  
-   Processar objetos  
  
-   Ler dados e metadados de todos os objetos no banco de dados, incluindo cubos, dimensões, grupos de medidas, perspectivas e modelos de mineração de dados  
  
-   Criar ou modificar as funções de banco de dados ao adicionar usuários ou permissões, incluindo a adição de usuários a funções que também têm permissões de Controle Total  
  
-   Excluir funções de banco de dados ou associação de função  
  
-   Registrar assemblies (ou procedimentos armazenados) para o banco de dados.  
  
 Observe que um administrador de banco de dados não pode adicionar nem excluir bancos de dados no servidor, nem conceder direitos de administrador para outros bancos de dados no mesmo servidor. Esse privilégio pertence apenas aos administradores do servidor. Consulte [Conceder direitos de administração de servidor a uma instância do Analysis Services](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md) para mais informações sobre esse nível de permissão.  
  
 Como todas as funções são definidas pelo usuário, recomendamos que você crie uma função dedicada para esse fim (por exemplo, uma função com o nome "dbadmin") e atribua contas de usuários e de grupos do Windows de acordo.  
  
#### <a name="create-roles-in-ssms"></a>Criar funções no SSMS  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], abra a pasta **Bancos de Dados** , selecione um banco de dados e clique com o botão direito do mouse em **Funções** | **Nova Função**.  
  
2.  No painel **Geral** , insira um nome, como por exemplo, DBAdmin.  
  
3.  Marque a caixa de seleção **Controle Total (Administrador)** para o cubo. Observe que **Processar Banco de Dados** e **Ler Definição** são selecionados automaticamente. Ambas as permissões são sempre incluídas nas funções que incluem **Controle Total**.  
  
4.  No painel **Associação**, insira as contas de usuário e de grupo do Windows que se conectam ao Analysis Services usando essa função.  
  
5.  Clique em **OK** para concluir a criação da função.  
  
## <a name="process-database"></a>Processar Banco de Dados  
 Ao definir uma função que concede permissões de banco de dados, você pode pular **Controle Total** e escolher apenas **Processar Banco de Dados**. Essa permissão, definida no nível de banco de dados, permite o processamento de todos os objetos do banco de dados. Consulte [Conceder permissões de processo &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)  
  
## <a name="read-definition"></a>Ler Definição  
 Da mesma forma que **Processar Banco de Dados**, configurar as permissões **Ler Definição** no nível de banco de dados tem um efeito cascata sobre os outros objetos do banco de dados. Se você deseja definir permissões de Ler Definição em um nível mais granular, desmarque Ler Definição como uma propriedade do banco de dados no painel Geral. Consultar [Conceder permissões para ler definição em metadados de objetos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md) para obter mais informações.  
  
## <a name="see-also"></a>Consulte também  
 [Conceder direitos de administração de servidor a uma instância do Analysis Services](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [Conceder permissões de processo & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)  
  
  

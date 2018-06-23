---
title: Conceder permissões de banco de dados (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- permissions [Analysis Services], full control
- full control permissions [Analysis Services]
ms.assetid: be7e5f64-af43-47d6-84a5-c5c1c277d644
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 37022a42bc8e5347551a49c24ffc0ae9f8b8dbf5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007796"
---
# <a name="grant-database-permissions-analysis-services"></a>Conceder permissões de banco de dados (Analysis Services)
  Se você estiver acessando a administração de banco de dados do Analysis Services com experiência em bancos de dados relacionais, a primeira coisa que você precisa entender é que, em termos de acesso a dados, o banco de dados não é o principal objeto protegível no Analysis Services.  
  
 A estrutura de consulta primária no Analysis Services é um cubo (ou um modelo de tabela), com permissões de usuário definidas nesses objetos particulares. Contrastado com o mecanismo de banco de dados relacional ─ banco de dados em que logons e permissões de usuário (geralmente `db_datareader`) são definidas no próprio banco de dados ─ um banco de dados do Analysis Services é principalmente um contêiner para os objetos de consulta principal em um modelo de dados. Se o objetivo imediato é permitir o acesso a dados para um modelo de cubo ou de tabela, você pode ignorar as permissões de banco de dados agora e ir direto para este tópico: [Conceder permissões de cubo ou modelo &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md).  
  
 As permissões de banco de dados no Analysis Services habilitam funções administrativas. Em um contexto mais amplo, como é o caso da permissão Controle Total do banco de dados ou de natureza mais granular se você estiver delegando operações de processamento. Os níveis de permissão para um banco de dados do Analysis Services são especificados no painel **Geral** da caixa de diálogo **Criar Função** , exibidos na ilustração a seguir e descritos abaixo.  
  
 Não há logons no Analysis Services. Basta criar funções e atribuir contas do Windows no painel **Associação** . Todos os usuários, inclusive os administradores, conectam-se ao Analysis Services usando uma conta do Windows.  
  
 ![Função diálogo mostrando as permissões Create database](../media/ssas-permsdbrole.png "função diálogo mostrando as permissões Create database")  
  
 Há três tipos de permissões especificadas em nível de banco de dados.  
  
 **Controle Total (Administrador)** ─ Controle Total é uma permissão abrangente que transmite amplos poderes sobre um banco de dados do Analysis Services, tais como a capacidade de consultar ou processar qualquer objeto dentro do banco de dados e gerenciar a segurança das funções. Controle Total é sinônimo de status de administrador de banco de dados. Ao selecionar `Full Control`, as permissões de `Process Database` e `Read Definition` também são selecionados e não podem ser removidas.  
  
> [!NOTE]  
>  Os administradores do servidor (membros da função de Administrador do Servidor) também têm Controle Total implícito sobre cada banco de dados no servidor.  
  
 `Process Database` ─ Esta permissão é usada para delegar o processamento no nível de banco de dados. Como administrador, você pode descarregar essa tarefa criando uma função que permita que outra pessoa ou serviço invoque as operações para qualquer objeto no banco de dados. Como alternativa, você também pode criar funções que permitam o processamento de objetos específicos. Consulte [Grant process permissions &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md) para obter mais informações.  
  
 `Read Definition` ─ Esta permissão concede a capacidade de ler os metadados de objeto, menos a capacidade de exibir os dados associados. Normalmente, essa permissão é usada em funções criados para processamento dedicado, adicionando a capacidade de usar ferramentas como [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ou [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] para processar um banco de dados de forma interativa. Sem `Read Definition`, a permissão `Process Database` só é eficaz em cenários de script. Se você pretende automatizar o processamento, talvez por meio de SSIS ou outro Agendador, provavelmente você deseja criar uma função que tenha `Process Database` sem `Read Definition`. Caso contrário, considere a combinação das duas propriedades na mesma função para dar suporte tanto para processamento autônomo quanto interativo com as ferramentas do SQL Server que visualizam o modelo de dados em uma interface de usuário.  
  
## <a name="full-control-administrator-permissions"></a>Permissões de Controle Total (Administrador)  
 Em [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], um administrador de banco de dados consiste em qualquer identidade de usuário do Windows atribuída a uma função que inclua permissões de Controle Total (Administrador). Um administrador de banco de dados pode executar qualquer tarefa dentro do banco de dados, incluindo:  
  
-   Processar objetos  
  
-   Ler dados e metadados de todos os objetos no banco de dados, incluindo cubos, dimensões, grupos de medidas, perspectivas e modelos de mineração de dados  
  
-   Criar ou modificar as funções de banco de dados ao adicionar usuários ou permissões, incluindo a adição de usuários a funções que também têm permissões de Controle Total  
  
-   Excluir funções de banco de dados ou associação de função  
  
-   Registrar assemblies (ou procedimentos armazenados) para o banco de dados.  
  
 Observe que um administrador de banco de dados não pode adicionar nem excluir bancos de dados no servidor, nem conceder direitos de administrador para outros bancos de dados no mesmo servidor. Esse privilégio pertence apenas aos administradores do servidor. Consulte [conceder permissões de administrador de servidor &#40;Analysis Services&#41; ](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md) para obter mais informações sobre esse nível de permissão.  
  
 Como todas as funções são definidas pelo usuário, recomendamos que você crie uma função dedicada para esse fim (por exemplo, uma função com o nome "dbadmin") e atribua contas de usuários e de grupos do Windows de acordo.  
  
#### <a name="create-roles-in-ssms"></a>Criar funções no SSMS  
  
1.  No [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], abra a pasta **Bancos de Dados** , selecione um banco de dados e clique com o botão direito do mouse em **Funções** | **Nova Função**.  
  
2.  No painel **Geral** , insira um nome, como por exemplo, DBAdmin.  
  
3.  Marque a caixa de seleção **Controle Total (Administrador)** para o cubo. Observe que `Process Database` e `Read Definition` são selecionados automaticamente. Ambas as permissões são sempre incluídas nas funções que incluem `Full Control`.  
  
4.  No painel **Associação** , insira as contas de usuário e de grupo do Windows que se conectam ao Analysis Services usando essa função.  
  
5.  Clique em **OK** para concluir a criação da função.  
  
## <a name="process-database"></a>Processar Banco de Dados  
 Ao definir uma função que concede permissões de banco de dados, você pode ignorar `Full Control` e escolher apenas `Process Database`. Essa permissão, definida no nível de banco de dados, permite o processamento de todos os objetos do banco de dados. Consulte [Grant process permissions &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md)  
  
## <a name="read-definition"></a>Ler Definição  
 Como `Process Database`, configuração `Read Definition` permissões no nível do banco de dados tem um efeito cascata sobre os outros objetos no banco de dados. Se você deseja definir permissões de Ler Definição em um nível mais granular, desmarque Ler Definição como uma propriedade do banco de dados no painel Geral. Consultar [Conceder permissões para ler definição em metadados de objetos &#40;Analysis Services&#41;](grant-read-definition-permissions-on-object-metadata-analysis-services.md) para obter mais informações.  
  
## <a name="see-also"></a>Consulte também  
 [Conceder permissões de administrador de servidor &#40;do Analysis Services&#41;](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [Conceder permissões de processo &#40;do Analysis Services&#41;](grant-process-permissions-analysis-services.md)  
  
  
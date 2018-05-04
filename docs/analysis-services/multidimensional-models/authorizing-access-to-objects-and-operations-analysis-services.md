---
title: Autorizar o acesso a objetos e operações (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5a8dc16e1f2885141f20395cbe5e150996919e06
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="authorizing-access-to-objects-and-operations-analysis-services"></a>Autorizando o acesso a objetos e operações (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  O acesso do usuário não administrativo a objetos como cubos, dimensões e modelos de mineração em um banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é concedido por meio de associação em uma ou mais funções de banco de dados. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Os administradores criam essas funções de banco de dados, concedem permissões de leitura ou leitura/gravação em objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e atribuem usuários e grupos do Windows [!INCLUDE[msCoName](../../includes/msconame-md.md)] a cada função.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determina as permissões efetivas para um usuário ou grupo específico do Windows combinando as permissões associadas a cada função de banco de dados à qual o usuário ou grupo pertence. Em resultado, se uma função de banco de dados não fornecer a um usuário ou grupo permissão para exibir uma dimensão, medida ou atributo, mas uma função de banco de dados diferente conceder essa permissão, o usuário ou grupo terá permissão para exibir o objeto.  
  
> [!IMPORTANT]  
>  Os membros da função Administrador de Servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e os membros de uma função de banco de dados que têm permissões de Controle Total (Administrador) podem acessar todos os dados e metadados no banco de dados e não precisam de nenhuma permissão adicional para exibir objetos específicos. Além disso, os membros da função de servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não podem ter o acesso negado a nenhum objeto de nenhum banco de dados e os membros de uma função de banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que tem permissões de Controle Total (Administrador) em um banco de dados não podem ter o acesso negado a nenhum objeto desse banco de dados. Operações administrativas especializadas, tais como processamento, podem ser autorizadas por meio de funções distintas com menos permissão. Consultar [Conceder permissões de processo &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md) para ver os detalhes.  
  
## <a name="list-roles-defined-for-your-database"></a>Listar funções definidas para o banco de dados  
 Os administradores podem executar uma única consulta DMV no SQL Server Management Studio para obter uma lista de todas as funções definidas no servidor.  
  
1.  No SSMS, clique com o botão direito do mouse em um banco de dados e selecione **Nova Consulta** | **MDX**.  
  
2.  Digite a consulta a seguir e pressione F5 para executá-la:  
  
    ```  
    Select * from $SYSTEM.DBSCHEMA_CATALOGS  
    ```  
  
     Os resultados incluem o nome do banco, descrição, nome da função e a data da última modificação. Usando essas informações como ponto de partida você pode ir para bancos de dados individuais para verificar a associação e as permissões de uma função específica.  
  
## <a name="top-down-overview-of-analysis-services-authorization"></a>Visão geral de cima para baixo da autorização do Analysis Services  
 Esta seção aborda o fluxo de trabalho básico para configurar permissões.  
  
 **Etapa 1: Administração de servidor**  
  
 Primeiro, decida quem terá direitos de administrador no nível do servidor. Durante a instalação, é preciso ter o administrador local que instala o SQL Server para especificar uma ou mais contas do Windows como administrador do servidor do Analysis Services. Os administradores do servidor têm todas as permissões possíveis em um servidor, inclusive a permissão para exibir, modificar e excluir qualquer objeto no servidor ou exibir os dados associados. Após a instalação ser concluída, o administrador do servidor pode adicionar ou remover contas para alterar a associação da função. Consulte [Conceder direitos de administração de servidor a uma instância do Analysis Services](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md) para ver os detalhes sobre esse nível de permissão.  
  
 **Etapa 2: Administração de banco de dados**  
  
 Na sequência, depois que o administrador cria uma solução de tabela ou multidimensional, ele a implanta no servidor como um banco de dados. Um administrador do servidor pode delegar tarefas de administração de banco de dados por definir uma função que tenha permissões de controle total para o banco de dados em questão. Os membros dessa função podem processar ou consultar objetos no banco de dados, bem como criar funções adicionais para acessar cubos, dimensões e outros objetos dentro do próprio banco de dados. Consulte [Conceder permissões de banco de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md) para obter mais informações.  
  
 **Etapa 3: Habilitar acesso do cubo ou modelo para consulta e processamento de cargas de trabalho**  
  
 Por padrão, somente servidores e administradores de banco de dados têm acesso a modelos de cubos e de tabela. Tornar essas estruturas de dados disponíveis para outras pessoas na sua organização exige atribuições de funções adicionais, que mapeiam contas de usuários e de grupos do Windows para cubos ou modelos, juntamente com as permissões que especificam privilégios de **Read** . Consulte [Conceder permissões de cubo ou modelo &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md) para ver os detalhes.  
  
 O processamento de tarefas pode ser isolado de outras funções administrativas, permitindo que administradores de servidor e de banco de dados deleguem essa tarefa a outras pessoas ou configurem o processamento autônomo, especificando contas de serviço que executam o software de agendamento. Consultar [Conceder permissões de processo &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md) para ver os detalhes.  
  
> [!NOTE]  
>  Os usuários não precisam de nenhuma permissão nas tabelas relacionais do banco de dados relacionais subjacentes por meio do qual o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] carrega os dados e não precisam de nenhuma permissão no nível do arquivo no computador em que a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] está em execução.  
  
 **Etapa 4 (opcional): Permitir ou negar acesso a objetos de cubo internos**  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece configurações de segurança para definir permissões para objetos individuais, incluindo membros e células da dimensão dentro de um modelo de dados. Para ver os detalhes, consulte [Conceder acesso personalizado a dados da dimensão &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) e [Conceder acesso personalizado a dados de célula &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md).  
  
 Você também pode variar as permissões com base na identidade do usuário. Isso é frequentemente chamado de segurança dinâmica e é implantada usando a função [UserName &#40;MDX&#41;](../../mdx/username-mdx.md)  
  
## <a name="best-practices"></a>Práticas recomendadas  
 Para gerenciar as permissões de uma melhor forma, sugerimos uma abordagem semelhante à seguinte:  
  
1.  Crie funções por função (por exemplo, dbadmin, cubedeveloper, processadmin), de modo que o usuário quem mantém as funções possa ver rapidamente o que a função permite. Como já observado, você pode definir as funções na definição do modelo, preservando-as, assim, em implantações posteriores da solução.  
  
2.  Crie um grupo de segurança do Windows correspondente no Active Directory e mantenha-o no Active Directory para garantir que nele estejam incluídas as contas individuais adequadas. Isso coloca a responsabilidade da associação do grupo de segurança em especialistas de segurança, os quais já dominam as ferramentas e os processos utilizados na manutenção das contas em sua organização.  
  
3.  Gere scripts no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] de modo que você possa replicar rapidamente as atribuições de função sempre que o modelo é reimplantado em um servidor a partir dos arquivos de origem. Consulte [Conceder permissões de cubo ou modelo &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md) para ver os detalhes sobre a rapidez de criação de um script.  
  
4.  Adote uma convenção de nomenclatura que reflita o escopo e a associação da função. Os nomes de função são visíveis apenas em ferramentas de design e de administração, portanto, use uma convenção de nomenclatura que faça sentido para os seus especialistas de segurança de cubo. Por exemplo, **processadmin-windowsgroup1** indica acesso de leitura e direitos de processamento para pessoas na sua organização cujas contas individuais de usuário do Windows são membros do grupo de segurança **windowsgroup1** .  
  
     Incluir informações da conta pode ajudá-lo a manter o controle de quais contas são usadas em várias funções. Como as funções são aditivas, as funções combinadas associadas ao **windowsgroup1** formam o conjunto de permissões eficazes para as pessoas que pertencem a esse grupo de segurança.  
  
5.  Os desenvolvedores de cubo necessitam de permissões de Controle Total para os modelos e bancos de dados em desenvolvimento, mas só precisam de permissões de Leitura após o banco de dados ser distribuído a um servidor de produção. Lembre-se de desenvolver definições e atribuições de funções para todos os cenários, inclusive para implantações de desenvolvimento, teste e produção.  
  
 Usar uma abordagem como essa minimiza a variação para definições de função e associação de função no modelo, além de fornecer visibilidade das atribuições de função que tornam as permissões do cubo mais fáceis de implantar e manter.  
  
## <a name="see-also"></a>Consulte também  
 [Conceder direitos de administração de servidor a uma instância do Analysis Services](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [Funções e permissões &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md)   
 [Metodologias de autenticação com suporte no Analysis Services](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)  
  
  

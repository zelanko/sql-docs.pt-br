---
title: Conceder permissões de cubo ou modelo (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5943d9910c5499b92ea1ff927c2dbfb5d072b4af
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="grant-cube-or-model-permissions-analysis-services"></a>Conceder permissões de cubo ou modelo (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Um cubo ou modelo de tabela é o objeto de consulta principal em um modelo de dados do Analysis Services. Ao se conectarem a dados multidimensionais ou de tabela do Excel para exploração de dados ad hoc, normalmente os usuários começam ao selecionar um cubo ou modelo de tabela específico como a estrutura de dados por trás do objeto de relatório dinâmico. Este tópico explica como conceder as permissões necessárias para acesso de dados de cubo ou de tabela.  
  
 Por padrão, ninguém além do administrador do servidor ou do banco de dados tem permissão para consultar cubos em um banco de dados. O acesso ao cubo por um não administrador requer associação a uma função criada para o banco de dados que contém o cubo. A associação tem suporte para contas de usuário ou de grupo do Windows, que pode ser definida no Active Directory ou em um computador local. Antes de iniciar, identifique a quais contas serão atribuídas associações nas funções que você vai criar.  
  
 Ter acesso de **Read** ao cubo também transmite a permissão sobre as dimensões, grupos de medidas e perspectivas dentro dele. A maioria dos administradores concederá permissões de leitura no nível do cubo e restringirá permissões sobre objetos específicos, sobre dados associados ou por identidade do usuário.  
  
 Para preservar as definições de função por implantações de solução sucessivas, uma prática recomendada é definir as funções no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] como parte integrante do modelo e ter um administrador de banco de dados para atribuir associações de função no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] após o banco de dados ser publicado. No entanto, você pode usar uma ou outra ferramenta para ambas as tarefas. Para simplificar o exercício, usaremos [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] tanto para definição e quanto para associação de função.  
  
> [!NOTE]  
>  Apenas administradores de servidor ou de banco de dados com permissões de Controle Total podem implantar um cubo em um servidor a partir de arquivos de origem ou criar funções e atribuir membros. Consulte [Conceder direitos de administração de servidor a uma instância do Analysis Services](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md) ou [Conceder direitos de administração de banco de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md) para obter detalhes sobre esses níveis de permissão.  
  
#### <a name="step-1-create-the-role"></a>Etapa 1: Criar a função  
  
1.  No SSMS, conecte-se ao Analysis Services. Consulte [Conectar-se de aplicativos cliente &#40;Analysis Services&#41;](../../analysis-services/instances/connect-from-client-applications-analysis-services.md) se precisar de ajuda com esta etapa.  
  
2.  Abra a pasta **Bancos de Dados** no Pesquisador de Objetos e escolha um banco de dados.  
  
3.  Clique com o botão direito do mouse em **Funções** e escolha **Nova Função**. Observe que as funções são criadas no nível do banco de dados e se aplicam aos objetos dentro dele. Você não pode compartilhar funções entre bancos de dados.  
  
4.  No painel **Geral** , insira um nome e, opcionalmente, uma descrição. Este painel também contém várias permissões de banco de dados, tais como Controle Total, Processar Banco de Dados e Ler Definição. Nenhuma dessas permissões é necessária para consultar um cubo ou modelo de tabela. Consulte [Conceder permissões de banco de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md) para obter mais informações sobre essas permissões.  
  
5.  Vá para a próxima etapa após inserir um nome e a descrição opcional.  
  
#### <a name="step-2-assign-membership"></a>Etapa 2: Atribuir a associação  
  
1.  No painel **Associação** , clique em **Adicionar** para inserir as contas de usuário ou de grupo do Windows que acessarão o cubo usando a função. O Analysis Services tem suporte apenas para identidades de segurança do Windows. Observe que você não está criando logons de banco de dados nesta etapa. No Analysis Services, os usuários se conectam por meio de contas do Windows.  
  
2.  Vá para a próxima etapa para definir as permissões do cubo.  
  
     Observe que estamos pulando o painel de Fonte de Dados. A maioria dos usuários regulares de dados do Analysis Services não precisa de permissões no objeto da fonte de dados. Consulte [Conceder permissões em um objeto de fonte de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md) para obter detalhes sobre quando você pode definir essa permissão.  
  
#### <a name="step-3-set-cube-permissions"></a>Etapa 3: Definir as permissões do cubo  
  
1.  No painel **Cubos** , selecione um cubo e clique em acesso de **Leitura** ou **Leitura/Gravação** .  
  
     O acesso de**Leitura** é suficiente para a maioria das operações. **Leitura/Gravação** é usado apenas para cenários de write-back, e não de processamento. Consulte [Set Partition Writeback](../../analysis-services/multidimensional-models/set-partition-writeback.md) para obter mais informações sobre esse recurso.  
  
     Observe que você pode escolher vários cubos, bem como outros objetos disponíveis na caixa de diálogo Criar Função. Conceder permissões a um cubo autoriza o acesso às dimensões e perspectivas associadas ao cubo. Não é necessário adicionar manualmente objetos já representados no cubo.  
  
     Se você precisar variar autorização por objetos ou usuário, por exemplo, para tornar certas medidas indisponíveis, é possível permitir ou negar acesso atomicamente a objetos específicos e até mesmo a células. Consulte [Conceder acesso personalizado a dados da dimensão &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) e [Conceder acesso personalizado a dados de célula &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md) para obter detalhes.  
  
2.  Neste ponto, após clicar em **OK**, todos os membros dessa função terão acesso aos cubos nos níveis de permissão que você especificou.  
  
     Observe que no painel **Cubos** , você pode conceder permissões aos usuários para criarem cubos locais a partir de um cubo de servidor por meio de **Detalhamento e de Cubo de Local**ou permitir apenas detalhamento com a permissão **Detalhamento** .  
  
     Finalmente, este painel permite que você conceda direitos para **Processar banco de dados** no cubo, para permitir que todos os membros dessa função processem dados para o cubo. Como o processamento é normalmente uma operação restrita, recomendamos deixar essa tarefa para os administradores ou definir funções separadas, especialmente para essa tarefa. Consulte [Conceder permissões de processo &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md) para obter mais informações sobre as práticas recomendadas de permissão de processamento.  
  
#### <a name="step-4-test"></a>Etapa 4: Testar  
  
1.  Use o Excel para testar as permissões de acesso ao cubo. Você também pode usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], de acordo com técnica descrita a seguir, para executar o aplicativo como usuário não administrador.  
  
    > [!NOTE]  
    >  Se você for um administrador do Analysis Services, as permissões de administrador serão combinadas com as funções que têm menos permissões, dificultando o teste das permissões de funções isoladamente. Para simplificar o teste, sugerimos que você abra uma segunda instância do SSMS, usando a conta atribuída à função a qual você está testando.  
  
2.  Mantenha pressionada a tecla Shift e clique com o botão direito do mouse no atalho do **Excel** para acessar a opção **Executar como usuário diferente** . Insira uma das contas de usuário ou de grupo do Windows que tenha associação à função.  
  
3.  Quando o Excel abrir, use a guia Dados para se conectar ao Analysis Services. Como você está executando o Excel como um usuário diferente do Windows, a opção **Usar Autenticação do Windows** é o tipo de credencial correto para testar funções. Consulte [Conectar-se de aplicativos cliente &#40;Analysis Services&#41;](../../analysis-services/instances/connect-from-client-applications-analysis-services.md) se precisar de ajuda com esta etapa.  
  
     Se ocorrer erros durante a conexão, verifique a configuração de porta do Analysis Services e confirme se o servidor aceita conexões remotas. Consulte [Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) para configuração de porta.  
  
#### <a name="step-5-script-role-definition-and-assignments"></a>Etapa 5: Definição e atribuições de função de script  
  
1.  Como etapa final, gere um script que capture a definição da função que você acabou de criar.  
  
     Reimplantar um projeto a partir do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] substituirá quaisquer funções ou associações de função que não estejam definidas no projeto. A maneira mais rápida de recriar funções e associação de função após a reimplantação é o script.  
  
2.  No SSMS, navegue até a pasta **Funções** e clique com o botão direito do mouse em uma função existente.  
  
3.  Selecione **Script de Função como **arquivo**** | **CRIAR PARA** | .  
  
4.  Salve o arquivo com uma extensão .xmla. Para testar o script, exclua a função atual, abra o arquivo no SSMS e pressione F5 para executar o script.  
  
## <a name="next-step"></a>Próxima etapa  
 Você pode refinar as permissões do cubo para restringir acesso às células ou aos dados de dimensão. Consulte [Conceder acesso personalizado a dados da dimensão &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) e [Conceder acesso personalizado a dados de célula &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md) para obter detalhes.  
  
## <a name="see-also"></a>Consulte também  
 [Metodologias de autenticação com suporte no Analysis Services](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)   
 [Conceder permissões em estruturas de mineração de dados e modelos de &#40;do Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [Conceder permissões em um objeto de fonte de dados & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md)  
  
  

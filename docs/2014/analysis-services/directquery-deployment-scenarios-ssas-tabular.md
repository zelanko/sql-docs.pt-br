---
title: Cenários de implantação do DirectQuery (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2aaf5cb8-294b-4031-94b3-fe605d7fc4c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a62a05c8908391b9ce925ecfe08ae30540b8fa29
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081646"
---
# <a name="directquery-deployment-scenarios-ssas-tabular"></a>Cenários de implantação do DirectQuery (SSAS tabular)
  Este tópico fornece um passo a passo do processo de design e implantação para modelos DirectQuery. Você pode configurar o DirectQuery para usar somente dados relacionais (somente DirectQuery) ou pode configurar o modelo para alternar entre usar somente dados armazenados em cache ou somente dados relacionais (modo híbrido). Este tópico explica o processo de implementação para ambos os modos e descreve possíveis diferenças em resultados da consulta dependendo do modo e da configuração de segurança.  
  
 [Design e as etapas de implantação](#bkmk_DQProcedure)  
  
 [Comparando configurações do DirectQuery](#bkmk_Configurations)  
  
##  <a name="bkmk_DQProcedure"></a> Design e as etapas de implantação  
 **Etapa 1. Criar a solução**  
  
 Independentemente de qual modo você usará, você deve revisar as informações que descrevem as limitações nos dados que podem ser usados em modelos DirectQuery. Por exemplo, todos os dados usados em seu modelo e relatórios devem vir de um único banco de dados do SQL Server. Para obter mais informações, consulte [Modo DirectQuery &#40;SSAS Tabular&#41;](tabular-models/directquery-mode-ssas-tabular.md).  
  
 Além disso, revise as limitações em medidas e colunas calculadas, e determine se as fórmulas que você pretende usar são compatíveis com o modo DirectQuery. Você pode precisar remover ou modificar os elementos a seguir:  
  
-   Não há suporte para colunas calculadas.  
  
-   Dados copiados e colados não podem ser usados. Se você importar um modelo do PowerPivot para iniciar sua solução, exclua as tabelas vinculadas antes de importar a solução, porque estes dados não podem ser excluídos e podem bloquear a validação do DirectQuery.  
  
 **Etapa 2. Habilitar o modo DirectQuery no designer de modelo**  
  
 Por padrão, o DirectQuery fica desabilitado. Portanto, você deve configurar o ambiente de design para oferecer suporte ao modo DirectQuery.  
  
 Clique com botão direito do **Model. BIM** nó no Gerenciador de soluções e defina a propriedade **o modo DirectQuery**, para `On`.  
  
 Você pode ativar a qualquer momento o DirectQuery; porém, verifique se você não criou colunas ou fórmulas que são incompatíveis com o modo DirectQuery, é recomendável habilitar o modo DirectQuery desde o início.  
  
 Inicialmente, mesmo os modelos DirectQuery são sempre criados na memória. O modo de consulta padrão para o banco de dados do workspace também é definido como **DirectQuery com Na Memória**. Este modo de funcionamento híbrido permite usar o cache de dados importados para desempenho aprimorado durante o processo de design de modelo, enquanto valida o modelo para requisitos de DirectQuery.  
  
 **Etapa 3. Resolver erros de validação**  
  
 Se você obtiver erros de validação quando ativar o DirectQuery, ou quando adicionar novos dados ou fórmulas, abra a **Lista de Erros**do Visual Studio e execute as ações necessárias.  
  
-   Altere qualquer configuração de propriedade exigida para o modo DirectQuery, conforme descrito nas mensagens de erro.  
  
-   Remova colunas calculadas. Se você precisar de uma coluna calculada para uma medida específica, você sempre pode criar a coluna usando o [Designer de consultas relacionais &#40;SSAS&#41; ](relational-query-designer-ssas.md) fornecido no Assistente de importação de tabela.  
  
-   Modifique ou remova fórmulas que são incompatíveis com o modo DirectQuery. Se você precisar de uma função específica para um cálculo, pense em maneiras de fornecer um equivalente usando Transact-SQL.  
  
-   Adicione dados conforme necessário.  Se seu modelo anteriormente usou dados copiados e colados ou dados de provedores diferentes do SQL Server, você pode criar novas exibições e colunas derivadas dentro da conexão existente ou usar consultas distribuídas.  Todos os dados usados em um modelo DirectQuery devem estar acessíveis por uma única fonte de dados do SQL Server.  
  
 **Etapa 4. Definir o método preferencial para responder consultas no modelo**  
  
|||  
|-|-|  
|**Somente DirectQuery**|Defina a propriedade como **DirectQuery**.|  
|**Modo híbrido**|Defina a propriedade para **Na Memória com DirectQuery** ou **DirectQuery com Na Memória**.<br /><br /> Você pode alterar este valor posteriormente para usar uma preferência diferente.<br /><br /> Observe que os clientes podem substituir o método preferido na cadeia de conexão.|  
  
 **Etapa 5. Especifique a partição DirectQuery**  
  
|||  
|-|-|  
|**Somente DirectQuery**|Opcional. Um modelo somente DirectQuery não precisa de uma partição.<br /><br /> Porém, se você criou partições no modelo durante a fase de design, lembre-se de que somente uma partição pode ser usada como a fonte de dados. Por padrão, a primeira partição que você criou será usada como a partição DirectQuery.<br /><br /> Para garantir que todos os dados exigidos pelo modelo estejam disponíveis pela partição DirectQuery, escolha uma partição DirectQuery e edite a instrução SQL para obter o conjunto de dados inteiro.|  
|**Modo híbrido**|Se alguma tabela em seu modelo tiver várias partições, você deverá escolher uma única partição como a *partição DirectQuery*. Se você não atribuir uma partição, por padrão, a primeira partição que foi criada será usada como a partição DirectQuery.<br /><br /> Defina opções de processamento em todas as partições exceto a DirectQuery. Normalmente a partição DirectQuery nunca é processada, porque os dados são passados por meio da fonte relacional.<br /><br /> Para obter mais informações, consulte [partições e modo DirectQuery &#40;SSAS de tabela&#41;](tabular-models/define-partitions-in-directquery-models-ssas-tabular.md).|  
  
 **Etapa 6. Configurar a representação**  
  
 A representação tem suporte somente para modelos DirectQuery. A opção de representação, **Configurações da representação**, define as credenciais que são usadas ao exibir dados da fonte de dados do SQL Server especificada.  
  
|||  
|-|-|  
|**Somente DirectQuery**|Para a propriedade  **Configurações de Representação** , especifique a conta que será usada na conexão à fonte de dados do SQL Server.<br /><br /> Se você usar o valor, **ImpersonateCurrentUser**, a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que hospeda o modelo passará as credenciais do usuário atual do modelo para o banco de dados do SQL Server.|  
|**Modo híbrido**|Para a propriedade **Configurações de Representação** , especifique a conta que será usada para acessar os dados na fonte de dados do SQL Server.<br /><br /> Esta configuração não afeta as credenciais que são usadas para processar o cache usado pelo modelo.|  
  
 **Etapa 7. Implantar o modelo**  
  
 Quando você estiver pronto para implantar o modelo, abra o **Project** menu do Visual Studio e selecione **propriedades**. Defina a propriedade **QueryMode** para um dos valores descritos na tabela a seguir:  
  
 Para obter mais informações, consulte [implantar do SQL Server Data Tools &#40;SSAS de tabela&#41;](tabular-models/deploy-from-sql-server-data-tools-ssas-tabular.md).  
  
|||  
|-|-|  
|**Somente DirectQuery**|**DirectQueryOnly**<br /><br /> Como você só especificou Consulta Direta, os metadados do modelo serão implantados no servidor, mas o modelo não será processado.<br /><br /> Observe que o cache que foi usado pelo banco de dados de workspace não será excluído automaticamente. Se você desejar garantir que os usuários não possam consultar os dados armazenados em cache, talvez convenha desmarcar o cache de tempo de design. Para obter mais informações, consulte [limpar os Caches do Analysis Services](instances/clear-the-analysis-services-caches.md).|  
|**Modo híbrido**|**DirectQuery com na memória**<br /><br /> **Na memória com DirectQuery**<br /><br /> Ambos os valores lhe permitem usar o cache ou a fonte de dados relacional, conforme necessário. A ordem define qual fonte de dados é usada por padrão ao responder consultas no modelo.<br /><br /> Em um modo híbrido, o cache deve ser processado ao mesmo tempo que os metadados modelo são implantados no servidor.<br /><br /> Você pode alterar esta configuração depois da implantação.|  
  
 **Etapa 8. Verifique se o modelo implantado**  
  
 No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], abra a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] na qual o modelo foi implantado. Clique com o botão direito do mouse no nome do banco de dados e selecione **Propriedades**.  
  
-   A propriedade, **DirectQueryMode**, foi definida quando você definiu as propriedades de implantação.  
  
-   A propriedade, **Informações de Representação de Fonte de Dados**, foi definida quando você definiu as opções de representação de usuário. Para obter mais informações, consulte [Definir opções de representação &#40;SSAS – Multidimensional&#41;](multidimensional-models/set-impersonation-options-ssas-multidimensional.md).  
  
-   Após a implantação do modelo, você poderá alterar essas propriedades.  
  
##  <a name="bkmk_Configurations"></a> Comparando opções do DirectQuery  
 **Somente DirectQuery**  
 Esta opção é preferida quando você deseja garantir uma única origem de dados, ou quando seus dados são muito grandes para caber na memória. Se você estiver trabalhando com uma fonte de dados relacional muito grande, durante o tempo de design, pode criar o modelo usando um subconjunto dos dados. Quando você implanta o modelo no modo somente DirectQuery, pode editar a definição de fonte de dados para incluir todos os dados necessários.  
  
 Esta opção também será preferida se você desejar usar a segurança fornecida pela fonte de dados relacional para controlar acesso aos dados de usuário. Com modelos de tabela armazenados em cache, você pode usar também funções [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] a acesso de dados de controle, mas os dados armazenados no cache também deve ser protegido. Você sempre deveria usar esta opção se seu contexto de segurança requerer aqueles dados nunca deveriam ser armazenados em cache.  
  
 A tabela a seguir descreve os possíveis resultados de implantação para o modo somente DirectQuery:  
  
|||  
|-|-|  
|**DirectQuery sem cache**|Nenhum dado é carregado no cache. O modelo nunca pode ser processado.<br /><br /> O modelo só pode ser consultado usando clientes que suporte consultas de DAX. Especifica a origem da qual os resultados da consulta são retornados.<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode** = **DirectQuery**|  
|**DirectQuery com consultas apenas no cache**|Falha na implantação. Não há suporte para essa configuração.<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode** = **Na Memória**|  
  
 **Modo híbrido**  
 A implantação de seu modelo em um modo híbrido tem muitas vantagens: você pode obter dados atualizados da fonte de dados do SQL Server, se necessário, mas a preservação do cache oferece a possibilidade de trabalhar com dados na memória para melhorar o desempenho ao criar relatórios ou testar o modelo.  
  
 Um modo híbrido do DirectQuery também será útil se seu modelo for muito grande. Em vez de os usuários acessarem dados obsoletos ou o modelo estar indisponível enquanto o cache estiver sendo processado, você pode alternar o modelo para a modo DirectQuery durante o processamento. Os usuários poderiam experimentar o desempenho ligeiramente mais lento mas eles obteriam dados diretamente do repositório relacional, garantindo que os resultados fossem atualizados.  
  
 A tabela a seguir compara o resultado de implantação em cada uma das combinações de opções do DirectQuery.  
  
|||  
|-|-|  
|**Modo híbrido com cache preferida**|O modelo pode ser processado e dados podem ser carregados no cache. Consultas usam o cache por padrão.  Se um cliente desejar usar a origem de DirectQuery, um parâmetro deverá ser inserido na cadeia de conexão.<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode** = **In-Memory with DirectQuery**|  
|**Modo híbrido com DirectQuery preferida**|O modelo pode ser processado e dados podem ser carregados no cache. Porém, consultas usam o DirectQuery por padrão. Se um cliente desejar usar os dados em cache, deverá ser inserido um parâmetro na cadeia de conexão. Se as tabelas do modelo forem particionadas, a partição principal do cache de dados também será definida como **Na Memória com DirectQuery**.<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode** = **DirectQuery com Na Memória**|  
  
## <a name="see-also"></a>Consulte também  
 [Modo DirectQuery &#40;SSAS de tabela&#41;](tabular-models/directquery-mode-ssas-tabular.md)   
 [Acesso a dados de modelo de tabela](tabular-models/tabular-model-data-access.md)  
  
  

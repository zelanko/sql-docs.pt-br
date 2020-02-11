---
title: Modo DirectQuery (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.realtime.f1
ms.assetid: 45ad2965-05ec-4fb1-a164-d8060b562ea5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9a9c1510030f61896f686b49f4bc134a7dfcb42b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67284870"
---
# <a name="directquery-mode-ssas-tabular"></a>Modo DirectQuery (SSAS tabular)
  O Analysis Services permite recuperar dados e criar relatórios de um modelo de tabela, recuperando dados e agregações diretamente de um sistema de banco de dados relacional, usando o *modo DirectQuery*. Este tópico apresenta as diferenças entre modelos de tabela padrão que só residem na memória e modelos de tabela que podem consultar uma fonte de dados relacional, e também explica como você pode criar e implantar um modelo para usar no modo DirectQuery.  
  
 Seções neste tópico:  
  
-   [Benefícios do modo DirectQuery](#bkmk_Benefits)  
  
-   [Criando modelos para uso com o modo DirectQuery](#bkmk_Design)  
  
    -   [Data Sources for DirectQuery Models](directquery-mode-ssas-tabular.md#bkmk_DataSources)  
  
    -   [Validação e restrições de design para o modo DirectQuery](#bkmk_Validation)  
  
    -   [Compatibilidade de fórmulas para modelos DirectQuery](#bkmk_FormulaCompat)  
  
    -   [Segurança no modo DirectQuery](#bkmk_Security)  
  
    -   [Segurança no modo DirectQuery](#bkmk_Security)  
  
-   [Propriedades DirectQuery](#bkmk_PropertyList)  
  
-   [Tópicos relacionados e tarefas](#bkmk_related_tasks)  
  
##  <a name="bkmk_Benefits"></a>Benefícios do modo DirectQuery  
 Por padrão, modelos de tabela usam um cache na memória para armazenar e consultar dados. Como modelos de tabela usam dados que residem na memória, até mesmo consultas complexas podem ser inacreditavelmente rápidas. Contudo, o uso de dados armazenados em cache apresenta algumas desvantagens:  
  
-   Os dados não são atualizados quando os dados de origem são alterados. Processe o modelo para obter atualizações nos dados.  
  
-   Quando você desativar o computador que hospeda o modelo, o cache será salvo em disco e deverá ser reaberto quando você carregar o modelo ou abrir o arquivo do PowerPivot. As operações de salvamento e carregamento podem ser demoradas.  
  
 Em contraste, o modo DirectQuery usa dados que são armazenados em um banco de dados do SQL Server.  Geralmente, você importa todos os dados ou uma pequena amostra deles para o cache ao criar o modelo e, quando implanta o modelo, especifica que a fonte de dados para consultas no modelo deve ser o SQL Server, e não os dados armazenados em cache. As consultas DAX nos dados são convertidas pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em instruções SQL equivalentes na fonte de dados relacional especificada.  
  
 Há muitas vantagens em implantar um modelo usando o modo DirectQuery:  
  
-   É possível ter um modelo sobre conjuntos de dados que são muito grandes para caber na memória no servidor do Analysis Services.  
  
-   Os dados são certamente atualizados e não há sobrecarga de gerenciamento adicional pela manutenção de uma cópia separada dos dados. As alterações nos dados de origem subjacentes podem ser refletidas imediatamente em consultas no modelo de dados.  
  
-   O DirectQuery pode aproveitar a aceleração de consulta no lado do provedor, como a fornecida por índices columnstore xVelocity de memória otimizada.  
  
-   Qualquer segurança imposta pelo banco de dados back-end é certamente imposta, usando a segurança em nível de linha. Em contraste, se você estiver usando dados armazenados em cache, talvez encontre dificuldade em garantir que o cache esteja protegido exatamente da mesma forma que no servidor.  
  
-   Se o modelo contiver fórmulas complexas que possam exigir várias consultas, o Analysis Services poderá executar a otimização para garantir que o plano de consulta da consulta executado no banco de dados back-end seja o mais eficiente possível.  
  
##  <a name="bkmk_Design"></a>Criando modelos para uso com o modo DirectQuery  
 Modelos de tabela são criados usando o designer de modelo do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. O designer cria todos os modelos na memória, o que significa que, quando você está criando modelos, se seus dados são muito grandes para ajuste na memória, você deve importar somente um subconjunto de dados para o cache usado pelo banco de dados de workspace.  
  
 Quando você estiver pronto para alternar para o modo DirectQuery, pode alterar uma propriedade que habilita o modo DirectQuery. Para obter mais informações, consulte [habilitar modo de design do DirectQuery &#40;SSAS de tabela&#41;](enable-directquery-mode-in-ssdt.md).  
  
 Quando você fizer isso, o designer de modelo configurará automaticamente o banco de dados de workspace para execução em um modo híbrido que permite continuar trabalhando com os dados armazenados em cache. O designer de modelo também o notificará sobre qualquer recurso em seu modelo que seja incompatível com o modo DirectQuery. A seguinte lista resume os requisitos principais a serem considerados:  
  
-   **Fontes de dados:** Os modelos DirectQuery só podem usar dados de uma única fonte de dados SQL Server. Quando o modo DirectQuery for ativado para um modelo, você não poderá usar outros tipos de dados no designer de modelo, inclusive tabelas adicionadas por operações de copiar-colar. Todas as outras opções de importação são desabilitadas. Qualquer tabela incluída em uma consulta deve fazer parte da fonte de dados do SQL Server. Consulte [Data Sources for DirectQuery Models](directquery-mode-ssas-tabular.md#bkmk_DataSources)para obter mais informações.  
  
-   **Suporte para colunas calculadas:** Não há suporte para colunas calculadas para modelos DirectQuery. Porém, você pode criar medidas e KPIs que operam em conjuntos de dados. Consulte a seção sobre [validação](#bkmk_Validation) para obter mais informações.  
  
-   **Uso limitado de funções Dax:** Algumas funções DAX não podem ser usadas no modo DirectQuery, portanto, você deve substituí-las por outras funções ou criar os valores usando colunas derivadas na fonte de dados. O designer de modelo oferece validação em tempo de design para qualquer erro que ocorra quando você cria fórmulas que são incompatíveis com o modo DirectQuery. Consulte as seções a seguir para obter mais informações: [Validação](#bkmk_Validation).  
  
-   **Compatibilidade de fórmulas:** Em determinados casos conhecidos, a mesma fórmula pode retornar resultados diferentes em um modelo em cache ou híbrido comparado a um modelo DirectQuery que usa apenas o repositório de dados relacional. Estas diferenças são uma consequência das diferenças semânticas entre o mecanismo analítico na memória xVelocity (VertiPaq) e o SQL Server. Para obter mais informações sobre essas diferenças, consulte esta seção: [Compatibilidade de fórmulas](#bkmk_FormulaCompat).  
  
-   **Segurança:** Você pode usar métodos diferentes para proteger modelos dependendo de como eles são implantados. Dados armazenados em cache para modelos de tabela são protegidos através do modelo de segurança da instância do Analysis Services. Modelos DirectQuery podem ser protegidos através de funções, mas você também pode usar segurança definida no repositório de dados relacional. O modelo pode ser configurado para que os usuários que abrem um relatório baseado em um modelo apenas DirectQuery podem ver apenas os dados aos quais têm permissão no SQL Server. Consulte esta seção para obter mais informações: [Segurança](#bkmk_Security).  
  
-   **Restrições de cliente:** Quando um modelo está no modo DirectQuery, ele só pode ser consultado usando DAX. Você não pode usar MDX para criar consultas. Isso significa que você não pode usar o Cliente Dinâmico do Excel porque o Excel usa MDX.  
  
     No entanto, você pode criar consultas em um modelo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] DirectQuery no se usar uma consulta de tabela Dax como parte de uma instrução de execução XMLA, para obter mais informações, consulte [referência de sintaxe de consulta Dax] (/DAX/Dax-Syntax-Reference
  
 Quando você tiver resolvido todos os problemas de design e testado seu modelo, estará pronto para a implantação. Neste momento, você pode definir o método preferencial para responder consultas em relação ao modelo. Você deseja que os usuários tenham acesso ao cache ou que sempre usem apenas a fonte de dados relacional?  
  
 Se você implantar o modelo em um *modo híbrido*, o cache ainda estará disponível e poderá ser usado para consultas. Um modo híbrido oferece várias opções:  
  
-   Quando o cache e a fonte de dados relacional estão disponíveis, você pode definir o método de conexão preferencial, mas é o cliente quem controla a fonte a ser usada, usando a propriedade de cadeia de conexão do DirectQueryMode.  
  
-   Você também pode configurar partições no cache de tal um modo que a partição primária usada no modo DirectQuery nunca seja processada e sempre referencie a fonte relacional. Há muitas formas de usar partições para otimizar o design de modelo e a experiência de relatórios. Para obter mais informações, consulte [partições e o modo DirectQuery &#40;SSAS tabular&#41;](define-partitions-in-directquery-models-ssas-tabular.md).  
  
-   Após a implantação do modelo, você pode alterar o método de conexão preferencial. Por exemplo, você pode usar um modo híbrido para testes e alternar o modelo para **apenas DirectQuery** somente depois de testar bem relatórios ou consultas que usam o modelo. Para obter mais informações, consulte [Definir ou alterar o método de conexão preferencial para DirectQuery](../set-or-change-the-preferred-connection-method-for-directquery.md).  
  
###  <a name="bkmk_DataSources"></a>Fontes de dados para modelos DirectQuery  
 Assim que você alterar o ambiente de design para habilitar o modo DirectQuery, as fontes de dados para o banco de dados de workspace serão validadas para garantir que elas provenham de uma única fonte de dados do SQL Server. Dados de outras fonte, inclusive dados copiados e colados, não são permitidos em modelos DirectQuery.  
  
 Se você pretende usar o modelo no modo DirectQuery, verifique se todos os dados necessários para relatórios estão armazenados no banco de dados do SQL Server especificado. Se os dados necessários para modelagem não estiverem disponíveis nesta origem, considere o uso do Integration Services ou de outras ferramentas de armazenagem de dados para importar os dados para um banco de dados do SQL Server que serve como a fonte de dados DirectQuery.  
  
###  <a name="bkmk_Validation"></a>Validação e restrições de design para o modo DirectQuery  
 Quando você criar um modelo para usar no modo DirectQuery, carregue inicialmente uma parte dos dados no cache. Se os dados que você usar eventualmente forem muito grandes para caber na memória, você poderá usar a opção de **filtro & de visualização** no assistente de importação de tabela para selecionar um subconjunto de dados ou gravar um script SQL para obter os dados desejados.  
  
> [!WARNING]  
>  Como o modo DirectQuery não oferece suporte ao uso de colunas calculadas, se houver colunas nas quais você deseja combinar ou executar outras operações, planeje previamente e crie a definição de coluna como parte de sua consulta de importação de dados ou script.  
  
 Para exibir e resolver erros de validação, abra a **Lista de Erros** no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Erros críticos que impedem o uso do modo DirectQuery são exibidos na guia **erros** . Você deve corrigir esses erros antes de alterar para o modo DirectQuery. Os erros de validação com maior dificuldade de solução costumam estar relacionados a fórmulas sem suporte no modo DirectQuery. Consulte a seção, [Compatibilidade de Fórmula](#bkmk_FormulaCompat), para obter uma visão geral de erros relacionados a fórmulas e colunas calculadas.  
  
 A seguinte lista descreve outras considerações ao criar um modelo para acesso do DirectQuery:  
  
-   Quando estiver no modo *apenas DirectQuery* , os resultados em um relatório podem variar de acordo com o contexto de segurança do usuário que está exibindo os resultados. Você deve testar modelos com credenciais diferentes para garantir que usuários obtenham os resultados esperados.  
  
-   Se você configurar um modelo para operar no modo híbrido, o que permite o uso do cache ou de dados do SQL Server, lembre-se de que clientes conectando-se a cada origem podem obter resultados diferentes, dependendo do modo especificado na cadeia de conexão. Se você precisar certificar-se de que seus usuários de relatório só vejam dados do SQL Server, deverá limpar o cache ou alterar o modelo para DirectQueryOnly.  
  
###  <a name="bkmk_FormulaCompat"></a>Compatibilidade de fórmulas para modelos DirectQuery  
 Alguns modelos podem conter fórmulas sem suporte no modo DirectQuery e o modelo deve ser reformulado para impedir erros de validação. Restrições em fórmulas sem suporte no modo DirectQuery incluem o seguinte:  
  
-   Colunas calculadas não têm suporte em modelos de tabela com o modo DirectQuery habilitado, nem mesmo em modelos híbridos. Se você precisar de colunas calculadas para um modelo, pense na possibilidade de convertê-las em colunas derivadas usando o Transact-SQL em sua definição de importação.  
  
-   Modelos DirectQuery não oferecem suporte ao uso de fórmulas DAX em medidas, que são convertidas em operações baseadas em conjunto no repositório de dados relacional. Todas as medidas que você cria usando medidas implícitas têm suporte.  
  
-   Nem todas as funções têm suporte. Como o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] converte todas as fórmulas DAX e definições de medida em instruções SQL ao consultar um modelo DirectQuery, qualquer fórmula contendo elementos que não podem ser convertidos no Transact-SQL disparará erros de validação no modelo. Por exemplo, funções de inteligência de dados temporais não têm suporte. Até mesmo funções com suporte podem apresentar outro comportamento, como as funções estatísticas. Para obter uma lista completa de problemas de compatibilidade, consulte [compatibilidade de fórmula no modo DirectQuery](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md).  
  
-   Algumas fórmulas no modelo podem ser validadas quando você alterna o modelo para o modo DirectQuery, mas retornam resultados diferentes quando executadas no cache versus armazenamento de dados relacionais. Isso ocorre porque cálculos em relação ao uso de cache usam a semântica do mecanismo analítico na memória xVelocity (VertiPaq), que contém muitos recursos que visam emular o comportamento do Excel, enquanto consultas a dados armazenados no repositório de dados relacional necessariamente usam a semântica do SQL Server. Para obter uma lista de funções DAX que podem retornar resultados diferentes quando o modelo é implantado em tempo real, consulte [compatibilidade de fórmula no modo DirectQuery](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md).  
  
###  <a name="bkmk_Connecting"></a>Conectando a modelos DirectQuery  
 Clientes que usam MDX como a linguagem de consulta não podem se conectar a modelos que usam o modo DirectQuery. Por exemplo, se você tentar criar uma consulta MDX em um modelo DirectQuery, obterá um erro indicando que o cubo não pode ser localizado, ou não foi processado. Você pode criar consultas em modelos DirectQuery usando o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], fórmulas DAX ou consultas XMLA. Para obter mais informações sobre como você pode executar consultas ad hoc em modelos de tabela, consulte [Tabular Model Data Access](tabular-model-data-access.md).  
  
 Se você estiver usando um modelo híbrido, poderá especificar se os usuários conectam-se ao cache ou usam dados do DirectQuery especificando a propriedade de cadeia de conexão, DirectQueryMode.  
  
###  <a name="bkmk_Security"></a>Segurança no modo DirectQuery  
 Durante a criação de modelos, você especifica as permissões que são usadas para recuperar os dados de origem. Isso geralmente será suas próprias credenciais ou uma conta usada para desenvolvimento. Porém, quando você alterna o modelo para usar o modo DirectQuery, o contexto de segurança é mais complexo:  
  
-   Considere se os usuários têm o nível necessário de acesso aos dados no repositório de dados relacional.  
  
-   Os usuários que exibem o mesmo modelo ou relatório podem ver dados diferentes, dependendo do contexto de segurança do usuário.  
  
-   Se o cache de modelo foi preservado, o cache será protegido usando o modelo de segurança (funções) do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . O cache pode conter dados que o designer de modelo tem o privilégio de visualizar, mas não o usuário. Designers de modelo ou relatório devem limpar o cache ou proteger esses dados controlando o acesso por meio de funções.  
  
-   Um modelo que responde consultas do cache não pode representar o usuário atual ao conectar-se à fonte de dados. Se você desejar representar o usuário atual ao conectar-se à fonte de dados, deverá usar o modo DirectQuery.  
  
-   Se seu modelo de relatório exige segurança, você tem duas opções: pode usar funções [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou definir permissões em nível de linha na fonte de dados. A segurança na fonte de dados relacional é usada para controlar o acesso a tabelas e a segurança em nível de coluna não tem suporte. Portanto, se os usuários em uma região não tiverem permissão para exibir valores de vendas de regiões diferentes, um relatório que inclua uma medida baseada na tabela Vendas retornará espaços em branco ou um erro.  
  
 A propriedade das configurações de representação especifica as credenciais usadas quando você está se conectando a um modelo usando DirectQuery, para um modelo somente DirectQuery ou para um modelo híbrido que responde consultas usando DirectQuery. A propriedade tem os valores seguintes:  
  
 **Default**  
 Usa as credenciais especificadas no assistente de importação para conectar-se à fonte de dados. Isso pode ser um usuário específico do Windows ou uma conta de serviço.  
  
 `ImpersonateCurrentUser`  
 Usa as credenciais do usuário atual para conectar-se à fonte de dados.  
  
 Para obter informações sobre como definir essas propriedades, consulte [cenários de implantação do DirectQuery &#40;SSAS de tabela&#41;](../directquery-deployment-scenarios-ssas-tabular.md).  
  
##  <a name="bkmk_PropertyList"></a>Propriedades do DirectQuery  
 A tabela a seguir lista as propriedades que você pode definir no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]e no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]para habilitar o DirectQuery e controlar a origem de dados usada em consultas no modelo.  
  
|Nome da propriedade|DESCRIÇÃO|  
|-------------------|-----------------|  
|**Propriedade DirectQueryMode**|Esta propriedade habilita o uso do modo DirectQuery no designer de modelo. Você deve definir esta propriedade como `On` para alterar qualquer outra propriedade DirectQuery.<br /><br /> Para obter mais informações, consulte [habilitar modo de design do DirectQuery &#40;SSAS de tabela&#41;](enable-directquery-mode-in-ssdt.md).|  
|**Propriedade QueryMode**|Esta propriedade especifica o método de consulta padrão para um modelo DirectQuery. Você define esta propriedade no designer de modelo quando implanta o modelo, mas pode substituí-la posteriormente. A propriedade tem estes valores:<br /><br /> **DirectQuery** -essa configuração especifica que todas as consultas ao modelo devem usar somente a fonte de dados relacional.<br /><br /> **DirectQuery com na memória** – essa configuração especifica, por padrão, que as consultas devem ser respondidas usando a origem relacional, a menos que especificado em contrário na cadeia de conexão do cliente.<br /><br /> **Na memória** -essa configuração especifica que as consultas devem ser respondidas usando apenas o cache.<br /><br /> **Na memória com DirectQuery** – essa configuração especifica, por padrão. que as consultas devem ser respondidas usando o cache, a menos que especificado em contrário na cadeia de conexão do cliente.<br /><br /> <br /><br /> Para obter mais informações, consulte [Definir ou alterar o método de conexão preferencial para DirectQuery](../set-or-change-the-preferred-connection-method-for-directquery.md).|  
|**Propriedade DirectQueryMode**|Depois que o modelo for implantado, você poderá alterar a fonte de dados de consulta preferencial para um modelo DirectQuery, alterando esta propriedade no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]<br /><br /> Como a propriedade anterior, esta propriedade especifica a fonte de dados padrão para o modelo e tem estes valores:<br /><br /> **Inmemory**: as consultas podem usar somente o cache.<br /><br /> **DirectQuerywithInMemory**: as consultas usam a fonte de dados relacional por padrão, a menos que especificado de outra forma na cadeia de conexão do cliente.<br /><br /> **InMemorywithDirectQuery**: as consultas usam o cache por padrão, a menos que especificado de outra forma na cadeia de conexão do cliente.<br /><br /> (**DirectQuery**: As consultas só usam a fonte de dados relacional.<br /><br /> <br /><br /> Para obter mais informações, consulte [Definir ou alterar o método de conexão preferencial para DirectQuery](../set-or-change-the-preferred-connection-method-for-directquery.md).|  
|**Propriedade Impersonation Settings**|Esta propriedade define as credenciais usadas na conexão à fonte de dados do SQL Server no momento de consulta. Você pode definir esta propriedade no designer de modelo e alterar o valor posteriormente, depois da implantação do modelo.<br /><br /> Observe que estas credenciais são usadas apenas para responder consultas no repositório de dados relacional; elas não são iguais às credenciais usadas para processar o cache de um modelo híbrido.<br /><br /> A representação não pode ser usada quando o modelo é usado apenas na memória. A configuração `ImpersonateCurrentUser` é inválida, a menos que o modelo esteja usando o modo DirectQuery.|  
  
 Além disso, se seu modelo incluir partições, escolha uma partição para usar como a fonte de consultas no modo DirectQuery. Para obter mais informações, consulte [partições e o modo DirectQuery &#40;SSAS tabular&#41;](define-partitions-in-directquery-models-ssas-tabular.md).  
  
##  <a name="bkmk_related_tasks"></a>Tópicos e tarefas relacionados  
  
|Tópico|DESCRIÇÃO|  
|-----------|-----------------|  
|[Partições e o modo DirectQuery &#40;SSAS de tabela&#41;](define-partitions-in-directquery-models-ssas-tabular.md)|Descreve como as partições são usadas em modelos configurados para o modo DirectQuery.|  
|[Compatibilidade de fórmula DAX no modo DirectQuery](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md)|Descreve restrições e requisitos de compatibilidade nas fórmulas que você pode usar em modelos configuradas para o modo DirectQuery.|  
|[Habilitar modo de design do DirectQuery &#40;SSAS de tabela&#41;](enable-directquery-mode-in-ssdt.md)|Descreve como você pode alterar o ambiente de tempo de design de modo que dê suporte ao uso do modo DirectQuery|  
|[Alterar a partição DirectQuery &#40;SSAS de tabela&#41;](../change-the-directquery-partition-ssas-tabular.md)|Descreve como alterar a partição do DirectQuery.|  
|[Definir ou alterar o método de conexão preferencial para DirectQuery](../set-or-change-the-preferred-connection-method-for-directquery.md)|Descreve como definir ou alterar o método de conexão para modelos configurados para DirectQuery.|  
|[Cenários de implantação do DirectQuery &#40;SSAS de tabela&#41;](../directquery-deployment-scenarios-ssas-tabular.md)|Descreve cenários de implantação do DirectQuery.|  
|[Configure o Acesso Na Memória ou DirectQuery para um banco de dados modelo de tabela](enable-directquery-mode-in-ssms.md)|Saiba mais sobre as configurações do DirectQuery|  
|[Limpar os caches do Analysis Services](../instances/clear-the-analysis-services-caches.md)|Limpe o cache do modelo de tabela|  
  
## <a name="see-also"></a>Consulte Também  
 [Partições &#40;SSAS de tabela&#41;](partitions-ssas-tabular.md)   
 [Projetos de modelo de tabela &#40;SSAS de tabela&#41;](tabular-model-projects-ssas-tabular.md)   
 [Analisar no Excel &#40;SSAS de tabela&#41;](analyze-in-excel-ssas-tabular.md)  

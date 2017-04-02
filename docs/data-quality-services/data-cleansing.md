---
title: "Limpeza de Dados | Microsoft Docs"
ms.custom: ""
ms.date: "10/01/2012"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e67136cc-f8c6-4cb3-ba0b-c966c636256c
caps.latest.revision: 31
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 31
---
# Limpeza de Dados
  Limpeza de dados é o processo de analisar a qualidade de dados em uma fonte de dados, aprovando/rejeitando as sugestões manualmente pelo sistema e fazer alterações assim aos dados. A limpeza de dados no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) inclui um processo auxiliado por computador que analisa a conformidade dos dados em relação ao conhecimento de uma base de dados de conhecimento, e um processo interativo que permite que o administrador de dados examine e modifique resultados de processo auxiliado por computador para garantir que a limpeza de dados seja executada exatamente como desejado.  
  
 O administrador de dados também pode executar a limpeza de dados no processo de empacotamento do Integration Services. Neste caso, o administrador de dados deve usar um componente do [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)] que executa automaticamente a limpeza de dados com o uso de uma base de conhecimento existente. Para obter mais informações, consulte [transformação de limpeza do DQS](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md).  
  
 O recurso de limpeza de dados no DQS tem os seguintes benefícios:  
  
-   Identifica dados incompletos ou incorretos em sua fonte de dados (arquivo do Excel ou banco de dados do SQL Server) e então corrige ou o alerta sobre os dados inválidos.  
  
-   Fornece um processo de duas etapas para limpar os dados: *auxiliada por computador* e *interativo*. O processo por computador usa o conhecimento em uma base de conhecimento de DQS para processar os dados automaticamente e sugere substituições/correções. A próxima etapa, interativa, permite que o administrador de dados aprove, rejeite ou modifique as alterações propostas pelo DQS durante a limpeza auxiliada por computador.  
  
-   Unifica e enriquece dados de cliente usando valores de domínio, regras de domínio e dados de referência. Por exemplo, padronize o uso do termo alterando "R." por "Rua", enriqueça os dados inserindo elementos ausentes ao alterar "1 Microsoft way Redmond 98006" por "1 Microsoft Way, Redmond, WA 98006".  
  
-   Oferece uma interface de assistente simples, intuitiva e consistente para que o usuário navegue pelos dados e inspecione erros em um conjunto muito grande de dados.  
  
 A ilustração seguinte mostra como a limpeza de dados é feita no DQS:  
  
 ![Processo de Limpeza de Dados do DQS](../data-quality-services/media/dqs-cleansingprocess.gif "Processo de Limpeza de Dados do DQS")  
  
##  <a name="ComputerAssisted"></a> Limpeza auxiliada por computador  
 O processo de limpeza de dados do DQS aplica a base de conhecimento aos dados a serem limpos e propõe alterações nos dados. O administrador de dados tem acesso a cada alteração proposta, o que permite que ele avalie e corrija as alterações. Para executar a limpeza de dados, o administrador de dados procede da seguinte maneira:  
  
1.  Criar um projeto de qualidade de dados, selecione uma base de dados de conhecimento em relação ao qual você deseja analisar e limpar sua fonte de dados e selecione o **Limpeza** atividade. Vários projetos de qualidade de dados podem usar a mesma base de dados de conhecimento.  
  
2.  Especifique a tabela de banco de dados/exibição ou um arquivo do Excel que contenha os dados de origem a serem limpos. O banco de dados ou o arquivo do Excel pode ser o mesmo que foi usado para a descoberta de conhecimento ou pode ser um banco de dados ou arquivo do Excel diferente.  
  
    > [!NOTE]  
    >  Se você selecionar a mesma fonte de dados para atividades de descoberta de conhecimento e de limpeza, não haverá nenhuma alteração aos dados. É recomendado que você execute a descoberta de conhecimento em dados de exemplo e posteriormente limpe seus dados de origem em relação ao conhecimento compilado durante a atividade de descoberta de conhecimento.  
  
3.  Mapeie os campos de dados a ser limpos para os domínios/domínios compostos apropriados na base de dados de conhecimento. Se você mapear um campo para um domínio composto, o mapeamento acontecerá entre o campo e o domínio composto, e não com os domínios individuais no domínio composto. Além disso, a limpeza de dados para o campo mapeado é feita com base nas regras especificadas para o domínio composto, e não para os domínios individuais no domínio composto. Para obter mais informações sobre domínios compostos, consulte [Bases de conhecimento do DQS e domínios](../data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
4.  Execute o processo de limpeza auxiliada por computador clicando **Iniciar** sobre o **Limpar** página.  
  
 O processo de limpeza de dados localiza a melhor correspondência de uma instância de dados a valores de domínio de dados conhecidos. O processo aplica conhecimento de qualidade de dados a todos os dados de origem, ao contrário do processo de descoberta da base de dados de conhecimento que é executado em um percentual dos dados de exemplo.  
  
 O processo auxiliado por computador exibe informações de qualidade dos dados no [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] que serão usadas no processo de limpeza interativo. Além da aderência às regras de erro de sintaxe, o DQS também usa dados de referência e algoritmos avançados para categorizar dados usando *nível de confiança*. O nível de confiança indica a extensão de certeza do DQS para a correção ou sugestão. O nível de confiança é baseado nos valores de limite a seguir:  
  
-   Um *limite de correção automática* valor acima do qual DQS irá sugerir uma alteração e torná-lo, a menos que o administrador de dados rejeitará. Você pode especificar o valor de limite de correção automática na guia **Configurações Gerais** na tela **Configuração** . Para obter mais informações, consulte [Configure Threshold Values for Cleansing and Matching](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md).  
  
-   Um *limite de sugestão automática* valor abaixo do limite de correção automática, acima do qual o DQS sugerir uma alteração e torná-lo se o administrador de dados aprová-lo. Você pode especificar o valor de limite de sugestão automática na guia **Configurações Gerais** na tela **Configuração** . Para obter mais informações, consulte [Configure Threshold Values for Cleansing and Matching](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md).  
  
 Qualquer valor com um nível de confiança debaixo do valor de limite de sugestão automática é deixado como está pelo DQS, a menos que o administrador de dados especifique uma alteração.  
  
##  <a name="Interactive"></a> Limpeza interativa  
 Com base no processo de limpeza auxiliada por computador, o DQS fornece ao administrador de dados as informações necessárias para que ele tome uma decisão sobre a alteração dos dados. O DQS categoriza os dados sob estas cinco guias:  
  
-   **Sugerido**: valores para os quais o DQS encontrou sugestões com um nível de confiança maior do que o *limite de sugestão automática* valor mas menor do que o *limite de correção automática* valor. Você deve revisar esses valores e aprovar ou rejeitar conforme apropriado.  
  
-   **Novo**: os valores válidos para o qual o DQS não tem informações suficientes (sugestão) e, portanto, não pode ser mapeado para nenhuma outra guia. Além disso, essa guia também contém valores que têm um nível de confiança menor do que o *limite de sugestão automática* valor, porém alto o suficiente para ser marcado como válido.  
  
-   **Inválido**: valores que foram marcados como inválidos no domínio na base de conhecimento ou valores que falharam em dados de regra ou referência de um domínio. Esta guia também conterá valores rejeitados pelo usuário em quaisquer das outras quatro guias durante o processo de limpeza interativo.  
  
-   **Corrigido**: valores corrigidos pelo DQS durante a limpeza automatizada de processo como o DQS localizou uma correção para o valor com o nível de confiança acima de *limite de correção automática* valor. Essa guia também conterá valores para os quais o usuário especificou um valor correto no **correto para** coluna durante a limpeza interativa e então aprovou clicando no botão de opção a **Aprovar** coluna em qualquer uma das outras quatro guias.  
  
-   **Correto**: valores que foram considerados corretos. Por exemplo, o valor correspondeu a um valor de domínio. Se necessário, você pode substituir a limpeza do DQS ao rejeitar valores desta guia ou especificando uma palavra alternativa no **correto para** coluna e, em seguida, clicando no botão de rádio do **aceitar** coluna. Essa guia também conterá valores que foram aprovados pelo usuário durante a limpeza interativa clicando no botão de opção a **Aprovar** coluna o **novo** ou **inválido** guia.  
  
> [!NOTE]  
>  No **sugerido**, **corrigido**, e **correto** guias, o DQS exibe o valor principal para um domínio, se aplicável, no **correto para** coluna o valor respectivo domínio.  
  
 O administrador de dados usa o cliente do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] para ver as alterações propostas pelo DQS e decidir se elas devem ser implementadas ou não. Ele pode verificar se os valores designados como corretos pelo DQS estão realmente corretos. Ele pode verificar se as alterações já feitas pelo DQS, com um alto nível de confiança, deveriam ter sido feitas. Ele pode decidir se deve aprovar as alterações sugeridas automaticamente. E pode examinar os valores que não foram alterados, no caso de desejar fazer uma alteração não localizada pelo processo assistido pelo computador.  
  
 O DQS mesclará todas as alterações feitas pelo administrador de dados com os resultados da limpeza de dados auxiliada por computador. Essas alterações ficarão no projeto, mas não serão adicionadas à base de conhecimento. Durante a limpeza de dados, a base de conhecimento associada é somente leitura.  
  
 Quando o processo de limpeza de dados for concluído, você poderá optar por exportar os dados processados para uma nova tabela no banco de dados do SQL Server, para um arquivo .csv ou para um arquivo do Excel. Os dados de origem nos quais a limpeza é executada são mantidos em seu estado original. O administrador de dados pode usar os dados limpos separados para corrigir os dados de origem reais.  
  
 A ilustração a seguir mostra como a limpeza de dados é feita usando o aplicativo [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]:  
  
 ![Limpeza de Dados no Cliente Data Quality](../data-quality-services/media/dqs-cleansingindqsclient.gif "Limpeza de Dados no Cliente Data Quality")  
  
##  <a name="Leading"></a> Correção de valor principal  
 A correção do valor principal se aplica a valores de domínio que possuem sinônimos, e o usuário deseja usar um dos valores de sinônimo como o valor principal, em vez de outros para a representação consistente do valor. Por exemplo, "Rio de Janeiro", "RJ" e "cidade maravilhosa" são sinônimos e o usuário deseja usar "Rio de Janeiro" como o valor principal em vez de "RJ" e "Cidade Maravilhosa". O DQS oferece suporte à correção do valor principal durante o processo de limpeza para ajudar você a padronizar seus dados. A correção de valor principal só será feita se o domínio tiver sido habilitado para o mesmo ao ser criado. Por padrão, todos os domínios são habilitados para correção de valor principal, a menos que você tenha desmarcado a **usar valores principais** caixa de seleção durante a criação de um domínio. Para obter mais informações sobre essa caixa de seleção, consulte [definir propriedades do domínio](../data-quality-services/set-domain-properties.md).  
  
##  <a name="Standardize"></a> Padronizar dados limpos  
 É possível optar por exportar os dados limpos no formato padronizado com base no formato de saída definido para domínios. Durante a criação de um domínio, você poderá selecionar a formatação que será aplicada quando forem gerados os valores de dados no domínio. Para obter mais informações sobre como especificar formatos de saída para um domínio, consulte o **formato de saída para** lista em [definir propriedades do domínio](../data-quality-services/set-domain-properties.md).  
  
 Ao exportar os dados limpos no **exportar** página no Assistente de limpeza dados qualidade projeto, especifique se deseja que os dados limpos sejam exportados no formato padronizado marcando o **padronizar saída** caixa de seleção. Por padrão, os dados limpos são exportados no formato unificado, ou seja, a caixa de seleção está marcada. Para obter mais informações sobre como exportar os dados limpos, consulte [Limpar dados usando o DQS & 40; interno & 41; Conhecimento](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md).  
  
##  <a name="Related"></a> Tarefas relacionadas  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como configurar valores de limites para a atividade de limpeza.|[Configure Threshold Values for Cleansing and Matching](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md)|  
|Descreve como limpar dados usando conhecimento criado no DQS.|[Limpar dados usando o DQS e 40; interno & 41; Dados de Conhecimento](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)|  
|Descreve como limpar dados usando conhecimento do serviço de dados de referência.|[Limpar dados usando dados de referência e 40; 41; & externos Dados de Conhecimento](../data-quality-services/cleanse-data-using-reference-data-external-knowledge.md)|  
|Descreve como limpar um domínio composto.|[Limpar dados em um domínio composto](../data-quality-services/cleanse-data-in-a-composite-domain.md)|  
  
## Consulte também  
 [Projetos de qualidade de dados e 40; DQS e 41;](../data-quality-services/data-quality-projects-dqs.md)   
 [Correspondência de dados](../data-quality-services/data-matching.md)  
  
  
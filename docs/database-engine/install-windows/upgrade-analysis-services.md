---
title: "Atualizar o Analysis Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "atualizando bancos de dados"
  - "bancos de dados [Analysis Services], atualizando"
  - "atualizando o Analysis Services, instalações lado a lado"
  - "atualizações do Analysis Services"
  - "atualizações do Analysis Services, sobre a atualização do Analysis Services"
  - "SSAS, migração de banco de dados"
  - "atualizando o Analysis Services"
  - "instalando o Analysis Services, atualizando"
  - "SSAS, atualizando"
ms.assetid: a131d329-386e-4470-aaa9-ffcde4e5ec0c
caps.latest.revision: 79
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 79
---
# Atualizar o Analysis Services
  As instâncias do Analysis Services podem ser atualizadas para uma versão do SQL Server 2016 do mesmo modo de servidor para tirar proveito dos recursos introduzidos na versão atual, conforme descrito em [What's New in Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md).  
  
 Você pode fazer uma atualização in-loco de cada instância, mesmo se houver outras instâncias em execução no mesmo hardware. No entanto, a maioria dos administradores opta por instalar uma nova instância da nova versão para teste de aplicativos, antes de transferir cargas de trabalho de produção para o novo servidor. Mas, para servidores de desenvolvimento ou de teste, pode ser mais prático fazer uma atualização in-loco.  
  
 Antes de atualizar para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], revise o seguinte:  
  
-   [Notas de versão do SQL Server 2016](http://go.microsoft.com/fwlink/?LinkID=398124) descreve problemas conhecidos e soluções alternativas.  
  
-   [Analysis Services Backward Compatibility](../../analysis-services/analysis-services-backward-compatibility.md) resume os recursos descontinuados, preteridos e modificados. Você deve examinar essas listas regularmente para avaliar o impacto das alterações do produto nos modelos, nos scripts ou no código personalizado. Normalmente, as transições de recursos são anunciadas durante a versão de pré-lançamento da próxima versão principal.  
  
## Atualização do servidor  
 Há dois métodos básicos para atualização de servidores e bancos de dados:  
  
-   As **atualizações in-loco** substituem os arquivos de programa existentes pelos arquivos de programa do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Os bancos de dados permanecem no mesmo local. As pastas de programa são atualizadas para refletir o novo nome.  
  
-   As **atualizações lado a lado** criam uma nova instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], normalmente no mesmo computador, a menos que esteja atualizando o hardware ao mesmo tempo. Esse método requer a transferência dos bancos de dados para a nova instância. Opcionalmente, você pode desinstalar a versão anterior para liberar espaço em disco.  
  
 Os níveis de compatibilidade de bancos de dados associados a um determinado servidor permanecem iguais, a menos que você os altere manualmente.  
  
### Atualização in-loco  
 É possível atualizar uma instância existente do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] and, as part of the upgrade process, aupara omatically migrate existing databases from the old instance para o the new instance. Como os metadados e os dados binários são incompatíveis entre as duas versões, você reterá os dados depois de atualizar e não precisará migrar os dados manualmente.  
  
 Para atualizar uma instância existente, execute a Instalação e especifique o nome da instância existente como o nome da nova instância.  
  
### Atualização lado a lado  
  
-   Faça um backup de todos os bancos de dados e verifique se é possível restaurá-los. Consulte [Backup and Restore of Analysis Services Databases](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md).  
  
-   Identifique um subconjunto dos relatórios, planilhas ou instantâneos de painel a ser usado posteriormente, como base para a confirmação das operações do servidor após a atualização. Se possível, colete medições de desempenho para que você possa fazer comparações em relação às cargas de trabalho em um servidor atualizado.  
  
-   Instale uma nova instância do Analysis Services, escolhendo o mesmo modo de servidor (Tabular ou Multidimensional), de acordo com o servidor que você pretende substituir. Consulte [Install Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services.md).  
  
     Execute as tarefas pós-instalação para configurar portas e adicionar administradores de servidor. Veja [Configuração de pós-instalação &#40;Analysis Services&#41;](../../analysis-services/instances/post-install-configuration-analysis-services.md).  
  
-   Anexe ou restaure os bancos de dados.  
  
-   Execute o DBCC para verificar a integridade do banco de dados. Os modelos de tabela passam por uma verificação mais completa com testes para objetos órfãos, em toda a hierarquia do modelo. Para modelos multidimensionais, somente os índices da partição são verificados. Veja [DBCC &#40;Verificador de Consistência de Banco de Dados&#41; para bancos de dados de tabela e multidimensionais do Analysis Services](../../analysis-services/instances/database consistency checker (dbcc) for analysis services.md).  
  
-   Faça testes em relatórios, planilhas e painéis para confirmar que não há alterações prejudiciais de comportamento ou de cálculos. Você terá um desempenho mais rápido para as cargas de trabalho multidimensionais e de tabela.  
  
-   Teste as operações de processamento para corrigir problemas de logon ou de permissão. Se estiver usando uma conta de serviço padrão para conexões, o novo serviço será executado em uma conta diferente. Veja [Configurar contas de serviço &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md) para obter mais informações sobre contas de inicialização para o Analysis Services.  
  
-   Teste as operações de backup e restauração no servidor atualizado, ajustando os scripts para usar o novo nome do servidor.  
  
## Atualização do banco de dados  
 Bancos de dados que foram criados em versões anteriores do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] são executados no servidor atualizado sob uma configuração em nível de compatibilidade do banco de dados mais antigo. De modo geral, você pode atualizar um banco de dados ou modelo para operar em um nível superior de compatibilidade para obter acesso a novos recursos. Mas, lembre-se de que, ao fazê-lo, estará associado a uma versão específica do servidor.  
  
 Para atualizar um banco de dados, normalmente você atualiza o modelo no SSDT (SQL Server Data Tools) e implanta a solução em uma instância do servidor atualizado. Confira o artigo [Baixar o SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) para obter a versão mais recente.  
  
 Os bancos de dados multidimensionais e de tabela seguem caminhos de versão diferentes. Coincidentemente, esses modelos multidimensionais e de tabela apresentam o nível de compatibilidade 1100.  Os modos se desenvolverão em diferentes proporções, caso as alterações do recurso afetem apenas um deles.  
  
 Para fins de conhecimento, a tabela a seguir resume os níveis de compatibilidade, mas não deixe de analisar os tópicos detalhadamente para entender o que cada nível fornece.  
  
||||  
|-|-|-|  
|Tabular|1200|SQL Server 2016|  
|Tabular|1103|SQL Server 2014|  
|Tabular|1100|SQL Server 2012|  
|Multidimensional|1100|SQL Server 2012 e posterior|  
|Multidimensional|1050|SQL Server 2005, 2008, 2008 R2|  
  
 Veja [Nível de compatibilidade de um banco de dados multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md) e [Nível de compatibilidade para modelos de tabela no Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) para obter mais informações.  
  
## Atualização do modelo de tabela para o nível de compatibilidade 1200  
 Os bancos de dados e os modelos de tabela se beneficiam ao máximo do SQL Server 2016. Esta versão oferece um modo DirectQuery revisado para modelos de tabela no nível de compatibilidade 1200, simplificado pela remoção do modo híbrido, pela adição de instruções de consulta para recuperar um subconjunto de dados em tempo de design e pela segurança em nível de linha por meio de DAX, em vez de permissões de linha no banco de dados back-end.  
  
 Uma segunda razão para atualizar é a nova construção de metadados de tabela dentro do modelo. Um modelo de tabela criado ou atualizado para o novo nível de compatibilidade 1200 usa terminologia nativa para definições de objetos, como modelo, tabela, relações e colunas, para descrever os elementos principais.  
  
 Para atualizar um modelo Tabular, use uma versão do [SSDT (SQL Server Data Tools)](https://msdn.microsoft.com/library/mt204009.aspx) criada para esta versão para alterar a propriedade **Nível de Compatibilidade** para **SQL Server 2016 RTM (1200)**.  
  
 Não use SSMS, código ou script para alterar o **CompatibilityLevel**. A alteração da propriedade, por si só, não produz nenhum efeito. A conversão de metadados ocorre no SSDT em resposta a atualização da propriedade, seguida da reabertura do projeto.  
  
 Como sempre, não deixe de salvar um backup do modelo antes de atualizar caso precise reverter a atualização para a versão anterior.  
  
1.  No SSDT > Gerenciador de Soluções, clique com o botão direito do mouse em **model.bim**, escolha **Exibir Código**, confirme que o modelo será fechado e reaberto em uma nova janela (a janela de código).  
  
2.  O modelo é aberto como um documento XMLA. Para fins de comparação após a conversão, copie o conteúdo em outro arquivo (você pode abrir um novo arquivo XML no SSDT).  
  
3.  Clique com o botão direito do mouse em **model.bim** e altere-o novamente para **Exibir Designer**.  
  
4.  Defina **CompatibilityLevel** como **SQL Server 2016 RTM (1200)**.  
  
5.  Esta ação não pode ser revertida, por isso haverá uma solicitação de confirmação. Clique em **Sim** para continuar. O projeto será atualizado.  
  
6.  Clique com o botão direito do mouse em **model.bim** e altere-o novamente para **Exibir Código**.  
  
     Observe que a definição do modelo agora está em JSON, usando metadados de tabela.  
  
 **Conversão de metadados**  
  
 Ao comparar os metadados anteriores e posteriores à conversão, você vai observar que eles foram convertidos em JSON e cortados de definições redundantes.  
  
 O modelo mantém todas as funcionalidades: associações de dados, fatias de partição, expressões, identificadores de objetos, nomes de objeto, descrições, legendas, traduções e anotações permanecem intactos. Mas, se você tiver um código ou script que faça referência a objetos específicos, parte da reescrita do código incluirá a remoção das referências a objetos que não existem mais. Por exemplo, um modelo 1050 ou 1103 terá seções para dimensões externas ao cubo, enquanto um modelo 1200 define uma tabela como um objeto único.  
  
> [!NOTE]  
>  Os níveis de compatibilidade anteriores de 1050 e 1103 têm suporte, embora sejam preteridos. Em versões futuras do SQL Server, os modelos de tabela convertidos em objetos multidimensionais não terão mais suporte. Confira o artigo [Deprecated Analysis Services Features in SQL Server 2016](../../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md) do anúncio.  
  
## Pós-atualização para modelos de tabela no nível de compatibilidade 1200  
 Depois que o modelo for convertido, você usará a [Referência de TMSL &#40;Linguagem de Script de Modelo de Tabela&#41;](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) em vez de XMLA para gerar script de operações de banco de dados. O TMSL é gerado automaticamente no SSMS, quando o modelo estiver no nível de compatibilidade 1200. O código personalizado, que se destina aos bancos de dados de tabela no nível de compatibilidade 1200, deve usar a API definida no namespace Microsoft.AnalysisServces.Tabular. O script e o código devem ser gravados desde o início; além disso, não há mecanismos para conversão interna. Confira [Documentação do Desenvolvedor do Analysis Services](../../analysis-services/analysis-services-developer-documentation.md) para obter ajuda a se familiarizar.  
  
 Se preferir, adicione os seguintes recursos para um modelo de tabela com suporte apenas para o nível de compatibilidade 1200:  
  
-   Uma implementação de DirectQuery com suporte para segurança em nível de linha por meio de DAX no modelo, mais fontes de dados, subconjuntos de dados para fins de modelagem e configuração mais simples.  
  
-   Colunas calculadas  
  
-   Pastas de exibição  
  
## Atualizar modelos de tabela no modo DirectQuery  
 O sistema não permite fazer atualização in-loco de modelos de tabela anteriores configurados para DirectQuery. A nova implementação de DirectQuery tem um volume menor de configuração e nem todas as configurações podem ser transportadas.  
  
1.  No SSDT, desative o modo **DirectQuery** para que o modelo use o armazenamento na memória. Consulte [Habilitar o modo de design do DirectQuery (SSAS de Tabela)](https://msdn.microsoft.com/library/hh270245.aspx) para obter instruções.  
  
2.  Defina **CompatibilityLevel** como SQL Server 2016 (RTM) 1200.  
  
3.  Salve e recompile ou implante o modelo.  
  
4.  Ative o **DirectQuery** novamente. Confira o artigo [DirectQuery for Tabular 1200 models](../Topic/DirectQuery%20for%20Tabular%201200%20models.md) para saber mais.  
  
## Consulte também  
 [Modo DirectQuery &#40;SSAS de tabela&#41;](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Novidades do Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [Recursos com suporte nas edições do SQL Server 2016](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)   
 [Planejando uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Atualizar Power Pivot para SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [Instalar o Analysis Services em modo multidimensional e de mineração de dados](../Topic/Install%20Analysis%20Services%20in%20Multidimensional%20and%20Data%20Mining%20Mode.md)   
 [Atualizar para o SQL Server 2016 usando o Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/upgrade-to-sql-server-2016-using-the-installation-wizard-setup.md)  
  
  
---
title: Exibir e trabalhar com a saída do Orientador de Otimização do Mecanismo de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dta.sessionmonitor.f1
- sql13.dta.reports.f1
- sql13.dta.recommendations.f1
- sql13.dta.applyrecommendations.f1
helpviewer_keywords:
- viewing logs
- recommendations [Database Engine Tuning Advisor]
- summary tuning information [SQL Server]
- Database Engine Tuning Advisor [SQL Server], recommendations
- Database Engine Tuning Advisor [SQL Server], logs
- Database Engine Tuning Advisor [SQL Server], viewing output
- Database Engine Tuning Advisor [SQL Server], reports
- logs [SQL Server], tuning
- reports [SQL Server], tuning
- viewing tuning output
ms.assetid: 47f9d9a7-80b0-416d-9d9a-9e265bc190dc
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e8b53d26f286bb9c1573292cbb29f0938eb58dc9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="view-and-work-with-the-output-from-the-database-engine-tuning-advisor"></a>Exibir e trabalhar com a saída do Orientador de Otimização do Mecanismo de Banco de Dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Quando o Orientador de Otimização do Mecanismo de Banco de Dados ajusta os bancos de dados, cria resumos, recomendações, relatórios e logs de ajuste. Você pode usar a saída do log de ajuste para solucionar problemas das sessões de ajuste do Orientador de Otimização do Mecanismo de Banco de Dados. Você pode usar os resumos, as recomendações e os relatórios para determinar se deseja implementar recomendações de ajuste ou continuar ajustando até atingir o desempenho de consulta necessário para instalar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter informações sobre como usar o Database Tuning Advisor para criar cargas de trabalho ou ajustar um banco de dados, consulte [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md).  
  
##  <a name="View"></a> Exibir saída de ajuste  
 Os procedimentos a seguir descrevem como exibir recomendações de ajuste, resumos, relatórios e logs de ajuste com a GUI do Orientador de Otimização do Mecanismo de Banco de Dados. Para obter mais informações sobre as opções da interface do usuário, consulte [Descrições da interface do usuário](#UI) posteriormente neste tópico.  
  
 Você também pode usar a GUI para exibir a saída de ajuste gerada pelo utilitário de linha de comando **dta** .  
  
> [!NOTE]  
>  Se você usar o utilitário de linha de comando **dta** e especificar que a saída deve ser gravada em um arquivo XML usando o argumento **-ox** , poderá abrir e exibir o arquivo de saída XML clicando em **Abrir Arquivo** no menu **Arquivo** do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte [Use SQL Server Management Studio](http://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be). Para obter informações sobre o utilitário de linha de comando **dta** , consulte [Utilitário dta](../../tools/dta/dta-utility.md).  
  
#### <a name="to-view-tuning-recommendations-with-the-database-engine-tuning-advisor-gui"></a>Para exibir as recomendações de ajuste com a GUI do Orientador de Otimização do Mecanismo de Banco de Dados  
  
1.  Ajuste um banco de dados usando a GUI do Orientador de Otimização do Mecanismo de Banco de Dados ou o utilitário de linha de comando **dta** . Para obter mais informações, consulte [Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md). Para usar uma sessão de ajuste existente, ignore esta etapa e passe à Etapa 2.  
  
2.  Inicie a GUI do Orientador de Otimização do Mecanismo de Banco de Dados. Para obter mais informações, consulte [Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md). Se você quiser exibir as recomendações de ajuste de uma sessão de ajuste existente, abra-a clicando duas vezes no nome de sessão na janela **Monitor de Sessão**.  
  
     Depois de encerrada a nova sessão de ajuste, ou depois de a ferramenta ter carregado a sessão existente, a página **Recomendações** é exibida.  
  
3.  Na página **Recomendações** , clique em **Recomendações de Partição** e **Recomendações de Índice** para exibir painéis com os resultados da sessão de ajuste. Se você não tiver especificado o particionamento ao definir as opções de ajuste para esta sessão, o painel **Recomendações de Partição** estará vazio.  
  
4.  No painel **Recomendações de Partição** ou **Recomendações de Índice** , use as barras de rolagem para exibir todas as informações exibidas na grade.  
  
5.  Desmarque a opção **Mostrar objetos existentes** na parte inferior da página com guias **Recomendações** . Com isso, a grade exibirá somente os objetos de banco de dados indicados na recomendação. Use a barra de rolagem inferior para exibir a coluna mais à direita na grade de recomendações e clique em um item na coluna **Definição** para exibir ou copiar o script [!INCLUDE[tsql](../../includes/tsql-md.md)] que cria aquele objeto em seu banco de dados.  
  
6.  Para salvar todos os scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] que criam ou descartam todos os objetos de banco de dados nesta recomendação em um arquivo de script, clique em **Salvar Recomendações** , no menu **Ações** .  
  
#### <a name="to-view-the-tuning-summary-and-reports-with-the-database-engine-tuning-advisor-gui"></a>Para exibir o resumo e os relatórios de ajuste com a GUI do Orientador de Otimização do Mecanismo de Banco de Dados  
  
1.  Ajuste um banco de dados usando a GUI do Orientador de Otimização do Mecanismo de Banco de Dados ou o utilitário de linha de comando **dta** . Para obter mais informações, consulte [Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md). Para usar uma sessão de ajuste existente, ignore esta etapa e passe à Etapa 2.  
  
2.  Inicie a GUI do Orientador de Otimização do Mecanismo de Banco de Dados. Para obter mais informações, consulte [Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md). Se você desejar exibir resumos e relatórios de ajuste de uma sessão de ajuste existente, abra-os clicando duas vezes no nome da sessão no **Monitor de Sessão**.  
  
3.  Depois de encerrada a nova sessão de ajuste, ou depois de a ferramenta ter carregado a sessão existente, clique na guia **Relatórios** .  
  
4.  O painel **Resumo do Ajuste** contém informações sobre a sessão de ajuste. As informações fornecidas pelos itens **Aperfeiçoamento de percentual esperado** e **Espaço usado por recomendação** podem ser especialmente úteis para decidir se deseja implementar a recomendação.  
  
5.  No painel **Relatórios de Ajuste** , clique em **Selecionar relatório** para escolher um relatório de ajuste a ser exibido.  
  
#### <a name="to-view-tuning-logs-with-the-database-engine-tuning-advisor-gui"></a>Para exibir os logs de ajuste com a GUI do Orientador de Otimização do Mecanismo de Banco de Dados  
  
1.  Ajuste um banco de dados usando a GUI do Orientador de Otimização do Mecanismo de Banco de Dados ou o utilitário de linha de comando **dta** . Ao ajustar a carga de trabalho, verifique se você marcou **Salvar log de ajuste** , na guia **Geral** . Para usar uma sessão de ajuste existente, ignore esta etapa e passe à Etapa 2.  
  
2.  Inicie a GUI do Orientador de Otimização do Mecanismo de Banco de Dados. Para obter mais informações, consulte [Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md). Se você desejar exibir resumos e relatórios de ajuste de uma sessão de ajuste existente, abra-os clicando duas vezes no nome da sessão na janela **Monitor de Sessão** .  
  
3.  Depois de encerrada a nova sessão de ajuste ou depois de a ferramenta ter carregado a sessão existente, clique na guia **Progresso** . O painel **Log de Ajuste** exibe o conteúdo do log. O log contém informações sobre eventos de carga de trabalho que o Orientador de Otimização do Mecanismo de Banco de Dados não pôde analisar.  
  
     Quando todos os eventos da sessão de ajuste tiverem sido analisados pelo Orientador de Otimização do Mecanismo de Banco de Dados, será exibida uma mensagem indicando que o log de ajuste está vazio para a sessão. Se **Salvar log de ajuste** não estiver marcado na guia **Geral** quando a sessão de ajuste foi executada originalmente, será exibida uma mensagem indicativa.  
  
##  <a name="Implement"></a> implementar recomendações de ajuste  
 Você pode implementar as recomendações do Orientador de Otimização do Mecanismo de Banco de Dados manualmente ou automaticamente como parte da sessão de ajuste. Se quiser examinar os resultados do ajuste antes de implementá-los, use a GUI do Orientador de Otimização do Mecanismo de Banco de Dados. Você pode usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para executar manualmente os scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] , que o Orientador de Otimização do Mecanismo de Banco de Dados gera como resultado da análise de uma carga de trabalho para implementar as recomendações. Se você não precisar examinar os resultados antes de implementá-los, poderá usar a opção **-a** com o utilitário de prompt de comando **dta** . Isso faz com que o utilitário implemente as recomendações de ajuste automaticamente depois de analisar sua carga de trabalho. Os procedimentos a seguir explicam como usar ambas as interfaces do Orientador de Otimização do Mecanismo de Banco de Dados para implementar as recomendações de ajuste.  
  
#### <a name="to-manually-implement-tuning-recommendations-with-the-database-engine-tuning-advisor-gui"></a>Para implementar manualmente as recomendações de ajuste com a GUI do Orientador de Otimização do Mecanismo de Banco de Dados  
  
1.  Ajuste um banco de dados usando a GUI do Orientador de Otimização do Mecanismo de Banco de Dados ou o utilitário de prompt de comando **dta** . Para obter mais informações, consulte [Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md). Para usar uma sessão de ajuste existente, ignore esta etapa e passe à Etapa 2.  
  
2.  Inicie a GUI do Orientador de Otimização do Mecanismo de Banco de Dados. Para obter mais informações, consulte [Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md). Se você quiser implementar recomendações de ajuste para uma sessão de ajuste existente, abra-a clicando duas vezes no nome de sessão em **Monitor de Sessão**.  
  
3.  Depois do término da nova sessão de ajuste, ou depois de a ferramenta carregar a sessão existente, clique em **Aplicar Recomendações** no menu **Ações** .  
  
4.  Na caixa de diálogo **Aplicar Recomendações** , escolha **Aplicar agora** ou **Agendar para mais tarde**. Se você escolher **Agendar para mais tarde**, selecione a data e o horário apropriados.  
  
5.  Clique em **OK** para aplicar as recomendações.  
  
#### <a name="to-automatically-implement-tuning-recommendations-using-the-dta-command-prompt-utility"></a>Para implementar automaticamente as recomendações de ajuste usando o utilitário de prompt de comando dta  
  
1.  Determine os recursos de banco de dados (índices, exibições indexadas, particionamento) que o Orientador de Otimização do Mecanismo de Banco de Dados deve considerar para adição, remoção ou retenção durante a análise.  
  
     Lembre-se das considerações a seguir antes de começar a ajustar:  
  
    -   Quando uma tabela de rastreamento é usada como uma carga de trabalho, ela deve existir no mesmo servidor em que o Orientador de Otimização do Mecanismo de Banco de Dados está ajustando. Se você criou a tabela de rastreamento em um servidor diferente, mova-a para o servidor em que o Orientador de Otimização do Mecanismo de Banco de Dados está ajustando.  
  
    -   Se uma sessão de ajuste continuar em execução por mais tempo do que o previsto, você poderá pressionar CTRL+C para terminar a sessão de ajuste. Pressionar CTRL+C nessas circunstâncias força o **dta** a produzir a melhor recomendação possível com base em quanto da carga de trabalho foi consumida e não desperdiça o tempo que a ferramenta já usou para ajustar a carga de trabalho.  
  
2.  Em um prompt de comando, digite o seguinte:  
  
    ```  
    dta -E -D DatabaseName -if WorkloadFile -s SessionName -a  
    ```  
  
     em que **-E** especifica que sua sessão de ajuste usa uma conexão confiável (em vez de uma ID de logon e uma senha), **-D** especifica o nome do banco de dados que você deseja ajustar ou uma lista delimitada por vírgula de vários bancos de dados que a carga de trabalho usa, **-if** especifica o nome e caminho para um arquivo de carga de trabalho, **-s** especifica um nome para sua sessão de ajuste, e **-a** especifica que você quer que o utilitário de prompt de comando **dta** aplique automaticamente as recomendações de ajuste depois que a carga de trabalho é analisada sem consultá-lo. Para obter mais informações sobre como usar o utilitário de prompt de comando **dta** para ajustar bancos de dados, consulte [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md).  
  
3.  Pressione ENTER.  
  
##  <a name="Analysis"></a> Executar análises exploratórias  
 O recurso de configuração especificado pelo usuário do Orientador de Otimização do Mecanismo de Banco de Dados permite que os administradores de banco de dados executem análises exploratórias. Usando esse recurso, os administradores de banco de dados especificam um design de banco de dados físico desejado no Orientador de Otimização do Mecanismo de Banco de Dados e, então, podem avaliar os efeitos de desempenho desse design sem implementá-lo. A configuração especificada pelo usuário é suportada pela interface gráfica do usuário (GUI) e pelo utilitário de linha de comando do Orientador de Otimização do Mecanismo de Banco de Dados. No entanto, o utilitário de linha de comando oferece maior flexibilidade.  
  
 Se você usar a interface gráfica do usuário do Orientador de Otimização do Mecanismo de Banco de Dados, poderá avaliar os efeitos da implementação de um subconjunto de uma recomendação de ajuste do Orientador, mas não poderá adicionar estruturas de design físicas hipotéticas do Orientador para avaliação.  
  
 Os procedimentos a seguir explicam como usar o recurso de configuração especificado pelo usuário com ambas as interfaces de ferramenta.  
  
### <a name="using-database-engine-tuning-advisor-gui-to-evaluate-tuning-recommendations"></a>Usando a interface gráfica do usuário do Orientador de Otimização do Mecanismo de Banco de Dados para avaliar recomendações de ajuste  
 O procedimento abaixo descreve como avaliar uma recomendação gerada pelo Orientador de Otimização do Mecanismo de Banco de Dados, mas a interface gráfica do usuário não permite que você especifique novas estruturas de design físicas para avaliação.  
  
##### <a name="to-evaluate-tuning-recommendations-with-the-database-engine-tuning-advisor-gui"></a>Para avaliar as recomendações de ajuste com a interface gráfica do usuário do Orientador de Otimização do Mecanismo de Banco de Dados  
  
1.  Use a interface gráfica do usuário do Orientador de Otimização do Mecanismo de Banco de Dados para ajustar um banco de dados. Para obter mais informações, consulte [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md). Se você desejar avaliar uma sessão de ajuste existente, clique duas vezes nela em **Monitor de Sessão**.  
  
2.  Na guia **Recomendações** , desmarque as estruturas de design físicas recomendadas que não desejar usar.  
  
3.  No menu **Ações** , clique em **Avaliar Recomendações**. Será criada uma nova sessão de ajuste para você.  
  
4.  Digite o novo **Nome da sessão**. Para exibir a configuração da estrutura de design do banco de dados físico que você está avaliando, escolha **Clique aqui para ver a seção de configuração** na área **Descrição** na parte inferior da janela do aplicativo Orientador de Otimização do Mecanismo de Banco de Dados.  
  
5.  Clique no botão **Iniciar Análise** na barra de ferramentas. Quando o Orientador de Otimização do Mecanismo de Banco de Dados for encerrado, você pode exibir os resultados na guia **Recomendações** .  
  
### <a name="using-database-engine-tuning-advisor-gui-to-export-tuning-session-results-for-what-if-tuning-analysis"></a>Usando a interface gráfica do usuário do Orientador de Otimização do Mecanismo de Banco de Dados para exportar os resultados da sessão de ajuste para análise de ajuste hipotética  
 O procedimento abaixo descreve como exportar os resultados da sessão de ajuste do Orientador de Otimização do Mecanismo de Banco de Dados para um arquivo XML, que você pode editar e, em seguida, ajustar com o utilitário de linha de comando **dta** . Isso permite executar uma análise de ajuste em novas estruturas de design físicas hipotéticas sem a sobrecarga de implementá-las em seu banco de dados antes de descobrir se geram as melhorias de desempenho necessárias. Usar a GUI do Orientador de Otimização do Mecanismo de Banco de Dados para ajustar inicialmente seu banco de dados e exportar os resultados do ajuste para um arquivo **.xml** são um bom modo para os usuários que estão começando com o XML usarem a flexibilidade do esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados para executar o teste de hipóteses.  
  
##### <a name="to-export-tuning-session-results-from-the-database-engine-tuning-advisor-gui-for-what-if-analysis-with-the-dta-command-line-utility"></a>Para exportar resultados da sessão de ajuste da interface gráfica do usuário do Orientador de Otimização do Mecanismo de Banco de Dados para a análise hipotética com o utilitário de linha de comando dta  
  
1.  Use a interface gráfica do usuário do Orientador de Otimização do Mecanismo de Banco de Dados para ajustar um banco de dados. Para obter mais informações, consulte [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md). Se você desejar avaliar uma sessão de ajuste existente, clique duas vezes em **Monitor de Sessão**.  
  
2.  No menu **Arquivo** , clique em **Resultados da Sessão de Exportação** e salve como um arquivo XML.  
  
3.  Abra o arquivo XML criado no passo 2 em seu editor de XML ou editor de textos favorito ou no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Role até o elemento **Configuration** . Copie e cole a seção do elemento **Configuration** em um modelo de arquivo de entrada XML depois do elemento **TuningOptions** . Salve esse arquivo de entrada XML.  
  
4.  No novo arquivo de entrada XML criado na Etapa 3, especifique as opções de ajuste desejadas no elemento **TuningOptions**, edite a seção do elemento **Configuration** (adicione ou exclua as estruturas de design físico conforme apropriado para sua análise), salve o arquivo e valide-o em relação ao esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados. Para obter informações sobre como editar esse arquivo XML, consulte [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md).  
  
5.  Use o arquivo XML criado na etapa 4 como entrada para o utilitário de linha de comando **dta** . Para obter informações sobre como usar arquivos de entrada XML com esta ferramenta, consulte a seção "Ajustar um banco de dados usando o utilitário dta" em [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md).  
  
### <a name="using-the-user-specified-configuration-feature-with-the-dta-command-line-utility"></a>Usando o recurso de configuração especificada pelo usuário com o utilitário de linha de comando dta  
 Se você for um desenvolvedor de XML experiente, poderá criar um arquivo de entrada XML do Orientador de Otimização do Mecanismo de Banco de Dados no qual é possível especificar uma carga de trabalho e uma configuração hipotética de estruturas de design do banco de dados físico, como índices, exibições indexadas ou particionamento. Em seguida, você pode usar o utilitário de linha de comando **dta** para analisar os efeitos que essa configuração hipotética causa no desempenho de consulta do banco de dados. O procedimento abaixo explica esse processo passo a passo:  
  
##### <a name="to-use-the-user-specified-configuration-feature-with-the-dta-command-line-utility"></a>Para usar o recurso de configuração especificado pelo usuário com o utilitário de linha de comando dta  
  
1.  Crie uma carga de trabalho de ajuste. Para obter mais informações sobre como executar essa tarefa, consulte [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md).  
  
2.  Copie e cole a [Amostra de arquivo de entrada XML com a configuração especificada pelo usuário &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md) no editor XML ou em um editor de texto. Use este exemplo para criar um arquivo de entrada XML para sua sessão de ajuste. Para obter informações sobre como executar esta tarefa, consulte a seção "Criar arquivos de entrada XML" em [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md).  
  
3.  Edite os elementos de **TuningOptions** e **Configuration** no exemplo de arquivo de entrada XML. No elemento de **TuningOptions** , especifique quais estruturas de design físicas deseja que o Orientador de Otimização do Mecanismo de Banco de Dados considere durante a sessão de ajuste. No elemento de **Configuration** , especifique as estruturas de design físicas que correspondem à configuração hipotética de estruturas de design de bancos de dados físicos que devem ser analisadas pelo Orientador de Otimização do Mecanismo de Banco de Dados. Para obter informações sobre quais atributos e elementos filho você pode usar com as **TuningOptions** e os elementos pai de **Configuration**, consulte [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md).  
  
4.  Salve o arquivo de entrada com uma extensão **.xml** .  
  
5.  Valide o arquivo de entrada XML que você salvou no passo 4 em relação ao esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados. Esse esquema será instalado no local abaixo quando você instalar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    ```  
    C:\Program Files\Microsoft SQL Server\100\Tools\Binn\schemas\sqlserver\2004\07\dta\dtaschema.xsd  
    ```  
  
     O esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados também está disponível online em [http://schemas.microsoft.com/sqlserver/2004/07/dta](http://schemas.microsoft.com/sqlserver/2004/07/dta).  
  
6.  Depois de criar uma carga de trabalho e um arquivo de entrada XML, você estará pronto para enviar o arquivo de entrada ao utilitário de linha de comando **dta** para análise. Verifique se foi especificado um nome do arquivo de saída XML para o argumento do utilitário **- ox** . Isso cria um arquivo de saída XML com uma configuração recomendada especificada no elemento de **Configuration** . Se quiser executar o Orientador de Otimização do Mecanismo de Banco de Dados novamente para verificar outra configuração hipotética baseada na saída, você poderá copiar e colar o conteúdo dos elementos **Configuration** do arquivo de saída em um arquivo de entrada XML novo ou no original. Para obter informações sobre como usar um arquivo de entrada XML com o utilitário **dta** , consulte a seção “Ajustar um banco de dados usando o utilitário dta" em [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md).  
  
     Depois que o ajuste terminar, use a interface gráfica do usuário do Orientador de Otimização do Mecanismo de Banco de Dados para exibir os relatórios de ajuste ou abra o arquivo de saída XML para exibir o **TuningSummary** e os elementos de **Configuration** para exibir as recomendações do Orientador. Para obter informações sobre como exibir os resultados de sua sessão de ajuste, consulte [Exibir saída de ajuste](#View) anteriormente neste tópico. Note também que o arquivo de saída XML pode conter relatórios de análise do Orientador de Otimização do Mecanismo de Banco de Dados.  
  
7.  Repita os passos 6 e 7 até criar uma configuração hipotética que produza a melhoria no desempenho de consulta que você deseja. Em seguida, você pode implementar a configuração nova. Para obter mais informações, consulte [Implementar recomendações de ajuste](#Implement) , anteriormente neste tópico.  
  
##  <a name="ReviewEvaluateClone"></a> Revisar, avaliar e clonar sessões de ajuste  
 O Orientador de Otimização do Mecanismo de Banco de Dados cria uma nova sessão de ajuste a cada vez que você começa a análise dos efeitos de uma carga de trabalho em seu banco de dados ou bancos de dados. Você pode usar o painel **Monitor de Sessão** da GUI do Orientador de Otimização do Mecanismo de Banco de Dados para exibir ou recarregar todas as sessões de ajuste executadas em uma determinada instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Dispor de todas as sessões de ajuste existentes disponíveis para revisão facilita: clonar sessões com base nas sessões existentes, editar recomendações existentes de ajuste e então usar o Orientador de Otimização do Mecanismo de Banco de Dados para avaliar a sessão editada ou executar o ajuste em intervalos regulares para monitorar o design físico dos seus bancos de dados. Por exemplo, você pode decidir ajustar o banco de dados com uma programação mensal.  
  
 Antes de poder revisar qualquer sessão de ajuste para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], crie sessões de ajuste na instância do servidor, ajustando cargas de trabalho com o Orientador de Otimização do Mecanismo de Banco de Dados. Para obter mais informações, consulte [Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md).  
  
### <a name="review-existing-tuning-sessions"></a>Revisar sessões de ajuste existentes  
 Siga as etapas a seguir para navegar pelas sessões de ajuste existentes em uma determinada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##### <a name="to-review-existing-tuning-sessions"></a>Para revisar sessões de ajuste existentes  
  
1.  Inicie a GUI do Orientador de Otimização do Mecanismo de Banco de Dados. Para obter mais informações, consulte [Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md).  
  
2.  Todas as sessões de ajuste existentes são exibidas na metade superior da janela **Monitor de Sessão** . O número de sessões exibidas depende de quantas vezes você ajustou os bancos de dados nessa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Use as barras de rolagem para exibir todas as sessões de ajuste.  
  
3.  Clique em um nome de sessão de ajuste uma vez e seus detalhes aparecem na metade inferior da janela **Monitor de Sessão** .  
  
4.  Clique duas vezes em um nome de sessão de ajuste e suas informações serão carregadas no Orientador de Otimização do Mecanismo de Banco de Dados. Depois que as informações de sessão são carregadas, você pode escolher quaisquer das guias para exibir as informações sobre essa sessão de ajuste.  
  
### <a name="evaluate-existing-tuning-sessions-as-hypothetical-configurations"></a>Avaliar sessões de ajuste existentes como configurações hipotéticas  
 Use as etapas a seguir para avaliar uma sessão de ajuste existente. A avaliação de uma sessão de ajuste existente envolve exibir e editar suas recomendações e depois fazer um reajuste. Por exemplo, você decide só deseja criar índices na **tabela1**, portanto exclui a criação de exibições indexadas e particionamento de uma recomendação de ajuste existente. O Orientador de Otimização do Mecanismo de Banco de Dados cria uma nova sessão de ajuste e ajusta a carga de trabalho com relação a seus bancos de dados usando as recomendações editadas como uma configuração hipotética. Isso significa que o Orientador de Otimização do Mecanismo de Banco de Dados ajusta a carga de trabalho com relação aos bancos de dados como se as recomendações editadas tivessem sido implementadas, permitindo a execução de uma análise hipotética limitada. É uma análise hipotética limitada porque você pode só escolher um subconjunto de uma recomendação existente ao usar a interface gráfica do usuário do Orientador de Otimização do Mecanismo de Banco de Dados. Para executar um teste de hipóteses completo, especificando uma configuração hipotética completamente nova que não é subconjunto de nenhuma sessão de ajuste prévia, use o arquivo de entrada XML do Orientador de Otimização do Mecanismo de Banco de Dados com o utilitário de linha de comando **dta** .  
  
##### <a name="to-evaluate-an-existing-tuning-session"></a>Para avaliar uma sessão de ajuste existente  
  
1.  Depois de iniciar o Orientador de Otimização do Mecanismo de Banco de Dados, clique duas vezes em uma sessão de ajuste na metade superior do **Monitor de Sessão**, que carrega as informações da sessão no Orientador de Otimização do Mecanismo de Banco de Dados.  
  
2.  Clique na guia **Progresso** para verificar o log de ajuste que contém informações de erro sobre os eventos na carga de trabalho que o Orientador de Otimização do Mecanismo de Banco de Dados não pôde ajustar. Essas informações podem ajudar a avaliar a eficácia da carga de trabalho.  
  
3.  Se você quiser revisar mais profundamente os resultados dos ajuste dessa sessão, clique na guia **Relatórios** . Lá você pode exibir o resumo de ajuste ou escolher um relatório de ajuste na lista **Selecionar relatório** .  
  
4.  Clique na guia **Recomendações** para exibir as recomendações de ajuste.  
  
5.  Se houver quaisquer recomendações que você não tenha certeza de como implementar, desmarque-as.  
  
6.  No menu **Ações** , clique em **Avaliar Recomendações**. O Orientador de Otimização do Mecanismo de Banco de Dados cria uma nova sessão de ajuste que usa a recomendação editada como configuração hipotética. Para exibir a configuração hipotética em XML, escolha **Clique aqui para ver a seção de configuração**.  
  
7.  Na guia **Geral** , digite um **Nome de sessão**e verifique se a **Carga de trabalho** correta está especificada.  
  
8.  Na guia **Opções de Ajuste** , você pode especificar um tempo de ajuste ou qualquer uma das **Opções Avançadas**.  
  
9. Clique no botão **Iniciar Análise** na barra de ferramentas. O Orientador de Otimização do Mecanismo de Banco de Dados é iniciado, ajustando os bancos de dados que usam a configuração hipotética. Quando o Orientador de Otimização do Mecanismo de Banco de Dados terminar, você pode exibir os resultados dessa sessão como faria normalmente com qualquer outra.  
  
### <a name="clone-existing-tuning-sessions"></a>Clonar sessões de ajuste existentes  
 Você pode criar novas sessões de ajuste com base em sessões existentes, selecionando a opção de clonagem no Orientador de Otimização do Mecanismo de Banco de Dados. Ao usar a opção de clonagem, você baseia uma nova sessão de ajuste a partir de uma sessão existente. Depois você pode alterar as opções de ajuste da nova sessão conforme necessário. Quando você avalia uma sessão existente, como descrito no procedimento anterior, o Orientador de Otimização do Mecanismo de Banco de Dados também cria uma nova sessão de ajuste, mas você não pode alterar as opções de ajuste.  
  
##### <a name="to-create-new-tuning-sessions-by-cloning-existing-sessions"></a>Para criar novas sessões de ajuste pela clonagem de sessões existentes  
  
1.  Depois de iniciar o Orientador de Otimização do Mecanismo de Banco de Dados, clique duas vezes em uma sessão de ajuste na metade superior do **Monitor de Sessão**, que carrega as informações da sessão no Orientador de Otimização do Mecanismo de Banco de Dados.  
  
2.  No menu **Ações** , clique em **Clonar Sessão**.  
  
3.  Na guia **Geral** , digite um **Nome de sessão**e verifique se a **Carga de trabalho** correta está especificada.  
  
4.  Na guia **Opções de Ajuste** , você pode especificar um tempo de ajuste, as estruturas físicas de projeto que o Orientador de Otimização do Mecanismo de Banco de Dados deve considerar para a criação e o que ele deve descartar na recomendação.  
  
5.  Clique em **Opções Avançadas** se você quiser definir um limite espacial para recomendações, um número máximo de colunas por índice, e se deseja que o Orientador de Otimização do Mecanismo de Banco de Dados gere recomendações que podem ser implementadas enquanto o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver online.  
  
6.  Clique no botão **Iniciar Análise** na barra de ferramentas para analisar os efeitos da carga de trabalho como em qualquer outra sessão de ajuste. Quando o Orientador de Otimização do Mecanismo de Banco de Dados terminar, você pode exibir os resultados dessa sessão como faria normalmente com qualquer outra.  
  
##  <a name="UI"></a> Descrições da interface do usuário  
  
### <a name="sessions-monitor"></a>Monitoramento de sessões  
 O**Monitor de Sessão** exibe informações sobre as sessões abertas no Orientador de Otimização do Mecanismo de Banco de Dados. Selecione um nome de sessão no **Monitor de Sessão**para exibir informações sobre a sessão na janela Propriedades.  
  
### <a name="recommendations-tab"></a>Guia Recomendações  
 A guia **Recomendações** aparece depois que o Orientador de Otimização do Mecanismo de Banco de Dados conclui a análise da carga de trabalho. Essa grade contém as recomendações para todos os objetos considerados. Quando houver recomendações de partição, elas serão apresentadas na grade superior, e as recomendações de índice, na grade inferior. As grades não aparecem quando não há recomendações.  
  
 A coluna **Definição** contém a definição da partição recomendada ou índice na forma de um hiperlink. Essa coluna, em geral, é muito estreita para exibir a definição inteira. Clique no hiperlink para exibir uma caixa de diálogo que contém a definição completa e o botão **Copiar na área de transferência** .  
  
#### <a name="partition-recommendations"></a>Recomendações de Partição  
 **Nome do Banco de Dados**  
 Banco de dados que contém os objetos recomendados a serem modificados.  
  
 **Recomendação**  
 Ação recomendada para aperfeiçoar o desempenho. Os valores possíveis são Criar e Descartar.  
  
 **Destino da Recomendação**  
 Função de partição ou esquema afetados pela recomendação. O ícone dessa coluna reflete a recomendação para descartar ou adicionar o **Destino da Recomendação** e se a recomendação consiste em uma função de partição ou esquema.  
  
 **Detalhes**  
 Uma descrição do **Destino da Recomendação**. Os valores possíveis incluem um intervalo de funções de partição ou em branco para esquemas de partição.  
  
 **N.º de partições**  
 Número de partições definido pelas funções particionamento recomendadas. Quando essa função é usada com um esquema e depois aplicada a uma tabela, os dados da tabela dividem-se entre essas várias partições.  
  
 **Definição**  
 A definição do **Destino da Recomendação**. Clique na coluna para abrir a caixa de diálogo Visualização de script SQL com um script para a ação recomendada.  
  
##### <a name="index-recommendations"></a>Recomendações de Índice  
 **Database Name**  
 Banco de dados que contém os objetos recomendados a serem modificados.  
  
 **Object Name**  
 Tabela relacionada à recomendação.  
  
 **Recomendação**  
 Ação recomendada para aperfeiçoar o desempenho. Os valores possíveis são Criar e Descartar.  
  
 **Destino da Recomendação**  
 Índice ou exibição afetados pela recomendação. O ícone dessa coluna reflete a recomendação para descartar ou adicionar o **Destino da Recomendação**.  
  
 **Detalhes**  
 Uma descrição do **Destino da Recomendação**. Os possíveis valores incluem exibição clusterizada, indexada ou espaço em branco indicando um índice não clusterizado. Indica igualmente quando o índice é exclusivo.  
  
 **Esquema de partição**  
 O esquema de partição é fornecido nessa coluna quando o particionamento é recomendado.  
  
 **Tamanho (KB)**  
 Tamanho esperado do novo objeto sendo recomendado. Se essa coluna estiver em branco, clique em **Consulte os relatórios para obter tamanhos de objetos existentes**.  
  
 **Definição**  
 A definição do **Destino da Recomendação**. Clique na coluna para abrir a caixa de diálogo Visualização de script SQL com um script para a ação recomendada.  
  
 **Mostrar objetos existentes**  
 Selecione para mostrar todos os objetos existentes na grade, mesmo se nenhuma recomendação relativa aos objetos for feita pelo Orientador de Otimização do Mecanismo de Banco de Dados.  
  
 **Consulte os relatórios para obter tamanhos de objetos existentes**  
 Selecione para exibir relatórios que fornecem o tamanho de objetos existentes na grade de recomendações.  
  
### <a name="actions-menuapply-recommendations-options"></a>Opções do menu Ações/Aplicar Recomendações  
 Depois que uma carga de trabalho foi analisada e as recomendações foram apresentadas, no menu **Ações** , clique em **Aplicar Recomendações** para abrir a caixa de diálogo **Aplicar Recomendações** .  
  
 **Aplicar agora**  
 Gera um script para as recomendações e executa-o a fim de implementar as recomendações.  
  
 **Agendar para mais tarde**  
 Gera um script para as recomendações e salva as ações como um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 **Date**  
 Especifica a data em que você quer executar o trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a fim de aplicar as recomendações.  
  
 **Time**  
 Especifica a hora em que você quer executar o trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a fim de aplicar as recomendações.  
  
### <a name="reports-tab-options"></a>Opções da guia Relatórios  
 A guia **Relatórios** aparece depois que o Orientador de Otimização do Mecanismo de Banco de Dados conclui a análise da carga de trabalho.  
  
 **Resumo do Ajuste**  
 Exibe um resumo das recomendações do Orientador de Otimização do Mecanismo de Banco de Dados.  
  
 **Date**  
 Data em que o Orientador de Otimização do Mecanismo de Banco de Dados cria o relatório.  
  
 **Hora**  
 Hora em que o Orientador de Otimização do Mecanismo de Banco de Dados cria o relatório.  
  
 **Servidor**  
 Servidor de destino da carga de trabalho do Orientador de Otimização do Mecanismo de Banco de Dados.  
  
 **Bancos de dados para ajustar**  
 Banco de dados afetado pelas recomendações do Orientador de Otimização do Mecanismo de Banco de Dados.  
  
 **Arquivo da carga de trabalho**  
 Aparece quando a carga de trabalho é um arquivo.  
  
 **Tabela da carga de trabalho**  
 Aparece quando a carga de trabalho é uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Carga de trabalho**  
 Aparece quando a carga de trabalho foi importada do Editor de Consultas em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Tempo máximo de ajuste**  
 Tempo máximo configurado para estar disponível para a análise do Orientador de Otimização do Mecanismo de Banco de Dados.  
  
 **Tempo gasto para ajustar**  
 Tempo gasto verdadeiramente pelo Orientador de Otimização do Mecanismo de Banco de Dados para analisar a carga de trabalho.  
  
 **Aperfeiçoamento de percentual esperado**  
 Porcentagem de aperfeiçoamento esperada com a carga de trabalho de destino se todas as recomendações do Orientador de Otimização do Mecanismo de Banco de Dados forem implementadas.  
  
 **Espaço máximo para a recomendação (MB)**  
 Espaço máximo considerado para as recomendações. Esse valor é configurado antes da realização da análise, usando o botão **Opções Avançadas** da guia **Opções de Ajuste** .  
  
 **Espaço usado atualmente (MB)**  
 Espaço usado atualmente pelos índices do banco de dados analisado.  
  
 **Espaço usado pela recomendação (MB)**  
 Espaço aproximado com expectativa de ser utilizado pelos índices se todas as recomendações do Orientador de Otimização do Mecanismo de Banco de Dados forem implementadas.  
  
 **Número de eventos na carga de trabalho**  
 Número de eventos contidos na carga de trabalho.  
  
 **Número de eventos ajustados**  
 Número de eventos da carga de trabalho que foram ajustados. Se o evento não puder ser ajustado, será listado no log de ajuste disponibilizado na guia **Progresso** .  
  
 **Número de instruções ajustadas**  
 Número de instruções da carga de trabalho que foram ajustadas. Se a instrução não puder ser ajustada, será listada no log de ajuste disponibilizado na guia **Progresso** .  
  
 **Porcentagem de instruções SELECT do conjunto ajustado**  
 Porcentagem de instruções ajustadas que são instruções SELECT. Aparece somente se houver instruções SELECT ajustadas.  
  
 **Porcentagem de instruções UPDATE do conjunto ajustado**  
 Porcentagem de instruções ajustadas que são instruções UPDATE. Aparece somente se houver instruções UPDATE ajustadas.  
  
 **Número de índices recomendados para serem [criados | descartados]**  
 Número recomendado de índices a serem criados ou descartados no banco de dados ajustado. Aparece somente se os índices fizerem parte da recomendação.  
  
 **Número de índices em exibições recomendadas para serem [criadas | descartadas]**  
 Número recomendado de índices em exibições a serem criados ou descartados do banco de dados ajustado. Aparece somente se os índices em exibições fizerem parte da recomendação.  
  
 **Número de estatísticas recomendadas para serem criadas**  
 Número recomendado de estatísticas a serem criadas no banco de dados ajustado. Aparece somente se as estatísticas forem recomendadas.  
  
 **Select Report**  
 Consulte os detalhes do relatório selecionado. As colunas da grade variam em todos os relatórios.  
  
## <a name="see-also"></a>Consulte Também  
 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [Utilitário dta](../../tools/dta/dta-utility.md)  
  
  

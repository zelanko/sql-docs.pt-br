---
title: Analisar o desempenho do script | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.codeanalysis.configuring
ms.assetid: f4bbdd31-12a5-4c57-b0fe-1c6683820f11
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 01b197d8c196bb94ae399a251563bba48f4fe5ef
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105797"
---
# <a name="analyze-script-performance"></a>Analisar o desempenho do script
Você pode usar as ferramentas fornecidas pelo SQL Server Data Tools para determinar se pode melhorar o desempenho de sua consulta, procedimentos armazenados ou scripts. Por exemplo, ao monitorar estatísticas de cliente como os tempos de resposta a consultas utilizadas com frequência, é possível determinar se são necessárias alterações na consulta ou nos índices das tabelas. Essas estatísticas podem incluir o tempo de execução do cliente, o perfil de consulta e pacotes/bytes enviados e recebidos.  
  
Além disso, determinados problemas de desempenho são melhor resolvidos analisando as consultas e atualizações do aplicativo que o aplicativo envia ao banco de dados e como essas consultas e atualizações interagem com os dados contidos no banco de dados e com o esquema de banco de dados. Os planos de execução exibem graficamente os métodos de recuperação de dados escolhidos pelo otimizador de consulta do SQL Server e mostram o custo de execução de instruções e consultas específicas. Assim, eles podem ajudá-lo a entender como o SQL Server processará sua consulta SQL e a determinar o que está causando o atraso do desempenho.  
  
## <a name="using-client-statistics"></a>Usando estatísticas do cliente  
Quando você executar um script ou consulta no Editor Transact\-SQL, poderá optar por coletar estatísticas do cliente, como perfil de aplicativo, rede e estatísticas de tempo para a execução. Essas métricas permitem que você meça a eficiência de seu script ou defina um parâmetro de comparação para diferentes scripts.  
  
Para ativar/desativar a coleta de estatísticas do cliente, quando o Editor Transact\-SQL estiver aberto, no menu **Dados**, aponte para Editor **Transact\-SQL**, clique em **Configurações de Execução** e em **Incluir Estatísticas do Cliente**. Como alternativa, clique no botão **Incluir Estatísticas do Cliente** (o quinto a partir da direita) na barra de ferramentas do Editor Transact\-SQL, ou clique com o botão direito do mouse no editor Transact\-SQL e selecione **Configurações de Execução** e **Incluir Estatísticas do Cliente**. Observe que, a fim de coletar estatísticas para uma consulta, você tem que ativar este recurso antes de executá-lo.  
  
Se você ativou as estatísticas de cliente, a guia **Estatísticas** será exibida ao lado da guia **Mensagem** após a execução da consulta. Se você desativou as estatísticas de cliente, a guia **Estatísticas** não será exibida. São listadas estatísticas de execuções de consulta sucessivas junto com os valores médios.  
  
Para saber mais sobre as estatísticas coletadas, confira [Painel de Estatísticas de Janela de Consulta](https://msdn.microsoft.com/library/aa216969(SQL.80).aspx) e a [seção "Guia de Estatísticas do Cliente" deste tópico](https://msdn.microsoft.com/library/aa833205.aspx).  
  
## <a name="using-execution-plans"></a>Utilizando planos de execução  
Os planos de execução exibem como o mecanismo de banco de dados navega nas tabelas e como usa os índices para acessar ou processar os dados para uma consulta ou outra instrução DML, como uma atualização. Essa abordagem gráfica é muito útil para entender as características de desempenho de uma consulta.  
  
Abra um script Transact\-SQL que contenha as consultas que você deseja analisar no editor Transact\-SQL. Você pode realçar o código que deseja analisar e optar por exibir um plano de execução estimado clicando no botão **Exibir Plano de Execução Estimado** na barra de ferramentas do editor. Se você clicar em **Exibir Plano de Execução Estimado**, as consultas ou lotes do Transact\-SQL não serão executadas(os). Em vez disso, o script será analisado e o plano de execução de consulta que o mecanismo de banco de dados teria maior probabilidade de usar se as consultas que foram realmente executadas fossem exibidas.  
  
Depois de o script ter sido analisado ou executado, clique na guia **Plano de execução** para ver uma representação gráfica da saída do plano de execução.  
  
A saída do plano de execução gráfica é lida da direita para a esquerda e de cima para baixo. Cada consulta no lote analisado é exibida, inclusive o custo de cada consulta, como uma porcentagem do custo total do lote. Para exibir mais informações como o custo e a operação para cada etapa, passe o mouse sobre os [ícones dos operadores lógicos e físicos](https://msdn.microsoft.com/library/ms175913.aspx) no plano gráfico.  
  
Para alterar a exibição do plano de execução, clique com o botão direito do mouse no **Plano de execução** e selecione **Ampliar**, **Reduzir**, **Zoom Personalizado** ou **Ajustar Nível de Zoom**. **Ampliar** e **Reduzir** permitem ampliar ou reduzir o plano de execução com valores fixos. **Zoom personalizado** permite que você defina sua própria ampliação da exibição, como ampliar em 80 por cento.  **Ajustar nível de zoom** ajusta o plano de execução de acordo com o painel de resultados.  
  
Planos de execução podem ser salvos e reabrir posteriormente para exame. Para isso, clique com o botão direito no **Plano de Execução** e selecione **Salvar Plano de Execução como**. Depois disso, você pode abrir o plano no Visual Studio assim como abre qualquer outro tipo de arquivo.  
  
## <a name="using-code-analysis"></a>Usando análise de código  
Você pode usar Análise de Código para descobrir problemas potenciais em seus scripts, como design, nomeação e problemas de desempenho.  As regras para projetos de bancos de dados são organizadas em conjuntos de regras predefinidas que se destinam a áreas específicas, e você pode habilitar ou desabilitar qualquer regra na guia **Análise de Código** na página de propriedades **Propriedades de Projeto** . Na mesma guia, você pode especificar a análise de código para ser executada automaticamente toda vez que um projeto é compilado, ou se os avisos são tratados como erros.  
  
Para usar a Análise de Código manualmente, clique com o botão direito do mouse no seu projeto no **Gerenciador de Soluções** e selecione **Executar Análise de Código**. Os avisos da análise de código são listados na janela **Lista de Erros** . Você pode clicar duas vezes em um aviso para navegar para o código-fonte que contém o problema e você pode exibir informações adicionais e possíveis correções para um aviso usando o menu contextual **Mostrar Ajuda para erros**.  
  
Para obter mais informações sobre Análise de Código, consulte [Analisando o código do banco de dados para melhorar a qualidade do código](https://msdn.microsoft.com/library/dd172133.aspx)(a página pode estar em inglês).  
  

---
title: "Orientador de Otimização do Mecanismo de Banco de Dados | Microsoft Docs"
ms.custom: 
ms.date: 01/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dta.general.f1
ms.assetid: 50dd0a0b-a407-4aeb-bc8b-b02a793aa30a
caps.latest.revision: "16"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 11720ea18ba01bd0cdaec11e4500dc5cba5ef24c
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="database-engine-tuning-advisor"></a>Database Engine Tuning Advisor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] O DTA (Orientador de Otimização do Mecanismo de Banco de Dados) do [!INCLUDE[msCoName](../../includes/msconame-md.md)] analisa bancos de dados e faz recomendações que você pode usar para otimizar desempenho de consulta. Você pode usar o Orientador de Otimização do Mecanismo de Banco de Dados para selecionar e criar um conjunto ideal de índices, exibições indexadas e partições de tabela sem precisar de conhecimentos avançados sobre a estrutura do banco de dados ou dos recursos internos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Com o DTA, é possível executar as tarefas a seguir.  
  
-   Solucionar problemas de desempenho de uma consulta de problema específica  
  
-   Ajustar um conjunto grande de consultas por um ou mais bancos de dados  
  
-   Executar uma análise E-Se exploratória de possíveis alterações de design físico  
  
-   Gerenciar o espaço de armazenamento  
  
## <a name="database-engine-tuning-advisor-benefits"></a>Benefícios do Orientador de Otimização do Mecanismo de Banco de Dados  
 A otimização do desempenho de consulta pode ser difícil sem uma compreensão completa da estrutura de banco de dados e as consultas que são executadas no banco de dados. O Orientador de Otimização do Mecanismo de Banco de Dados pode fazer essa tarefa com mais facilidade analisando o cache de planos da consulta atual ou analisando uma carga de trabalho de consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] que você cria e recomendando um design físico apropriado. Para administradores de banco de dados mais experientes, o DTA expõe um mecanismo avançado para executar a análise E-Se exploratória de diferentes alternativas de design físico. O DTA pode fornecer as seguintes informações.  
  
-   Recomendar a melhor combinação de índices rowstore e [columnstore](../../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md) para bancos de dados utilizando o otimizador de consulta para analisar consultas em uma carga de trabalho.  
  
-   Recomendar partições alinhadas ou desalinhadas para bancos de dados referenciados em uma carga de trabalho.  
  
-   Recomendar exibições indexadas para bancos de dados referenciados em uma carga de trabalho.  
  
-   Analisar os efeitos das mudanças propostas, inclusive o uso de índice, distribuição de consultas entre tabelas e desempenho de consultas na carga de trabalho.  
  
-   Recomendar modos de ajuste do banco de dados para um pequeno conjunto de consultas de problema.  
  
-   Permitir a personalização da recomendação especificando opções avançadas, como restrição de espaço em disco.  
  
-   Fornecer relatórios que resumam os efeitos de implementação das recomendações para uma determinada carga de trabalho.  

-   Considerar alternativas em que você fornece possíveis escolhas de design no formulário de configurações hipotéticas para avaliação do Orientador de Otimização do Mecanismo de Banco de Dados.

-  Ajustar cargas de trabalho de uma variedade de fontes, incluindo arquivo e tabela do Repositório de Consultas do SQL Server, do Plan Cache, de Rastreamento do SQL Server Profiler ou um arquivo .SQL.

  
 O Orientador de Otimização do Mecanismo de Banco de Dados é projetado para tratar os seguintes tipos de cargas de trabalho de consulta.  
  
-   Processamento de transações online (OLTP) somente consulta  
  
-   Processamento analítico online (OLAP) somente consulta  
  
-   Consultas OLAP e OLTP mistas  
  
-   Cargas de trabalho de consulta pesadas (mais consultas do que modificações de dados)  
  
-   Cargas de trabalho de atualização pesadas (mais modificações de dados do que consultas)  
  
## <a name="dta-components-and-concepts"></a>Componentes e conceitos do DTA  
 Interface gráfica do usuário do Orientador de Otimização do Mecanismo de Banco de Dados  
 Uma interface fácil de usar na qual você pode especificar a carga de trabalho e selecionar várias opções de ajuste.  
  
 Utilitário**dta**   
 A versão do prompt de comando do Orientador de Otimização do Mecanismo de Banco de Dados. O utilitário **dta** foi projetado para permitir o uso da funcionalidade do Orientador de Otimização do Mecanismo de Banco de Dados em aplicativos e scripts.  
  
 carga de trabalho  
 Um arquivo de script, um arquivo de rastreamento ou uma tabela de rastreamento Transact-SQL que contém uma carga de trabalho representativa para os bancos de dados a serem ajustados. Começando com o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], você pode especificar o cache de planos como carga de trabalho.  A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], é possível [especificar o Repositório de Consultas como a carga de trabalho](../../relational-databases/performance/tuning-database-using-workload-from-query-store.md). 
  
 Arquivo de entrada XML  
 Um arquivo formatado pelo XML que o Orientador de Otimização do Mecanismo de Banco de Dados pode usar para ajustar cargas de trabalho. O arquivo de entrada XML dá suporte a opções de ajuste avançadas que não estão disponível na GUI nem no utilitário **dta** .  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 O Orientador de Otimização do Mecanismo de Banco de Dados tem as seguintes limitações e restrições:  
  
-   Ele não pode adicionar ou remover índices exclusivos ou índices que impõem restrições PRIMARY KEY ou UNIQUE.  
  
-   Ele não pode analisar um banco de dados que está definido para modo de usuário único.  
  
-   Se você especificar um espaço máximo em disco para ajustar recomendações que excedem o espaço disponível real, o Orientador de Otimização do Mecanismo de Banco de Dados usará o valor especificado. No entanto, quando você executa o script de recomendação para implementá-lo, o script poderá apresentar erro se antes não for adicionado mais espaço em disco. O espaço máximo em disco pode ser especificado com a opção **-B** do utilitário **dta** , ou inserindo um valor na caixa de diálogo **Opções de Ajuste Avançadas** .  
  
-   Por razões de segurança, o Orientador de Otimização do Mecanismo de Banco de Dados não pode ajustar uma carga de trabalho em uma tabela de rastreamento que reside em um servidor remoto. Para driblar essa limitação, você pode usar um arquivo de rastreamento em vez de uma tabela de rastreamento ou pode copiar a tabela de rastreamento para o servidor remoto.  
  
-   Quando você impõe restrições, como as impostas quando você especifica um espaço máximo em disco ao ajustar recomendações (usando a opção **-B** ou a caixa de diálogo **Opções de Ajuste Avançadas** ), o Orientador de Otimização do Mecanismo de Banco de Dados pode ser forçado a remover certos índices existentes. Nesse caso, a recomendação Orientador de Otimização do Mecanismo de Banco de Dados resultante pode produzir um aperfeiçoamento esperado negativo.  
  
-   Quando você especifica uma restrição para limitar o tempo de ajuste (usando a opção **-A** com o utilitário **dta** ou marcando **Limitar tempo de ajuste** na guia **Opções de Ajuste** ), o Orientador de Otimização do Mecanismo de Banco de Dados pode exceder o tempo limite para produzir um aperfeiçoamento esperado preciso e os relatórios de análise para as porções da carga de trabalho consumidas até o momento.  
  
-   O Orientador de Otimização do Mecanismo de Banco de Dados não faz recomendações nas seguintes circunstâncias:  
  
    1.  A tabela que está sendo ajustada contém menos de 10 páginas de dados.  
  
    2.  Os índices recomendados não oferecem aperfeiçoamento suficiente no desempenho da consulta no design do banco de dados físico atual.  
  
    3.  O usuário que executa o Orientador de Otimização do Mecanismo de Banco de Dados não é um membro da função de banco de dados **db_owner** nem da função de servidor fixa **sysadmin** . As consultas na carga de trabalho são analisadas no contexto de segurança do usuário que executa o Orientador de Otimização do Mecanismo de Banco de Dados. O usuário deve ser um membro da função de banco de dados **db_owner** .  
  
-   O Orientador de Otimização do Mecanismo de Banco de Dados armazena dados de sessão de ajuste e outras informações no banco de dados **msdb** . Se forem feitas mudanças no banco de dados **msdb** você poderá perder dados da sessão de ajuste. Para eliminar esse risco, implemente uma estratégia de backup apropriada para o banco de dados **msdb** .  
  
## <a name="performance-considerations"></a>Considerações sobre desempenho  
 O Orientador de Otimização do Mecanismo de Banco de Dados pode consumir recursos de processador e memória significativos durante a análise. Para evitar a redução de velocidade do servidor de produção, siga uma destas estratégias:  
  
-   Ajuste os bancos de dados quando o servidor estiver livre. O Orientador de Otimização do Mecanismo de Banco de Dados pode afetar o desempenho da tarefa de manutenção.  
  
-   Use o recurso servidor de teste/servidor de produção. Para obter mais informações, consulte  [Reduzir a carga de ajuste do servidor de produção](../../relational-databases/performance/reduce-the-production-server-tuning-load.md).  
  
-   Especifique só as estruturas de design de banco de dados físico que você quer que o Orientador de Otimização do Mecanismo de Banco de Dados analise. O Orientador de Otimização do Mecanismo de Banco de Dados fornece muitas opções, mas só especifica as que são necessárias.  
  
## <a name="dependency-on-xpmsver-extended-stored-procedure"></a>Dependência em Procedimento armazenado estendido xp_msver  
 O Orientador de Otimização do Mecanismo de Banco de Dados depende do procedimento armazenado estendido **xp_msver** para fornecer a funcionalidade completa. Esse procedimento armazenado estendido é ativado por padrão. O Orientador de Otimização do Mecanismo de Banco de Dados usa esse procedimento armazenado estendido para buscar o número de processadores e a memória disponível no computador onde o banco de dados que está sendo ajustado está localizado. Se o **xp_msver** não estiver disponível, o Orientador de Otimização do Mecanismo de Banco de Dados assumirá as características de hardware do computador no qual o Orientador de Otimização do Mecanismo de Banco de Dados está sendo executado. Se as características de hardware do computador onde o Orientador de Otimização do Mecanismo de Banco de Dados está sendo executado não estiverem disponíveis, supõe-se um processador e 1024 megabytes (MBs) de memória.  
  
 Essa dependência afeta as recomendações de particionamento porque o número de partições recomendado depende destes dois valores (número de processadores e memória disponível). A dependência também afeta os resultados de ajustes quando você usar um servidor de teste para ajustar o servidor de produção. Nesse cenário,o Orientador de Otimização do Mecanismo de Banco de Dados usa o **xp_msver** para buscar propriedades de hardware do servidor de produção. Após ajustar a carga de trabalho no servidor de teste, o Orientador de Otimização do Mecanismo de Banco de Dados usa estas propriedades de hardware para gerar uma recomendação. Para obter mais informações, veja [xp_msver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-msver-transact-sql.md).  
  
## <a name="database-engine-tuning-advisor-tasks"></a>Tarefas do Orientador de Otimização do Mecanismo de Banco de Dados  
 A tabela a seguir lista as tarefas comuns do Orientador de Otimização do Mecanismo de Banco de Dados e os tópicos que descrevem como executá-los.  
  
|Tarefa do Orientador de Otimização do Mecanismo de Banco de Dados|Tópico|  
|-----------------------------------------|-----------|  
|Inicializar e iniciar o Orientador de Otimização do Mecanismo de Banco de Dados.<br /><br /> Criar uma carga de trabalho especificando o cache de planos, criando um script ou gerando um arquivo de rastreamento ou uma tabela de rastreamento.<br /><br /> Ajuste um banco de dados usando a ferramenta de interface gráfica Orientador de Otimização do Mecanismo de Banco de Dados<br /><br /> Criar arquivos de entrada XML para ajustar cargas de trabalho.<br /><br /> Exibir as descrições das opções de interface do usuário do Orientador de Otimização do Mecanismo de Banco de Dados.|[Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)|  
|Exibir os resultados da operação de ajuste do banco de dados.<br /><br /> Selecionar e implementar recomendações de ajuste.<br /><br /> Executar uma análise E-Se exploratória na carga de trabalho.<br /><br /> Revisar sessões de ajuste existente, clonar sessões com base nas existentes <br />ou editar recomendações de ajuste existente para avaliação adicional ou implementação.<br /><br /> Exibir as descrições das opções de interface do usuário do Orientador de Otimização do Mecanismo de Banco de Dados.|[Exibir e trabalhar com a saída do Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)|  
  
  

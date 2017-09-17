---
title: Atualizado - Advanced Analytics para documentos do SQL Server | Microsoft Docs
description: "Trechos de código de exibição de conteúdo atualizado recentemente alterada na documentação de, para Advanced Analytics para o Microsoft SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.workload: advanced-analytics
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: fb6185aae04a1fb53a4db03cbab267e3f52dc779
ms.contentlocale: pt-br
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>Novos e atualizados recentemente: Advanced Analytics para o SQL Server



A Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/) todos os dias. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **2017-07-18** &nbsp; - para - &nbsp; **2017-09-11**
- *Área de assunto:* &nbsp; **Advanced Analytics para o SQL Server**.

<!-- Repo = 'MicrosoftDocs/sql-docs'.   Branch = 'live'. -->



&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir saltar para novos artigos que foram adicionados recentemente.


1. [Como realizar em tempo real de pontuação ou pontuação nativo no SQL Server](r/how-to-do-realtime-scoring.md)
2. [Instalar pré-treinado modelos no SQL Server de aprendizado de máquina](r/install-pretrained-models-sql-server.md)
3. [Pontuação nativa](sql-native-scoring.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados a partir de artigos que encontraram recentemente uma atualização grande.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compact fornece links para todos os artigos atualizados que estão listados na seção foram extraídas.

1. [Configurar os serviços de aprendizado de máquina do Python (no banco de dados)](#TitleNum_1)
2. [Introdução ao revoscalepy](#TitleNum_2)
3. [Diferenças nos recursos de aprendizado de máquina entre edições do SQL Server](#TitleNum_3)
4. [Utilizar o código de R (serviços de aprendizado de máquina)](#TitleNum_4)
5. [Desempenho de serviços de R: resultados e recursos](#TitleNum_5)
6. [Desempenho de serviços do R - otimização de dados](#TitleNum_6)
7. [Gerenciamento de pacotes de R para o SQL Server](#TitleNum_7)
8. [Configurar os serviços de Machine Learning do SQL Server (no banco de dados)](#TitleNum_8)
9. [Configuração do SQL Server para uso com R](#TitleNum_9)
10. [Ajuste de desempenho de R no SQL Server](#TitleNum_10)
11. [Cenários de ciência de dados e modelos da solução](#TitleNum_11)
12. [O que há de novo nos serviços de aprendizado de máquina no SQL Server](#TitleNum_12)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-set-up-python-machine-learning-services-in-databasepythonsetup-python-machine-learning-servicesmd"></a>1. &nbsp;[Configurar serviços de aprendizado de máquina do Python (no banco de dados)](python/setup-python-machine-learning-services.md)

*Atualizado em: 2017-09-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([próxima](#TitleNum_2))

<!-- Source markdown line 263.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 fbe2ef55a5caecd64bb21ce854617a10b2d65567 8cd65baf77f27db00a0a4f07f3129a4231edb48b  (PR=3084  ,  Filename=setup-python-machine-learning-services.md  ,  Dirpath=docs\advanced-analytics\python\  ,  MergeCommitSha40=05976158e43d7dfafaf02289462d1537f5beeb36) -->



     [Modify the user account pool for SQL Server R Services--../r/modify-the-user-account-pool-for-sql-server-r-services.md)

Se você estiver usando o SQL Server Standard Edition e não tiver o administrador de recursos, você pode usar modos de exibição de gerenciamento dinâmico e eventos estendidos para ajudá-lo a gerenciar recursos do servidor. Você também pode usar o monitoramento de eventos do Windows para essa finalidade. Para obter mais informações, consulte [monitoramento e gerenciamento R Services –... /r/Managing-and-Monitoring-r-Solutions.MD).

**Atualizar a componentes de aprendizado de máquina**


Quando você instala os serviços de aprendizado de máquina usando o SQL Server 2017, que obter a versão dos componentes no momento em que a versão publicada. Cada vez que você corrigir ou atualiza a instância do SQL Server, os componentes de aprendizado de máquina são atualizados também.

Você pode atualizar a componentes em um agendamento mais rápido do que há suporte para de aprendizado de máquina por versões do SQL Server, instalando o servidor de aprendizado de máquina do Microsoft. Quando você fizer isso, você também obter os novos recursos de suporte na versão mais recente do servidor de aprendizado de máquina, como:

+ Atualizações para pacotes do Python para [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) e [microsoftml para Python](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).
+ [Modelos de classificação](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models) para análise de texto e de classificação de imagem.

Para obter informações sobre como atualizar uma instância, consulte [componentes de R atualizar por meio de associação-... \r\use-sqlbindr-exe-to-upgrade-an-instance-of-SQL-Server.MD).

> [!NOTE]
>
> A versão atual contém a versão mais recente de todos os componentes de aprendizado de máquina. Portanto, embora há suporte para atualizações através do servidor de aprendizado de máquina do Microsoft para SQL Server 2017, a atualização que está disponível no momento se aplica apenas às instâncias do SQL Server 2016.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-introducing-revoscalepypythonwhat-is-revoscalepymd"></a>2. &nbsp;[Apresentando revoscalepy](python/what-is-revoscalepy.md)

*Atualizado em: 2017-08-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1) | [próxima](#TitleNum_3))

<!-- Source markdown line 79.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 33f4e0e2421fa79fc11931dc7f29bff4432c6f5a d2eac3313a74bc5d5afd754fc357b3693e6801e1  (PR=2939  ,  Filename=what-is-revoscalepy.md  ,  Dirpath=docs\advanced-analytics\python\  ,  MergeCommitSha40=91098c850b0f6affb8e4831325d0f18fd163d71a) -->



| (column_1) | (Coluna_2) | (column_3) |
| :-- | :-- | :-- |
|`rx_btrees` | Ajustar as árvores de decisão ampliada de gradiente estocástico|`rx_btrees_ex`No CTP 2.0|
|`rx_dforest` | Ajustar a classificação e regressão florestas de decisão|`rx_dforest_ex`No CTP 2.0|
|`rx_dtree` | Árvores de classificação e regressão de ajuste |`rx_dtree_ex`No CTP 2.0|
|`rx_lin_mod` | Criar um modelo linear|`rx_lin_mod_ex`No CTP 2.0|
|`rx_logit` | Criar um modelo de regressão logística|`rx_logit_ex`No CTP 2.0|
|`rx_predict` | Gerar previsões de um modelo treinado|`rx_predict_ex`No CTP 2.0|
|`rx_summary` | Gerar um resumo do modelo||

Novos algoritmos de aprendizado de máquina também são fornecidos pela versão do Python [MicrosoftML](https://docs.microsoft.com/en-us/r-server/python-reference/microsoftml/microsoftml-package):

| Função| Description|
| ------ | ------ |
|`rx_fast_forest` |Criar um modelo de floresta de decisão|
|`rx_fast_linear` | Regressão linear com estocástico ascendente coordenada dupla|
|`rx_fast_trees` | Criar um modelo de árvore aprimorado |
|`rx_logistic_regression` | Criar um modelo de regressão logística|
|`rx_neural_network` | Criar um modelo de rede neural personalizável |
|`rx_oneclass_svm` | Cria um modelo SVM em um conjunto de dados desequilibrado, para uso na detecção de anomalias|

> [!TIP]
> Muitos desses algoritmos já são fornecidos como módulos no aprendizado de máquina do Azure.

MicrosoftML para Python também inclui uma variedade de transformações e funções auxiliares, como:

+ `rx_predict`gera previsões de um modelo treinado e pode ser usado para pontuação em tempo real
+ funções de personalização de imagem
+ funções para extração de sensibilidade e processamento de texto

Para obter detalhes, consulte [Introdução ao MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)


> [!NOTE]
> A comunidade de Python usa convenções de codificação que podem ser diferentes do que você está acostumado, incluindo todas as letras minúsculas e sublinhados em vez de concatenação com maiusculas e minúsculas para nomes de parâmetro. Além disso, talvez você tenha notado que o **revoscalepy** biblioteca está sempre em minúsculas. É isso! Outra convenção de Python.



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-differences-in-machine-learning-features-between-editions-of-sql-serverrdifferences-in-r-features-between-editions-of-sql-servermd"></a>3. &nbsp;[Diferenças nos recursos de aprendizado de máquina entre as edições do SQL Server](r/differences-in-r-features-between-editions-of-sql-server.md)

*Atualizado em: 2017-08-28* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_2) | [próxima](#TitleNum_4))

<!-- Source markdown line 47.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b5890e212063f3ef228e69afe54e226320d2467f 4e0357701d960c0b8dbda1ac8d56a82f3335c77f  (PR=2964  ,  Filename=differences-in-r-features-between-editions-of-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=7b4f037616e0559ac62bbae5dbe04aeffe529b06) -->



     Only Express Edition with Advanced Services includes the machine learning features. The performance limitations are similar to Standard Edition. Web edition is not intended for tasks such as creating machine learning models; however, you can use the PREDICT function to perform scoring using models trained elsewhere.

-   **Banco de Dados SQL do Azure**

     Recursos de aprendizado de máquina, como R e script de Python atualmente não têm suporte no banco de dados do SQL Azure.

     Para obter mais informações e anúncios sobre quando este recurso estará disponível, consulte o blog do SQL Server: [Python no SQL Server 2017: aprimorada de aprendizado de máquina no banco de dados](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)


**Idiomas com suporte em todas as edições**


Os idiomas de aprendizado de máquina a seguir têm suporte para todas as edições:

+ SQL Server 2017: R e Python
+ SQL Server 2016: Somente para R

O Microsoft R Open é incluído em todas as edições.



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-operationalize-r-code-machine-learning-servicesroperationalizing-your-r-codemd"></a>4. &nbsp;[Código de R operacionalizar (serviços de aprendizado de máquina)](r/operationalizing-your-r-code.md)

*Atualizado em: 2017-07-27* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_3) | [próxima](#TitleNum_5))

<!-- Source markdown line 56.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 7e11d9a5db93932ec89ca96b5337aa4ea03c1d13 0779f06444b5b73ae2dff8bc190d0e388b4ae8e7  (PR=2660  ,  Filename=operationalizing-your-r-code.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=70a1fd4dbec68d22187585de69a1d603c39e259e) -->



+ [Em tempo real –... / scoring.md de tempo real) de pontuação, otimizado para lotes pequenos
+ Pontuação de chamada de um aplicativo de linha única
+ [Nativo pontuação-... / sql-nativo-scoring.md), para previsão de lote rápido do SQL Server sem chamar o R

Este passo a passo fornece exemplos de pontuação usando um procedimento armazenado no lote e modos de única linha:

+ [Ponta a ponta passo a passo de ciência de dados para R no SQL Server--... / tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

Consulte esses modelos de solução para obter exemplos de como integrar um aplicativo de pontuação:

+ [Previsão de varejo](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [Detecção de fraudes](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/FraudDetection/Introduction.md)
+ [Clustering de cliente](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

**Aumentar o desempenho e escala**


Embora a linguagem R de software livre tenha limitações, o pacote RevoScaleR APIs podem operar em grandes conjuntos de dados e se beneficiar de cálculos no banco de dados de vários segmentos, com vários núcleos e vários processos.

Se sua solução R usa agregações complexas ou envolve grandes conjuntos de dados, você pode aproveitar as agregações do altamente eficientes na memória e índices columnstore do SQL Server e permitem que o código R tratar os cálculos estatísticos e pontuação.

Para obter mais informações sobre como melhorar o desempenho no aprendizado de máquina do SQL Server, consulte:

+ [Ajuste de desempenho para o SQL Server R Services--... /.. / advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [Truques e dicas de otimização do desempenho](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**Adaptar o código de R para outras plataformas ou contextos de computação**




&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-performance-for-r-services-results-and-resourcesrperformance-case-study-r-servicesmd"></a>5. &nbsp;[Desempenho para serviços de R: resultados e recursos](r/performance-case-study-r-services.md)

*Atualizado em: 2017-07-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_4) | [próxima](#TitleNum_6))

<!-- Source markdown line 282.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 40c8cd255ead88edc60531d45dd0377ecbaf7c9b eeca5eed96e2223508910b246dbff18173eecea3  (PR=2565  ,  Filename=performance-case-study-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=cf8509cab2424529ca0ed16c936fa63a139dfca4) -->



Pacotes de RevoScaleR e MicrosoftML foram usados para treinar um modelo de previsão em uma solução R complexo que envolvem grandes conjuntos de dados. Consultas SQL e código R foram idênticos. Todos os testes foram realizados em uma única VM do Azure com o SQL Server instalado. O autor, em seguida, em comparação com pontuação vezes com e sem essas otimizações fornecidas pelo SQL Server:

- Tabelas na memória
- Soft-NUMA
- Administrador de Recursos

Para avaliar o efeito de de software na execução do script R, a equipe de ciência de dados testado a solução em uma máquina virtual do Azure com 20 núcleos físicos. Nesses núcleos físicos, quatro nós de software foram criado automaticamente, de forma que cada nó contido cinco núcleos.

A relação de CPU foi imposta no cenário de correspondência de retomada, para avaliar o impacto sobre trabalhos em R. Quatro **pools de recursos SQL** e quatro **pools de recursos externos** foram criados, e a afinidade de CPU foi especificada para garantir que o mesmo conjunto de CPUs seria usado em cada nó.

Cada um dos pools de recursos foi atribuída a um grupo de carga de trabalho diferente, para otimizar a utilização do hardware. O motivo é que o Soft-NUMA e afinidade de CPU não é possível dividir a memória física em nós NUMA físicos; Portanto, por definição, todos os nós NUMA flexíveis que se baseiam no mesmo nó NUMA físico devem usar memória no mesmo bloco de memória do sistema operacional. Em outras palavras, não há nenhuma afinidade de processador de memória.

O processo a seguir foi usado para criar esta configuração:

1. Reduza a quantidade de memória alocada por padrão para o SQL Server.

2. Crie quatro novos pools para executar os trabalhos de R em paralelo.

3. Crie quatro grupos de cargas de trabalho, de modo que cada grupo de carga de trabalho está associado um pool de recursos.

4. Reinicie o administrador de recursos com as atribuições e novos grupos de carga de trabalho.

5. Crie uma função de classificador definida pelo usuário (UDF) para atribuir tarefas diferentes em grupos de cargas de trabalho diferentes.

6. Atualize a configuração do administrador de recursos para usar a função para grupos de cargas de trabalho apropriado.



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-performance-for-r-services---data-optimizationrr-and-data-optimization-r-servicesmd"></a>6. &nbsp;[Desempenho para serviços do R - otimização de dados](r/r-and-data-optimization-r-services.md)

*Atualizado em: 2017-07-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_5) | [próxima](#TitleNum_7))

<!-- Source markdown line 107.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2ae2e54e8c5c8a3ec92fd2017088dd6ee879a9a1 9cb06bdce4ad6dfa2e9dc19da49103a6cd9817b3  (PR=2565  ,  Filename=r-and-data-optimization-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=cf8509cab2424529ca0ed16c936fa63a139dfca4) -->



> Se uma tabela for especificada na fonte de dados em vez de uma consulta, R Services usa heurística interna para determina as colunas necessárias para buscar da tabela; No entanto, essa abordagem é improvável que resultam em execução em paralelo.

Para garantir que os dados podem ser analisados em paralelo, a consulta usada para recuperar os dados deve ser estruturada de forma que o mecanismo de banco de dados pode criar um plano de consulta paralela. Se o código ou o algoritmo usa grandes volumes de dados, verifique se a consulta fornecida ao `RxSqlServerData` é otimizado para execução paralela. Uma consulta que não resulta em um plano de execução paralela pode resultar em um único processo de computação.

Se você precisar trabalhar com grandes conjuntos de dados, use o Management Studio ou o outro analisador de consultas do SQL antes de executar seu código R, para analisar o plano de execução. Em seguida, execute as etapas recomendadas para melhorar o desempenho da consulta. Por exemplo, um índice ausente em uma tabela pode afetar o tempo necessário para executar uma consulta. Para obter mais informações, consulte [Monitor e ajuste de desempenho--... /.. / relational-databases/performance/monitor-and-tune-for-performance.md).

Outro erro comum que pode afetar o desempenho é uma consulta recupera mais colunas que são necessárias. Por exemplo, se uma fórmula se baseia apenas três colunas, mas sua tabela de origem tem 30 colunas, você está movendo dados desnecessariamente.

 + Evite usar `SELECT *`!
 + Reserve algum tempo para examinar as colunas no conjunto de dados e identificar apenas aqueles necessários para análise
 + Remova todas as colunas que contêm tipos de dados que são incompatíveis com o código de R, como GUIDS e rowguids suas consultas
 + Verificação de suporte para formatos de data e hora
 + Em vez de carregar uma tabela, criar uma exibição que seleciona certos valores ou converte colunas para evitar erros de conversão

**Otimizando o algoritmo de aprendizado de máquina**


Esta seção fornece dicas diversas e recursos que são específicos para RevoScaleR e outras opções no Microsoft R.



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-r-package-management-for-sql-serverrr-package-management-for-sql-server-r-servicesmd"></a>7. &nbsp;[Gerenciamento de pacotes de R para o SQL Server](r/r-package-management-for-sql-server-r-services.md)

*Atualizado em: 2017-08-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_6) | [próxima](#TitleNum_8))

<!-- Source markdown line 22.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2add5a7e1aef02487ac875e353c51161658050a4 5da92dd8b5402266a837172bda9aaabed3162ce8  (PR=2939  ,  Filename=r-package-management-for-sql-server-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=91098c850b0f6affb8e4831325d0f18fd163d71a) -->



Este tópico descreve os recursos de gerenciamento de pacote que você pode usar para gerenciar pacotes de R em execução em uma instância do SQL Server.

**Aplica-se a:** R Services do SQL Server 2016, SQL Server 2017 serviços de aprendizado de máquina

**Gerenciamento de pacotes usando o T-SQL**


Você pode continuar a instalar pacotes R como um administrador no computador, se você tiver esses privilégios, e se você for a única pessoa usando o servidor para trabalhos de aprendizado de máquina.

No entanto, se você precisa compartilhar pacotes com outras pessoas ou se precisam de várias pessoas executar tarefas de aprendizado de máquina no servidor, é mais eficiente para configurar uma biblioteca compartilhada de pacote. SQL Server oferece suporte a isso por meio de funções de banco de dados.

O administrador de banco de dados é responsável por configurar funções e adicionar usuários às funções. Por meio de funções, o administrador de banco de dados pode controlar quem tem permissão para adicionar ou remover pacotes de R de ambiente do SQL Server e pode fazer a auditoria de instalação do pacote.

**Funções de banco de dados de gerenciamento de pacote**


As novas funções de banco de dados a seguir dão suporte a uma instalação segura e gerenciamento de pacotes de R no SQL Server:

- `rpkgs-users`: Permite que os usuários usem qualquer compartilhados pacotes que foram instalados por membros do `rpkgs-shared` função.

- `rpkgs-private`: Fornece acesso aos pacotes compartilhados com as mesmas permissões que o `rpkgs-users` função. Os membros desta função também podem instalar, remover e usar pacotes com escopo definido como particular.

-  `rpkgs-shared`: Fornece as mesmas permissões que o `rpkgs-private` função. Os usuários que são membros dessa função também podem instalar ou remover pacotes compartilhados.

- `db_owner`: Tem as mesmas permissões que o `rpkgs-shared` função. Também pode conceder o aos usuários o direito de instalar ou remover pacotes compartilhados e privados.

**Criar uma biblioteca de pacote externo usando o T-SQL**


Além disso, o SQL Server 2017 suporta a instrução T-SQL, **criar biblioteca externa**, para dar suporte ao gerenciamento pelo administrador de banco de dados de bibliotecas externas. No momento, você pode usar essa instrução para criar bibliotecas com base em Windows adicionais de R. o suporte está planejado no futuro para pacotes do Python e para pacotes desenvolvidos para execução em outras plataformas, como o Linux.



&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-set-up-sql-server-machine-learning-services-in-databaserset-up-sql-server-r-services-in-databasemd"></a>8. &nbsp;[Configurar serviços de aprendizado de máquina do SQL Server (no banco de dados)](r/set-up-sql-server-r-services-in-database.md)

*Atualizado em: 2017-09-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_7) | [próxima](#TitleNum_9))

<!-- Source markdown line 240.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 452dc36b4d0097f9562642238ba49eea0373d25b 4d355f6494b417dd90dce3943e7176eaece7336e  (PR=3070  ,  Filename=set-up-sql-server-r-services-in-database.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=0b832a9306244210e693bde7c476269455e9b6d8) -->



Se você cria uma solução R em um computador de cliente de ciência de dados e precisa executar o código usando o computador do SQL Server como o contexto de computação, você pode usar um logon do SQL ou a autenticação integrada do Windows.

* Para logons SQL: certifique-se de que o logon tenha as permissões apropriadas no banco de dados em que os dados serão lidos. Você pode fazer isso adicionando *se conectem* e *selecione* permissões, ou adicionando o logon para o *db_datareader* função. Para logons que precisa para criar objetos, adicionar *funções DDL_admin* direitos. Para logons que devem salvar dados em tabelas, adicione o logon para o *db_datawriter* função.

* Para autenticação do Windows: talvez seja necessário configurar uma fonte de dados ODBC no cliente de ciência de dados que especifica o nome da instância e outras informações de conexão. Para obter mais informações, consulte [administrador de fonte de dados ODBC](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator).

**Próximas etapas**


Após ter verificado que o recurso de execução do script funciona no SQL Server, você pode executar comandos de R e Python do SQL Server Management Studio, o código do Visual Studio ou qualquer outro cliente que pode enviar instruções T-SQL para o servidor.

No entanto, você talvez queira fazer algumas alterações à configuração do sistema para dar suporte a um uso intenso do aprendizado de máquina, ou adicionar novos pacotes de R.

Esta seção lista algumas modificações comuns que você pode fazer para dar suporte ao aprendizado de máquina.

**Adicionar mais contas de trabalho**


Se você achar que você pode usar o R muito ou se você espera que muitos usuários scripts em execução ao mesmo tempo, você pode aumentar o número de contas de trabalho que são atribuídos ao serviço barra inicial. Para obter mais informações, consulte [modificar o pool de conta de usuário para SQL Server R Services--modify-the-user-account-pool-for-sql-server-r-services.md).

**<a name="bkmk_optimize"></a>Otimizar o servidor para execução de scripts externos**




&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-sql-server-configuration-for-use-with-rrsql-server-configuration-r-servicesmd"></a>9. &nbsp;[a configuração do SQL Server para uso com R](r/sql-server-configuration-r-services.md)

*Atualizado em: 2017-07-27* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_8) | [próxima](#TitleNum_10))

<!-- Source markdown line 149.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 3f57bae70e3c118c1e2bcd57017322940bae83f8 f296242d470db47077cba4215ef420bd0c60bf33  (PR=2660  ,  Filename=sql-server-configuration-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=70a1fd4dbec68d22187585de69a1d603c39e259e) -->



Se a consulta retorna um nó de memória único (nó 0), você não tem de hardware ou o hardware está configurado como intercalado (não NUMA). SQL Server também ignora de hardware quando há quatro ou menos CPUs, ou se pelo menos um nó tiver apenas uma CPU.

Se o computador tiver vários processadores, mas não tem de hardware, você também pode usar [Soft-NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server) subdividir as CPUs em grupos menores.  No SQL Server 2016 e no SQL Server 2017, o recurso de software é habilitado automaticamente ao iniciar o serviço do SQL Server.

Quando o NUMA é habilitado, o SQL Server gerencia automaticamente os nós para você; No entanto, para otimizar para cargas de trabalho específicas, você pode desabilitar _afinidade flexível_ e configurar manualmente a afinidade de CPU para nós NUMA flexíveis. Isso pode dar a você mais controle sobre quais cargas de trabalho são atribuídas a quais nós, especialmente se você estiver usando uma edição do SQL Server que oferece suporte à administração de recursos. Especificando a afinidade de CPU e alinhamento de pools de recursos com grupos de CPUs, você pode reduzir a latência e certifique-se de que os processos relacionados são executados no mesmo nó NUMA.

O processo geral para a configuração de soft-NUMA e afinidade de CPU para oferecer suporte a cargas de trabalho de R é o seguinte:

1. Habilitar o NUMA, se disponível
2. Definir a afinidade de processador
3. Criar pools de recursos para processos externos, usando [Resource Governor-... /r/Resource-Governance-for-r-Services.MD)
4. Atribuir [grupos de cargas de trabalho-... /.. / relational-databases/resource-governor/resource-governor-workload-group.md) para grupos de afinidade específicos

Para obter detalhes, incluindo o código de exemplo, consulte este tutorial: [SQL otimização dicas e truques (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**Outros recursos:**



&nbsp;

&nbsp;

---

<a name="TitleNum_10"/>

### <a name="10-nbsp-performance-tuning-for-r-in-sql-serverrsql-server-r-services-performance-tuningmd"></a>10. &nbsp;[Ajuste de desempenho de R no SQL Server](r/sql-server-r-services-performance-tuning.md)

*Atualizado em: 2017-07-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_9) | [próxima](#TitleNum_11))

<!-- Source markdown line 76.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9c30753efdec81e499d5654b5b7a07f0cfe5b003 136a9f483bc8c9e1f69cf9d340d1472c21a52ec4  (PR=2565  ,  Filename=sql-server-r-services-performance-tuning.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=cf8509cab2424529ca0ed16c936fa63a139dfca4) -->



- Configurar a instância do SQL Server para operações de mecanismo de banco de dados de saldo e R ou execução em níveis apropriados do script de Python. Isso pode incluir a alteração de padrões do SQL Server para memória e uso de CPU, NUMA e as configurações de afinidade do processador e criação de grupos de recursos.

- Otimize o computador do servidor para dar suporte a uso eficiente de scripts externos. Isso pode incluir a aumentar o número de contas usadas para a execução do script externo, permitindo o gerenciamento de pacote, e atribuir usuários relacionados a funções de segurança.

- Aplicando otimizações específicas para o armazenamento de dados e transferência no SQL Server, incluindo a indexação e estratégias de estatísticas, design de consulta e otimização de consulta e o design de tabelas que são usados para aprendizado de máquina. Você também pode analisar as fontes de dados e dados de métodos de transporte ou modificar os processos ETL para otimizar a extração do recurso.

- Ajuste o modelo analítico para evitar ineficiências. O escopo das otimizações de possíveis dependem da complexidade do seu código R e os pacotes e os dados que você está usando. As principais tarefas incluem eliminar transformações de dados cara ou descarregar dados preparação ou recurso engenharia tarefas de R ou Python para processos de ETL ou SQL. Você também pode refatorar scripts, eliminar instalações de pacote na linha, divida o código R em procedimentos separados para treinamento, pontuação e avaliação ou simplificar o código para trabalhar com mais eficiência um procedimento armazenado.

**Esta série de artigos**


+ [Ajuste de desempenho de R no SQL Server - hardware--... \r\sql-Server-Configuration-r-Services.MD)

    Fornece orientação para configurar o hardware que …! NCLUIR-NotShown - ssNoVersion_md-... \..\includes\ssnoversion-md.md)] é instalado e para configurar a instância do SQL Server para oferecer melhor suporte a scripts externos. Isso é especialmente útil para **os administradores de banco de dados**.

+ [Ajuste de desempenho de R no SQL Server - otimização de código e os dados –... \r\r-and-Data-Optimization-r-Services.MD)



&nbsp;

&nbsp;

---

<a name="TitleNum_11"/>

### <a name="11-nbsp-data-science-scenarios-and-solution-templatestutorialsdata-science-scenarios-and-solution-templatesmd"></a>11. &nbsp;[Cenários de ciência de dados e modelos de solução](tutorials/data-science-scenarios-and-solution-templates.md)

*Atualizado em: 2017-08-28* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_10) | [próxima](#TitleNum_12))

<!-- Source markdown line 45.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 22c621731015f2192cb0b8d61b22062a4be50e70 6cf9e3f0a3803ed2bce9c4ffadfd7314f15f6b51  (PR=2964  ,  Filename=data-science-scenarios-and-solution-templates.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=7b4f037616e0559ac62bbae5dbe04aeffe529b06) -->



[Prever como e quando entrar em contato com clientes potenciais](https://microsoft.github.io/r-server-campaign-optimization/)

**O que:** esta solução usa dados do setor de seguros para prever os clientes potenciais com base em dados demográficos, dados históricos de resposta e detalhes específicos do produto.  As recomendações são também geradas para indicar os melhores canal e tempo para os usuários a abordagem para influenciar o comportamento de compra.

**Como:** a solução cria e compara vários modelos. A solução também demonstra a integração de dados automatizado e preparação de dados usando procedimentos armazenados. São fornecidas amostras paralelas para SQL Server no banco de dados, no Azure e HDInsight Spark.

**Saúde: prever a duração da permanência na hospital**


[Prever a duração da permanência na hospitais](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**O que:** prever com precisão qual pacientes podem exigir a longo prazo hospitalization é uma parte importante do planejamento e cuidado. Os administradores precisam ser capaz de determinar quais recursos exigem mais recursos e profissionais deseja garantir que eles podem atender às necessidades de pacientes.

**Como:** essa solução utiliza a máquina de Virtual de ciência de dados e inclui uma instância do SQL Server com o aprendizado de máquina habilitado. Ele também inclui um conjunto de relatórios do Power BI que você pode usar para interagir com um modelo implantado.

**Variação de cliente**


[Modelo de previsão de rotatividade de cliente (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/Introduction.md)

**O que:** analisando e prevendo a variação do cliente é importante em qualquer setor onde a perda de clientes a concorrência deve ser gerenciada e impediu: transações bancárias, telecomunicações e comercial, para citar alguns. O objetivo da análise de variação é identificar quais clientes têm a probabilidade de variação e tomar medidas apropriadas para manter esses clientes e seus negócios.



&nbsp;

&nbsp;

---

<a name="TitleNum_12"/>

### <a name="12-nbsp-whats-new-in-machine-learning-services-in-sql-serverwhat-s-new-in-sql-server-machine-learning-servicesmd"></a>12. &nbsp;[o que há de novo nos serviços de aprendizado de máquina no SQL Server](what-s-new-in-sql-server-machine-learning-services.md)

*Atualizado em: 2017-08-02* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_11))

<!-- Source markdown line 33.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 025e68a93895a3788a63847cd91bff068775acf3 6dc0be2920c670235038a126d135e08d6f16ec3a  (PR=2712  ,  Filename=what-s-new-in-sql-server-machine-learning-services.md  ,  Dirpath=docs\advanced-analytics\  ,  MergeCommitSha40=ea75391663eb4d509c10fb785fcf321558ff0b6e) -->



> Serviços de aprendizado de máquina, incluindo o uso de R ou Python, atualmente não têm suporte durante a execução do SQL Server no Linux ou no banco de dados do SQL Azure. Procure as alterações em uma versão posterior.
>
> No entanto, a pontuação nativo usando a função de previsão é suportada atualmente na edição Linux.

**Integração de Python no banco de dados**


Você pode executar o Python em procedimentos armazenados ou executar remotamente usando o computador do SQL Server como o contexto de computação de Python. Essa integração abre novos caminhos para a grande comunidade de Python dados e desenvolvedores cientistas Use o poder do SQL Server e para explorar as inovações da Microsoft, como **revoscalepy** e **microsoftml**.

Os desenvolvedores do SQL Server acessar as bibliotecas Python abrangentes do ecossistema de software livre, incluindo estruturas conhecidas, como scikit-saber, Tensorflow, Caffe e Theano/Keras.

Mas executando o Python não está no banco de dados apenas do aprendizado de máquina; Há uma grande variedade de outros aplicativos potenciais para integrar o Python com SQL, aproveitando os pontos fortes do respectivos idiomas para fornecer soluções mais inteligentes e eficientes.

+ **revoscalepy**

    Esta versão inclui a versão final do **revoscalepy**, que fornece Pythonic equivalentes de escalonável, streaming algoritmos em RevoScaleR. Você pode criar modelos de Python para árvores de decisão, regressão linear e logística, árvores aumentadas e florestas aleatórias, todos os paralelizáveis e é capazes de está sendo executado em contextos de computação remota.

    Para obter mais informações, consulte [What ' s revoscalepy – python/e-for-revoscalepy.md).

+ Contextos de computação remota para Python

    Esta versão dá suporte ao uso de várias fontes de dados e contextos de computação remota. O cientista de dados ou o desenvolvedor pode executar o código Python em um servidor SQL remoto, para explorar dados ou criar modelos sem mover os dados. O uso de contextos de computação remota requer **revoscalepy**.







## <a name="similar-articles"></a>Artigos Semelhantes

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

Esta seção lista os artigos muito semelhantes para artigos atualizados recentemente em outras áreas de assunto, em nosso repositório público de GitHub.com: [sql/MicrosoftDocs-documentos](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que têm artigos novos ou atualizados recentemente

- [Novo + atualizado (3 + 12): **Advanced Analytics para o SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + atualizado (5 + 0): **conectar-se ao SQL** documentos](../connect/new-updated-connect.md)
- [Novo + atualizado (5 + 1): **mecanismo de banco de dados do SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Novo + atualizado (19 + 82): **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Novo + atualizado (1 + 8): **Linux para o SQL** documentos](../linux/new-updated-linux.md)
- [Novo + atualizado (12 + 1): **bancos de dados relacionais do SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Novo + atualizado (0 + 1): **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Novo + atualizado (7 + 1): **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Novo + atualizado (1 + 1): **SQL Server Data Tools (SSDT)** documentos](../ssdt/new-updated-ssdt.md)
- [Novo + atualizado (0 + 2): **Migration Assistant SSMA (SQL Server)** documentos](../ssma/new-updated-ssma.md)
- [Novo + atualizado (1 + 4): **SQL Server Management Studio (SSMS)** documentos](../ssms/new-updated-ssms.md)
- [Novo + atualizados (4 + 1): **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)
- [Novo + atualizado (0 + 1): **Tools para SQL** documentos](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas de assunto que não têm nenhum artigo novo ou atualizado recentemente

- [Novo + atualizado (0 + 0): documentos do **ADO (ActiveX Data Objects) para SQL**](../ado/new-updated-ado.md)
- [Novo + atualizado (0 + 0): **Analysis Services para SQL** documentos](../analysis-services/new-updated-analysis-services.md)
- [Novo + atualizado (0 + 0): documentos do **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): documentos de **Extensões DMX (Data Mining) para SQL**](../dmx/new-updated-dmx.md)
- [Novo + atualizado (0 + 0): **Master Data Services (MDS) para SQL** documentos](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): documentos de **Expressão MDX para SQL**](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): documentos do **ODBC (Open Database Connectivity) para SQL**](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): documentos do **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Novo + atualizado (0 + 0): documentos de **Exemplos para SQL**](../sample/new-updated-sample.md)
- [Novo + atualizado (0 + 0): documentos do **XQuery para SQL**](../xquery/new-updated-xquery.md)




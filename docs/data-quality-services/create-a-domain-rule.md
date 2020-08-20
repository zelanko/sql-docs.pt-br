---
description: Criar uma regra de domínio
title: Criar uma regra de domínio
ms.date: 11/08/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.dm.testdomainrule.f1
- sql13.dqs.dm.rules.f1
ms.assetid: 339fa10d-e22c-4468-b366-080c33f1a23f
author: swinarko
ms.author: sawinark
ms.openlocfilehash: b85a6f50b7e0759c5b691389c102236ce3df082b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487912"
---
# <a name="create-a-domain-rule"></a>Criar uma regra de domínio

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  Este tópico descreve como criar uma regra de domínio no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Uma regra de domínio é uma condição usada para validar, corrigir e padronizar valores de domínio. A regra de domínio deve se repetir em um domínio para que os valores de domínio sejam considerados precisos e em conformidade com os requisitos comerciais. As regras de domínio podem incluir regras de validação usadas para validar valores de domínio, mas não são usadas para corrigir dados em um projeto de qualidade de dados. As regras também incluem regras de padronização que são aplicadas com base nos dados válidos e usadas na correção de dados.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
 Para criar uma regra de domínio, você deve ter uma base de dados de conhecimento e um domínio aberto na atividade de Gerenciamento de Domínio.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_administrator no banco de dados DQS_MAIN para criar uma regra de domínio.  
  
##  <a name="build-domain-rules"></a><a name="Build"></a> Criar regras de domínio  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Execute o aplicativo Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , abra ou crie uma base de dados de conhecimento. Selecione **Gerenciamento de Domínio** como a atividade e, depois, clique em **Abrir** ou **Criar**. Para obter mais informações, consulte [Criar uma base de dados de conhecimento](../data-quality-services/create-a-knowledge-base.md) ou [Abrir uma base de dados de conhecimento](../data-quality-services/open-a-knowledge-base.md).  
  
    > [!NOTE]  
    >  O gerenciamento de domínio é executado em uma página do cliente Data Quality Services que contém cinco guias para operações de gerenciamento de domínio separadas. Não se trata de um processo controlado por assistente; qualquer operação de gerenciamento pode ser executada separadamente.  
  
3.  Na **Lista de domínios** na página **Gerenciamento de Domínio** , selecione o domínio para o qual você deseja criar uma regra de domínio ou crie um novo domínio. Se você precisar criar um novo domínio, consulte [Criar um Domínio](../data-quality-services/create-a-domain.md).  
  
4.  Clique na guia **Regras do Domínio** .  
  
5.  Clique em **Adicione uma nova regra de domínio**e digite um nome exclusivo na base de dados de conhecimento e uma descrição para a regra.  
  
6.  Selecione **Ativa** para especificar que a regra será executada (o padrão) ou anule a seleção para impedir a execução da regra.  
  
7.  No painel **criar uma regra** , selecione uma condição na lista suspensa na caixa de cláusula da regra.  
  
8.  Se a condição exigir um valor, insira o valor na caixa de texto associada.  
  
9. Clique no ícone **Adiciona uma nova condição à cláusula selecionada** se outra cláusula for necessária.  
  
10. Selecione **AND** ou **OR** como operador.  
  
11. Selecione uma condição na lista suspensa e insira um valor para o operando, se necessário.  
  
12. Para alterar a ordem em que as cláusulas aparecerão na lista, selecione uma cláusula e clique na seta para cima ou para baixo. Isso alterará a ordem em que elas serão executadas, o que poderia afetar os resultados.  
  
13. Adicione mais cláusulas quando necessário. Se necessário, exclua uma cláusula selecionando-a e clicando em **Exclui a cláusula selecionada**.  
  
14. Repita para adicionar novas regras, quando necessário.  
  
15. Para consultar o impacto que uma regra de validação terá nos valores se implementada, clique no ícone **Analise o impacto da regra de domínio nos valores de domínio** .  
  
16. Continue o procedimento de teste a seguir.  
  
##  <a name="test-domain-rules"></a><a name="Test"></a> Regras de domínio de teste  
  
1.  Com uma regra selecionada, clique no ícone **Executar a regra de domínio selecionada em dados de teste** .  
  
2.  Na caixa de diálogo Testar Regra de Domínio, clique no ícone **Adicionar um novo termo de teste para a regra de domínio** . Insira um valor para testar. Insira outros valores quando necessário. Selecione um valor e clique no ícone **Remover o termo de teste selecionado** se necessário.  
  
3.  Clique no ícone **Teste a regra de domínio em todos os termos** .  
  
4.  Verifique a validade de cada termo. Uma marca de verificação significa "correto", uma cruz significa "erro" e um triângulo significa "inválido".  
  
5.  Clique em **Fechar** quando terminar de usar a caixa de diálogo de teste.  
  
6.  Repita o mesmo procedimento para as outras regras, quando necessário.  
  
7.  Continue o procedimento de aplicação a seguir.  
  
##  <a name="apply-domain-rules"></a><a name="Apply"></a> Aplicar regras de domínio  
  
1.  Clique em **Aplicar Todas as Regras** para aplicar as regras aos valores do domínio. Se você clicar em **Aplicar Todas as Regras**, uma janela pop-up será exibida informando quantos valores em determinados estados serão afetados pela regra. Clique em **Sim** se você ainda desejar aplicar a regra; caso contrário, clique em **Não** . Se você clicar em **Sim**, clique em **OK** para fechar a janela pop-up de resultados.  
  
    > [!NOTE]  
    >  Quando você criar ou alterar uma regra, não precisará salvar as alterações. No entanto, você deve aplicar a regra para que as alterações entrem em vigor.  
  
2.  Clique em **Descartar Todas as Alterações** para remover qualquer alteração feita nas regras de domínio, fazendo a reversão para as regras previamente aplicadas, sabendo que qualquer alteração feita após a última aplicação das regras não se aplicará mais. A validade de cada valor no domínio será atualizada para estar em conformidade com as regras aplicadas anteriormente, e não com as alterações descartadas.  
  
3.  Clique em **Concluir** para concluir a atividade de gerenciamento de domínio, conforme descrito em [Terminar a atividade Gerenciamento de Domínio](https://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0).  
  
##  <a name="follow-up-after-creating-a-domain-rule"></a><a name="FollowUp"></a> Acompanhamento: depois de criar uma regra de domínio  
 Depois que você criar uma regra de domínio, poderá executar outras tarefas de gerenciamento de domínio, executar a descoberta da base de dados de conhecimento para adicionar conhecimento ao domínio ou adicionar uma política de correspondência ao domínio. Para obter mais informações, consulte [Executar a descoberta de conhecimento](../data-quality-services/perform-knowledge-discovery.md), [Gerenciando um domínio](../data-quality-services/managing-a-domain.md) ou [Criar uma política de conciliação](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="domain-rule-conditions"></a><a name="Conditions"></a> Condições de regra de domínio  
 A tabela a seguir descreve as condições que podem ser aplicadas na regra de domínio e fornece um exemplo para ilustrar como as condições podem ser aplicadas.  
  
 Quando uma regra de domínio é aplicada e um valor de domínio não obedece à regra, o valor é designado como Inválido. Um valor designado como Inválido será alterado para Correto se a regra que está fazendo com que ele seja inválido for excluída, for desativada ou se a regra tive sido alterada de modo que o valor não desobedeça mais à regra. Se você tiver designado manualmente um valor como Inválido (na guia Valores de Domínio da atividade de Gerenciamento de Domínio), e uma regra que dite a falha do valor tiver sido excluída, desativada ou alterada, o valor ainda será designado como Inválido, conforme a designação manual.  
  
 Uma regra de domínio com uma condição definitiva aplicará a lógica de regras a sinônimos do valor em uma ou mais condições, bem como os próprios valores. As condições definitivas são Valor é igual a, Valor não é igual a, Valor está em ou Valor não está em. Por exemplo, suponhamos que você tenha a seguinte regra de domínio: "Para ‘Cidade’, Valor é igual a ‘Los Angeles’". Se 'Los Angeles' e 'LA' forem sinônimos, ambos estarão corretos. Por outro lado, se a regra não contivesse uma condição definitiva, por exemplo, "Para Cidade, Valor termina com "s", então "Los Angeles" estaria correto, mas seu sinônimo "LA" seria um erro.  
  
 Você tem alternativas para escolher ao criar uma regra de domínio. Por exemplo, para validar se os valores começarão com a letra A, B ou C, você pode criar uma regra simples com uma condição complexa (como uma expressão regular com caracteres de pipe) ou criar uma regra complexa que contém várias condições simples. Um exemplo da primeira regra é "Valor contém a expressão regular (^A|^B|^C)". Um exemplo da segunda regra é "'Valor começa com A' OU 'Valor começa com B' OU 'Valor começa com C'".  
  
|Condição|Descrição|Exemplo|  
|---------------|-----------------|-------------|  
|Comprimento é igual a|Somente os valores compostos pelo número de caracteres designado pelo operando serão válidos.|Operando de exemplo: 3<br /><br /> Valor válido: BB1<br /><br /> Valor inválido: AA|  
|O comprimento é maior ou igual a|Somente os valores compostos pelo número de caracteres designado pelo operando, ou um número de caracteres superior, serão válidos.|Operando de exemplo: 3<br /><br /> Valores válidos: BB1, BBAA<br /><br /> Valor inválido: AA|  
|O comprimento é menor ou igual a|Somente os valores compostos pelo número de caracteres designado pelo operando, ou um número de caracteres inferior, serão válidos.|Operando de exemplo: 3<br /><br /> Valores válidos: BB1, AA<br /><br /> Valor inválido: BBAA|  
|Valor é igual a|Somente os valores idênticos ao operando serão válidos.|Operando de exemplo: BB1<br /><br /> Valor válido: BB1<br /><br /> Valor inválido: BB, BB1#|  
|Valor não é igual a|Somente os valores que não são idênticos ao operando serão válidos.|Operando de exemplo: BB1<br /><br /> Valor válido: BB, BB1#<br /><br /> Valor inválido: BB1|  
|Valor contém|Somente os valores cujos caracteres estão contidos no operando, em qualquer ordem, serão válidos.|Operando de exemplo: A1<br /><br /> Valores válidos: A1, AA1<br /><br /> Valor inválido: 1A, AA|  
|Valor não contém|Somente os valores que não estão contidos no operando serão válidos.|Operando de exemplo: A1<br /><br /> Valores válidos: 1A, AA<br /><br /> Valores inválidos: A1, AA1|  
|Valor começa com|Somente os valores que começam com os caracteres do operando serão válidos.|Operando de exemplo: AA<br /><br /> Valores válidos: AA1<br /><br /> Valores inválidos: 1AAB|  
|Valor termina com|Somente os valores que terminam com os caracteres do operando serão válidos.|Operando de exemplo: AA<br /><br /> Valores válidos: 1AA<br /><br /> Valores inválidos: 1AAB|  
|Valor é numérico|Somente os valores que têm um tipo de dados numérico do SQL Server serão válidos. Isso inclui int, decimal, float etc.|Operando de exemplo: N/A<br /><br /> Valores válidos: 1, 25, 345,1234<br /><br /> Valores inválidos: 2b, bcdef|  
|Valor é data/hora|Somente os valores que têm um tipo de dados de data/hora do SQL Server serão válidos. Isso inclui datetime, time, date etc.|Operando de exemplo: N/A<br /><br /> Valores válidos: 1916-06-04; 1916-06-04 18:24:24; March 21, 2001; 5/18/2011; 18:24:24<br /><br /> Valores inválidos: March 213, 2006|  
|Valor está em|Somente os valores que estão no conjunto do operando serão válidos.<br /><br /> Para inserir os valores no conjunto, clique na caixa de texto do operando, insira o primeiro valor, pressione Enter, insira o segundo valor, repita o procedimento para tantos valores quanto você deseja inserir no conjunto e clique novamente na caixa de texto do operando. O DQS adicionará uma vírgula entre os valores do conjunto. Se você inserir uma cadeia de caracteres com vírgulas e nenhum retorno de carro (por exemplo, "A1, B1"), o DQS considerará essa cadeia de caracteres um único valor no conjunto.|Operando de exemplo: [A1, B1]<br /><br /> Valores válidos: A1, B1<br /><br /> Valores inválidos: AA, 11|  
|Valor não está em|Somente os valores que não estão no conjunto do operando serão válidos.|Operando de exemplo: [A1, B1]<br /><br /> Valores válidos: AA, 11<br /><br /> Valores inválidos: A1, B1|  
|Padrão de correspondências de valor|Somente os valores que correspondem ao padrão de caracteres, dígitos ou caracteres especiais do operando serão válidos.<br /><br /> Algumas letras (A...Z) podem ser usadas como um padrão para qualquer letra, sem diferenciação entre maiúsculas e minúsculas. Qualquer dígito (0...9) pode ser usado como um padrão para qualquer dígito. Qualquer caractere especial, exceto uma letra ou um dígito, pode ser usado como um padrão para si mesmo. Os colchetes, [], definem correspondência opcional.|Operando de exemplo: AA:000 (um padrão de *quaisquer* dois caracteres seguidos de dois-pontos (:), seguidos novamente de *quaisquer* três dígitos.<br /><br /> Valores válidos: AB:012, df:257<br /><br /> Valores inválidos: abc:123, FJ-369<br /><br /> Para obter mais informações sobre as regras do padrão no DQS e exemplos, consulte [Correspondência de padrão nas regras de domínio do DQS](https://blogs.msdn.com/b/dqs/archive/2012/10/08/pattern-matching-in-dqs-domain-rules.aspx).|  
|Valor não corresponde ao padrão|Somente os valores que não correspondem ao padrão de caracteres, dígitos ou caracteres especiais do operando serão válidos.|Operando de exemplo: A1 (o valor não deve corresponder a um padrão de *qualquer* caractere seguido de *qualquer* dígito.)<br /><br /> Valores válidos: AB1, A, A:5<br /><br /> Valores inválidos: B7, c9|  
|Valor contém o padrão|Somente valores contendo o padrão de caracteres, dígitos ou caracteres especiais do operando serão válidos.|Operando de exemplo: AA-12 (o valor contém um padrão de *quaisquer* dois caracteres seguidos de um hífen (-), seguidos novamente de *quaisquer* dois dígitos.)<br /><br /> Valores válidos: AAA-01, ab-975<br /><br /> Valor inválido: A7, AA-6, C-45, aa;98|  
|Valor não contém o padrão|Somente os valores que não contêm o padrão de caracteres do operando serão válidos.|Operando de exemplo: AB-12 (o valor não deve conter um padrão de *quaisquer* dois caracteres seguidos de um hífen (-), seguidos novamente de *quaisquer* dois dígitos.)<br /><br /> Valores válidos: A7, AA-6, C-45, aa;98<br /><br /> Valor inválido: AAA-01, ab-975|  
|O valor corresponde à expressão regular|Somente os valores iguais à expressão regular no operando serão válidos.<br /><br /> Não inclua a âncora "^" ou "$" à expressão regular, porque o DQS adiciona automaticamente essas âncoras a uma cláusula que contém Valor é igual à expressão regular. (Como alternativa, você pode colocar a expressão regular contendo "^" e "$" âncoras com parênteses.) Para obter mais informações sobre expressões regulares, consulte [elementos de linguagem de expressão regular](https://go.microsoft.com/fwlink/?LinkId=225561).|Operando de exemplo: [1-5] + (cada caractere deve ser um dígito numérico de 1 a 5, ocorrendo uma ou mais vezes)<br /><br /> Valores válidos: 123, 12345, 14352<br /><br /> Valores inválidos: 456, ABC|  
|O valor não corresponde a uma expressão regular|Somente os valores que não correspondem à expressão regular no operando serão válidos.|Operando de exemplo: [1-5] + (a cadeia de caracteres não deve conter apenas dígitos numéricos de 1 a 5)<br /><br /> Valores válidos: 456, ABC<br /><br /> Valor inválido: 123, 123456, 14352|  
  
  

---
title: Importar domínios de um arquivo do Excel na descoberta de conhecimento | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.component: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4d3a3940-6c2a-4dc4-90eb-86f26012c165
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b7baab0db19dc5ec9a9b7833c0a03c6f62b3d2ea
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="import-domains-from-an-excel-file-in-knowledge-discovery"></a>Importar domínios de um arquivo do Excel na descoberta da base de dados de conhecimento

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Este tópico descreve como importar um ou mais domínios de um arquivo do Excel na atividade de descoberta da base de dados de conhecimento do [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). O processo de importação simplifica o processo de geração de conhecimento, economizando tempo e esforço. Isso permite que as pessoas que têm dados em um arquivo do Excel ou arquivo de texto criem uma base de dados de conhecimento com esses dados. (Consulte [Importar valores de um arquivo do Excel para um domínio](../data-quality-services/import-values-from-an-excel-file-into-a-domain.md) para obter mais informações sobre como importar valores para um domínio de uma base de dados de conhecimento existente.) Não há suporte para a exportação para um arquivo do Excel.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Para importar domínios de um arquivo do Excel, o Excel deve ser instalado no computador em que o [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] está instalado; você deve criar um arquivo do Excel com valores de domínio (consulte [How the import works](#How)); você deve criar e abrir uma base de dados de conhecimento para a qual o domínio será importado.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_administrator no banco de dados DQS_MAIN para importar domínios de um arquivo do Excel.  
  
##  <a name="Import"></a> Importar domínios de um arquivo do Excel para uma base de dados de conhecimento  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , siga um destes procedimentos:  
  
    -   Crie uma nova base de conhecimento para a qual os dados serão importados clicando em **Nova base de dados de conhecimento**, selecionando **Nenhum** para **Criar base de dados de conhecimento de**, selecionando a atividade **Descoberta de Conhecimento** e clicando em **Criar**.  
  
    -   Abra uma base de dados de conhecimento existente para a qual os dados serão importados clicando em **Abrir base de dados de conhecimento**, selecionando a base de dados de conhecimento, selecionando **Descoberta de Conhecimento**e clicando em **Avançar**.  
  
3.  Na página **Mapear** , selecione **Arquivo do Excel** em **Fonte de Dados**.  
  
4.  Clique em **Procurar** na linha **Arquivo do Excel** .  
  
5.  Na caixa de diálogo **Selecionar um Arquivo do Excel** , vá para a pasta que contém o arquivo do Excel do qual os dados serão importados, selecione o arquivo do Excel e clique em **Abrir**.  
  
6.  Na lista suspensa **Planilha** , selecione a planilha do arquivo do Excel a partir da qual será realizada a importação.  
  
7.  Selecione **Usar primeira linha como cabeçalho** se desejar que a primeira linha seja considerada um cabeçalho de dados, e se desejar que os valores da primeira linha sejam usados como nomes de coluna. Anule a seleção de **Usar primeira linha como cabeçalho** se desejar que a primeira linha seja considerada um valor de dados; nesse caso, o DQS usará os nomes de cabeçalho do Excel (letras alfabéticas) para a coluna.  
  
8.  Selecione uma coluna e mapeie um domínio existente para a coluna ou crie um novo domínio clicando no ícone **Criar um Domínio** , criando um domínio na caixa de diálogo **Criar um domínio** e mapeando o domínio para a coluna. O tipo de dados do domínio de corresponder ao tipo de dados da coluna. Repita isso para todas as colunas da planilha.  
  
9. Clique em **Avançar**.  
  
10. Na página **Descobrir** , clique em **Iniciar** para analisar os dados na planilha do Excel.  
  
    > [!NOTE]  
    >  Se você sair da página antes que os dados sejam carregados, o processo de carregamento de arquivo será encerrado.  
  
11. Verifique se a análise foi concluída com êxito e clique em **Avançar**.  
  
12. Na página **Gerenciar Valores de Domínio** , verifique se os domínios corretos são listados na lista **Domínios** e se os valores são inseridos na tabela de domínio.  
  
13. Clique em **Concluir**e em **Publicar** para publicar a base de dados de conhecimento ou clique em **Não** para não publicar.  
  
14. Verifique se a base de dados de conhecimento foi publicada e clique em **OK**.  
  
##  <a name="FollowUp"></a> Acompanhamento: Após importar domínios de um arquivo do Excel  
 Depois que você importar domínios de um arquivo do Excel, poderá adicionar conhecimento aos domínios ou usar os domínios em um projeto de limpeza ou de correspondência, dependendo do conteúdo dos domínios. Para obter mais informações, consulte [Executar a descoberta de conhecimento](../data-quality-services/perform-knowledge-discovery.md), [Gerenciando um domínio](../data-quality-services/managing-a-domain.md), [Gerenciando um domínio de composição](../data-quality-services/managing-a-composite-domain.md), [Criar uma política de conciliação](../data-quality-services/create-a-matching-policy.md), [Limpeza de dados](../data-quality-services/data-cleansing.md) ou [Correspondência de dados](../data-quality-services/data-matching.md).  
  
##  <a name="How"></a> How the import works  
 Na operação de importação, o DQS interpreta um arquivo do Excel, da seguinte maneira:  
  
-   Uma coluna representa um domínio  
  
-   Uma linha representa um registro de dados  
  
-   A primeira linha representa nomes de domínio ou é o primeiro valor de dados ou registro, dependendo da configuração da caixa de seleção **Usar primeira linha como cabeçalho** .  
  
 As regras a seguir se aplicam à operação de importação:  
  
-   Essa operação importa valores de domínio para uma base de dados de conhecimento. Ela não importa regras de domínio ou uma política de correspondência.  
  
-   O arquivo do Excel pode ter a extensão .xlsx, .xls ou .csv. O Microsoft Excel deve ser instalado no computador do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] para importar valores de domínio ou um domínio completo. Há suporte para as versões 2003 e posteriores do Excel. Se a versão de 64 bits do Excel for usada, haverá suporte somente para arquivos do Excel 2003; não haverá suporte para os arquivos do Excel 2007 ou 2010.  
  
-   Não há suporte para arquivos do Excel do tipo .xlsx em uma instalação de 64 bits do Excel. Se você estiver usando o Excel de 64 bits, salve o arquivo de planilha como um arquivo .xls.  
  
-   Nos arquivos .xlsx e .xls, o tipo de dados da coluna é determinado pelo tipo de dados mais frequente nas oito primeiras linhas. Se uma célula para não estiver em conformidade com esse tipo de dados, ela receberá um valor nulo.  
  
-   Nos arquivos .csv, o tipo de dados é determinado pelo tipo de dados mais frequente nas oito primeiras linhas.  
  
-   Um valor em uma planilha do Excel que não esteja em conformidade com uma regra de domínio será importado como um valor inválido.  
  
-   Se o arquivo do Excel não estiver no formato certo ou estiver danificado, a operação de importação resultará em um erro.  
  
  

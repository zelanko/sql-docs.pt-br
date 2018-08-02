---
title: Importar valores de um arquivo do Excel para um domínio | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.importfailing.f1
- sql13.dqs.kb.importselect.f1
- sql13.dqs.kb.failingvalues.f1
ms.assetid: 04cde693-2043-477f-8417-fcc463ca7195
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b2c08d8310e399a6b48e53f5e53ced3734f9af54
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35310765"
---
# <a name="import-values-from-an-excel-file-into-a-domain"></a>Importar valores de um arquivo do Excel para um domínio

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Este tópico descreve como importar valores de um arquivo do Excel para um domínio no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). O uso de um arquivo do Excel para importar valores de domínio para o aplicativo [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] simplifica o processo de geração de conhecimento, economizando tempo e esforço. Isso permite que as pessoas que têm uma lista de valores de dados válidos em um arquivo do Excel ou um arquivo de texto importem esses valores para um domínio. De um arquivo do Excel, você pode importar valores de domínio para um ou vários domínios em uma base de dados de conhecimento. (Consulte [Importar domínios de um arquivo do Excel na descoberta de conhecimento](../data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md) para obter mais informações sobre como importar domínios para uma base de dados de conhecimento.) Não há suporte para a exportação para um arquivo do Excel.  
  
 Você pode importar valores de dados de duas maneiras:  
  
-   Crie um novo domínio e importe valores de um arquivo do Excel para ele; nesse caso, todos os valores são adicionados ao domínio.  
  
-   Importe valores para um domínio existente e populado; nesse caso, somente os novos valores são importados. Todos os valores que já existem não serão importados.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Para importar domínios de um arquivo do Excel, o Excel deve ser instalado no computador em que o aplicativo [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] está instalado para que os valores de domínio ou um domínio completo sejam importados; você deve criar um arquivo do Excel com valores de domínio (consulte [How the import works](#How)); você deve criar e abrir uma base de dados de conhecimento para a qual o domínio será importado.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_administrator no banco de dados DQS_MAIN para importar valores de domínio de um arquivo do Excel.  
  
##  <a name="Import"></a> Importar valores de um arquivo do Excel para um domínio  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , abra uma base de dados de conhecimento na atividade Gerenciamento de Domínio.  
  
3.  Se estiver adicionando valores a um novo domínio, crie um novo domínio através do ícone **Criar um Domínio** e selecione o novo domínio na lista de domínios.  
  
4.  Se estiver adicionando valores a um domínio existente, selecione o domínio na lista de domínios.  
  
5.  Clique na guia **Valores do Domínio** , clique no ícone **Importar Valores** na barra de ícones e clique em **Importar valores válidos do Excel**.  
  
6.  Na caixa de diálogo **Importar Valores de Domínio** , clique em **Procurar**.  
  
7.  Na caixa de diálogo **Selecionar arquivo** , vá para a pasta que contém o arquivo do Excel do qual serão importados valores de domínio, selecione o arquivo (que tem a extensão .xlsx, .xls ou .csv) e clique em **Abrir**. O arquivo deve estar no cliente no qual você executa o DQS ou em um arquivo de compartilhamento ao qual o usuário tem acesso.  
  
8.  Na lista suspensa **Planilha** , selecione a planilha a partir da qual está realizando a importação.  
  
9. Selecione **Usar primeira linha como cabeçalho** se a primeira linha da planilha representar o nome do domínio e todas as outras linhas representarem valores de domínio válidos.  
  
10. Clique em **OK**. Uma barra de progresso é exibida, com uma indicação de quantos valores foram importados com êxito, quantos valores não foram importados e o número total de valores. Clique no botão **Cancelar** para cancelar o processo.  
  
11. Verifique se “Importação concluída” é exibido na caixa de diálogo **Importar Valores de Domínio** . Nesta caixa de diálogo, veja quais valores foram importados com êxito e quais não foram. Ela indica o nome e o caminho do arquivo, o status de conclusão da operação, quantos valores foram importados com êxito, quantos valores não foram importados e o número total de valores processados.  
  
12. Para os valores que não foram importados com êxito, clique em **Log** para exibir a caixa de diálogo **Importar Valores de Domínio – Valores com Falha** para saber por que a operação de importação falhou. A coluna **Valor com Falha** mostra os valores que não puderam ser importados de um arquivo do Excel para um domínio, e a coluna **Razão** explica por que a importação falhou. Clique em **Copiar para a área de transferência** para copiar a tabela **Valor com Falha** para a área de transferência, a partir da qual você poderá copiá-la para outro programa, como uma planilha do Excel ou um arquivo do Bloco de Notas. Clique em **OK** para fechar a caixa de diálogo **Valores com Falha** .  
  
13. Clique em **OK** para concluir a operação de importação e fechar a caixa de diálogo. Quando a importação for concluída com êxito, a lista de valores de domínio da página **Valores de Domínio** é atualizada e incluirá os novos valores importados. O filtro é alterado para **Todos Valores** , e **Mostrar Somente Novo** é selecionado. Quando **Mostrar Somente Novo** é selecionado depois da operação de importação, somente os valores importados do arquivo do Excel são exibidos.  
  
14. Clique em **Concluir** para adicionar os valores à base de dados de conhecimento.  
  
##  <a name="FollowUp"></a> Acompanhamento: Após importar valores de um arquivo do Excel para um domínio  
 Depois que você importar valores para um domínio, poderá executar outras tarefas de gerenciamento de domínio, executar a descoberta da base de dados de conhecimento para adicionar conhecimento ao domínio ou adicionar uma política de correspondência ao domínio. Para obter mais informações, consulte [Executar a descoberta de conhecimento](../data-quality-services/perform-knowledge-discovery.md), [Gerenciando um domínio](../data-quality-services/managing-a-domain.md) ou [Criar uma política de conciliação](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="Synonyms"></a> Importando sinônimos  
 Os sinônimos são importados da seguinte maneira:  
  
-   Primeiro, todos os valores são importados; depois, a conexão de sinônimo é estabelecida.  
  
-   Se for impossível conectar valores de sinônimo, um erro aparecerá na tela de log. É possível que os valores principais e os sinônimos do arquivo sejam importados para o domínio, mas não sejam definidos como sinônimos.  
  
 As seguintes condições se aplicam ao processo de definição de conexões de sinônimo:  
  
-   Se o valor principal no arquivo do Excel já existir no domínio como sinônimo de um valor diferente, você precisará definir os sinônimos manualmente (por exemplo, no arquivo do Excel, desejamos que o valor A seja o valor principal do valor B, mas, no domínio, o valor A aparece como sinônimo do valor C). Além de definir sinônimos manualmente depois que a importação for concluída, você também poderá desvincular valores que estão nos sinônimos presentes (por exemplo, desvincule os valores A e C) e importar o arquivo.  
  
-   Se o sinônimo já for conectado a um valor principal diferente, você terá que definir os sinônimos manualmente.  
  
-   Se os valores não puderem ser conectados manualmente no aplicativo por algum motivo, isso não será aplicável através da operação de importação.  
  
##  <a name="How"></a> How the import works  
 Os seguintes valores são importados por esta operação:  
  
 Na operação de importação, o DQS realiza a importação a partir de um arquivo do Excel, da seguinte maneira:  
  
-   Os valores corretos e novos são importados. Se houver um ou mais valores de domínio importados, eles não serão importados.  
  
-   Um valor que contradiz uma regra de domínio será importado como um valor inválido.  
  
-   Um valor não será importado do arquivo se o valor não for do tipo de dados do domínio ou for nulo.  
  
-   Os valores são importados na ordem em que aparecem no arquivo.  
  
-   Cada linha representa um valor de domínio.  
  
-   A primeira linha representa nomes de domínio ou é o primeiro valor de dados ou registro, dependendo da configuração da caixa de seleção **Usar primeira linha como cabeçalho** . Se você selecionar **Usar primeira linha como cabeçalho** ao usar um arquivo .xslx ou .xls, qualquer nome de coluna nulo será convertido automaticamente em F*n*e qualquer duplicada terá um número acrescentado a eles.  
  
-   Se você cancelar a operação de importação antes de concluí-la, a operação será revertida e nenhum dado será importado.  
  
-   Os valores da primeira coluna são importados para o domínio. Se, além da primeira coluna, uma ou mais colunas adicionais forem populadas, os valores dessas colunas serão adicionados como sinônimos (consulte [Importando sinônimos](#Synonyms)).  
  
    -   O formato esperado é que a primeira coluna será os valores principais, enquanto a segunda coluna e acima serão sinônimos.  
  
    -   Você pode importar vários sinônimos da mesma linha ou de linhas diferentes. Por exemplo, se você deseja importar “CNI” e “Cidade de Nova Iorque” como sinônimos para “Nova Iorque”, importe uma única linha com “Nova Iorque” na coluna 1, “CNI” na coluna 2, e “Cidade de Nova Iorque” na coluna 3; ou você pode importar uma linha com “Nova Iorque” na coluna 1 e “CNI” na coluna 2, e outra linha com “Nova Iorque” na coluna 1 e “Cidade de Nova Iorque” na coluna 2. Observe que, se o valor “Nova Iorque” já existir no domínio, somente os sinônimos serão adicionados, e o usuário não receberá um erro durante o processo de importação informando que o valor já existe. Se o primeiro valor ainda não existir, ele será adicionado ao domínio.  
  
 As regras a seguir se aplicam ao arquivo do Excel que está sendo usado para a importação:  
  
-   O arquivo do Excel pode ter a extensão .xlsx, .xls ou .csv. O Microsoft Excel deve ser instalado no computador em que o aplicativo [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] está instalado para importar valores de domínio ou um domínio completo. Há suporte para as versões 2003 e posteriores do Excel. Se a versão de 64 bits do Excel for usada, haverá suporte somente para arquivos do Excel 2003; não haverá suporte para os arquivos do Excel 2007 ou 2010.  
  
-   Não há suporte para arquivos do Excel do tipo .xlsx em uma instalação de 64 bits do Excel. Se você estiver usando o Excel de 64 bits, salve o arquivo de planilha como um arquivo .xls ou .csv, ou instale uma versão de 32 bits do Excel.  
  
-   Nos arquivos .xlsx e .xls, o tipo de dados da coluna é determinado pelas oito primeiras linhas. Se o tipo de dados de coluna das oito primeiras linhas for misto, o tipo de coluna será cadeia de caracteres. Se uma célula para a linha 9 e superior não estiver em conformidade com esse tipo de dados, ela receberá um valor nulo.  
  
-   Nos arquivos .csv, o tipo de dados é determinado pelo tipo de dados mais frequente nas oito primeiras linhas.  
  
-   Se o arquivo do Excel não estiver no formato certo ou estiver danificado, a operação de importação resultará em um erro.  
  
  

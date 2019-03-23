---
title: Origem do Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.excelsource.f1
helpviewer_keywords:
- Excel [Integration Services]
- sources [Integration Services], Excel
ms.assetid: e66349f3-b1b8-4763-89b7-7803541a4d62
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: eb7800a18e8df28848d775746bab6d90f75d7439
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58390924"
---
# <a name="excel-source"></a>Origem do Excel
  A origem do Excel extrai dados de planilhas ou intervalos em pastas de trabalho do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel.  
  
 A origem do Excel fornece quatro modos de acesso a dados diferentes para extrair dados:  
  
-   Uma tabela ou exibição.  
  
-   Uma tabela ou exibição especificada em uma variável.  
  
-   Os resultados de uma instrução SQL. A consulta pode ser uma consulta parametrizada.  
  
-   Os resultados de uma instrução SQL armazenados em uma variável.  
  
> [!IMPORTANT]  
>  No Excel, uma planilha de trabalho ou intervalo é equivalente a uma tabela ou exibição. A lista de tabelas disponíveis nos Editores de Origem e Destino do Excel exibe planilhas de trabalho existentes (identificadas pelo sinal $ anexado ao nome da planilha, por exemplo, Planilha1$) e os intervalos nomeados (identificados pela ausência desse sinal $, como Meu Intervalo). Para obter mais informações, consulte a seção de Considerações de uso.  
  
 A origem do Excel usa um gerenciador de conexões do Excel para se conectar a uma fonte de dados e o gerenciador de conexões especifica o arquivo da planilha de trabalho a ser usado. Para obter mais informações, consulte [Excel Connection Manager](../connection-manager/excel-connection-manager.md).  
  
 A origem do Excel tem uma saída comum e uma saída de erro.  
  
## <a name="usage-considerations"></a>Considerações de uso  
 O Gerenciador de Conexões do Excel usa o Provedor [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB para Jet 4.0 e driver ISAM do Excel com suporte para se conectar, além de ler e gravar dados nas fontes de dados do Excel.  
  
 Muitos artigos da Base de Dados de Conhecimento da [!INCLUDE[msCoName](../../includes/msconame-md.md)] documentam o comportamento desse provedor e driver e, embora esses artigos não sejam específicos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ou de seus serviços de transformação de dados anteriores, talvez você queira obter mais informações sobre determinados comportamentos que podem levar a resultados inesperados. Para obter informações gerais sobre o uso e o comportamento do driver do Excel, consulte [HOWTO: Usar o ADO com dados do Excel do Visual Basic ou VBA](https://support.microsoft.com/kb/257819).  
  
 Os seguintes comportamentos do provedor Jet com o driver do Excel podem levar a resultados inesperados ao ler dados de uma fonte de dados do Excel.  
  
-   **Fontes de dados**. A fonte de dados em uma pasta de trabalho do Excel pode ser uma planilha de trabalho, à qual o sinal $ deve ser anexado (por exemplo, Planilha1$), ou um intervalo nomeado (por exemplo, MeuIntervalo). Em uma instrução SQL, o nome de uma planilha de trabalho deve ser delimitado (por exemplo, [Planilha1$]) para evitar um erro de sintaxe causado pelo sinal $. O Construtor de Consultas adiciona automaticamente esses delimitadores. Quando você especifica uma planilha de trabalho ou um intervalo, o driver lê o bloco contínuo de células começando com a primeira célula não vazia no canto superior esquerdo da planilha de trabalho ou do intervalo. Dessa forma, você não pode ter linhas vazias nos dados de origem ou uma linha vazia entre o título ou as linhas de cabeçalho e de dados.  
  
-   **Valores ausentes**. O driver do Excel lê um determinado número de linhas (por padrão, 8 linhas) na fonte especificada para determinar o tipo de dados de cada coluna. Quando uma coluna parece conter tipos de dados mistos, especialmente dados numéricos combinados com dados de texto, o driver decide em favor do tipo de dados majoritário e retorna valores nulos para as células que contêm dados de outro tipo. (Em uma ligação, o tipo numérico vence.) A maioria das opções de formatação de células na planilha de trabalho do Excel não parece afetar a determinação desse tipo de dados. Você pode modificar esse comportamento de driver do Excel especificando Modo de Importação. Para especificar o modo de importação, adicione `IMEX=1` como o valor de propriedades estendidas na cadeia de conexão do Gerenciador de conexão do Excel na **propriedades** janela. Para obter mais informações, consulte [PRB: Valores retornados como nulos usando DAO OpenRecordset do Excel](https://support.microsoft.com/kb/194124).  
  
-   **Texto truncado**. Quando o driver determina que uma coluna do Excel contém dados de texto, ele seleciona o tipo de dados (cadeia ou memorando) com base no valor mais longo que ele obtém. Se o driver não descobre nenhum valor maior que 255 caracteres nas linhas que ele verifica, ele trata a coluna como uma coluna de cadeia de 255 caracteres, não como uma coluna de memorando. Assim, valores com mais de 255 caracteres podem estar truncados. Para importar dados de uma coluna de memorando sem que haja truncamento, você deve certificar-se de que essa coluna, em pelo menos uma das linhas de amostra, contenha um valor com mais 255 caracteres ou deve aumentar o número de linhas de amostra pelo driver para incluir esse tipo de linha. Você pode aumentar o número de linhas de amostra aumentando o valor de **TypeGuessRows** na chave do Registro **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Jet\4.0\Engines\Excel** . Para obter mais informações, consulte [PRB: Transferência de dados de origem do Jet 4.0 OLEDB falha com erro](https://support.microsoft.com/kb/281517).  
  
-   **Tipos de dados**. O driver do Excel reconhece apenas um conjunto limitado de tipos de dados. Por exemplo, todas as colunas numéricas são interpretadas como duplas (DT_R8) e todas as colunas de cadeia de caracteres (que não sejam colunas de memorando) são interpretadas como cadeias Unicode de 255 caracteres (DT_WSTR). [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mapeia os tipos de dados do Excel da seguinte maneira:  
  
    -   Numérico – flutuante de precisão dupla (DT_R8)  
  
    -   Moeda – moeda (DT_CY)  
  
    -   Booliano – booliano (DT_BOOL)  
  
    -   Data/hora - `datetime` (DT_DATE)  
  
    -   Cadeia de caracteres – cadeia Unicode, 255 de comprimento (DT_WSTR)  
  
    -   Memorando – fluxo de texto Unicode (DT_NTEXT)  
  
-   **Conversões de tipo e comprimento de dados**. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não converte tipos de dados implicitamente. Como resultado, você pode precisar usar as transformações Coluna Derivada ou Conversão de Dados para converter explicitamente dados do Excel antes de carregá-los em um destino que não seja Excel ou para converter dados que não sejam do Excel antes de carregá-los em um destino Excel. Nesse caso, pode ser útil criar o pacote inicial usando o Assistente de Importação e Exportação, que configura as conversões necessárias. Alguns exemplos de conversões que podem ser necessárias incluem:  
  
    -   Conversão entre colunas de cadeias Unicode e não Unicode do Excel com páginas de código específicas  
  
    -   Conversão entre colunas de cadeias de 255 caracteres e de comprimentos diferentes do Excel  
  
    -   Conversão entre colunas numéricas de precisão dupla e de outros tipos de colunas numéricas do Excel  
  
## <a name="excel-source-configuration"></a>Configuração da origem do Excel  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Origem do Excel** clique em um dos seguintes tópicos:  
  
-   [Editor de Origem do Excel &#40;Página Gerenciador de Conexões&#41;](../excel-source-editor-connection-manager-page.md)  
  
-   [Editor de Fonte do Excel &#40;Página Colunas&#41;](../excel-source-editor-columns-page.md)  
  
-   [Editor de Origem do Excel &#40;Página Saída de Erro&#41;](../excel-source-editor-error-output-page.md)  
  
 A caixa de diálogo **Editor Avançado** reflete todas as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../common-properties.md)  
  
-   [Propriedades personalizadas do Excel](excel-custom-properties.md)  
  
 Para obter informações sobre loop através de um grupo de arquivos do Excel, consulte [Loop por meio de arquivos do Excel e tabelas usando um contêiner de Loop Foreach](../control-flow/foreach-loop-container.md).  
  
## <a name="related-tasks"></a>Related Tasks  

-   [Importar dados do Excel ou exportar dados para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md)

-   [Mapear parâmetros de consulta para variáveis em um componente de fluxo de dados](map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [Definir as propriedades de um componente de fluxo de dados](set-the-properties-of-a-data-flow-component.md)  
  
-   [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
-   [Loop por meio de arquivos do Excel e tabelas usando um contêiner de Loop Foreach](../control-flow/foreach-loop-container.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Entrada de blog, [Importando dados do Excel de 64 bits no SSIS](https://go.microsoft.com/fwlink/?LinkId=217673), em hrvoje.piasevoli.com  
  
-   Entrada de blog, [Excel no Integration Services, parte 1 de 3: Conexões e componentes](https://go.microsoft.com/fwlink/?LinkId=217674), em dougbert.com  
  
-   Entrada de blog, [Excel no Integration Services, parte 2 de 3: Tipos de dados e tabelas](https://go.microsoft.com/fwlink/?LinkId=217675), em dougbert.com.  
  
-   Entrada de blog, [Excel no Integration Services, parte 3 de 3: Problemas e alternativas](https://go.microsoft.com/fwlink/?LinkId=217676), em dougbert.com.  
  
-   Entrada de blog [usando arquivos XLSX no SSIS](https://go.microsoft.com/fwlink/?LinkId=233704), no site sqlservergeeks.com.  
  
  

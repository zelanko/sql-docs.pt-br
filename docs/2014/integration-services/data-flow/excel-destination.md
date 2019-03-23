---
title: Destino do Excel | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.exceldest.f1
helpviewer_keywords:
- destinations [Integration Services], Excel
- Excel [Integration Services]
ms.assetid: 37c07446-1264-4814-b4f5-9c66d333bb24
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 84647752eb549bd5d3607637d679e58356597a6b
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58387464"
---
# <a name="excel-destination"></a>Destino do Excel
  O destino do Excel carrega dados em planilhas ou intervalos em pastas de trabalho do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel.  
  
## <a name="access-modes"></a>Modos de acesso  
 O destino do Excel fornece três modos de acesso diferentes para carregar dados:  
  
-   Uma tabela ou exibição.  
  
-   Uma tabela ou exibição especificada em uma variável.  
  
-   Os resultados de uma instrução SQL. A consulta pode ser uma consulta parametrizada.  
  
> [!IMPORTANT]  
>  No Excel, uma planilha de trabalho ou intervalo é equivalente a uma tabela ou exibição. As listas de tabelas disponíveis nos Editores de Origem e Destino do Excel exibem somente planilhas existentes (identificadas pelo sinal $ anexado ao nome da planilha, por exemplo, Planilha1$) e os intervalos nomeados (identificados pela ausência desse sinal $, como MyRange).  
  
## <a name="usage-considerations"></a>Considerações de uso  
 O Gerenciador de Conexões do Excel usa o Provedor [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB para Jet 4.0 e driver ISAM do Excel com suporte para se conectar, além de ler e gravar dados nas fontes de dados do Excel.  
  
 Muitos artigos da Base de Dados de Conhecimento da [!INCLUDE[msCoName](../../includes/msconame-md.md)] documentam o comportamento desse provedor e driver e, embora esses artigos não sejam específicos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ou de seus serviços de transformação de dados anteriores, talvez você queira obter mais informações sobre determinados comportamentos que podem levar a resultados inesperados. Para obter informações gerais sobre o uso e o comportamento do driver do Excel, consulte [HOWTO: Usar o ADO com dados do Excel do Visual Basic ou VBA](https://support.microsoft.com/kb/257819).  
  
 Os seguintes comportamentos do provedor Jet que está incluído no driver do Excel podem levar a resultados inesperados ao salvar dados em um destino do Excel.  
  
-   **Salvando dados de texto**. Quando o driver do Excel salva valores de dados de texto em um destino do Excel, o driver coloca aspas simples (') antes do texto de cada célula para garantir que os valores salvos serão interpretados como texto. Se você tem ou desenvolve outros aplicativos que leem ou processam os dados salvos, será necessário incluir um tratamento especial para as aspas simples que precedem cada texto.  
  
     Para obter informações sobre como evitar incluir aspas simples, consulte esta postagem no blog, [Aspas simples são acrescentadas a todas as cadeias de caracteres quando os dados são transformados para Excel ao usar o componente de fluxo de dados de destino do Excel no pacote SSIS](https://go.microsoft.com/fwlink/?LinkId=400876), no msdn.com.  
  
-   **Salvando dados de memorando (ntext)**. Antes de salvar com sucesso cadeias de caracteres com mais de 255 caracteres em uma coluna do Excel, o driver deve reconhecer o tipo de dados da coluna de destino como **memorando** e não como **cadeia de caracteres**. Se a tabela de destino já contém linhas de dados, então as primeiras linhas que serão amostradas pelo driver devem conter pelo menos uma instância com um valor maior que 255 caracteres na coluna de memorando. Se a tabela de destino for criada durante o desenvolvimento de pacote ou em tempo de execução, a instrução CREATE TABLE deve usar LONGTEXT (ou um de seus sinônimos) como o tipo de dados da coluna de memorando.  
  
-   **Tipos de dados**. O driver do Excel reconhece apenas um conjunto limitado de tipos de dados. Por exemplo, todas as colunas numéricas são interpretadas como duplas (DT_R8) e todas as colunas de cadeia de caracteres (que não sejam colunas de memorando) são interpretadas como cadeias Unicode de 255 caracteres (DT_WSTR). [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mapeia os tipos de dados do Excel da seguinte maneira:  
  
    -   Numérico    flutuante de precisão dupla (DT_R8)  
  
    -   Moeda     moeda (DT_CY)  
  
    -   Booliano     booliano (DT_BOOL)  
  
    -   Data/hora `datetime` (DT_DATE)  
  
    -   Cadeia de caracteres     cadeia de caracteres Unicode com 255 caracteres (DT_WSTR)  
  
    -   Memorando     fluxo de texto Unicode (DT_NTEXT)  
  
-   **Conversões de tipo e comprimento de dados**. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não converte tipos de dados implicitamente. Como resultado, talvez seja necessário usar as transformações Coluna Derivada ou Conversão de Dados para converter explicitamente os dados do Excel antes de carregá-los em um destino que não seja Excel ou para converter dados que não sejam do Excel antes de carregá-los em um destino do Excel. Nesse caso, pode ser útil criar o pacote inicial usando o Assistente de Importação e Exportação, que configura as conversões necessárias. Alguns exemplos de conversões que podem ser necessárias incluem:  
  
    -   Conversão entre colunas de cadeia de caracteres Unicode e não Unicode do Excel com páginas de código específicas.  
  
    -   Conversão entre colunas de cadeia de 255 caracteres e de comprimentos diferentes do Excel.  
  
    -   Conversão entre colunas numéricas de precisão dupla e outros tipos de colunas numéricas do Excel.  
  
## <a name="configuration-of-the-excel-destination"></a>Configuração do destino do Excel  
 O destino do Excel usa um gerenciador de conexões do Excel para se conectar a uma fonte de dados e o gerenciador de conexões especifica o arquivo de pasta de trabalho a ser usado. Para obter mais informações, consulte [Excel Connection Manager](../connection-manager/excel-connection-manager.md).  
  
 O destino do Excel tem uma entrada regular e uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Destinos do Excel** , clique em um dos seguintes tópicos:  
  
-   [Editor de Destinos do Excel &#40;Página Gerenciador de Conexões&#41;](../excel-destination-editor-connection-manager-page.md)  
  
-   [Editor de Destinos do Excel &#40;página Mapeamentos&#41;](../excel-destination-editor-mappings-page.md)  
  
-   [Editor de Destinos do Excel &#40;Página Saída de Erro&#41;](../excel-destination-editor-error-output-page.md)  
  
 A caixa de diálogo **Editor Avançado** reflete todas as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../common-properties.md)  
  
-   [Propriedades personalizadas do Excel](excel-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Importar dados do Excel ou exportar dados para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md)  
  
-   [Loop através de arquivos e tabelas do Excel por meio de um contêiner do Loop Foreach](../control-flow/foreach-loop-container.md)  
  
-   [Definir as propriedades de um componente de fluxo de dados](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Entrada de blog, [Excel no Integration Services, parte 1 de 3: Conexões e componentes](https://go.microsoft.com/fwlink/?LinkId=217674), em dougbert.com  
  
-   Entrada de blog, [Excel no Integration Services, parte 2 de 3: Tipos de dados e tabelas](https://go.microsoft.com/fwlink/?LinkId=217675), em dougbert.com.  
  
-   Entrada de blog, [Excel no Integration Services, parte 3 de 3: Problemas e alternativas](https://go.microsoft.com/fwlink/?LinkId=217676), em dougbert.com.  
  
## <a name="see-also"></a>Consulte também  
 [Origem do Excel](excel-source.md)   
 [Variáveis do SSIS &#40;Integration Services&#41;](../integration-services-ssis-variables.md)   
 [Fluxo de Dados](data-flow.md)   
 [Trabalhar com arquivos do Excel com a tarefa Script](../extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
  
  

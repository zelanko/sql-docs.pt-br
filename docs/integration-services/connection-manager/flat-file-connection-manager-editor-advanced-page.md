---
title: "Editor do Gerenciador de Conex&#245;es de Arquivos Simples (p&#225;gina Avan&#231;ado) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.ffileconnection.columnproperties.f1"
helpviewer_keywords: 
  - "Editor do Gerenciador de Conexões de Arquivos Simples"
ms.assetid: 58aa3dee-4774-4e0b-a956-96d199be4c3a
caps.latest.revision: 36
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 36
---
# Editor do Gerenciador de Conex&#245;es de Arquivos Simples (p&#225;gina Avan&#231;ado)
  Use a página **Avançado** da caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos Simples** para definir propriedades que especificam como o Integration Services lê e grava dados em arquivos simples. Você pode alterar os nomes das colunas no arquivo simples e definir propriedades que incluem tipo de dados e delimitadores em cada coluna no arquivo.  
  
 Por padrão, o tamanho da coluna de cadeia de caracteres é de 50 caracteres. Você pode redimensionar o tamanho dessas colunas para prevenir truncamento de dados ou excesso de largura nas colunas. Também é possível atualizar outros metadados para habilitar a compatibilidade com as colunas de destino. Por exemplo, você pode alterar o tipo de dados de uma coluna que contém apenas dados inteiros para um tipo de dados numérico, como DT_I2. Você pode fazer essas modificações manualmente ou clicar no botão **Selecionar Tipos** para usar a caixa de diálogo **Sugerir Tipos de Coluna** para avaliar dados de amostra e tornar automáticas algumas dessas alterações.  
  
 Para obter mais informações sobre o gerenciador de conexões de Arquivo Simples, consulte [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
## Opções  
 **Nome do gerenciador de conexões**  
 Forneça um nome exclusivo para o gerenciador de conexões de arquivo simples no fluxo de trabalho. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Description**  
 Descreva o gerenciador de conexões. Como prática recomendável, descreva o gerenciador de conexões em termos de objetivo, para tornar os pacotes autodocumentados e mais fáceis de manter.  
  
 **Configurar as propriedades de cada coluna**  
 Selecione uma coluna no painel esquerdo para exibir suas propriedades no painel direito. Consulte a tabela a seguir para obter uma descrição das propriedades dos tipos de dados. Algumas das propriedades listadas são configuráveis apenas para alguns formatos de arquivo simples.  
  
|Propriedade|Description|  
|--------------|-----------------|  
|**ColumnType**|Denota se a coluna é delimitada, de largura fixa ou com imperfeição à direita. Esta propriedade é somente leitura. Arquivos irregulares à direita são arquivos em que toda coluna tem uma largura fixa, à exceção da última coluna. Ela é delimitada pelo delimitador de linha.|  
|**OutputColumnWidth**|Especifique um valor a ser armazenado como contagem de bytes; para arquivos Unicode, esse valor corresponde a uma contagem de caracteres. Na tarefa Fluxo de Dados, esse valor é usado para definir a largura de coluna de saída para a fonte de Arquivo Simples. No modelo de objeto, o nome desta propriedade é MaximumWidth.|  
|**DataType**|Seleciona na lista de tipos de dados disponíveis. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**TextQualified**|Indique se os dados de texto são delimitados por caracteres qualificadores de texto, como aspas.<br /><br /> True: os dados de texto no arquivo simples são qualificados. False: os dados de texto no arquivo simples NÃO são qualificados.|  
|**Nome**|Forneça um nome de coluna descritivo. Se você não digitar um nome, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] criará um nome automaticamente, no formato Coluna 0, Coluna 1 e assim por diante.|  
|**DataScale**|Especifica a escala de dados numéricos. A escala se refere ao número de casas decimais. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**ColumnDelimiter**|Seleciona na lista de delimitadores de coluna disponíveis. Escolha delimitadores com pouca probabilidade de ocorrer no texto. Esse valor é ignorado para colunas de largura fixa.<br /><br /> **{CR}{LF}**. As colunas são delimitadas por uma combinação de retorno de carro e alimentação de linha.<br /><br /> **{CR}**. As colunas são delimitadas por um retorno de carro.<br /><br /> **{LF}**. As colunas são delimitadas por uma alimentação de linha.<br /><br /> **Porto e vírgula {;}**. As colunas são delimitadas por um ponto-e-vírgula.<br /><br /> **Dois pontos {:}**. As colunas são delimitadas por dois-pontos.<br /><br /> **Vírgula {,}**. As colunas são delimitadas por uma vírgula.<br /><br /> **Tabulação {t}**. As colunas são delimitadas por uma tabulação.<br /><br /> **Barra vertical {&#124;}**. As colunas são delimitadas por uma barra vertical.|  
|**DataPrecision**|Especifica a precisão de dados numéricos. A precisão se refere ao número de dígitos. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**InputColumnWidth**|Especifica um valor a ser armazenado como contagem de bytes; no caso de arquivos Unicode, isso será exibido como contagem de caracteres. Este valor é ignorado nas colunas delimitadas.<br /><br /> **Observação** No modelo de objeto, o nome desta propriedade é ColumnWidth.|  
  
 **Nova**  
 Adicione uma nova coluna, clicando em **Nova**. Por padrão, o botão **Nova** adiciona uma nova coluna ao final da lista. O botão também tem as opções a seguir, disponíveis na lista suspensa.  
  
|Value|Description|  
|-----------|-----------------|  
|**Adicionar Coluna**|Adiciona uma nova coluna fim da lista.|  
|**Insert Before**|Insere uma nova coluna antes da coluna selecionada.|  
|**Insert After**|Insere uma nova coluna depois da coluna selecionada.|  
  
 **Delete (excluir)**  
 Selecione uma coluna e remova-a, clicando em **Excluir**.  
  
 **Sugerir Tipos**  
 Use a caixa de diálogo **Sugerir Tipos de Coluna** para avaliar dados de amostra no arquivo e obter sugestões de tipo de dados e tamanho de cada coluna. Para obter mais informações, consulte [Referência da interface do usuário da caixa de diálogo Sugerir Tipos de Coluna](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md).  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Geral&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)   
 [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Colunas&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)   
 [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Visualização&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)  
  
  
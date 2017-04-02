---
title: "Revisar mapeamento de tipo de dados (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.reviewissues.f1"
ms.assetid: 0625c4f9-b8ff-4593-b884-39398b9d43af
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# Revisar mapeamento de tipo de dados (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server)
Se você especificou um mapeamento de tipo de dados que pode não ter êxito na lista **Mapeamentos** da caixa de diálogo **Mapeamentos de coluna**, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostra a página **Revisar mapeamento de tipo de dados**. Nesta página, examine as informações detalhadas sobre conversões de tipo de dados que o assistente precisa executar para tornar os dados de origem compatíveis com o destino. As informações incluem dicas visuais para fazer distinção entre conversões que se espera sejam bem sucedidas de conversões que podem causar erros ou truncamentos. Para cada conversão, decida se deseja aceitar a conversão sugerida pelo assistente e especifique como manipular qualquer eventual erro que possa surgir.   
  
Para obter informações sobre como o assistente mapeia tipos de dados das colunas de origem para as de destino, consulte [Como o assistente mapeia tipos de dados entre a origem e o destino?](Import%20and%20Export%20Data%20with%20the%20SQL%20Server%20Import%20and%20Export%20Wizard.md\#wizardMapping).

> [!TIP] Não é possível alterar os mapeamentos de tipo de dados na página **Revisar mapeamento de tipo de dados**. No entanto, você pode clicar em **Voltar** para retornar para a página **Selecionar tabelas de origem e exibições** e, em seguida, clique em **Editar mapeamentos** para abrir a caixa de diálogo **Mapeamentos de coluna** novamente. Na caixa de diálogo **Mapeamentos de coluna**, você pode especificar mapeamentos de tipo de dados que têm mais probabilidade de êxito. Para ver a caixa de diálogo **Mapeamentos de coluna**, consulte [Mapeamentos de coluna](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  
  
## <a name="screen-shot-of-the-review-data-type-mapping-page"></a>Captura de tela da página Revisar Mapeamento de Tipo de Dados
 A captura de tela a seguir mostra a página **Revisar mapeamento de tipo de dados** do Assistente depois de o usuário especificar um mapeamento que pode não ter êxito na caixa de diálogo **Mapeamentos de coluna**.
 
 Neste exemplo:
 -   O ícone de aviso na linha da lista **Tabela** indica que há um problema convertendo pelo menos uma coluna de dados dos resultados da consulta em um tipo de dados compatíveis na tabela de destino.
 -   O ícone de aviso na primeira coluna da lista **Mapeamento de tipo de dados** indica que o mapeamento do tipo de dados **int** da coluna de origem para o tipo de dados **smalldatetime** da coluna de destino pode causar perda de dados.
 
 ![Review Data Type Mapping page of the Import and Export Wizard](../../integration-services/import-export-data/media/review-mapping.png "Review Data Type Mapping page of the Import and Export Wizard") 
 
## <a name="review-the-source-and-destination-tables"></a>Examinar as tabelas de origem e de destino  
 A seção superior da página **Revisar Mapeamento de Tipo de Dados** é uma lista **Tabela** que lista as tabelas a serem copiadas da fonte para o destino. Para ver informações de conversão sobre uma tabela individual, selecione uma tabela na lista **Tabela**. As informações de conversão das colunas da tabela selecionada são exibidas na grade **Mapeamento de tipo de dados** localizada na parte inferior da página.
 
![Examinar mapeamento – tabelas](../../integration-services/import-export-data/media/review-mapping-tables.png)
  
 A tabela a seguir descreve as colunas na lista **Tabela**.  
  
|Coluna|Description|  
|------------|-----------------|  
|Ícone da fonte|Indica a probabilidade de sucesso para as conversões de tipo de dados:<br /> –   Um ícone de sinal de verificação **verde** indica que o assistente espera que todas as conversões de tipo de dados da tabela sejam bem sucedidas.<br />–   Um ícone de aviso **amarelo** indica que você deveria examinar as conversões individuais que o assistente executará. Para revisar essas conversões, selecione a tabela e revise as conversões das colunas individuais na lista **Mapeamento de tipo de dados** .<br />–   Um ícone de erro **vermelho** indica que o assistente não pode executar algumas das conversões da tabela de maneira segura.|  
|**Origem**|O nome da tabela de origem.|  
|Ícone de destino|Indica se o destino já existe ou será criado pelo assistente:<br /> –   Um ícone de tabela indica que o destino é uma tabela existente.<br />–   Um ícone de tabela com um clarão de sol indica que o destino é uma tabela nova que será criada pelo assistente.|  
|**Destino**|O nome da tabela de destino.|  
  
## <a name="review-the-data-type-mappings-from-source-to-destination"></a>Examinar os mapeamentos de tipo de dados da origem ao destino  
 A seção do meio da página **Revisar Mapeamento de Tipo de Dados** é a lista **Mapeamento de tipo de dados**. Esta grade fornece informações detalhadas de conversão sobre as colunas na tabela selecionada na lista **Tabela** .
 
![Examinar mapeamento – mapeamentos](../../integration-services/import-export-data/media/review-mapping-mappings.png)  

A tabela a seguir descreve as colunas da lista **Mapeamento de tipo de dados**. 

|Coluna|Description|  
|------------|-----------------|  
|Ícone de conversão|Indica a probabilidade de sucesso para as conversões de tipo de dados:<br /> –   Um ícone de sinal de verificação **verde** indica que o assistente espera que a conversão de tipo de dados da coluna sejam bem sucedida.<br />–   Um ícone de aviso **amarelo** indica que você deveria examinar a conversão que o assistente executará. Para examinar a conversão, clique duas vezes na coluna para exibir a caixa de diálogo **Detalhes da Conversão de Coluna**. Para obter mais informações, consulte [Caixa de diálogo Detalhes da Conversão de Coluna](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md).<br />–   Um ícone de erro **vermelho** indica que o assistente não pode executar a conversão de maneira segura.|  
|**Coluna de Origem**|O nome da coluna de origem.|  
|**Tipo de Origem**|O tipo de dados da coluna de origem.|  
|**Coluna de Destino**|O nome da coluna de destino.|  
|**Tipo de Destino**|O tipo de dados da coluna de destino.|  
|**Converter**|Especifique se deseja continuar com a conversão planejada:<br /> –   Marque a caixa de seleção para que o assistente continue com a conversão planejada.<br />–   Desmarque a caixa de seleção para cancelar a conversão de tipo de dados.|  
|**Se Houver Erro**|Especifique como o assistente lida com erros:<br /> –   Use a configuração **Se houver erro (global)**, que você pode especificar na parte inferior desta página.<br />–   Falha com um erro, e interrompe o processo de importação ou exportação.<br />–   Ignore o erro.|  
|**Se Houver Truncamento**|Especifique como o assistente controla truncamentos:<br /> –   Use a configuração **Se houver truncamento (global)**, que você pode especificar na parte inferior desta página.<br />–   Falha com um erro, e interrompe o processo de importação ou exportação<br />–   Ignore o truncamento.|  

> [!TIP] Para ver informações detalhadas sobre a conversão de uma coluna particular de dados, clique duas vezes em qualquer linha na lista. A caixa de diálogo **Detalhes da Conversão de Coluna** abre e exibe informações de conversão mais detalhadas da coluna. Para obter mais informações, consulte [Caixa de diálogo Detalhes da Conversão de Coluna](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md).
 
## <a name="specify-global-error-handling-options"></a>Especificar as opções globais de tratamento de erro  
 A seção inferior da página **Revisar mapeamento de tipo de dados** permite que você especifique opções de tratamento de erro aplicáveis por padrão a todas as colunas. Essas configurações são aplicáveis a todas as conversões com **Usar Global** selecionado nas colunas **Se Houver Erro** ou **Se Houver Truncamento** da lista **Mapeamento de tipo de dados**.   
 
![Examinar mapeamento – erros](../../integration-services/import-export-data/media/review-mapping-errors.png)

 **Se Houver Erro (global)**  
 Especifique como o assistente lida com erros:  
 -   Falha com um erro, e interrompe o processo de importação ou exportação.  
 -   Ignore o erro e continue o processo de importação ou exportação.  
  
 **Se Houver Truncamento (global)**  
 Especifique como o assistente controla truncamentos de dados:  
 -   Falha com um erro, e interrompe o processo de importação ou exportação.  
 -   Ignore o truncamento e continue o processo de importação ou exportação.  
   
## <a name="whats-next"></a>O que vem a seguir?  
 Depois de examinar os avisos, especifique opções de conversão e como tratar erros. A página **Revisar mapeamento de tipo de dados** leva você de volta para a caixa de diálogo **Mapeamentos de coluna**. Para obter mais informações, consulte [Mapeamentos de coluna](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  

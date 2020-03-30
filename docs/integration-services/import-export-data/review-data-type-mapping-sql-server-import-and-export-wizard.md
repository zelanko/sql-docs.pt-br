---
title: Examinar Mapeamento de Tipo de Dados (Assistente para Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.reviewissues.f1
ms.assetid: 0625c4f9-b8ff-4593-b884-39398b9d43af
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f0bd7fe34b1945c3f0f2255e256ead38a6d15e3a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71296262"
---
# <a name="review-data-type-mapping-sql-server-import-and-export-wizard"></a>Revisar mapeamento de tipo de dados (Assistente de Importação e Exportação do SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Se você especificou um mapeamento de tipo de dados que pode não ter êxito na lista **Mapeamentos** da caixa de diálogo **Mapeamentos de coluna** , o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostra a página **Revisar mapeamento de tipo de dados** . Nesta página, examine as informações detalhadas sobre conversões de tipo de dados que o assistente precisa executar para tornar os dados de origem compatíveis com o destino. Essas informações incluem dicas visuais para fazer distinção entre conversões de tipo de dados que se espera que sejam bem-sucedidas de conversões que podem causar erros ou truncamentos. Para cada conversão, decida se deseja aceitar a conversão sugerida pelo assistente e especifique como manipular qualquer eventual erro que possa surgir.   
  
> [!TIP]
> Não é possível alterar os mapeamentos de tipo de dados na página **Revisar mapeamento de tipo de dados** . No entanto, você pode clicar em **Voltar** para retornar para a página **Selecionar tabelas de origem e exibições** e, em seguida, clique em **Editar mapeamentos** para abrir a caixa de diálogo **Mapeamentos de coluna** novamente. Na caixa de diálogo **Mapeamentos de coluna** , você pode especificar mapeamentos de tipo de dados que têm mais probabilidade de êxito. Para ver a caixa de diálogo **Mapeamentos de coluna** , consulte [Mapeamentos de coluna](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  
  
## <a name="screen-shot-of-the-review-data-type-mapping-page"></a>Captura de tela da página Revisar Mapeamento de Tipo de Dados
 A captura de tela a seguir mostra um exemplo da página **Examinar Mapeamento de Tipo de Dados** do assistente.
 
 Neste exemplo:
 -   O usuário especificou um mapeamento na caixa de diálogo **Mapeamentos de Coluna** que pode não ter êxito.
 -   O ícone de aviso na linha da lista **Tabela** indica que há um problema convertendo pelo menos uma coluna de dados dos resultados da consulta em um tipo de dados compatíveis na tabela de destino.
 -   O ícone de aviso na primeira linha da lista **Mapeamento de tipo de dados** indica que o mapeamento do tipo de dados **int** da coluna de origem para o tipo de dados **smalldatetime** da coluna de destino pode causar perda de dados.
 
 ![Página Examinar Mapeamento de Tipo de Dados do Assistente de Importação e Exportação](../../integration-services/import-export-data/media/review-mapping.png "Página Examinar Mapeamento de Tipo de Dados do Assistente de Importação e Exportação") 
 
## <a name="review-the-source-and-destination-tables"></a>Examinar as tabelas de origem e de destino  
 A seção superior da página **Revisar Mapeamento de Tipo de Dados** é uma lista **Tabela** que lista as tabelas a serem copiadas da fonte para o destino. Para ver informações de conversão sobre uma tabela individual, selecione uma tabela na lista **Tabela** . As informações de conversão das colunas individuais da tabela selecionada são exibidas na parte inferior da página na grade **Mapeamento de tipo de dados**.

Neste exemplo, os resultados da consulta que o usuário forneceu serão copiados para a tabela Sales.CustomerNew2 no destino. O ícone de aviso indica que há um problema ao converter pelo menos uma coluna de dados dos resultados da consulta em um tipo de dados compatíveis na tabela de destino.

![Examinar mapeamento – tabelas](../../integration-services/import-export-data/media/review-mapping-tables.png)
  
 A tabela a seguir descreve as colunas na lista **Tabela** .  
  
|Coluna|DESCRIÇÃO|  
|------------|-----------------|  
|(Ícone de origem)|Indica a probabilidade de sucesso para as conversões de tipo de dados:<br /> –   Um ícone de sinal de verificação **verde** indica que o assistente espera que todas as conversões de tipo de dados da tabela sejam bem sucedidas.<br />–   Um ícone de aviso **amarelo** indica que você deveria examinar as conversões individuais que o assistente executará. Para revisar essas conversões, selecione a tabela e revise as conversões das colunas individuais na lista **Mapeamento de tipo de dados** .<br />–   Um ícone de erro **vermelho** indica que o assistente não pode executar algumas das conversões da tabela de maneira segura.|  
|**Origem**|O nome da tabela de origem.|  
|(Ícone de destino)|Indica se o destino já existe ou será criado pelo assistente:<br /> –   Um ícone de tabela indica que o destino é uma tabela existente.<br />–   Um ícone de tabela com um clarão de sol indica que o destino é uma tabela nova que será criada pelo assistente.|  
|**Destino**|O nome da tabela de destino.|  
  
## <a name="review-the-data-type-mappings"></a>Examinar os mapeamentos de tipo de dados  
 A seção do meio da página **Revisar Mapeamento de Tipo de Dados** é a lista **Mapeamento de tipo de dados** . Esta grade fornece informações detalhadas de conversão sobre as colunas na tabela de origem selecionada na lista **Tabela** na parte superior da página.

Neste exemplo, cada coluna na origem será copiada para uma coluna com o mesmo nome e tipo de dados no destino. O ícone de aviso na primeira linha da lista **Mapeamento de tipo de dados** indica que o mapeamento do tipo de dados **int** da coluna de origem para o tipo de dados **smalldatetime** da coluna de destino pode causar perda de dados.
 
![Examinar mapeamento – mapeamentos](../../integration-services/import-export-data/media/review-mapping-mappings.png)  

A tabela a seguir descreve as colunas da lista **Mapeamento de tipo de dados** . 

|Coluna|DESCRIÇÃO|  
|------------|-----------------|  
|(Ícone de conversão)|Indica a probabilidade de sucesso para as conversões de tipo de dados:<br /> –   Um ícone de sinal de verificação **verde** indica que o assistente espera que a conversão de tipo de dados da coluna sejam bem sucedida.<br />–   Um ícone de aviso **amarelo** indica que você deveria examinar a conversão que o assistente executará. Para examinar a conversão, clique duas vezes na coluna para exibir a caixa de diálogo **Detalhes da Conversão de Coluna** . Para obter mais informações, consulte [Caixa de diálogo Detalhes da Conversão de Coluna](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md).<br />–   Um ícone de erro **vermelho** indica que o assistente não pode executar a conversão de maneira segura.|  
|**Coluna de Origem**|O nome da coluna de origem.|  
|**Tipo de Origem**|O tipo de dados da coluna de origem.|  
|**Coluna de Destino**|O nome da coluna de destino.|  
|**Tipo de Destino**|O tipo de dados da coluna de destino.|  
|**Converter**|Especifique se deseja continuar com a conversão planejada:<br /> –   Marque a caixa de seleção para que o assistente continue com a conversão planejada.<br />–   Desmarque a caixa de seleção para cancelar a conversão de tipo de dados.|  
|**Se Houver Erro**|Especifique como o assistente lida com erros:<br /> –   Use a configuração **Se houver erro (global)** , que você pode especificar na parte inferior desta página.<br />–   Falha com um erro, e interrompe o processo de importação ou exportação.<br />–   Ignore o erro.|  
|**Se Houver Truncamento**|Especifique como o assistente controla truncamentos:<br /> –   Use a configuração **Se houver truncamento (global)** , que você pode especificar na parte inferior desta página.<br />–   Falha com um erro, e interrompe o processo de importação ou exportação<br />–   Ignore o truncamento.|  

> [!TIP]
> Para ver informações detalhadas sobre a conversão de uma coluna particular de dados, clique duas vezes em qualquer linha na lista. A caixa de diálogo **Detalhes da Conversão de Coluna** abre e exibe informações de conversão mais detalhadas da coluna. Para obter mais informações, consulte [Caixa de diálogo Detalhes da Conversão de Coluna](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md).
 
## <a name="specify-global-error-handling-options"></a>Especificar as opções globais de tratamento de erro  
 A seção inferior da página **Revisar mapeamento de tipo de dados** permite que você especifique opções de tratamento de erro aplicáveis por padrão a todas as colunas. Essas configurações são aplicáveis a todas as conversões com **Usar Global** selecionado nas colunas **Se Houver Erro** ou **Se Houver Truncamento** da lista **Mapeamento de tipo de dados** .   

Este exemplo mostra os valores padrão para as duas opções de tratamento de erro global.

![Examinar mapeamento – erros](../../integration-services/import-export-data/media/review-mapping-errors.png)

 **Se Houver Erro (global)**  
 Especifique como o assistente lida com erros:  
 -   Falha com um erro, e interrompe o processo de importação ou exportação. Esse é o valor padrão.
 -   Ignore o erro e continue o processo de importação ou exportação.  
  
 **Se Houver Truncamento (global)**  
 Especifique como o assistente controla truncamentos de dados:  
 -   Falha com um erro, e interrompe o processo de importação ou exportação. Esse é o valor padrão.
 -   Ignore o truncamento e continue o processo de importação ou exportação.  
   
## <a name="whats-next"></a>O que vem a seguir?  
 Depois de examinar os avisos, especifique opções de conversão e como tratar erros. A página **Revisar mapeamento de tipo de dados** leva você de volta para a caixa de diálogo **Mapeamentos de coluna** . Para obter mais informações, consulte [Mapeamentos de coluna](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  
 
 ## <a name="see-also"></a>Confira também
[Mapeamento de Tipo de Dados no Assistente para Importação e Exportação do SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)


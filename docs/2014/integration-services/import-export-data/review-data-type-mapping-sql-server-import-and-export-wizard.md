---
title: Examinar Mapeamento de Tipo de Dados (Assistente para Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.reviewissues.f1
ms.assetid: 0625c4f9-b8ff-4593-b884-39398b9d43af
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 108256e1d8a3638da5cd676a0ee57894b3ee874c
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966196"
---
# <a name="review-data-type-mapping-sql-server-import-and-export-wizard"></a>Revisar mapeamento de tipo de dados (Assistente de Importação e Exportação do SQL Server)
  Use a página **examinar mapeamento de tipo de dados** para examinar informações detalhadas sobre conversões de tipo de dados que o assistente precisa executar para tornar os dados de origem compatíveis com o destino. As informações incluem dicas visuais para fazer distinção entre conversões que se espera sejam bem sucedidas de conversões que podem causar erros ou truncamentos. Para cada conversão, é possível decidir se deseja aceitar a conversão sugerida pelo assistente, além de especificar como manipular qualquer eventual erro.  
  
 Para obter mais informações sobre este assistente, consulte [Assistente de Importação e Exportação do SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para saber mais sobre as opções de inicialização do assistente e sobre as permissões necessárias para executar o assistente com êxito, consulte [executar o assistente de importação e exportação do SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 O objetivo do Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é copiar dados de uma origem para um destino. O assistente também pode criar um banco de dados de destino e tabelas de destino para você. No entanto, se for necessário copiar vários bancos de dados ou tabelas, ou outros tipos de objetos de banco de dados, será necessário usar o Assistente para Copiar Banco de Dados. Para obter mais informações, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opções  
 A página **Revisar Mapeamento de Tipo de Dados** consiste de uma lista **Tabela** , uma lista de **Mapeamento de tipo de dados** e opções de tratamento de erros.  
  
### <a name="table-list"></a>Lista Tabela  
 A parte superior da página **examinar problemas de tipo de dados** é **uma lista de tabelas que** lista as tabelas a serem transferidas da origem para o destino. A tabela a seguir descreve as colunas nessa lista.  
  
|Coluna|Descrição|  
|------------|-----------------|  
|Ícone da fonte|Indica a probabilidade de sucesso para as conversões de tipo de dados:<br /><br /> Um ícone de sinal de verificação, verde, indica que o assistente espera que todas as conversões de tipo de dados da tabela sejam bem sucedidas.<br /><br /> Um ícone de advertência, amarelo, indica que você deveria revisar as conversões individuais que o assistente executará. Para revisar essas conversões, selecione a tabela e revise as conversões das colunas individuais na lista **Mapeamento de tipo de dados** .<br /><br /> Um ícone de erro, vermelho, indica que o assistente não pode executar algumas das conversões da tabela de maneira segura.|  
|**Origem**|Exibe o nome da tabela de origem.|  
|Ícone de destino|Indica se o destino já existe ou será criado pelo assistente:<br /><br /> Um ícone de tabela indica que o destino é uma tabela existente.<br /><br /> Um ícone de tabela com um clarão de sol indica que o destino é uma tabela nova que será criada pelo assistente.|  
|**Destino**|Exibe o nome da tabela de destino.|  
  
 Para exibir informações de conversão sobre uma tabela individual, selecione uma tabela nesta grade de **tabela** . As informações de conversão da tabela selecionada são exibidas nas colunas na grade **Mapeamento de tipo de dados** localizada na parte inferior da página.  
  
### <a name="data-type-mapping-list"></a>Lista Mapeamento de tipo de dados  
 A parte inferior da página **examinar problemas de tipo de dados** é a lista **mapeamento de tipo de dados** . Esta grade fornece informações detalhadas de conversão sobre as colunas na tabela selecionada na lista **Tabela** . A tabela a seguir descreve as colunas nessa lista.  
  
|Coluna|Descrição|  
|------------|-----------------|  
|Ícone de conversão|Indica a probabilidade de sucesso para as conversões de tipo de dados:<br /><br /> Um ícone de sinal de verificação, verde,  indica que o assistente espera que a conversão de tipo de dados da coluna sejam bem sucedida.<br /><br /> Um ícone de advertência, amarelo, indica que você deveria revisar a conversão que o assistente executará. Para examinar a conversão, clique duas vezes na coluna para exibir a caixa de diálogo **Detalhes da Conversão de Coluna** .<br /><br /> Um ícone de erro, vermelho, indica que o assistente não pode executar a conversão de maneira segura.|  
|**Coluna de Origem**|Exibe o nome da coluna de origem.|  
|**Tipo de origem**|Exibe o tipo de dados da coluna de origem.|  
|**Coluna de destino**|Exibe o nome da coluna de destino.|  
|**Tipo de destino**|Exibe o tipo de dados da coluna de destino.|  
|**Vertê**|Especifique se a conversão planejada deve prosseguir:<br /><br /> Marque a caixa de seleção para que o assistente continue com a conversão planejada.<br /><br /> Desmarque a caixa de seleção para cancelar a conversão de tipo de dados.|  
|**Se houver erro**|Especifique como o assistente lida com erros:<br /><br /> Use a configuração se houver **erro (global)** .<br /><br /> Falha com um erro, e interrompe o processo de importação ou exportação.<br /><br /> Ignore o erro.|  
|**Se Houver Truncamento**|Especifique como o assistente controla truncamentos:<br /><br /> Use a configuração **em truncamento (global)** .<br /><br /> Falha com um erro e interrompe o processo de importação ou exportação<br /><br /> Ignore o truncamento.|  
  
 Para exibir informações detalhadas sobre a conversão de uma coluna particular de dados, clique duas vezes em qualquer linha na lista. A caixa de diálogo **Detalhes da Conversão de Coluna** abre e exibe informações de conversão mais detalhadas da coluna.  
  
### <a name="error-handling-options"></a>Opções de tratamento de erros  
 **Se Houver Erro (global)**  
 Especifique como o assistente lida com erros:  
  
-   Falha com um erro, e interrompe o processo de importação ou exportação.  
  
-   Ignore o erro e continue o processo de importação ou exportação.  
  
 Esta configuração é aplicável a todas as conversões com **Usar Global** selecionado na coluna **Se Houver Erro** da lista **Mapeamento de tipo de dados** .  
  
 **Se Houver Truncamento (global)**  
 Especifique como o assistente controla truncamentos:  
  
-   Falha com um erro, e interrompe o processo de importação ou exportação.  
  
-   Ignore o truncamento e continue o processo de importação ou exportação.  
  
 Esta configuração é aplicável a todas as conversões com **Usar Global** selecionado na coluna **Se Houver Truncamento** da lista **Mapeamento de tipo de dados** .  
  
  

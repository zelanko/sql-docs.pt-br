---
description: Mapeamentos de coluna (Assistente de Importação e Exportação do SQL Server)
title: Mapeamentos de coluna (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.columnmapandtransform.f1
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9b74aaec705f3de493f105218adedffb173090ac
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484118"
---
# <a name="column-mappings-sql-server-import-and-export-wizard"></a>Mapeamentos de coluna (Assistente de Importação e Exportação do SQL Server)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Depois de selecionar as tabelas existentes e exibições para copiar ou examinar a consulta que você forneceu, ao clicar em **Editar mapeamentos**, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostra a caixa de diálogo **Mapeamentos de Colunas** . Nesta página você especifica e configura colunas de destino para receber os dados copiados das colunas de origem. Geralmente, você não precisa alterar nada nesta página.
  
Se não desejar copiar todas as colunas na tabela selecionada, uma coisa que você pode fazer nesta página é excluir as colunas que não deseja. Selecione **ignorar** na coluna **Destino** da lista **Mapeamentos** para as colunas que você não deseja copiar.
 
## <a name="screen-shot-of-the-column-mappings-page"></a>Captura de tela da página Mapeamentos de Colunas 
 A captura de tela a seguir mostra um exemplo da caixa de diálogo **Mapeamentos de Coluna** do assistente. 
 
 Neste exemplo, você verá que o assistente vai criar uma nova tabela de destino, porque a opção **Criar tabela de destino** está selecionada. Por padrão, o assistente dá a cada coluna na nova tabela de destino tem o mesmo nome, tipo de dados e propriedades que os da coluna de origem correspondente. 
  
 ![Página Mapeamentos de coluna do Assistente de Importação e Exportação](../../integration-services/import-export-data/media/column-mappings.png "Página Mapeamentos de coluna do Assistente de Importação e Exportação")  
  
## <a name="review-the-source-and-destination"></a>Examinar as tabelas de origem e de destino 
![Página de mapeamentos de coluna, seção origem e destino](../../integration-services/import-export-data/media/column-mappings-page-source-and-destination-section.png)

 **Origem**  
 A tabela, exibição ou consulta de origem selecionada.  
  
 **Destino**  
 A tabela ou a exibição de destino selecionada.  

## <a name="optionally-create-a-new-destination-table"></a>Opcionalmente, criar uma nova tabela de destino
![Página de mapeamentos de coluna, seção nova tabela](../../integration-services/import-export-data/media/column-mappings-page-new-table-section.png)

 **Criar tabela/arquivo de destino**  
 Crie a tabela de destino se ela ainda não existir.    
  
 **Editar SQL**  
Clique em **Editar SQL** para abrir a caixa de diálogo **Instrução Criar Tabela SQL** . Use a instrução CREATE TABLE gerada automaticamente ou modifique-a para seus propósitos. Se você alterar essa instrução manualmente, precisará verificar se a lista de mapeamentos de coluna reconhece as alterações. Para obter mais informações, consulte [Instrução Criar Tabela SQL](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md).  

### <a name="sometimes-these-options-are-disabled"></a>Às vezes, essas opções são desabilitadas
A opção **Criar tabela/arquivo de destino** e o botão **Editar SQL** são automaticamente habilitados ou desabilitados.

-   **Habilitado.** Se você tiver especificado uma **nova** tabela de destino na página **Selecionar Tabelas e Exibições de Origem**, a opção **Criar tabela de destino** será selecionada automaticamente e o botão **Editar SQL** será habilitado.

-   **Desabilitado.** Se você tiver selecionado uma tabela de destino **existente** na página **Selecionar Tabelas e Exibições de Origem**, a opção **Criar tabela de destino** e o botão **Editar SQL** serão desabilitados. Se você desejar criar uma nova tabela de destino, volte para a página **Selecionar tabelas e exibições de origem** e digite o nome de uma **nova** tabela na coluna **Destino**.  

## <a name="what-about-existing-data-in-the-destination"></a>E quanto aos dados existentes no destino?
![Página de mapeamentos de coluna, seção opções](../../integration-services/import-export-data/media/column-mappings-page-options-section.png)

 **Excluir linhas na tabela/arquivo de destino**  
 Especifique se deseja limpar os dados de uma tabela existente antes de carregar os novos dados.  
  
 **Acrescentar linhas à tabela/arquivo de destino**  
 Especifique se deseja acrescentar os dados novos aos dados já presentes em uma tabela existente.  
  
 **Ignorar e recriar tabela de destino**  
 Escolha esta opção para substituir a tabela de destino. Esta opção só está disponível ao usar o assistente para criar a tabela de destino. A tabela de destino será ignorada e recriada somente se o pacote criado pelo assistente for salvo e executado novamente. Essa é uma opção conveniente quando você deseja testar suas configurações mais de uma vez.
  
 **Habilitar inserção de identidade**  
 Escolha esta opção para permitir que valores de identidade existentes nos dados de origem sejam inseridos em uma coluna de identidade na tabela de destino. Por padrão, a coluna de identidade de destino geralmente não permite isto.  
  
> [!TIP]
> Se suas chaves primárias existentes estiverem em uma coluna de identidade, uma coluna autonumber ou equivalente, normalmente você precisará selecionar esta opção para manter os valores de chave primária existentes.  Caso contrário, a coluna de identidade de destino normalmente atribui novos valores.  

## <a name="keep-your-autonumber-or-identity-values"></a>Manter os valores de identidade ou de numeração automática
Se você estiver exportando dados que tenham uma coluna de numeração automática ou uma coluna de identidade (por exemplo, se você estiver exportando do Microsoft Access), verifique se a opção **Habilitar inserção de identidade** foi selecionada, conforme descrito logo acima.

## <a name="review-column-mappings"></a>Examinar mapeamentos de coluna
![Página de mapeamentos de coluna, seção mapeamentos](../../integration-services/import-export-data/media/column-mappings-page-mappings-section.png)

 **Mapeamentos**  
 Exibe como cada coluna na fonte de dados mapeia para uma coluna no destino.
 
A lista **Mapeamentos** tem as colunas a seguir.  
  
-    **Origem**  
     Exiba cada coluna de origem.  
  
-   **Destino**  
    Exiba a coluna de destino mapeada ou selecione uma coluna diferente.
    
    Você não precisa copiar todas as colunas da tabela de origem. Selecione **ignorar** nesta coluna para as colunas que você deseja ignorar. Antes de mapear colunas, é necessário ignorar todas as colunas que não serão mapeadas.  
  
-   **Tipo**  
    Exiba o tipo de dados da coluna de destino ou selecione um tipo de dados diferente.
  
-   **Permite valor nulo**  
    Especifique se a coluna de destino permite um valor nulo.  
  
-   **Tamanho**  
    Especifique o número de caracteres da coluna de destino, se aplicável.  
  
-    **Precisão**  
    Especifique a precisão dos dados numéricos na coluna de destino, ou seja, o número de dígitos, se aplicável.  
  
 -   **Escala**  
    Especifique a escala dos dados numéricos na coluna de destino, ou seja, o número de casas decimais, se aplicável.  
  
## <a name="whats-next"></a>O que vem a seguir?  
 Depois de examinar e configurar colunas de destino para receber os dados copiados das colunas de origem e clicar em **OK**, a caixa de diálogo **Mapeamentos de Coluna** retornará a página **Selecionar tabelas e exibições de origem** ou a página **Configurar destino do arquivo simples**. Para obter mais informações, consulte [Selecionar tabelas e exibições de origem](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) ou [Configurar destino do arquivo simples](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).  
  
 Se tiver especificado um mapeamento que pode não ter êxito na lista **Mapeamentos** , a caixa de diálogo **Mapeamentos de Coluna** levará você para a página **Revisar mapeamento de tipo de dados** . Nessa página, você deve examinar os avisos, especificar as opções de conversão e também definir como tratar os erros. Para obter mais informações, consulte [Revisar mapeamento de tipo de dados](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).  
 
 ## <a name="see-also"></a>Confira também
[Mapeamento de Tipo de Dados no Assistente para Importação e Exportação do SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)  
[Começar com esse exemplo simples de Assistente de Importação e Exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


---
title: "Mapeamentos de coluna (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server) | Microsoft Docs"
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
  - "sql13.dts.impexpwizard.columnmapandtransform.f1"
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
caps.latest.revision: 69
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 58
---
# Mapeamentos de coluna (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server)
  Depois de selecionar as tabelas existentes e exibições para copiar ou examinar a consulta que você forneceu, ao clicar em **Editar mapeamentos**, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostra a caixa de diálogo **Mapeamentos de Colunas**. Nesta página você especifica e configura colunas de destino para receber os dados copiados.  
 
## <a name="screen-shot-of-the-column-mappings-page"></a>Captura de tela da página Mapeamentos de Colunas 
 A captura de tela a seguir mostra a caixa de diálogo **Mapeamentos de Coluna** do assistente. 
 
 Neste exemplo, você verá que o assistente vai criar uma nova tabela de destino, porque a opção **Criar tabela de destino** está selecionada. Por padrão, cada coluna na nova tabela de destino tem o mesmo nome, tipo de dados e propriedades da coluna de origem correspondente. 
  
 ![Column mappings page of the Import and Export Wizard](../../integration-services/import-export-data/media/column-mappings.png "Column mappings page of the Import and Export Wizard")  
  
## <a name="confirm-the-source-and-destination"></a>Confirmar a origem e o destino  
 **Origem**  
 Identifica a tabela, exibição ou consulta de origem selecionada.  
  
 **Destino**  
 Identifica a tabela ou a exibição de destino selecionada.  

## <a name="create-a-new-destination-table"></a>Criar uma nova tabela de destino
 **Criar tabela/arquivo de destino**  
 Crie a tabela de destino se ela ainda não existir.    
  
 **Editar SQL**  
Clique em **Editar SQL** para abrir a caixa de diálogo **Instrução Criar Tabela SQL**. Use a instrução CREATE TABLE padrão ou modifique-a para seus propósitos. Se você alterar essa instrução manualmente, precisará verificar se a lista de mapeamentos de coluna reconhece as alterações. Para obter mais informações, consulte [Instrução Criar Tabela SQL](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md).  
  
 > [!TIP] Se você tiver especificado uma nova tabela de destino na página **Selecionar Tabelas e Exibições de Origem**, a opção **Criar tabela de destino** será selecionada automaticamente e o botão **Editar SQL** estará habilitado. Caso contrário, se você desejar criar a tabela de destino, é necessário voltar para a página **Selecionar tabelas e exibições de origem** e insira o nome de uma **nova** tabela na coluna **Destino**.
>
> Se a opção **Criar tabela de destino** e o botão **Editar SQL** estiverem desabilitados na página **Mapeamentos de Coluna**, volte para a página **Selecionar tabelas e exibições de origem** e digite o nome de uma **nova** tabela na coluna **Destino**. Depois de especificar uma nova tabela ou tabelas de destino e clicar em na página **Avançar**, a opção **Criar tabela de destino** estará selecionada automaticamente e o botão **Editar SQL** estará habilitado na página **Mapeamentos de Coluna**. Selecione **Editar SQL** para mostrar a caixa de diálogo **Instrução Criar Tabela SQL**.  

## <a name="specify-options-for-existing-data-in-the-destination"></a>Especificar opções para os dados existentes no destino
 **Excluir linhas na tabela/arquivo de destino**  
 Especifique se deseja limpar os dados de uma tabela existente antes de carregar os novos dados.  
  
 **Acrescentar linhas à tabela/arquivo de destino**  
 Especifique se deseja acrescentar os dados novos aos dados já presentes em uma tabela existente.  
  
 **Ignorar e recriar tabela de destino**  
 Escolha esta opção para substituir a tabela de destino. Esta opção só está disponível ao usar o assistente para criar a tabela de destino. A tabela de destino será ignorada e recriada somente se o pacote criado pelo assistente for salvo e executado novamente. Essa é uma opção conveniente quando você deseja testar suas configurações mais de uma vez.
  
 **Habilitar inserção de identidade**  
 Escolha esta opção para permitir que valores de identidade existentes nos dados de origem sejam inseridos em uma coluna de identidade na tabela de destino. Por padrão, a coluna de identidade de destino geralmente não permite isto.  
  
> [!TIP] Se suas chaves primárias existentes estiverem em uma coluna de identidade, uma coluna autonumber ou equivalente, normalmente você precisará selecionar esta opção para manter os valores de chave primária existentes.  Caso contrário, a coluna de identidade de destino normalmente atribui novos valores.  

## <a name="review-column-mappings-and-destination-data-types"></a>Examinar os mapeamentos de colunas e os tipos de dados de destino 
 **Mapeamentos**  
 Exibe como cada coluna na fonte de dados mapeia para uma coluna no destino.
 
 Selecione **ignorar** na coluna **Destino** para as colunas que você não deseja copiar. Você não precisa copiar todas as colunas em uma tabela.  
 
 ![Mapeamentos de coluna – mapeamentos](../../integration-services/import-export-data/media/column-mappings-mappings.png)
  
 A lista **Mapeamentos** tem as colunas a seguir.  
  
-    **Origem**  
     Exiba cada coluna de origem para a qual você pode especificar as configurações de conversão se necessário.  
  
-   **Destino**  
    Exiba a coluna de destino mapeada ou selecione uma coluna diferente.
    
    Especifique se você deseja ignorar uma coluna durante a operação de cópia. É possível copiar somente um subconjunto de colunas selecionando **ignorar** nesta coluna para as colunas que você deseja ignorar. Antes de mapear colunas, é necessário ignorar todas as colunas que não serão mapeadas.  
  
-   **Tipo**  
    Exiba o tipo de dados da coluna de destino ou selecione um tipo de dados diferente.
  
-   **Permite valor nulo**  
    Especifique se a coluna de destino permite um valor nulo.  
  
-   **Tamanho**  
    Especifique o número de caracteres da coluna de destino, se aplicável.  
  
-    **Precisão**  
    Especifique a precisão dos dados numéricos na coluna de destino com relação ao número de dígitos, se aplicável.  
  
 -   **Escala**  
    Especifique a escala dos dados numéricos na coluna de destino com relação ao número de casas decimais, se aplicável.  
  
## <a name="whats-next"></a>O que vem a seguir?  
 Depois de especificar e configurar colunas de destino para receber os dados copiados e clicar em **OK**, a caixa de diálogo **Mapeamentos de Coluna** retornará a página **Selecionar tabelas e exibições de origem** ou a página **Configurar destino do arquivo simples**. Para obter mais informações, consulte [Selecionar tabelas e exibições de origem](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) ou [Configurar destino do arquivo simples](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).  
  
 Se tiver especificado um mapeamento que pode não ter êxito na lista **Mapeamentos**, a caixa de diálogo **Mapeamentos de Coluna** levará você para a página **Revisar mapeamento de tipo de dados**. Nessa página, você deve examinar os avisos, especificar as opções de conversão e também definir como tratar os erros. Para obter mais informações, consulte [Revisar mapeamento de tipo de dados](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).  
 
 ## <a name="see-also"></a>Consulte também
[Mapeamento de Tipo de Dados no Assistente para Importação e Exportação do SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)

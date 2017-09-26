---
title: "Mapeamentos de coluna (Assistente de exportação e importação do SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.columnmapandtransform.f1
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b1ed879f21396c3c8d588307eaf087daea8c44c3
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="column-mappings-sql-server-import-and-export-wizard"></a>Mapeamentos de coluna (Assistente de Importação e Exportação do SQL Server)
  Depois de selecionar as tabelas existentes e exibições para copiar ou examinar a consulta que você forneceu, ao clicar em **Editar mapeamentos**, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostra a caixa de diálogo **Mapeamentos de Colunas** . Nessa página você especifica e configurar colunas de destino para receber os dados copiados da colunas de origem. Geralmente, você não precisa alterar nada nesta página.
  
Se não desejar copiar todas as colunas na tabela selecionada, uma coisa que você pode fazer nesta página é excluir as colunas que não deseja. Selecione **ignorar** no **destino** coluna do **mapeamentos** lista de colunas que você não deseja copiar.
 
## <a name="screen-shot-of-the-column-mappings-page"></a>Captura de tela da página Mapeamentos de Colunas 
 A captura de tela a seguir mostra um exemplo de como o **mapeamentos de coluna** caixa de diálogo do assistente. 
 
 Neste exemplo, você verá que o assistente vai criar uma nova tabela de destino, porque a opção **Criar tabela de destino** está selecionada. Por padrão, o assistente dá a cada coluna na nova tabela de destino o mesmo nome, tipo de dados e propriedades como a coluna de origem correspondente. 
  
 ![Página de mapeamentos de coluna do Assistente de importação e exportação](../../integration-services/import-export-data/media/column-mappings.png "página de mapeamentos de coluna do Assistente de importação e exportação")  
  
## <a name="review-the-source-and-destination"></a>Examine a origem e destino 
![Seção de página, origem e destino de mapeamentos de coluna](../../integration-services/import-export-data/media/column-mappings-page-source-and-destination-section.png)

 **Origem**  
 A tabela de origem selecionada, exibição ou consulta.  
  
 **Destino**  
 A tabela de destino selecionada ou a exibição.  

## <a name="optionally-create-a-new-destination-table"></a>Opcionalmente, crie uma nova tabela de destino
![Página de mapeamentos de coluna, nova seção de tabela](../../integration-services/import-export-data/media/column-mappings-page-new-table-section.png)

 **Criar tabela/arquivo de destino**  
 Crie a tabela de destino se ele ainda não existir.    
  
 **Editar SQL**  
Clique em **Editar SQL** para abrir a caixa de diálogo **Instrução Criar Tabela SQL** . Use a instrução CREATE TABLE gerada automaticamente ou modificá-lo para suas finalidades. Se você alterar essa instrução manualmente, precisará verificar se a lista de mapeamentos de coluna reconhece as alterações. Para obter mais informações, consulte [Instrução Criar Tabela SQL](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md).  

### <a name="sometimes-these-options-are-disabled"></a>Às vezes, essas opções serão desabilitadas
O **criar tabela/arquivo de destino** opção e o **Editar SQL** botão são automaticamente habilitados ou desabilitados automaticamente.

-   **Habilitado.** Se você tiver especificado um **novo** tabela de destino no **selecionar tabelas de origem e exibições** página, o **criar tabela de destino** opção é selecionada automaticamente e o ** Editar SQL** botão é habilitado.

-   **Desabilitado.** Se você tiver selecionado um **existente** tabela de destino no **selecionar tabelas de origem e exibições** página, o **criar tabela de destino** opção e o **Editar SQL ** botão estiver desabilitado. Se você quiser criar uma nova tabela de destino, volte para o **selecionar tabelas de origem e exibições** página e digite o nome de um **novo** tabela o **destino** coluna.  

## <a name="what-about-existing-data-in-the-destination"></a>O que os dados existentes no destino?
![Página de mapeamentos de coluna, seção de opções](../../integration-services/import-export-data/media/column-mappings-page-options-section.png)

 **Excluir linhas na tabela/arquivo de destino**  
 Especifique se deseja limpar os dados de uma tabela existente antes de carregar os novos dados.  
  
 **Acrescentar linhas à tabela/arquivo de destino**  
 Especifique se deseja acrescentar os dados novos aos dados já presentes em uma tabela existente.  
  
 **Ignorar e recriar tabela de destino**  
 Escolha esta opção para substituir a tabela de destino. Essa opção só está disponível quando você usou o Assistente para criar a tabela de destino. A tabela de destino será ignorada e recriada somente se o pacote criado pelo assistente for salvo e executado novamente. Essa é uma opção conveniente quando você deseja testar suas configurações mais de uma vez.
  
 **Habilitar inserção de identidade**  
 Escolha esta opção para permitir que valores de identidade existentes nos dados de origem sejam inseridos em uma coluna de identidade na tabela de destino. Por padrão, a coluna de identidade de destino geralmente não permite isto.  
  
> [!TIP]
> Se suas chaves primárias existentes estiverem em uma coluna de identidade, uma coluna autonumber ou equivalente, normalmente você precisará selecionar esta opção para manter os valores de chave primária existentes.  Caso contrário, a coluna de identidade de destino normalmente atribui novos valores.  

## <a name="keep-your-autonumber-or-identity-values"></a>Manter os valores de identidade ou de numeração automática
Se você estiver exportando dados que tenha uma coluna de numeração automática ou uma coluna de identidade - por exemplo, se você estiver exportando do Microsoft Access - verifique se você selecionar **habilitar inserção de identidade** imediatamente descritos acima.

## <a name="review-column-mappings"></a>Revise os mapeamentos de coluna
![Página de mapeamentos de coluna, mapeamentos](../../integration-services/import-export-data/media/column-mappings-page-mappings-section.png)

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
    Especifica a precisão de dados numéricos na coluna de destino - ou seja, o número de dígitos - se aplicável.  
  
 -   **Escala**  
    Especifica a escala de dados numéricos na coluna de destino - ou seja, o número de casas decimais - se aplicável.  
  
## <a name="whats-next"></a>O que vem a seguir?  
 Depois de examinar e configurar colunas de destino para receber os dados copiados da colunas de origem e clique em **Okey**, o **mapeamentos de coluna** caixa de diálogo de volta para o **Selecionar origem Tabelas e exibições** página ou o **configurar o destino de arquivo simples** página. Para obter mais informações, consulte [Selecionar tabelas e exibições de origem](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) ou [Configurar destino do arquivo simples](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).  
  
 Se tiver especificado um mapeamento que pode não ter êxito na lista **Mapeamentos** , a caixa de diálogo **Mapeamentos de Coluna** levará você para a página **Revisar mapeamento de tipo de dados** . Nessa página, você deve examinar os avisos, especificar as opções de conversão e também definir como tratar os erros. Para obter mais informações, consulte [Revisar mapeamento de tipo de dados](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).  
 
 ## <a name="see-also"></a>Consulte também
[Mapeamento de Tipo de Dados no Assistente para Importação e Exportação do SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)  
[Começar com esse exemplo simples de Assistente de Importação e Exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)



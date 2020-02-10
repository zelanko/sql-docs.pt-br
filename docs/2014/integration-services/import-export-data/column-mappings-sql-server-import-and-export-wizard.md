---
title: Mapeamentos de coluna (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.columnmapandtransform.f1
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0108004bc7fb5743ab92c455f4aee99a9f3df498
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62893037"
---
# <a name="column-mappings-sql-server-import-and-export-wizard"></a>Mapeamentos de coluna (Assistente de Importação e Exportação do SQL Server)
  Use a caixa de diálogo **mapeamentos de coluna** para editar parâmetros de transformação.  
  
> [!NOTE]  
>  Não é necessário copiar todas as colunas em uma tabela ao selecionar a opção Cópia de Tabela. Selecione ** \<ignorar>** na coluna **destino** desta caixa de diálogo para as colunas que você deseja ignorar.  
  
 Para obter mais informações sobre este assistente, consulte [Assistente de Importação e Exportação do SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para saber mais sobre as opções de inicialização do assistente, bem como as permissões necessárias para executar o assistente com êxito, consulte [executar o assistente de importação e exportação do SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 O objetivo do Assistente de Importação e Exportação do SQL Server é copiar dados de uma origem para um destino. O assistente também pode criar um banco de dados de destino e tabelas de destino para você. No entanto, se for necessário copiar vários bancos de dados ou tabelas, ou outros tipos de objetos de banco de dados, será necessário usar o Assistente para Copiar Banco de Dados. Para obter mais informações, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opções  
 **Origem**  
 Identifica a tabela, exibição ou consulta de origem selecionada.  
  
 **Destino**  
 Identifica a tabela, exibição ou consulta de destino selecionada.  
  
 **Criar tabela/arquivo de destino**  
 Especifique se deseja criar a tabela de destino, se ainda não existir.  
  
 **Excluir linhas na tabela/arquivo de destino**  
 Especifique se deseja limpar os dados de uma tabela existente antes de carregar dados novos.  
  
 **Acrescentar linhas à tabela/arquivo de destino**  
 Especifique se deseja acrescentar os dados novos aos dados já presentes em uma tabela existente.  
  
 **Editar SQL**  
 Use a instrução padrão na caixa de diálogo **instrução SQL CREATE TABLE** ou modifique-a para suas finalidades. Se essa instrução for modificada, também será necessário fazer alterações associadas no mapeamento de tabela.  
  
 **Remover e recriar tabela de destino**  
 Escolha esta opção para substituir a tabela de destino. Esta opção só está disponível ao usar o assistente para criar a tabela de destino. A tabela de destino é ignorada e recriada somente se o pacote criado pelo assistente for salvo e o pacote for executado novamente.  
  
 **Habilitar inserção de identidade**  
 Escolha esta opção para permitir que valores de identidade existentes nos dados de origem sejam inseridos em uma coluna de identidade na tabela de destino. Por padrão, a coluna de identidade de destino não permite isto.  
  
 **Mapeamentos**  
 Exibe como cada coluna na fonte de dados mapeia para uma coluna no destino.  
  
 Esta lista tem as seguintes colunas:  
  
 **Origem**  
 Exiba cada coluna de origem para a qual é possível definir parâmetros de transformação.  
  
 **Destino**  
 Especifique se você deseja ignorar uma coluna durante a operação de cópia. Você pode copiar apenas um subconjunto de colunas selecionando ** \<ignorar>** nesta coluna para colunas que você deseja ignorar. Antes de mapear colunas, é necessário ignorar todas as colunas que não serão mapeadas.  
  
 **Tipo**  
 Selecione um tipo de dados para a coluna.  
  
 **Nullable**  
 Especifique se uma coluna permitirá um valor nulo.  
  
 **Tamanho**  
 Especifique o número de caracteres na coluna.  
  
 **Precisão**  
 Especifique a precisão de dados exibidos, com relação ao número de dígitos.  
  
 **Escala**  
 Especifique a escala de dados exibidos, com relação ao número de casas decimais.  
  
  

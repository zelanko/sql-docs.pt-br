---
title: Selecionar tabelas e colunas Oracle | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- selTabCol
ms.assetid: bf73f80e-a954-4c5f-874e-17fdd4082715
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fe951cb7811bb8cc92414564fda466657d2fae8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771052"
---
# <a name="select-oracle-tables-and-columns"></a>Selecionar tabelas e colunas Oracle
  Use a página Selecione tabelas e colunas Oracle para selecionar as tabelas do banco de dados de origem Oracle onde as alterações são capturadas. Esta página tem os seguintes elementos:  
  
## <a name="options"></a>Opções  
 **Lista de tabelas**  
 A lista de tabelas tem três colunas:  
  
-   **Nome da tabela Oracle**: o nome da tabela, incluindo o esquema de tabela.  
  
-   **Instância de captura**: o nome da instância de captura usada para nomear objetos do Change Data Capture específicos. A instância de captura não pode ser NULL.  
  
     Se não for especificado, o nome será derivado do nome do esquema de origem mais o nome da tabela de origem, no formato `<schema-name>_<table-name>`. O nome da instância de captura não pode exceder 100 caracteres e deve ser exclusivo no banco de dados.  
  
     Você pode clicar em qualquer célula nesta coluna para editar manualmente **capture_instance**.  
  
-   **Função de segurança**: o nome da função de banco de dados de associação usada para controlar o acesso aos dados de alteração.  
  
     Você pode clicar em qualquer célula nesta coluna para editar manualmente **security_role**.  
  
 **Adicionar tabelas**  
 Clique em **Adicionar Tabelas** para abrir a caixa de diálogo Seleção de Tabela em que você pode [Selecionar as tabelas Oracle para capturar alterações](select-oracle-tables-for-capturing-changes.md).  
  
 **Editar**  
 Selecione uma tabela da lista e selecione **Editar** para abrir a caixa de diálogo **Propriedades** para a tabela em que você pode [Fazer alterações nas tabelas selecionadas para capturar alterações](make-changes-to-the-tables-selected-for-capturing-changes.md).  
  
 **Remover**  
 Selecione uma tabela da lista e clique em **Remover** para remover a tabela da instância CDC.  
  
 Depois que você [Selecionar tabelas Oracle para capturar alterações](select-oracle-tables-for-capturing-changes.md) e/ou [Fizer alterações nas tabelas selecionadas para capturar alterações](make-changes-to-the-tables-selected-for-capturing-changes.md) usando as caixas de diálogo corretas, clique em **Avançar** para [Gerar e executar scripts de log suplementares](generate-and-run-the-supplemental-logging-script.md).  
  
## <a name="see-also"></a>Consulte também  
 [Como criar a instância de banco de dados de alteração do SQL Server](how-to-create-the-sql-server-change-database-instance.md)   
 [Editar tabelas](edit-tables.md)   
 [Adicionar tabelas a uma instância CDC](add-tables-to-a-cdc-instance.md)   
 [Editar as propriedades da tabela](edit-the-table-properties.md)  
  
  

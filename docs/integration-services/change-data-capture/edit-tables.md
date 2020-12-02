---
description: Editar tabelas
title: Editar Tabelas | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- tabProps
ms.assetid: fed8fada-2abc-45e2-8228-0656f9c599cb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7d691afbf3f32b249674627b4aa1430075910c68
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96130673"
---
# <a name="edit-tables"></a>Editar tabelas

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Use a guia **Tables** para fazer alterações às tabelas e colunas selecionadas do banco de dados de origem Oracle. Esta guia tem os seguintes elementos:  
  
 **Lista Tabela**  
 A lista de tabelas tem três colunas:  
  
-   **Nome da tabela Oracle**: o nome da tabela, incluindo esquema de tabela.  
  
-   **Instância de Captura**: é o nome da instância de captura usada para nomear objetos do Change Data Capture específicos. A instância de captura não pode ser NULL. Se não for especificado, o nome será derivado do nome do esquema de origem mais o nome da tabela de origem, no formato `<schema-name>_<table-name>.` . O nome da instância de captura não pode exceder a 100 caracteres e deve ser exclusivo dentro do banco de dados. Você pode clicar em qualquer célula nesta coluna para editar manualmente **capture_instance**.  
  
-   **Security Role**: o nome da função de banco de dados usada para obter acesso aos dados de alteração. Você pode clicar em qualquer célula nesta coluna para editar manualmente **security_role**.  
  
 **Adicionar tabelas**  
 Clique em **Adicionar Tabelas** para abrir a caixa de diálogo Seleção de Tabela em que você pode [Adicionar tabelas a uma instância CDC](../../integration-services/change-data-capture/add-tables-to-a-cdc-instance.md). Da primeira vez nesta sessão que você acessa o banco de dados Oracle, é preciso [Connect to Oracle](../../integration-services/change-data-capture/connect-to-oracle.md).  
  
 **Editar**  
 Selecione uma tabela da lista e selecione **Editar** para abrir a caixa de diálogo **Propriedades** para a tabela em que você pode [Editar as propriedades da tabela](../../integration-services/change-data-capture/edit-the-table-properties.md).  
  
> [!NOTE]  
>  Você não pode editar o mapeamento de tipo para tabelas que já tenham tabelas de espelho. Você só pode fazer isto para novas tabelas.  
  
 **Remover**  
 Selecione uma tabela da lista e clique em **Remover** para remover a tabela da instância CDC.  
  
## <a name="see-also"></a>Consulte Também  
 [Como editar as propriedades de instância CDC](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [Selecionar tabelas e colunas Oracle](../../integration-services/change-data-capture/select-oracle-tables-and-columns.md)  
  
  

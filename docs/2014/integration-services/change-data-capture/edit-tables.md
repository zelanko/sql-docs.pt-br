---
title: Editar Tabelas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- tabProps
ms.assetid: fed8fada-2abc-45e2-8228-0656f9c599cb
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e3d3fdde44b1dba2c467f25b6f338ae8b6b15ece
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120843"
---
# <a name="edit-tables"></a>Editar tabelas
  Use a guia **Tables** para fazer alterações às tabelas e colunas selecionadas do banco de dados de origem Oracle. Esta guia tem os seguintes elementos:  
  
 **Lista Tabela**  
 A lista de tabelas tem três colunas:  
  
-   **Nome da tabela Oracle**: o nome da tabela, incluindo esquema de tabela.  
  
-   **Instância de Captura**: é o nome da instância de captura usada para nomear objetos do Change Data Capture específicos. A instância de captura não pode ser NULL. Se não for especificado, o nome será derivado do nome do esquema de origem mais o nome da tabela de origem, no formato `<schema-name>_<table-name>.` . O nome da instância de captura não pode exceder a 100 caracteres e deve ser exclusivo dentro do banco de dados. Você pode clicar em qualquer célula nesta coluna para editar manualmente **capture_instance**.  
  
-   **Security Role**: o nome da função de banco de dados usada para obter acesso aos dados de alteração. Você pode clicar em qualquer célula nesta coluna para editar manualmente **security_role**.  
  
 **Adicionar tabelas**  
 Clique em **Adicionar Tabelas** para abrir a caixa de diálogo Seleção de Tabela em que você pode [Adicionar tabelas a uma instância CDC](add-tables-to-a-cdc-instance.md). Da primeira vez nesta sessão que você acessa o banco de dados Oracle, é preciso [Connect to Oracle](connect-to-oracle.md).  
  
 **Editar**  
 Selecione uma tabela da lista e selecione **Editar** para abrir a caixa de diálogo **Propriedades** para a tabela em que você pode [Editar as propriedades da tabela](edit-the-table-properties.md).  
  
> [!NOTE]  
>  Você não pode editar o mapeamento de tipo para tabelas que já tenham tabelas de espelho. Você só pode fazer isto para novas tabelas.  
  
 **Remover**  
 Selecione uma tabela da lista e clique em **Remover** para remover a tabela da instância CDC.  
  
## <a name="see-also"></a>Consulte também  
 [Como editar as propriedades de instância CDC](how-to-edit-the-cdc-instance-properties.md)   
 [Selecionar tabelas e colunas Oracle](select-oracle-tables-and-columns.md)  
  
  
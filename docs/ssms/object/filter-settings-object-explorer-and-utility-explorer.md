---
title: Configurações de Filtro (Pesquisador de Objetos e Gerenciador do Utilitário)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.common.filtersettings.f1
- sql13.ag.job.filtersettings.f1
ms.assetid: 4aab04bc-e1ab-4d4b-ab74-b287fc805bc2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 66ae081ad6fcfb5b5d361201430ea9fb4d8dcd6c
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86001961"
---
# <a name="filter-settings-object-explorer-and-utility-explorer"></a>Configurações de Filtro (Pesquisador de Objetos e Gerenciador do Utilitário)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Use essa caixa de diálogo para especificar um filtro. Um filtro permite que você configure o Pesquisador de Objetos e o Gerenciador do Utilitário para exibir apenas os itens que atendam aos critérios específicos. Por exemplo, você pode usar um filtro para mostrar apenas os trabalhos com nomes que contêm a palavra "Manutenção". O cabeçalho da caixa de diálogo **Configurações de Filtro** contém o nome do servidor e pode conter o nome do banco de dados.  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
**Propriedade**  
Exibe a propriedade a ser filtrada.  
  
**Operador**  
Seleciona o modo que o filtro aplica o valor à propriedade. Existem as seguintes opções:  
  
-   **Igual a**  
  
    O filtro mostra os itens onde a propriedade e o valor têm uma correspondência exata.  
  
-   **Contém**  
  
    O filtro mostra os itens onde a propriedade contém o valor. A propriedade pode conter outro texto.  
  
-   **Não contém**  
  
    O filtro mostra os itens onde a propriedade não contém o valor.  
  
-   **Menor que**  
  
    Disponível para datas, esse filtro mostra os itens cuja data está antes do valor fornecido.  
  
-   **Menor ou igual a**  
  
    Disponível para datas, esse filtro mostra os itens cuja data contém ou está antes do valor fornecido.  
  
-   **Maior que**  
  
    Disponível para datas, esse filtro mostra os itens cuja data está depois do valor fornecido.  
  
-   **Maior ou igual a**  
  
    Disponível para datas, esse filtro mostra os itens cuja data contém ou está depois do valor fornecido.  
  
-   **Entre**  
  
    Disponível para datas, este filtro mostra os itens cuja data está entre duas datas fornecidas. Selecione **Entre** e pressione TAB para adicionar outra linha permitindo a entrada da segunda data.  
  
-   **Não entre**  
  
    Disponível para datas, esse filtro mostra os itens cuja data está antes ou depois das duas datas fornecidas. Selecione **Não entre** e saia da coluna **Operador** para adicionar outra linha permitindo a entrada da segunda data.  
  
**Valor**  
Digite o valor para comparar à propriedade. Para datas, clique na seta para baixo para mostrar um calendário para selecionar a data.  
  
**Limpar Filtro**  
Remove todas as configurações de filtro atuais.  
  
## <a name="see-also"></a>Consulte Também  
[Usar o SQL Server Management Studio](../../ssms/use-sql-server-management-studio.md)  
[Visão geral do Utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  

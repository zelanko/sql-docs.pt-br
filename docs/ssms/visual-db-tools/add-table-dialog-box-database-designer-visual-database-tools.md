---
title: Adicionar Caixa de Diálogo de Tabela (Designer de Banco de Dados)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65555
- vdt.dlgbox.schema.addtable
ms.assetid: 3c0b1b30-795c-4240-91d6-890b8348014a
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 9c005a61a742a0c589cf5ccc26f818b8479b6a14
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86000762"
---
# <a name="add-table-dialog-box-database-designer-visual-database-tools"></a>Caixa de diálogo Adicionar Tabela (Designer de Banco de Dados) (Visual Database Tools)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Permite adicionar tabelas no Designer de Banco de Dados.  
  
> [!NOTE]  
> Se a tabela for publicada para replicação, você precisará fazer alterações no esquema usando a instrução Transact-SQL [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) ou o SMO (SQL Server Management Objects). Ao fazer alterações no esquema com o Criador de Tabelas ou com o Criador do Diagrama de Banco de Dados, ele tenta descartar e recriar a tabela. Não é possível descartar objetos publicados, portanto, haverá falha na alteração de esquema.  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
**Atualizar**  
Atualizou a lista de tabelas para que correspondesse ao estado atual do banco de dados.  
  
**Adicionar**  
Adiciona a tabela ou tabelas selecionadas.  
  
> [!NOTE]  
> Para adicionar várias tabelas ao diagrama, você pode selecionar todas elas antes de clicar em **Adicionar**. Se preferir, clique duas vezes em cada tabela que desejar adicionar e clicar em **Fechar** ao final.  
  
**Fechar**  
Fecha a caixa de diálogo sem adicionar mais tabelas.  
  
## <a name="see-also"></a>Consulte Também  
[Adicionar tabelas a diagramas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-tables-to-diagrams-visual-database-tools.md)  
  

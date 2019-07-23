---
title: Criar relações entre tabelas em um diagrama (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- diagrams [SQL Server], designing
ms.assetid: 28e9630c-dff4-46cc-bb0e-fe77998b6ac2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e6ad73857c6eddd459f86663acffb2a49d74d16e
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264289"
---
# <a name="create-relationships-between-tables-on-a-diagram-visual-database-tools"></a>Criar relações entre tabelas em um diagrama (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Você pode criar relações entre colunas em tabelas diferentes no Designer de Diagrama arrastando colunas entre tabelas.  
  
### <a name="to-create-a-relationship-graphically"></a>Para criar uma relação graficamente  
  
1.  No Designer de Banco de Dados, clique no seletor de linha de uma ou mais colunas do banco de dados que você quer relacionar a uma coluna em outra tabela.  
  
2.  Arraste as colunas selecionadas para a tabela relacionada.  
  
3.  Duas caixas de diálogo são exibidas: **Relação de Chaves Estrangeiras** e **Tabelas e Colunas**, com a última aparecendo no primeiro plano.  
  
4.  **Nome da relação** tem um nome fornecido pelo sistema no formato FK_*localtable*\_*foreigntable*. Você pode alterar esse valor.  
  
5.  Verifique se a **Tabela de chaves primárias** especifica a tabela correta.  
  
6.  A grade lista as colunas locais e as suas colunas estrangeiras correspondentes. Você pode adicionar ou remover colunas de tabela ou alterar mapeamentos.  
  
7.  Escolha **OK**.  
  
    A caixa de diálogo **Relação de Chaves Estrangeiras** é exibida. **Relação Selecionada** mostra a relação que você criou.  
  
8.  Altere as propriedades da relação na grade.  
  
9. Escolha **OK** para criar a relação.  
  
    O Designer de Banco de Dados mostra uma relação entre as colunas que você escolheu.  
  
## <a name="see-also"></a>Consulte Também  
[Caixa de diálogo Tabelas e Colunas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/tables-and-columns-dialog-box-visual-database-tools.md)  
[Trabalhando com restrições (Visual Database Tools)](https://msdn.microsoft.com/637098af-2567-48f8-90f4-b41df059833e)  
[Trabalhar com tabelas no diagrama de banco de dados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-tables-in-database-diagram-visual-database-tools.md)  
  

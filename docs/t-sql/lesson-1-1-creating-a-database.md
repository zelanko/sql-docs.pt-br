---
title: Criando um banco de dados (Tutorial) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- tutorial creating a database
ms.assetid: e1e2c83f-dfad-4bb8-aa7a-09d3f69517ae
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6628dcf0ab38db441de9bd9324e69993e5759c38
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-1-1---creating-a-database"></a>Lição 1-1-criação de um banco de dados
Como muitas instruções [!INCLUDE[tsql](../includes/tsql-md.md)] , a instrução CREATE DATABASE tem um parâmetro obrigatório: o nome do banco de dados. CREATE DATABASE também tem muitos parâmetros opcionais, como o local de disco onde você deseja armazenar os arquivos de banco de dados. Quando você executa CREATE DATABASE sem os parâmetros opcionais, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa valores padrão para muitos destes parâmetros. Este tutorial usa poucos parâmetros de sintaxe opcionais.  
  
### <a name="to-create-a-database"></a>Para criar um banco de dados  
  
1.  Em uma janela do Editor de Consultas, digite, mas não execute o seguinte código:  
  
    ```  
    CREATE DATABASE TestData  
    GO  
    ```  
  
2.  Use o ponteiro para selecionar as palavras `CREATE DATABASE`e, em seguida, pressione **F1**. O tópico CREATE DATABASE será exibido em Manuais Online do SQL. Você pode usar esta técnica para localizar a sintaxe completa de CREATE DATABASE e para as outras instruções que são usadas neste tutorial.  
  
3.  No Editor de Consultas, pressione **F5** para executar a instrução e criar um banco de dados denominado `TestData`.  
  
Ao criar um banco de dados, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] faz uma cópia do banco de dados **modelo** e renomeia a cópia para o nome do banco de dados. Esta operação deve levar somente alguns segundos, a menos que você especifique um tamanho inicial grande do banco de dados como um parâmetro opcional.  
  
> [!NOTE]  
> A palavra-chave GO separa instruções quando mais de uma instrução é enviada em um único lote. GO é opcional quando o lote contém somente uma instrução.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Criando uma tabela &#40;Tutorial&#41;](../t-sql/lesson-1-2-creating-a-table.md)  
  
## <a name="see-also"></a>Consulte também  
[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
  
  


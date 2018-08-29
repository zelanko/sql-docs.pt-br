---
title: Criando um banco de dados (tutorial) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- tutorial creating a database
ms.assetid: e1e2c83f-dfad-4bb8-aa7a-09d3f69517ae
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: f7143d762de9a2b445e0904dcd2b4619abc3e1b7
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43036826"
---
# <a name="creating-a-database-tutorial"></a>Criando um banco de dados (tutorial)
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
>  A palavra-chave GO separa instruções quando mais de uma instrução é enviada em um único lote. GO é opcional quando o lote contém somente uma instrução.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Criando uma tabela &#40;Tutorial&#41;](lesson-1-2-creating-a-table.md)  
  
## <a name="see-also"></a>Consulte também  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
  

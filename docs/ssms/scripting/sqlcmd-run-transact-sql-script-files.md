---
title: Executar arquivos de script Transact-SQL usando sqlcmd
description: Saiba como usar o sqlcmd para executar um arquivo de script Transact-SQL. Ele pode conter instruções Transact-SQL, comandos sqlcmd e variáveis de script.
ms.custom: seo-lt-2019
ms.date: 07/15/2016
ms.prod: sql
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- transact sql scripts
ms.assetid: 90067eb8-ca3e-44e8-bb1a-bf7d1a359423
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b1914ed4748a14bc7af7fc7113493e18c34604e8
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036289"
---
# <a name="sqlcmd---run-transact-sql-script-files"></a>sqlcmd – Executar arquivos de script do Transact-SQL
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
 Use **sqlcmd** para executar um arquivo de script do Transact-SQL. Um arquivo de script do Transact-SQL é um arquivo de texto que pode conter uma combinação de instruções Transact-SQL, comandos **sqlcmd** e variáveis de script.  

## <a name="create-a-script-file"></a>Criar um arquivo de script  
 Para criar um arquivo de script simples do Transact-SQL usando o Bloco de Notas, siga estas etapas:  
  
1.  Clique em **Iniciar**, selecione **Todos os Programas**, vá até **Acessórios**e, depois, clique em **Bloco de Notas**.  
  
2.  Copie e cole o seguinte código do Transact-SQL no Bloco de Notas:  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT p.FirstName + ' ' + p.LastName AS 'Employee Name',  
    a.AddressLine1, a.AddressLine2 , a.City, a.PostalCode   
    FROM Person.Person AS p   
       INNER JOIN HumanResources.Employee AS e   
            ON p.BusinessEntityID = e.BusinessEntityID  
        INNER JOIN Person.BusinessEntityAddress bea   
            ON bea.BusinessEntityID = e.BusinessEntityID  
        INNER JOIN Person.Address AS a   
            ON a.AddressID = bea.AddressID;  
    GO  
    ```  
  
3.  Salve o arquivo como **myScript.sql** na unidade C.  
  
## <a name="run-the-script-file"></a>Executar o arquivo de script  
  
1.  Abra una janela de prompt de comando.  
  
2.  Na janela do Prompt de Comando, digite: **sqlcmd -S myServer\nomeInstância -i C:\myScript.sql**  
  
3.  Pressione ENTER.  
  
 Uma lista de nomes e endereços de funcionários do [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] é escrita na janela do prompt de comando.  

## <a name="save-the-output-to-a-text-file"></a>Salvar a saída em um arquivo de texto
  
1.  Abra una janela de prompt de comando.  
  
2.  Na janela do Prompt de comando, digite: **sqlcmd -S myServer\nomeInstância -i C:\myScript.sql -o C:\EmpAdds.txt**  
  
3.  Pressione ENTER.  
  
 Nenhuma saída é retornada na janela de prompt de comando. Em vez disso, a saída é enviada ao arquivo EmpAdds.txt. Você pode verificar essa saída abrindo o arquivo EmpAdds.txt.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar o utilitário sqlcmd](./sqlcmd-start-the-utility.md)   
 [Utilitário sqlcmd](../../tools/sqlcmd-utility.md)  
  

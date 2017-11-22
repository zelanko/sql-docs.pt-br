---
title: "Criando arquivos do valor da variável (DB2ToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 122f3fbe-46a0-40df-ac3b-d43bf33d96ba
caps.latest.revision: "5"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 088943be06c8c544f57bc68d9593d8175ff2995c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="creating-variable-value-files-db2tosql"></a>Criando arquivos do valor da variável (DB2ToSQL)
Arquivo de valor de variável é um arquivo XML que inclui os valores dos parâmetros de comandos como o nome do servidor de origem ou destino que mudam frequentemente de migração de um servidor para outro. Quando ocorre um grande número de migrações de banco de dados, vários arquivos de variável para armazenar o valor de cada servidor de origem serão criados e referenciados em um arquivo de script mestre com o **– v** alternar na linha de comando. Isso ajuda a manter valores estáticos em alguns arquivos de script com os valores das variáveis em vários arquivos de variável.  
  
> [!NOTE]  
> 1.  Nomes de variáveis são o prefixo e sufixo com um símbolo de $ (cifrão). Se as variáveis não estão atribuídas a um valor no arquivo de valor da variável, você encontrará um erro durante a análise do arquivo de script, resultando em atrasando o processo de execução do console.  
> 2.  The escape character for **$** is **$$**. Se o valor de uma variável ou estáticos de um parâmetro contém  **$**  símbolo (cifrão), em seguida,  **$$**  devem ser especificados para tratá-lo como um caractere em vez de uma variável.  
> 3.  Para fins de facilidade de manutenção, as variáveis podem ser declaradas dentro `‘variable-group’` variáveis definidas de elementos de uma separação lógica do usuário.  O uso desse elemento não é obrigatório.  
  
**Exemplos:**  
  
**Exemplo 1:**  
  
```  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$project_folder$" value="<project-folder>"/>  
  
    <variable name="$project_name$" value="<project-name>"/>  
  
    <variable name="$project_overwrite$" value="<true/false>"/>  
  
    <variable name="$project_type$" value="<project-type>"/>  
  
  </variable-group>  
  
</variables>  
```  
**Exemplo 2:**  
  
```  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetServerName$" value="<server-name>"/>  
  
      <variable name="$TargetDB$" value="<database-name>"/>  
  
      <variable name="$TargetUserName$" value="<user-name>"/>  
  
      <variable name="$TargetPassword$" value="<password>"/>  
  
      <variable name="$TrustedConnection$" value="<true/false>"/>  
  
    </variable-group>  
  
    <variable-group name="SqlServerObjectParams">  
  
      <variable name="$ObjectName1$" value="<object-name>"/>  
  
      <variable name="$ObjectName2$" value="<object-name>"/>  
  
    </variable-group>  
  
  </variable-group>  
  
</variables>  
```  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no operando o console é [criar os arquivos de Conexão do servidor &#40; DB2ToSQL &#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Criar os arquivos de conexão de servidor](http://msdn.microsoft.com/en-us/002f129e-0868-48ad-a4b4-c68b5007e12e)  
  

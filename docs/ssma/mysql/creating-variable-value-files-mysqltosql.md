---
title: Criando arquivos do valor da variável (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Creating variable value files
- variable value file validation
ms.assetid: 1dc56a7b-8e3a-4576-ad4f-47050bf7e28a
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 67d08fcef37c1fbb8e2c740233c0d84176c7f5bb
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="creating-variable-value-files-mysqltosql"></a>Criando arquivos do valor da variável (MySQLToSQL)
Arquivo de valor de variável é um arquivo XML que inclui os valores dos parâmetros de comandos como o nome do servidor de origem ou destino que mudam frequentemente de migração de um servidor para outro. Quando ocorre um grande número de migrações de banco de dados, vários arquivos de variável para armazenar o valor de cada servidor de origem serão criados e referenciados em um arquivo de script mestre com o **– v** alternar na linha de comando. Isso ajuda a manter valores estáticos em alguns arquivos de script com os valores das variáveis em vários arquivos de variável.  
  
> [!NOTE]  
> 1.  Nomes de variáveis são o prefixo e sufixo com um símbolo de $ (cifrão). Se as variáveis não estão atribuídas a um valor no arquivo de valor da variável, você encontrará um erro durante a análise do arquivo de script, resultando em atrasando o processo de execução do console.  
> 2.  The escape character for **$** is **$$**. Se o valor de uma variável ou estáticos de um parâmetro contém **$** símbolo (cifrão), em seguida, **$$** devem ser especificados para tratá-lo como um caractere em vez de uma variável.  
> 3.  Para fins de facilidade de manutenção, as variáveis podem ser declaradas dentro `‘variable-group’` variáveis definidas de elementos de uma separação lógica do usuário.  O uso desse elemento não é obrigatório.  
  
**Exemplos:**  
  
**Exemplo 1:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$project_folder$" value="<folder-name>"/>  
  
    <variable name="$project_name$" value="<project-name>"/>  
  
    <variable name="$project_overwrite$" value="<true/false>"/>  
  
    <variable name="$project_type$" value="<project-type>"/>  
  
  </variable-group>  
  
</variables>  
```  
**Exemplo 2:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetUserName$ value="<user-name>"/>  
  
      <variable name="$TargetServerName$" value="<server-name>"/>  
  
      <variable name="$TargetDB$" value="<database-name>"/>  
  
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
  
## <a name="variable-value-file-validation"></a>Validação de arquivo do valor da variável  
O usuário pode facilmente validar seu arquivo de valor da variável no arquivo de definição de esquema **'ConsoleScriptVariablesSchema.xsd'** disponíveis na pasta 'Esquemas'.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no operando o console é [criar os arquivos de Conexão de servidor &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Criar os arquivos de Conexão de servidor (MySQL)](http://msdn.microsoft.com/en-us/df0e970c-da0b-4118-b359-c9dcbbad16d6)  
  

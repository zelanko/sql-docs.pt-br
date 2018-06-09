---
title: Criando arquivos do valor da variável (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Sybase Console,Creating Variable Value Files
- Sybase Console,Variable Value File Validation
ms.assetid: 395be464-4b19-44f7-91e5-b8876d6743dc
caps.latest.revision: 15
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 10bbb156c439ca6642b0b705dff3339e04bf41e8
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34778522"
---
# <a name="creating-variable-value-files-sybasetosql"></a>Criando arquivos do valor da variável (SybaseToSQL)
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
  
    <variable name="$project_folder$" value="<project-folder>"/>  
  
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
  
      <variable name="$TargetUserName$" value="<user-name>"/>  
  
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
O usuário pode facilmente validar seu arquivo de valor da variável no arquivo de definição de esquema **ConsoleScriptVariablesSchema.xsd** disponíveis na pasta 'Esquemas'.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no operando o console é [criar os arquivos de Conexão de servidor &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Criar os arquivos do servidor (Sybase)](http://msdn.microsoft.com/en-us/35ef396f-9f98-429d-9fc5-4f413d08fb37)  
  

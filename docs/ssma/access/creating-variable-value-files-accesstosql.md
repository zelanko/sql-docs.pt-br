---
title: "Criando arquivos do valor da variável (AccessToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 08/17/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 808595c3-8ef1-40bd-a93e-5cf237950e08
caps.latest.revision: "15"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4d19975c619dcbcbf2b0c99b26d6065940d7414f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="creating-variable-value-files-accesstosql"></a>Criando arquivos do valor da variável (AccessToSQL)
Um arquivo de valor de variável é um arquivo XML que inclui os valores dos parâmetros de comandos (como o nome de servidor de origem ou destino) que mudam frequentemente em migrações de servidor. Quando ocorre um grande número de migrações de banco de dados, vários arquivos de variável para armazenar o valor de cada servidor de origem são criados e referenciados em um arquivo de script mestre com o **– v** alternar na linha de comando. Esse comportamento ajuda a manter valores estáticos em alguns arquivos de script com os valores das variáveis em vários arquivos de variável.  
  
> [!NOTE]  
> -  Nomes de variáveis são o prefixo e sufixo com um símbolo de $ (cifrão). Se uma variável não for atribuída um valor no arquivo de valor da variável, ocorrerá um erro durante a análise do arquivo de script, resultando em atrasando o processo de execução do console.  
> -  The escape character for **$** is **$$**. Se o valor de uma variável ou estáticos de um parâmetro contiver um  **$**  símbolo (cifrão), em seguida,  **$$**  devem ser especificados para tratá-lo como um caractere em vez de uma variável.  
> -  Para fins de facilidade de manutenção, as variáveis podem ser declaradas dentro `‘variable-group’` elementos para uma separação lógica de variáveis definidas pelo usuário.  O uso desse elemento não é obrigatório.  
  
**Exemplos:**  
  
**Exemplo 1:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$type$" value="MyProject"/>  
  
    <variable name="$project_folder$" value=".\$project_name$"/>  
  
    <variable name="$project_name$" value="$type$ConsoleProject"/>  
  
    <variable name="$project_overwrite$" value="true"/>  
  
    <variable name="$project_type$" value="sql-server-2008"/>  
  
  </variable-group>  
  
</variables>  
```  
**Exemplo 2:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetServerName$" value="xxx"/>  
  
      <variable name="$TargetDB$" value="xxx"/>  
  
      <variable name="$TargetUserName$" value="xxx"/>  
  
      <variable name="$TargetPassword$" value="xxx"/>  
  
      <variable name="$TargetIsTrusted$" value="xxx"/>  
  
      <variable name="$TrustedConnection$" value="xxx"/>  
  
    </variable-group>  
  
    <variable-group name="SqlServerObjectParams">  
  
      <variable name="$ObjectName1$" value="TestTable1"/>  
  
      <variable name="$ObjectName2$" value="TestProc1"/>  
  
    </variable-group>  
  
  </variable-group>  
  
</variables>  
```  
  
## <a name="variable-value-file-validation"></a>Validação de arquivo do valor da variável  
O usuário pode facilmente validar seu arquivo de valor da variável no arquivo de definição de esquema **ConsoleScriptVariablesSchema.xsd** disponíveis na pasta 'Esquemas'.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no operando o console é [criar os arquivos de Conexão do servidor &#40; AccessToSQL &#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Criar os arquivos de Conexão de servidor (acesso)](http://msdn.microsoft.com/829153be-aa8e-4162-87e8-69882feecf19)  
  

---
title: Criando arquivos de valor de variável (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Creating variable value files
- variable value file validation
ms.assetid: 1dc56a7b-8e3a-4576-ad4f-47050bf7e28a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: be1530bdec1c1523a873dc93b1d70e6e72c880ff
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68103019"
---
# <a name="creating-variable-value-files-mysqltosql"></a>Criar arquivos de valor da variável (MySQLToSQL)
O arquivo de valor da variável é um arquivo XML que inclui os valores de parâmetro de comandos, como, o nome do servidor de origem ou de destino que costuma ser alterado de uma migração de servidor para outra. Quando ocorre um grande número de migrações de banco de dados, vários arquivos de variáveis para armazenar o valor de cada servidor de origem serão criados e referenciados em um arquivo de script mestre com a opção **-v** na linha de comando. Isso ajuda a manter valores estáticos em alguns arquivos de script com os valores de variáveis em vários arquivos de variáveis.  
  
> [!NOTE]  
> 1.  Os nomes de variáveis são prefixados e sufixos com um símbolo de $ (dólar). Se as variáveis não forem atribuídas a um valor no arquivo de valor de variável, você encontrará um erro durante a análise do arquivo de script, resultando na parada do processo de execução do console.  
> 2.  O caractere de escape **$** para **$$** é. Se o valor de uma variável ou valor estático de um parâmetro contiver **$** um símbolo (dólar) **$$** , deverá ser especificado para tratá-lo como um caractere em vez de uma variável.  
> 3.  Para fins de manutenção, as variáveis podem ser declaradas dentro `'variable-group'` de elementos para separação lógica de variáveis definidas pelo usuário.  O uso deste elemento não é obrigatório.  
  
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
  
## <a name="variable-value-file-validation"></a>Validação de arquivo de valor de variável  
O usuário pode facilmente validar seu arquivo de valor de variável com o arquivo de definição de esquema **' ConsoleScriptVariablesSchema. xsd '** disponível na pasta ' schemas '.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa na operação do console é [criar os arquivos de conexão do servidor &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Criando os arquivos de conexão do servidor (MySQL)](https://msdn.microsoft.com/df0e970c-da0b-4118-b359-c9dcbbad16d6)  
  

---
title: Criando arquivos de valor de variável (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 808595c3-8ef1-40bd-a93e-5cf237950e08
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 051ded7d675f81998718b858c71488ba968ec680
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68006598"
---
# <a name="creating-variable-value-files-accesstosql"></a>Criando arquivos de valor de variável (AccessToSQL)
Um arquivo de valor de variável é um arquivo XML que inclui os valores de parâmetro de comandos (como o nome do servidor de origem ou de destino) que são alterados com frequência nas migrações do servidor. Quando ocorre um grande número de migrações de banco de dados, vários arquivos variáveis para armazenar o valor de cada servidor de origem são criados e referenciados em um arquivo de script mestre com a opção **-v** na linha de comando. Esse comportamento ajuda a manter valores estáticos em alguns arquivos de script com os valores de variáveis em vários arquivos de variáveis.  
  
> [!NOTE]  
> -  Os nomes de variáveis são prefixados e sufixos com um símbolo de $ (dólar). Se uma variável não for atribuída a um valor no arquivo de valor da variável, ocorrerá um erro durante a análise do arquivo de script, resultando na parada do processo de execução do console.  
> -  O caractere de escape **$** para **$$** é. Se o valor de uma variável ou valor estático de um parâmetro contiver **$** um símbolo (dólar), **$$** deverá ser especificado para tratá-lo como um caractere em vez de uma variável.  
> -  Para fins de manutenção, as variáveis podem ser declaradas dentro `'variable-group'` de elementos para separação lógica de variáveis definidas pelo usuário.  O uso deste elemento não é obrigatório.  
  
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
  
## <a name="variable-value-file-validation"></a>Validação de arquivo de valor de variável  
O usuário pode facilmente validar seu arquivo de valor de variável em relação ao arquivo de definição de esquema **ConsoleScriptVariablesSchema. xsd** disponível na pasta ' schemas '.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa na operação do console é [criar os arquivos de conexão do servidor &#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
## <a name="see-also"></a>Confira também  
[Criando os arquivos de conexão do servidor (Access)](https://msdn.microsoft.com/829153be-aa8e-4162-87e8-69882feecf19)  
  

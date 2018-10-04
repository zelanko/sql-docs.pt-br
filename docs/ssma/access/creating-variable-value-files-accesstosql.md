---
title: Criando arquivos de valor da variável (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 808595c3-8ef1-40bd-a93e-5cf237950e08
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 005be9b3009ba8812219a6974fa13465bf786747
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47680944"
---
# <a name="creating-variable-value-files-accesstosql"></a>Criando arquivos de valor da variável (AccessToSQL)
Um arquivo de valores de variável é um arquivo XML que compõem os valores de parâmetro de comandos (como o nome de servidor de origem ou destino) que mudam frequentemente em migrações de servidor. Quando ocorre um grande número de migrações de banco de dados, vários arquivos de variável para armazenar o valor de cada servidor de origem são criados e referenciados em um arquivo de script mestre com o **– v** alternar na linha de comando. Esse comportamento ajuda a manter os valores estáticos em alguns arquivos de script com os valores das variáveis em vários arquivos de variável.  
  
> [!NOTE]  
> -  Nomes de variáveis são o prefixo e o sufixo com um símbolo $ (cifrão). Se uma variável não for atribuída um valor no arquivo de valor da variável, ocorrerá um erro durante a análise do arquivo de script, resultando em atrasando o processo de execução do console.  
> -  O caractere de escape para o **$** é **$$**. Se o valor de um valor estático ou variável de um parâmetro contém um **$** símbolo (cifrão), em seguida, **$$** devem ser especificados para tratá-lo como um caractere em vez de uma variável.  
> -  Para fins de facilidade de manutenção, as variáveis podem ser declaradas dentro `‘variable-group’` elementos para separação lógica de variáveis definidas pelo usuário.  O uso desse elemento não é obrigatório.  
  
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
  
## <a name="variable-value-file-validation"></a>Validação de valor da variável de arquivo  
O usuário pode validar com facilidade seu arquivo de valor da variável em relação ao arquivo de definição de esquema **ConsoleScriptVariablesSchema.xsd** disponível na pasta "Esquemas".  
  
## <a name="next-step"></a>Próxima etapa  
É a próxima etapa no operando o console [criar os arquivos de Conexão de servidor &#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
## <a name="see-also"></a>Confira também  
[Criar os arquivos de Conexão de servidor (acesso)](http://msdn.microsoft.com/829153be-aa8e-4162-87e8-69882feecf19)  
  

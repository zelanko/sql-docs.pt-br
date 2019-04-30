---
title: Criar arquivos de valor da variável (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Variable Value File Creation
- Variable Value File, Variable Value File Validation
ms.assetid: f583d81a-8e34-41b1-8100-ee3a6a82213b
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 067781fd998c9e7763fe3a9f2befacab59687250
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63287174"
---
# <a name="creating-variable-value-files-oracletosql"></a>Criar arquivos de valor da variável (OracleToSQL)
Arquivo de valor de variável é um arquivo XML que compõem os valores de parâmetro de comandos, como o nome do servidor de origem ou destino que mudam frequentemente de migração de um servidor para outro. Quando ocorre um grande número de migrações de banco de dados, vários arquivos de variável para armazenar o valor de cada servidor de origem serão criados e referenciados em um arquivo de script mestre com o **- v** alternar na linha de comando. Isso ajuda a manter os valores estáticos em alguns arquivos de script com os valores das variáveis em vários arquivos de variável.  
  
> [!NOTE]  
> 1.  Nomes de variáveis são o prefixo e o sufixo com um símbolo $ (cifrão). Se as variáveis não são atribuídas a um valor no arquivo de valor da variável, você encontrará um erro durante a análise do arquivo de script, resultando em atrasando o processo de execução do console.  
> 2.  O caractere de escape para o **$** é **$$**. Se o valor de um valor estático ou variável de um parâmetro contiver **$** símbolo (cifrão), em seguida, **$$** devem ser especificados para tratá-lo como um caractere em vez de uma variável.  
> 3.  Para fins de facilidade de manutenção, as variáveis podem ser declaradas dentro `'variable-group'` variáveis definidas de elementos para uma separação lógica do usuário.  O uso desse elemento não é obrigatório.  
  
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
É a próxima etapa no operando o console [criar os arquivos de Conexão de servidor &#40;OracleToSQL&#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Criar os arquivos do servidor (Oracle)](https://msdn.microsoft.com/002f129e-0868-48ad-a4b4-c68b5007e12e)  
  

---
title: Criando arquivos de valor da variável (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 122f3fbe-46a0-40df-ac3b-d43bf33d96ba
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 945b7e86641c796e79bfb87b8b7b5de25949e4c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989774"
---
# <a name="creating-variable-value-files-db2tosql"></a>Criando arquivos de valor da variável (DB2ToSQL)
Arquivo de valor de variável é um arquivo XML que compõem os valores de parâmetro de comandos, como o nome do servidor de origem ou destino que mudam frequentemente de migração de um servidor para outro. Quando ocorre um grande número de migrações de banco de dados, vários arquivos de variável para armazenar o valor de cada servidor de origem serão criados e referenciados em um arquivo de script mestre com o **- v** alternar na linha de comando. Isso ajuda a manter os valores estáticos em alguns arquivos de script com os valores das variáveis em vários arquivos de variável.  
  
> [!NOTE]  
> 1.  Nomes de variáveis são o prefixo e o sufixo com um símbolo $ (cifrão). Se as variáveis não são atribuídas a um valor no arquivo de valor da variável, você encontrará um erro durante a análise do arquivo de script, resultando em atrasando o processo de execução do console.  
> 2.  O caractere de escape para o **$** é **$$** . Se o valor de um valor estático ou variável de um parâmetro contiver **$** símbolo (cifrão), em seguida, **$$** devem ser especificados para tratá-lo como um caractere em vez de uma variável.  
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
É a próxima etapa no operando o console [criar os arquivos de Conexão de servidor &#40;DB2ToSQL&#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Criar os arquivos de conexão de servidor](../oracle/creating-the-server-connection-files-oracletosql.md)  
  

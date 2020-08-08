---
title: Criando arquivos de valor de variável (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 122f3fbe-46a0-40df-ac3b-d43bf33d96ba
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: f5a1b2fe01fd9800ee9d56e3a01f9861bfb3a046
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87933851"
---
# <a name="creating-variable-value-files-db2tosql"></a>Criando arquivos de valor de variável (DB2ToSQL)
O arquivo de valor da variável é um arquivo XML que inclui os valores de parâmetro de comandos, como, o nome do servidor de origem ou de destino que costuma ser alterado de uma migração de servidor para outra. Quando ocorre um grande número de migrações de banco de dados, vários arquivos de variáveis para armazenar o valor de cada servidor de origem serão criados e referenciados em um arquivo de script mestre com a opção **-v** na linha de comando. Isso ajuda a manter valores estáticos em alguns arquivos de script com os valores de variáveis em vários arquivos de variáveis.  
  
> [!NOTE]  
> 1.  Os nomes de variáveis são prefixados e sufixos com um símbolo de $ (dólar). Se as variáveis não forem atribuídas a um valor no arquivo de valor de variável, você encontrará um erro durante a análise do arquivo de script, resultando na parada do processo de execução do console.  
> 2.  O caractere de escape para **$** é **$$** . Se o valor de uma variável ou valor estático de um parâmetro contiver um **$** símbolo (dólar), **$$** deverá ser especificado para tratá-lo como um caractere em vez de uma variável.  
> 3.  Para fins de manutenção, as variáveis podem ser declaradas dentro `'variable-group'` de elementos para separação lógica de variáveis definidas pelo usuário.  O uso deste elemento não é obrigatório.  
  
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
A próxima etapa na operação do console é [criar os arquivos de conexão do servidor &#40;DB2ToSQL&#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Criar os arquivos de conexão de servidor](../oracle/creating-the-server-connection-files-oracletosql.md)  
  

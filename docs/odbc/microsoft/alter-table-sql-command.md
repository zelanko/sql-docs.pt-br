---
title: ALTER TABLE - comando SQL | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: alter table [ODBC]
ms.assetid: 3a01a291-f4d9-43bc-a725-5a95546ff364
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 79fbb4e4f6c143d693e1b41cc1660938bc61cde1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="alter-table---sql-command"></a>ALTER TABLE - comando SQL
Modifica programaticamente a estrutura de uma tabela.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER TABLE TableName1  
   ADD | ALTER [COLUMN] FieldName1  
      FieldType [(nFieldWidth [, nPrecision])]  
      [NULL | NOT NULL]  
      [CHECK lExpression1 [ERROR cMessageText1]]  
      [DEFAULT eExpression1]  
      [PRIMARY KEY | UNIQUE]  
      [REFERENCES TableName2 [TAG TagName1]]  
      [NOCPTRANS]  
 - Or -  
ALTER TABLE TableName1  
   ALTER [COLUMN] FieldName2  
      [NULL | NOT NULL]  
      [SET DEFAULT eExpression2]  
      [SET CHECK lExpression2 [ERROR cMessageText2]]  
      [DROP DEFAULT]  
      [DROP CHECK]  
 - Or -  
ALTER TABLE TableName1  
   [DROP [COLUMN] FieldName3]  
   [SET CHECK lExpression3 [ERROR cMessageText3]]  
   [DROP CHECK]  
   [ADD PRIMARY KEY eExpression3 TAG TagName2]  
   [DROP PRIMARY KEY]  
   [ADD UNIQUE eExpression4 [TAG TagName3]]  
   [DROP UNIQUE TAG TagName4]  
   [ADD FOREIGN KEY [eExpression5] TAG TagName4  
      REFERENCES TableName2 [TAG TagName5]]  
   [DROP FOREIGN KEY TAG TagName6 [SAVE]]  
   [RENAME COLUMN FieldName4 TO FieldName5]  
   [NOVALIDATE]  
```  
  
## <a name="arguments"></a>Argumentos  
 *TableName1*  
 Especifica o nome da tabela cuja estrutura é modificada.  
  
 Adicionar [coluna] *FieldName1*  
 Especifica o nome do campo para adicionar.  
  
 ALTER [coluna] *FieldName1*  
 Especifica o nome de um campo existente para modificar.  
  
 *FieldType* [( *nFieldWidth* [, *nPrecision*]])  
 Especifica o tipo de campo, a largura de campo e a precisão de campo (número de casas decimais) para um campo novo ou modificado.  
  
 *FieldType* é uma única letra que indica o campo [tipo de dados](../../odbc/microsoft/visual-foxpro-field-data-types.md). Alguns tipos de dados do campo exigem que você especifique *nFieldWidth* ou *nPrecision* ou ambos.  
  
 *nFieldWidth* e *nPrecision* para D, G, I, L, M, P, T e Y são ignoradas tipos. Por padrão, *nPrecision* é zero (sem casas decimais) se *nPrecision* não está incluído para os tipos de B, F ou N.  
  
 NULL &#124; NÃO NULO  
 Permite ou impede que valores nulos no campo.  
  
 Se você omite NULL e NOT NULL, a configuração atual de SET NULL determina se valores nulos são permitidos no campo. No entanto, se você omite NULL e NOT NULL e incluem a chave primária ou exclusiva cláusula, a configuração atual de SET NULL é ignorada e o campo não é nulo por padrão.  
  
 VERIFICAR *lExpression1*  
 Especifica uma regra de validação para o campo. *lExpression1* devem ser avaliados como uma expressão lógica e pode ser uma função definida pelo usuário ou um procedimento armazenado. Sempre que é anexado a um registro em branco, a regra de validação é verificada. Um erro será gerado se a regra de validação não permite que um valor de campo em branco em um registro anexado.  
  
 Erro *cMessageText1*  
 Especifica a mensagem de erro exibida quando a regra de validação de campo gera um erro.  
  
 PADRÃO *eExpression1*  
 Especifica um valor padrão para o campo. O tipo de dados *eExpression1* deve ser o mesmo que o tipo de dados para o campo.  
  
 PRIMARY KEY  
 Cria uma marca de índice primário. A marca de índice tem o mesmo nome do campo.  
  
 UNIQUE  
 Cria uma marca de índice de candidato com o mesmo nome do campo.  
  
> [!NOTE]  
>  Candidato índices (criados, incluindo a opção exclusiva, fornecida para compatibilidade de ANSI em ALTER TABLE ou CREATE TABLE) diferem dos índices criados usando a opção exclusiva no comando de índice. Um índice criado usando o comando de índice UNIQUE permite que chaves de índice duplicadas; índices de candidato não permitem chaves de índice duplicadas.  
  
 Valores nulos e registros duplicados não são permitidos em um campo que é usado para um índice primárias ou candidatas.  
  
 Se você estiver criando um novo campo usando Adicionar coluna, Visual FoxPro não irá gerar um erro, se você criar um índice primárias ou candidatas para um campo que oferece suporte a valores nulos. No entanto, o Visual FoxPro gerará um erro se você tentar inserir um valor nulo ou duplicado em um campo que é usado para um índice primárias ou candidatas.  
  
 Se você estiver modificando um campo existente e o primário ou expressão de índice de candidato consiste em campos na tabela, do Visual FoxPro verifica os campos para ver se eles contêm valores nulos ou registros duplicados. Se isso ocorrer, Visual FoxPro gerará um erro e a tabela não é alterada.  
  
 REFERÊNCIAS *TableName2* marca *TagName1*  
 Especifica a tabela pai ao qual será estabelecida uma relação persistente. MARCA *TagName1* Especifica a marca de índice da tabela pai na qual a relação é baseada. Nomes de marca de índice podem conter até 10 caracteres.  
  
 NOCPTRANS  
 Impede que a conversão em uma página de código diferente para campos de caractere e de memorando. Se a tabela é convertida em outra página de código, os campos para os quais foi especificado NOCPTRANS não são traduzidos. NOCPTRANS pode ser especificado apenas para campos de caractere e de memorando.  
  
 O exemplo a seguir cria uma tabela chamada mytable que contém dois campos de caractere e dois campos de memorando. O segundo campo de caractere, char2 e o segundo campo de memorando, memo2, incluem NOCPTRANS para evitar a conversão.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 ALTER [coluna] *FieldName2*  
 Especifica o nome de um campo existente para modificar.  
  
 Definir como padrão *eExpression2*  
 Especifica um novo valor padrão para um campo existente. O tipo de dados *eExpression2* deve ser o mesmo que o tipo de dados para o campo.  
  
 SELEÇÃO de conjunto *lExpression2*  
 Especifica uma nova regra de validação para um campo existente. *lExpression2* devem ser avaliados como uma expressão lógica e pode ser uma função definida pelo usuário ou um procedimento armazenado.  
  
 Erro *cMessageText2*  
 Especifica a mensagem de erro exibida quando a regra de validação de campo gera um erro. A mensagem é exibida somente quando os dados são alterados em uma janela Procurar ou editar.  
  
 DROP DEFAULT  
 Remove o valor padrão para um campo existente.  
  
 SELEÇÃO DE SOLTAR  
 Remove a regra de validação para um campo existente.  
  
 DROP [coluna] *FieldName3*  
 Especifica um campo para remover da tabela. Remover um campo da tabela também remove a configuração do campo padrão valor e a regra de validação de campo.  
  
 Se o campo de referenciam a expressões de gatilho ou a chave de índice, as expressões de se tornar inválidas quando o campo é removido. Nesse caso, um erro não é gerado quando o campo é removido, mas as expressões de gatilho ou a chave de índice inválido irá gerar erros em tempo de execução.  
  
 SELEÇÃO de conjunto *lExpression3*  
 Especifica a regra de validação da tabela. *lExpression3* devem ser avaliados como uma expressão lógica e pode ser uma função definida pelo usuário ou um procedimento armazenado.  
  
 Erro *cMessageText3*  
 Especifica a mensagem de erro exibida quando a regra de validação de tabela gera um erro. A mensagem é exibida somente quando os dados são alterados em uma janela Procurar ou editar.  
  
 SELEÇÃO DE SOLTAR  
 Remove a regra de validação da tabela.  
  
 CHAVE primária adicionar *eExpression3*marca *TagName2*  
 Adiciona um índice primário na tabela. *eExpression3* Especifica a expressão de chave de índice primário e *TagName2* Especifica o nome da marca do índice primário. Nomes de marca de índice podem conter até 10 caracteres. Se marca *TagName2* for omitido e *eExpression3* é um campo único, a marca do índice primário tem o mesmo nome como o campo especificado em *eExpression3*.  
  
 DESCARTE A CHAVE PRIMÁRIA  
 Remove o índice primário e sua marca de índice. Como uma tabela pode ter somente uma chave primária, não é necessário especificar o nome da chave primária. Remover o índice primário também exclui todos os parceiros persistentes com base na chave primária.  
  
 Adicionar UNIQUE *eExpression4*[marca *TagName3*]  
 Adiciona um índice de candidato para a tabela. *eExpression4* Especifica a expressão de chave de índice de candidato, e *TagName3* Especifica o nome da marca de índice do candidato. Nomes de marca de índice podem conter até 10 caracteres. Se você omitir marca *TagName3* e se *eExpression4* é um campo único, a marca de índice candidato tem o mesmo nome que o campo especificado em *eExpression4*.  
  
 MARCA exclusivo DROP *TagName4*  
 Remove o índice de candidato e marcação de índice. Como uma tabela pode ter várias chaves de candidato, você deve especificar o nome da marca de índice do candidato.  
  
 CHAVE estrangeira adicionar [ *eExpression5*] marca *TagName4*  
 Adiciona um índice (as) estrangeiro à tabela. *eExpression5* Especifica a expressão de chave estrangeira de índice, e *TagName4* Especifica o nome da marca externa do índice. Nomes de marca de índice podem conter até 10 caracteres.  
  
 REFERÊNCIAS *TableName2*[marca *TagName5*]  
 Especifica a tabela pai ao qual será estabelecida uma relação persistente. MARCA include *TagName5* para estabelecer uma relação com base em uma marca de índice existente para a tabela pai. Nomes de marca de índice podem conter até 10 caracteres. Se você omitir marca *TagName5*, a relação é estabelecida usando a marca de índice primário da tabela pai.  
  
 MARCA de chave estrangeira DROP *TagName6*[Salvar]  
 Exclui uma chave estrangeira marca cujo índice é *TagName6*. Se você omitir salvar, a marca de índice é excluída do índice estrutural. Incluir Salvar para impedir a exclusão da marca do índice do índice estrutural.  
  
 RENOMEAR coluna *FieldName4*para *FieldName5*  
 Permite que você altere o nome de um campo na tabela. *FieldName4* Especifica o nome do campo que é renomeado. *FieldName5* Especifica o novo nome do campo.  
  
> [!CAUTION]  
>  Tenha cuidado ao renomear campos de tabela como expressões de índice, as regras de validação de campo e tabela, comandos e funções podem fazer referência os nomes de campo original.  
  
 NOVALIDATE  
 Especifica que o Visual FoxPro permite que as alterações sejam feitas para a estrutura da tabela; Essas alterações podem violar a integridade dos dados na tabela. Por padrão, Visual FoxPro impede ALTER TABLE fazendo alterações que violam a integridade dos dados na tabela. Inclua NOVALIDATE para substituir esse comportamento padrão.  
  
## <a name="remarks"></a>Comentários  
 ALTER TABLE pode ser usado para modificar a estrutura de uma tabela que não foi adicionada ao banco de dados. No entanto, o Visual FoxPro gerará um erro se você incluir o padrão, a chave estrangeira, a chave primária, a referências ou definir cláusulas ao modificar uma tabela livre.  
  
 ALTER TABLE pode recriar a tabela de criação de um novo cabeçalho de tabela e anexando registros para o cabeçalho da tabela. Por exemplo, alterar o tipo ou a largura de um campo pode causar a tabela devem ser recriados.  
  
 Depois que uma tabela é recriada, regras de validação de campo são executadas para os campos cujo tipo ou a largura são alterados. Se você alterar o tipo ou a largura de qualquer campo na tabela, a regra de tabela é executada.  
  
 Se você modificar as regras de validação de campo ou de tabela para uma tabela que tem registros, Visual FoxPro testa as regras de validação de campo ou tabela nova em relação aos dados existentes e emite um aviso na primeira ocorrência de uma regra de validação de campo ou de tabela ou de uma violação de gatilho.  
  
 Se a tabela que você modificar um banco de dados, ALTER TABLE - SQL requer o uso exclusivo do banco de dados. Para abrir um banco de dados para uso exclusivo, incluem exclusivo no banco de dados aberto.  
  
## <a name="see-also"></a>Consulte também  
 [Criar tabela - comando SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [Comando INDEX](../../odbc/microsoft/index-command.md)

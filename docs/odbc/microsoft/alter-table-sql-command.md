---
title: ALTER TABLE – comando SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- alter table [ODBC]
ms.assetid: 3a01a291-f4d9-43bc-a725-5a95546ff364
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f656396455a8d5669debc158c3edc866491fcb5
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207005"
---
# <a name="alter-table---sql-command"></a>ALTER TABLE – comando SQL
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
 Especifica o nome do campo a ser adicionado.  
  
 ALTER [coluna] *FieldName1*  
 Especifica o nome de um campo existente para modificar.  
  
 *FieldType* [( *nFieldWidth* [, *nPrecision*]])  
 Especifica o tipo de campo, a largura do campo e a precisão de campo (número de casas decimais) para um campo de novo ou modificado.  
  
 *FieldType* é uma única letra que indica o campo [tipo de dados](../../odbc/microsoft/visual-foxpro-field-data-types.md). Alguns tipos de dados do campo exigem que você especifique *nFieldWidth* ou *nPrecision* ou ambos.  
  
 *nFieldWidth* e *nPrecision* são ignoradas para D, G, eu, L, M, P, T e Y tipos. Por padrão, *nPrecision* é zero (sem casas decimais) se *nPrecision* não está incluído para os tipos de B, F ou N.  
  
 NULL &#124; NOT NULL  
 Permite ou impede que os valores nulos no campo.  
  
 Se você omite o NULL e NOT NULL, a configuração atual de SET NULL determina se são permitidos valores nulos no campo. No entanto, se você omite NULL e NOT NULL e incluir a chave primária ou uma cláusula exclusiva, a configuração atual de SET NULL é ignorada e o campo não é nulo por padrão.  
  
 VERIFICAR *lExpression1*  
 Especifica uma regra de validação para o campo. *lExpression1* deve ser avaliada como uma expressão lógica e pode ser uma função definida pelo usuário ou um procedimento armazenado. Sempre que um registro em branco for anexado, a regra de validação é verificada. Um erro será gerado se a regra de validação não permite um valor de campo em branco em um registro acrescentado.  
  
 Erro *cMessageText1*  
 Especifica a mensagem de erro exibida quando a regra de validação de campo gera um erro.  
  
 PADRÃO *eExpression1*  
 Especifica um valor padrão para o campo. O tipo de dados *eExpression1* deve ser o mesmo que o tipo de dados para o campo.  
  
 PRIMARY KEY  
 Cria uma marca de índice primário. A marca de índice tem o mesmo nome que o campo.  
  
 UNIQUE  
 Cria uma marca de índice de candidato com o mesmo nome que o campo.  
  
> [!NOTE]  
>  Candidato índices (criados, incluindo a opção exclusiva, fornecida para compatibilidade com ANSI em ALTER TABLE ou CREATE TABLE) diferem dos índices criados usando a opção exclusiva no comando de índice. Um índice criado com o uso exclusivo no comando índice permite que as chaves de índice duplicados; índices de candidato não permitem chaves de índice duplicados.  
  
 Valores nulos e registros duplicados não são permitidos em um campo que é usado para um índice primárias ou candidatas.  
  
 Se você estiver criando um novo campo usando Adicionar coluna, do Visual FoxPro não gerará um erro se você criar um índice primárias ou candidatas para um campo que dá suporte a valores nulos. No entanto, o Visual FoxPro gerará um erro se você tentar inserir um valor nulo ou duplicado em um campo que é usado para um índice primárias ou candidatas.  
  
 Se você estiver modificando um campo existente e o primário ou expressão de índice de candidato consiste em campos na tabela, do Visual FoxPro verifica os campos para ver se eles contêm valores nulos ou registros duplicados. Se Sim, do Visual FoxPro gera um erro e a tabela não for alterada.  
  
 As referências *TableName2* marca *TagName1*  
 Especifica a tabela pai para o qual é estabelecida uma relação de persistente. MARCA *TagName1* Especifica a marca de índice da tabela pai na qual a relação é baseada. Nomes de marca de índice podem conter até 10 caracteres.  
  
 NOCPTRANS  
 Impede que a conversão para uma página de código diferente para os campos de caractere e Memorando. Se a tabela é convertida em outra página de código, os campos para o qual foi especificado NOCPTRANS não são traduzidos. NOCPTRANS pode ser especificado somente para campos de caractere e Memorando.  
  
 O exemplo a seguir cria uma tabela chamada mytable que contém dois campos de caractere e dois campos de memorando. O segundo campo de caractere, char2 e o segundo campo de memorando, memo2, incluem NOCPTRANS para evitar a conversão.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 ALTER [coluna] *FieldName2*  
 Especifica o nome de um campo existente para modificar.  
  
 Definir padrão *eExpression2*  
 Especifica um novo valor padrão para um campo existente. O tipo de dados *eExpression2* deve ser o mesmo que o tipo de dados para o campo.  
  
 SELEÇÃO de conjunto *lExpression2*  
 Especifica uma nova regra de validação para um campo existente. *lExpression2* deve ser avaliada como uma expressão lógica e pode ser uma função definida pelo usuário ou um procedimento armazenado.  
  
 Erro *cMessageText2*  
 Especifica a mensagem de erro exibida quando a regra de validação de campo gera um erro. A mensagem é exibida somente quando dados são alterados em uma janela Procurar ou editar.  
  
 DROP DEFAULT  
 Remove o valor padrão para um campo existente.  
  
 REMOVER SELEÇÃO  
 Remove a regra de validação para um campo existente.  
  
 SOLTAR [coluna] *FieldName3*  
 Especifica um campo a ser removido da tabela. Também remover um campo da tabela remove a configuração do valor do campo padrão e a regra de validação de campo.  
  
 Se as expressões de índice de chave ou gatilho fazem referência ao campo, as expressões de se tornar inválidas quando o campo é removido. Nesse caso, um erro não é gerado quando o campo é removido, mas as expressões de gatilho ou de chave de índice inválido irão gerar erros em tempo de execução.  
  
 SELEÇÃO de conjunto *lExpression3*  
 Especifica a regra de validação de tabela. *lExpression3* deve ser avaliada como uma expressão lógica e pode ser uma função definida pelo usuário ou um procedimento armazenado.  
  
 Erro *cMessageText3*  
 Especifica a mensagem de erro exibida quando a regra de validação de tabela gera um erro. A mensagem é exibida somente quando dados são alterados em uma janela Procurar ou editar.  
  
 REMOVER SELEÇÃO  
 Remove a regra de validação da tabela.  
  
 Adicionar a chave primária *eExpression3*marca *TagName2*  
 Adiciona um índice primário na tabela. *eExpression3* Especifica a expressão de chave de índice primário, e *TagName2* Especifica o nome da marca do índice primário. Nomes de marca de índice podem conter até 10 caracteres. Se marca *TagName2* for omitido e *eExpression3* é um único campo, a marca de índice primário tem o mesmo nome que o campo especificado na *eExpression3*.  
  
 REMOVER CHAVE PRIMÁRIA  
 Remove o índice primário e sua marca de índice. Como uma tabela pode ter somente uma chave primária, não é necessário especificar o nome da chave primária. Remover o índice primário também exclui a todos os parceiros persistentes com base na chave primária.  
  
 Adicionar UNIQUE *eExpression4*[marca *TagName3*]  
 Adiciona um índice de candidato à tabela. *eExpression4* Especifica a expressão de chave de índice de candidato, e *TagName3* Especifica o nome da marca de índice do candidato. Nomes de marca de índice podem conter até 10 caracteres. Se você omitir a marca *TagName3* e, se *eExpression4* é um único campo, a marca de índice do candidato tem o mesmo nome que o campo especificado na *eExpression4*.  
  
 MENU de marca exclusivo *TagName4*  
 Remove o índice da candidata e sua marca de índice. Como uma tabela pode ter várias chaves de candidato, você deve especificar o nome da marca de índice do candidato.  
  
 Adicionar a chave estrangeira [ *eExpression5*] marca *TagName4*  
 Adiciona um índice (não primária) externo à tabela. *eExpression5* Especifica a expressão de chave estrangeira de índice, e *TagName4* Especifica o nome da marca externa do índice. Nomes de marca de índice podem conter até 10 caracteres.  
  
 As referências *TableName2*[marca *TagName5*]  
 Especifica a tabela pai para o qual é estabelecida uma relação de persistente. Marcação include *TagName5* para estabelecer uma relação com base em uma marca de índice existente para a tabela pai. Nomes de marca de índice podem conter até 10 caracteres. Se você omitir a marca *TagName5*, a relação é estabelecida usando a marca de índice primário da tabela pai.  
  
 MARCA de chave estrangeira SOLTAR *TagName6*[Salvar]  
 Exclui uma marca cujo índice é de chave estrangeira *TagName6*. Se você omitir o salvamento, a marca de índice é excluída do índice estrutural. Incluir Salvar para impedir a exclusão da marca do índice do índice estrutural.  
  
 COLUNA de RENOMEAÇÃO *FieldName4*TO *FieldName5*  
 Permite que você altere o nome de um campo na tabela. *FieldName4* Especifica o nome do campo que é renomeado. *FieldName5* Especifica o novo nome do campo.  
  
> [!CAUTION]  
>  Tenha cuidado ao renomear campos de tabela porque as expressões de índice, as regras de validação de campo e tabela, comandos e funções podem fazer referência os nomes de campo original.  
  
 NOVALIDATE  
 Especifica que o Visual FoxPro permite que alterações sejam feitas para a estrutura da tabela; Essas alterações podem violar a integridade dos dados na tabela. Por padrão, Visual FoxPro impede que ALTER TABLE fazendo alterações que violam a integridade dos dados na tabela. Inclua NOVALIDATE para substituir esse comportamento padrão.  
  
## <a name="remarks"></a>Comentários  
 ALTER TABLE pode ser usado para modificar a estrutura de uma tabela que não foi adicionada a um banco de dados. No entanto, o Visual FoxPro gerará um erro se você incluir o padrão, a chave estrangeira, a chave primária, a referências ou cláusulas conjunto ao modificar uma tabela livre.  
  
 ALTER TABLE pode recriar a tabela, criando um novo cabeçalho de tabela e anexando registros para o cabeçalho da tabela. Por exemplo, alterar o tipo ou a largura de um campo pode causar a tabela a serem recriados.  
  
 Depois que uma tabela é recriada, as regras de validação de campo são executadas para todos os campos cujo tipo ou a largura são alterados. Se você alterar o tipo ou a largura de qualquer campo na tabela, a regra de tabela é executada.  
  
 Se você modificar as regras de validação de campo ou uma tabela para uma tabela que tem registros, do Visual FoxPro testa as regras de validação de campo ou uma tabela nova com os dados existentes e emite um aviso na primeira ocorrência de uma regra de validação do campo ou uma tabela ou de uma violação de gatilho.  
  
 Se a tabela que você modificar está em um banco de dados, ALTER TABLE - SQL requer o uso exclusivo do banco de dados. Para abrir um banco de dados para uso exclusivo, incluem exclusivo no banco de dados aberto.  
  
## <a name="see-also"></a>Consulte também  
 [CREATE TABLE – comando SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [Comando INDEX](../../odbc/microsoft/index-command.md)

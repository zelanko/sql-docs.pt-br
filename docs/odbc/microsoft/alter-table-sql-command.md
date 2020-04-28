---
title: ALTER TABLE-comando SQL | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 587d721522503f9b392bb8be7433850fd7449efb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304707"
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
  
 ALTER [COLUMN] *FieldName1*  
 Especifica o nome de um campo existente a ser modificado.  
  
 *FieldType* [( *NFieldWidth* [, *nPrecision*]])  
 Especifica o tipo de campo, a largura do campo e a precisão do campo (número de casas decimais) para um campo novo ou modificado.  
  
 *FieldType* é uma única letra que indica o tipo de [dados](../../odbc/microsoft/visual-foxpro-field-data-types.md)do campo. Alguns tipos de dados de campo exigem que você especifique *nFieldWidth* ou *nPrecision* ou ambos.  
  
 *nFieldWidth* e *nPrecision* são ignorados para os tipos D, G, I, L, M, P, T e Y. Por padrão, *nPrecision* será zero (sem casas decimais) se *nPrecision* não estiver incluído para os tipos B, F ou N.  
  
 NULL &#124; NOT NULL  
 Permite ou impede valores nulos no campo.  
  
 Se você omitir NULL e NOT NULL, a configuração atual de SET NULL determinará se os valores nulos são permitidos no campo. No entanto, se você omitir NULL e NOT NULL e incluir a chave primária ou a cláusula UNIQUE, a configuração atual de SET NULL será ignorada e o campo não será nulo por padrão.  
  
 VERIFICAR *lExpression1*  
 Especifica uma regra de validação para o campo. *lExpression1* deve ser avaliado como uma expressão lógica e pode ser uma função definida pelo usuário ou um procedimento armazenado. Sempre que um registro em branco é anexado, a regra de validação é verificada. Um erro será gerado se a regra de validação não permitir um valor de campo em branco em um registro anexado.  
  
 ERRO *cMessageText1*  
 Especifica a mensagem de erro exibida quando a regra de validação de campo gera um erro.  
  
 *EEXPRESSION1* padrão  
 Especifica um valor padrão para o campo. O tipo de dados de *eExpression1* deve ser o mesmo que o tipo de dados para o campo.  
  
 PRIMARY KEY  
 Cria uma marca de índice primário. A marca de índice tem o mesmo nome que o campo.  
  
 UNIQUE  
 Cria uma marca de índice candidato com o mesmo nome que o campo.  
  
> [!NOTE]  
>  Os índices candidatos (criados incluindo a opção exclusiva, fornecidos para compatibilidade com ANSI em ALTER TABLE ou CREATE TABLE) diferem dos índices criados usando a opção UNIQUE no comando de índice. Um índice criado usando UNIQUE no comando de índice permite chaves de índice duplicadas; os índices candidatos não permitem chaves de índice duplicadas.  
  
 Valores nulos e registros duplicados não são permitidos em um campo usado para um índice primário ou candidato.  
  
 Se você estiver criando um novo campo usando adicionar coluna, o Visual FoxPro não gerará um erro se você criar um índice primário ou candidato para um campo que dê suporte a valores nulos. No entanto, o Visual FoxPro gerará um erro se você tentar inserir um valor nulo ou duplicado em um campo usado para um índice primário ou candidato.  
  
 Se você estiver modificando um campo existente e a expressão de índice principal ou candidato consistir em campos na tabela, o Visual FoxPro verificará os campos para ver se eles contêm valores nulos ou duplicados. Se isso for feito, o Visual FoxPro gerará um erro e a tabela não será alterada.  
  
 FAZ referência a *TagName1* de marca *TableName2*  
 Especifica a tabela pai à qual uma relação persistente é estabelecida. A marca *TagName1* especifica a marca de índice da tabela pai na qual a relação se baseia. Os nomes de marcas de índice podem conter até 10 caracteres.  
  
 NOCPTRANS  
 Impede a conversão em uma página de código diferente para campos de caractere e memorando. Se a tabela for convertida em outra página de código, os campos para os quais NOCPTRANS foi especificado não serão traduzidos. NOCPTRANS pode ser especificado somente para campos de caracteres e memorando.  
  
 O exemplo a seguir cria uma tabela chamada MyTable que contém dois campos de caractere e dois campos de memorando. O segundo campo de caractere, char2 e o segundo campo de memorando, memo2, incluem NOCPTRANS para impedir a tradução.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 ALTER [COLUMN] *FieldName2*  
 Especifica o nome de um campo existente a ser modificado.  
  
 DEFINIR *EEXPRESSION2* padrão  
 Especifica um novo valor padrão para um campo existente. O tipo de dados de *eExpression2* deve ser o mesmo que o tipo de dados para o campo.  
  
 DEFINIR *lExpression2* de verificação  
 Especifica uma nova regra de validação para um campo existente. *lExpression2* deve ser avaliado como uma expressão lógica e pode ser uma função definida pelo usuário ou um procedimento armazenado.  
  
 ERRO *cMessageText2*  
 Especifica a mensagem de erro exibida quando a regra de validação de campo gera um erro. A mensagem é exibida somente quando os dados são alterados em uma janela de navegação ou de edição.  
  
 DROP DEFAULT  
 Remove o valor padrão de um campo existente.  
  
 DESCARTAR VERIFICAÇÃO  
 Remove a regra de validação de um campo existente.  
  
 DROP [coluna] *FieldName3*  
 Especifica um campo a ser removido da tabela. A remoção de um campo da tabela também remove a configuração de valor padrão do campo e a regra de validação de campo.  
  
 Se as expressões de chave de índice ou de gatilho fizerem referência ao campo, as expressões se tornarão inválidas quando o campo for removido. Nesse caso, um erro não é gerado quando o campo é removido, mas a chave de índice ou as expressões de gatilho inválidas gerarão erros em tempo de execução.  
  
 DEFINIR *lExpression3* de verificação  
 Especifica a regra de validação de tabela. *lExpression3* deve ser avaliado como uma expressão lógica e pode ser uma função definida pelo usuário ou um procedimento armazenado.  
  
 ERRO *cMessageText3*  
 Especifica a mensagem de erro exibida quando a regra de validação de tabela gera um erro. A mensagem é exibida somente quando os dados são alterados em uma janela de navegação ou de edição.  
  
 DESCARTAR VERIFICAÇÃO  
 Remove a regra de validação da tabela.  
  
 ADICIONAR marca *eExpression3*de chave primária *TagName2*  
 Adiciona um índice primário à tabela. *eExpression3* especifica a expressão de chave de índice primária e *TagName2* especifica o nome da marca de índice primário. Os nomes de marcas de índice podem conter até 10 caracteres. Se a TAG *TagName2* for omitida e *eExpression3* for um único campo, a marca de índice principal terá o mesmo nome que o campo especificado em *eExpression3*.  
  
 DESCARTAR CHAVE PRIMÁRIA  
 Remove o índice primário e sua marca de índice. Como uma tabela pode ter apenas uma chave primária, não é necessário especificar o nome da chave primária. A remoção do índice primário também exclui todas as relações persistentes com base na chave primária.  
  
 Adicionar *EEXPRESSION4*exclusivo [tag *TagName3*]  
 Adiciona um índice candidato à tabela. *eExpression4* especifica a expressão de chave de índice candidato e *TagName3* especifica o nome da marca de índice candidato. Os nomes de marcas de índice podem conter até 10 caracteres. Se você omitir a marca *TagName3* e se *eExpression4* for um único campo, a marca de índice candidato terá o mesmo nome que o campo especificado em *eExpression4*.  
  
 DROP ununique TAG *TagName4*  
 Remove o índice candidato e sua marca de índice. Como uma tabela pode ter várias chaves candidatas, você deve especificar o nome da marca de índice candidato.  
  
 Adicionar chave estrangeira [ *eExpression5*] marca *TagName4*  
 Adiciona um índice externo (não primário) à tabela. *eExpression5* especifica a expressão de chave de índice estrangeiro e *TagName4* especifica o nome da marca de índice estrangeiro. Os nomes de marcas de índice podem conter até 10 caracteres.  
  
 REFERENCEs *TableName2*[tag *TagName5*]  
 Especifica a tabela pai à qual uma relação persistente é estabelecida. Inclua a marca *TagName5* para estabelecer uma relação com base em uma marca de índice existente para a tabela pai. Os nomes de marcas de índice podem conter até 10 caracteres. Se você omitir a marca *TagName5*, a relação será estabelecida usando a marca de índice principal da tabela pai.  
  
 REMOVER marca de chave estrangeira *TagName6*[salvar]  
 Exclui uma chave estrangeira cuja marca de índice é *TagName6*. Se você omitir salvar, a marca de índice será excluída do índice estrutural. Incluir salvar para evitar a exclusão da marca de índice do índice estrutural.  
  
 Renomear a coluna *FieldName4*para *FieldName5*  
 Permite alterar o nome de um campo na tabela. *FieldName4* especifica o nome do campo que é renomeado. *FieldName5* especifica o novo nome do campo.  
  
> [!CAUTION]  
>  Tenha cuidado ao renomear campos de tabela porque expressões de índice, regras de validação de campo e tabela, comandos e funções podem fazer referência aos nomes de campo originais.  
  
 NOVALIDATE  
 Especifica que o Visual FoxPro permite que as alterações sejam feitas na estrutura da tabela; essas alterações podem violar a integridade dos dados na tabela. Por padrão, o Visual FoxPro impede que ALTER TABLE faça alterações que violem a integridade dos dados na tabela. Inclua novalidate para substituir esse comportamento padrão.  
  
## <a name="remarks"></a>Comentários  
 ALTER TABLE pode ser usado para modificar a estrutura de uma tabela que não foi adicionada a um banco de dados. No entanto, o Visual FoxPro gerará um erro se você incluir as cláusulas padrão, FOREIGN KEY, PRIMARY KEY, REFERENCEs ou SET ao modificar uma tabela gratuita.  
  
 ALTER TABLE pode recriar a tabela criando um novo cabeçalho de tabela e acrescentando registros ao cabeçalho da tabela. Por exemplo, alterar o tipo ou a largura de um campo pode fazer com que a tabela seja recriada.  
  
 Depois que uma tabela é recriada, as regras de validação de campo são executadas para todos os campos cujo tipo ou largura seja alterado. Se você alterar o tipo ou a largura de qualquer campo na tabela, a regra de tabela será executada.  
  
 Se você modificar as regras de validação de campo ou tabela para uma tabela que tem registros, o Visual FoxPro testará as novas regras de validação de campo ou tabela em relação aos dados existentes e emitirá um aviso na primeira ocorrência de uma regra de validação de campo ou de tabela ou de uma violação de gatilho.  
  
 Se a tabela que você modificar estiver em um banco de dados, ALTER TABLE-SQL exigirá o uso exclusivo do banco de dados. Para abrir um banco de dados para uso exclusivo, inclua exclusivo no banco de dados aberto.  
  
## <a name="see-also"></a>Consulte Também  
 [Comando CREATE TABLE-SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [Comando INDEX](../../odbc/microsoft/index-command.md)

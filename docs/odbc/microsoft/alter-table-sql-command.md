---
title: TABELA ALTER - Comando SQL | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304707"
---
# <a name="alter-table---sql-command"></a>ALTER TABLE – comando SQL
Programaticamente modifica a estrutura de uma tabela.  
  
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
 *Nome da tabela1*  
 Especifica o nome da tabela cuja estrutura é modificada.  
  
 ADICIONAR [COLUNA] *Nome de campo1*  
 Especifica o nome do campo a ser adicionado.  
  
 ALTER [COLUNA] *Nome de campo1*  
 Especifica o nome de um campo existente para modificar.  
  
 *FieldType* *[(nFieldWidth* *[nPrecision]])*  
 Especifica o tipo de campo, a largura do campo e a precisão do campo (número de casas decimais) para um campo novo ou modificado.  
  
 *FieldType* é uma única letra que indica o tipo de dados do [campo](../../odbc/microsoft/visual-foxpro-field-data-types.md). Alguns tipos de dados de campo exigem que você especifique *nFieldWidth* ou *nPrecision* ou ambos.  
  
 *nFieldWidth* e *nPrecision* são ignorados para os tipos D, G, I, L, M, P, T e Y. Por padrão, *nPrecision* é zero (sem casas decimais) se *nPrecision* não estiver incluído para os tipos B, F ou N.  
  
 NULL &#124; NOT NULL  
 Permite ou impede valores nulos no campo.  
  
 Se você omitir NUU E NÃO NULO, a configuração atual do SET NULL determina se valores nulos são permitidos no campo. No entanto, se você omitir NULA e NÃO NULA e incluir a chave primária ou cláusula ÚNICA, a configuração atual do SET NULL será ignorada e o campo NÃO será NULO por padrão.  
  
 CHECK *lExpression1*  
 Especifica uma regra de validação para o campo. *lExpression1* deve avaliar uma expressão lógica e pode ser uma função definida pelo usuário ou um procedimento armazenado. Sempre que um registro em branco é anexado, a regra de validação é verificada. Um erro é gerado se a regra de validação não permitir um valor de campo em branco em um registro anexado.  
  
 ERRO *cMessageText1*  
 Especifica a mensagem de erro exibida quando a regra de validação de campo gera um erro.  
  
 EExpression *1* PADRÃO  
 Especifica um valor padrão para o campo. O tipo de dados do *eExpression1* deve ser o mesmo do tipo de dados para o campo.  
  
 PRIMARY KEY  
 Cria uma tag de índice primário. A etiqueta de índice tem o mesmo nome do campo.  
  
 UNIQUE  
 Cria uma tag de índice de candidato com o mesmo nome do campo.  
  
> [!NOTE]  
>  Os índices dos candidatos (criados pela inclusão da opção UNIQUE, prevista para compatibilidade ANSI em TABELA ALTER ou TABELA CRIAR) diferem dos índices criados usando a opção UNIQUE no comando INDEX. Um índice criado usando UNIQUE no comando INDEX permite chaves de índice duplicadas; índices de candidatos não permitem chaves de índice duplicadas.  
  
 Valores nulos e registros duplicados não são permitidos em um campo que é usado para um índice primário ou candidato.  
  
 Se você estiver criando um novo campo usando ADD COLUMN, o Visual FoxPro não gerará um erro se você criar um índice de candidato sumido ou principal para um campo que suporte valores nulos. No entanto, o Visual FoxPro gerará um erro se você tentar inserir um valor nulo ou duplicado em um campo que é usado para um índice primário ou candidato.  
  
 Se você estiver modificando um campo existente e a expressão de índice principal ou candidato consiste em campos na tabela, o Visual FoxPro verifica os campos para ver se eles contêm valores nulos ou registros duplicados. Se o fizerem, o Visual FoxPro gera um erro e a tabela não é alterada.  
  
 REFERÊNCIAS *TableName2* *TAGName1*  
 Especifica a tabela pai para a qual uma relação persistente é estabelecida. Tag *TagName1* especifica a tag de índice da tabela pai na qual a relação é baseada. Os nomes das marcas de índice podem conter até 10 caracteres.  
  
 NOCPTRANS  
 Impede a tradução para uma página de código diferente para campos de caracteres e memorandos. Se a tabela for convertida em outra página de código, os campos para os quais o NOCPTRANS foi especificado não serão traduzidos. Nocptrans pode ser especificado apenas para os campos de caracteres e memorandos.  
  
 O exemplo a seguir cria uma tabela chamada mytable que contém dois campos de caracteres e dois campos de memorando. O segundo campo de caracteres, char2, e o segundo campo de memorando, memo2, incluem NOCPTRANS para impedir a tradução.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 ALTER [COLUNA] *Nome de campo2*  
 Especifica o nome de um campo existente para modificar.  
  
 DEFINIR *EExpression2* PADRÃO  
 Especifica um novo valor padrão para um campo existente. O tipo de dados do *eExpression2* deve ser o mesmo do tipo de dados para o campo.  
  
 DEFINIR VERIFICAR *lExpression2*  
 Especifica uma nova regra de validação para um campo existente. *lExpression2* deve avaliar para uma expressão lógica e pode ser uma função definida pelo usuário ou um procedimento armazenado.  
  
 ERRO *cMessageText2*  
 Especifica a mensagem de erro exibida quando a regra de validação de campo gera um erro. A mensagem é exibida somente quando os dados são alterados dentro de uma janela Procurar ou Editar.  
  
 DROP DEFAULT  
 Remove o valor padrão de um campo existente.  
  
 VERIFICAÇÃO DE QUEDA  
 Remove a regra de validação de um campo existente.  
  
 DROP [COLUNA] *FieldName3*  
 Especifica um campo para remover da tabela. A remoção de um campo da tabela também remove a configuração de valor padrão do campo e a regra de validação de campo.  
  
 Se a tecla de índice ou as expressões de gatilho fizerem referência ao campo, as expressões se tornarão inválidas quando o campo é removido. Neste caso, um erro não é gerado quando o campo é removido, mas a chave de índice inválida ou as expressões de gatilho gerarão erros no tempo de execução.  
  
 DEFINIR VERIFICAR *lExpression3*  
 Especifica a regra de validação da tabela. *lExpression3* deve avaliar para uma expressão lógica e pode ser uma função definida pelo usuário ou um procedimento armazenado.  
  
 ERRO *cMessageText3*  
 Especifica a mensagem de erro exibida quando a regra de validação da tabela gera um erro. A mensagem é exibida somente quando os dados são alterados dentro de uma janela Procurar ou Editar.  
  
 VERIFICAÇÃO DE QUEDA  
 Remove a regra de validação da tabela.  
  
 ADICIONAR TECLa PRIMÁRIA *eExpression3* *TAGName2*  
 Adiciona um índice primário à tabela. *O eExpression3* especifica a expressão da chave de índice principal e *o TagName2* especifica o nome da tag de índice principal. Os nomes das marcas de índice podem conter até 10 caracteres. Se *tagName2* for omitido e *eExpression3* for um único campo, a tag de índice principal tem o mesmo nome do campo especificado no *eExpression3*.  
  
 SOLTAR A CHAVE PRIMÁRIA  
 Remove o índice primário e sua etiqueta de índice. Como uma tabela pode ter apenas uma chave primária, não é necessário especificar o nome da chave principal. A remoção do índice primário também exclui quaisquer relações persistentes com base na chave primária.  
  
 ADICIONAR *EExpression4*EXCLUSIVO *[TAGName3*]  
 Adiciona um índice de candidatos à mesa. *O eExpression4* especifica a expressão da chave do índice do candidato e *o TagName3* especifica o nome da tag índice do candidato. Os nomes das marcas de índice podem conter até 10 caracteres. Se você omitir *TAGName3* e se *eExpression4* for um único campo, a tag de índice do candidato tem o mesmo nome do campo especificado no *eExpression4*.  
  
 SOLTAR *TAGTAG'S4 EXCLUSIVOTAGNAME4*  
 Remove o índice do candidato e sua etiqueta de índice. Como uma tabela pode ter várias chaves de candidato, você deve especificar o nome da tag de índice do candidato.  
  
 ADICIONAR TECLA ESTRANGEIRA [ *eExpression5* *]TAGName4*  
 Adiciona um índice estrangeiro (não primário) à tabela. *o eExpression5* especifica a expressão da chave de índice estrangeiro, e *o TagName4* especifica o nome da tag de índice estrangeiro. Os nomes das marcas de índice podem conter até 10 caracteres.  
  
 REFERÊNCIAS *TableName2*[TAG *TagName5*]  
 Especifica a tabela pai para a qual uma relação persistente é estabelecida. Inclua *TAGName5* para estabelecer uma relação com base em uma tag de índice existente para a tabela pai. Os nomes das marcas de índice podem conter até 10 caracteres. Se você omitir *TAGName5,* a relação será estabelecida usando a tag de índice principal da tabela pai.  
  
 SOLTAR TAGNAME DE TECA *ESTRANGEIRA6*[SALVAR]  
 Exclui uma chave estrangeira cuja tag de índice é *TagName6*. Se você omitir SAVE, a tag de índice será excluída do índice estrutural. Inclua SAVE para evitar a exclusão da etiqueta de índice do índice estrutural.  
  
 RENOMEAR COLUNA *Nome de Campo4*PARA *FieldName5*  
 Permite alterar o nome de um campo na tabela. *FieldName4* especifica o nome do campo que é renomeado. *FieldName5* especifica o novo nome do campo.  
  
> [!CAUTION]  
>  O cuidado de exercício ao renomear campos de tabela porque expressões de índice, regras de validação de campo e tabela, comandos e funções podem fazer referência aos nomes de campo originais.  
  
 Novalidate  
 Especifica que o Visual FoxPro permite que sejam feitas alterações na estrutura da tabela; essas alterações podem violar a integridade dos dados na tabela. Por padrão, o Visual FoxPro impede que a TABELA ALTER esuas alterações que violem a integridade dos dados na tabela. Inclua NOVALIDATE para substituir esse comportamento padrão.  
  
## <a name="remarks"></a>Comentários  
 TABELA ALTER pode ser usada para modificar a estrutura de uma tabela que não foi adicionada a um banco de dados. No entanto, o Visual FoxPro gera um erro se você incluir as cláusulas DEFAULT, FOREIGN KEY, PRIMARY KEY, REFERENCES ou SET ao modificar uma tabela gratuita.  
  
 ALTER TABLE pode reconstruir a tabela criando um novo cabeçalho de tabela e anexando registros para o cabeçalho da tabela. Por exemplo, alterar o tipo ou a largura de um campo pode fazer com que a tabela seja reconstruída.  
  
 Depois que uma tabela é reconstruída, as regras de validação de campo são executadas para quaisquer campos cujo tipo ou largura seja alterado. Se você alterar o tipo ou a largura de qualquer campo da tabela, a regra da tabela será executada.  
  
 Se você modificar as regras de validação de campo ou tabela para uma tabela que tenha registros, o Visual FoxPro testa as novas regras de validação de campo ou tabela contra os dados existentes e emite uma advertência sobre a primeira ocorrência de uma regra de validação de campo ou tabela ou de uma violação de gatilho.  
  
 Se a tabela que você modificar estiver em um banco de dados, ALTER TABLE - SQL requer uso exclusivo do banco de dados. Para abrir um banco de dados para uso exclusivo, inclua EXCLUSIVO em BANCO DE DADOS ABERTO.  
  
## <a name="see-also"></a>Consulte Também  
 [CRIAR TABELA - Comando SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [Comando INDEX](../../odbc/microsoft/index-command.md)

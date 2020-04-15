---
title: CRIAR TABELA - Comando SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE TABLE [ODBC]
ms.assetid: be2143ba-fc16-42c9-84f7-8985cd924860
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dfc80a56a021b1bfeda38115e79f7086632900c8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298686"
---
# <a name="create-table---sql-command"></a>CREATE TABLE – comando SQL
Cria uma tabela com os campos especificados.  
  
 O Visual FoxPro ODBC Driver suporta a sintaxe nativa visual foxpro para este comando. Para obter informações específicas do motorista, consulte **Observações do motorista**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE TABLE | DBF TableName1 [NAME LongTableName] [FREE]  
   (FieldName1FieldType [(nFieldWidth [, nPrecision])]  
      [NULL | NOT NULL]   
      [CHECK lExpression1 [ERROR cMessageText1]]  
      [DEFAULT eExpression1]  
      [PRIMARY KEY | UNIQUE]  
      [REFERENCES TableName2 [TAG TagName1]]  
      [NOCPTRANS]  
   [, FieldName2 ...]  
      [, PRIMARY KEY eExpression2 TAG TagName2  
      |, UNIQUE eExpression3 TAG TagName3]  
      [, FOREIGN KEY eExpression4 TAG TagName4 [NODUP]  
            REFERENCES TableName3 [TAG TagName5]]  
      [, CHECK lExpression2 [ERROR cMessageText2]])  
| FROM ARRAY ArrayName  
```  
  
## <a name="arguments"></a>Argumentos  
 CRIAR TABELA &#124; DBF *TableName1*  
 Especifica o nome da tabela a ser criada. As opções TABLE e DBF são idênticas.  
  
 NOME *LongTableName*  
 Especifica um nome longo para a tabela. Um nome de tabela longo só pode ser especificado quando um banco de dados está aberto, porque nomes de tabelas longas são armazenados em bancos de dados.  
  
 Nomes longos podem conter até 128 caracteres e podem ser usados no lugar de nomes de arquivos curtos no banco de dados.  
  
 FREE  
 Especifica que a tabela não será adicionada a um banco de dados aberto. Grátis não é necessário se um banco de dados não estiver aberto.  
  
 *(FieldName1 FieldType* *[(nFieldWidth* [, *nPrecision*]]]  
 Especifica o nome do campo, o tipo de campo, a largura do campo e a precisão do campo (número de casas decimais), respectivamente.  
  
 *FieldType* é uma única letra que indica o tipo de dados do [campo](../../odbc/microsoft/visual-foxpro-field-data-types.md). Alguns tipos de dados de campo exigem que você especifique *nFieldWidth* ou *nPrecision* ou ambos.  
  
 *nFieldWidth* e *nPrecision* são ignorados para os tipos D, G, I, L, M, P, T e Y. *nA precisão* é padrão para zero (sem casas decimais) se *nPrecision* não estiver incluído para os tipos B, F ou N.  
  
 NULO  
 Permite valores nulos no campo.  
  
 NOT NULL  
 Previne valores nulos no campo.  
  
 Se você omitir NUU E NÃO NULO, a configuração atual do SET NULL determina se valores nulos são permitidos no campo. No entanto, se você omitir NULA e NÃO NULA e incluir a chave primária ou cláusula ÚNICA, a configuração atual do SET NULL será ignorada e o campo não será nulo.  
  
 CHECK *lExpression1*  
 Especifica uma regra de validação para o campo. *lExpression1* pode ser uma função definida pelo usuário. Sempre que um registro em branco é anexado, a regra de validação é verificada. Um erro é gerado se a regra de validação não permitir um valor de campo em branco em um registro anexado.  
  
 ERRO *cMessageText1*  
 Especifica a mensagem de erro que o Visual FoxPro exibe quando a regra de campo gera um erro. A mensagem é exibida somente quando os dados são alterados dentro de uma janela Procurar ou de editar.  
  
 EExpression *1* PADRÃO  
 Especifica um valor padrão para o campo. O tipo de dados do *eExpression1* deve ser o mesmo do tipo de dados do campo.  
  
 PRIMARY KEY  
 Cria um índice primário para o campo. A tag de índice primário tem o mesmo nome do campo.  
  
 UNIQUE  
 Cria um índice de candidatos para o campo. A tag de índice do candidato tem o mesmo nome do campo.  
  
> [!NOTE]  
>  Os índices dos candidatos (criados por incluir a opção UNIQUE em TABELA DE CRIAÇÃO ou TABELA ALTER - SQL) não são os mesmos que os índices criados com a opção UNIQUE no comando INDEX. Um índice criado com a opção UNIQUE no comando INDEX permite chaves de índice duplicadas; índices de candidatos não permitem chaves de índice duplicadas. Consulte [INDEX](../../odbc/microsoft/index-command.md) para obter informações adicionais sobre sua opção UNIQUE.  
  
 Valores nulos e registros duplicados não são permitidos em um campo usado para um índice primário ou candidato. No entanto, o Visual FoxPro não gerará um erro se você criar um índice de candidato súdito ou principal para um campo que suporte valores nulos. Visual FoxPro gerará um erro se você tentar inserir um valor nulo ou duplicado em um campo usado para um índice primário ou candidato.  
  
 REFERÊNCIAS *Nomede tabela2*[TagName1 ] *TagName1*  
 Especifica a tabela pai para a qual uma relação persistente é estabelecida. Se você omitir *TAGName1,* a relação será estabelecida usando a tecla de índice principal da tabela pai. Se a tabela pai não tiver um índice primário, o Visual FoxPro gerará um erro.  
  
 Inclua *TAGName1* para estabelecer uma relação com base em uma tag de índice existente para a tabela pai. Os nomes das marcas de índice podem conter até 10 caracteres.  
  
 A mesa dos pais não pode ser uma mesa livre.  
  
 NOCPTRANS  
 Impede a tradução para uma página de código diferente para campos de caracteres e memorandos. Se a tabela for convertida em outra página de código, os campos para os quais o NOCPTRANS foi especificado não serão traduzidos. Nocptrans pode ser especificado apenas para os campos de caracteres e memorandos.  
  
 O exemplo a seguir cria uma tabela chamada mytable contendo dois campos de caracteres e dois campos de memorando. O segundo campo de caracteres, char2, e o segundo campo de memorando, memo2, incluem NOCPTRANS para impedir a tradução.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 TECLa primária *eExpression2* *TAGName2*  
 Especifica um índice primário para criar. *o eExpression2* especifica qualquer campo ou combinação de campos na tabela. TAG *TagName2* especifica o nome da tag de índice principal criada. Os nomes das marcas de índice podem conter até 10 caracteres.  
  
 Como uma tabela pode ter apenas um índice primário, você não pode incluir esta cláusula se você já criou um índice primário para um campo. Visual FoxPro gera um erro se você incluir mais de uma cláusula DE CHAVE PRIMÁRIA na TABELA CRIAR.  
  
 TAG *Name3* *eExpression3*EXCLUSIVO  
 Cria um índice de candidatos. *o eExpression3* especifica qualquer campo ou combinação de campos na tabela. No entanto, se você criou um índice primário com uma das opções PRIMARY KEY, você não poderá incluir o campo especificado para o índice principal. TAG *TagName3* especifica um nome de tag para a tag candidate index que foi criada. Os nomes das marcas de índice podem conter até 10 caracteres.  
  
 Uma tabela pode ter vários índices de candidatos.  
  
 TECLA *ESTRANGEIRA eExpression4* *TAGName4*[NODUP]  
 Cria um índice estrangeiro (não primário) e estabelece uma relação com uma tabela pai. *O eExpression4* especifica a expressão da chave de índice estrangeiro, e *o TagName4* especifica o nome da tag de tecla de índice estrangeiro criada. Os nomes das marcas de índice podem conter até 10 caracteres. Inclua nodup para criar um índice estrangeiro candidato.  
  
 Você pode criar vários índices estrangeiros para a tabela, mas as expressões de índice sumário devem especificar diferentes campos na tabela.  
  
 REFERÊNCIAS *TableName3*[TAG *TagName5*]  
 Especifica a tabela pai para a qual uma relação persistente é estabelecida. Inclua *TAGName5* para estabelecer uma relação com base em uma tag de índice para a tabela pai. Os nomes das marcas de índice podem conter até 10 caracteres. Por padrão, se você omitir *TAGName5,* a relação será estabelecida usando a chave de índice principal da tabela pai.  
  
 VERIFIQUE *eExpression2*[ERROR *cMessageText2*]  
 Especifica a regra de validação da tabela. ERRO *cMessageText2* especifica a mensagem de erro que o Visual FoxPro exibe quando a regra de validação da tabela é executada. A mensagem é exibida somente quando os dados são alterados dentro de uma janela Procurar ou editar.  
  
 DE ARRAY *ArrayName*  
 Especifica o nome de uma matriz existente cujo conteúdo é o nome, tipo, precisão e escala para cada campo na tabela. O conteúdo da matriz pode ser definido com a função **AFIELDS**( ).  
  
## <a name="remarks"></a>Comentários  
 A nova tabela é aberta na área de trabalho mais baixa disponível e pode ser acessada por seu pseudônimo. A nova tabela é aberta exclusivamente, independentemente da configuração atual do SET EXCLUSIVE.  
  
 Se um banco de dados estiver aberto e você não incluir a cláusula FREE, a nova tabela será adicionada ao banco de dados. Não é possível criar uma nova tabela com o mesmo nome de uma tabela no banco de dados.  
  
 Se um banco de dados estiver aberto, CREATE TABLE - SQL requer uso exclusivo do banco de dados. Para abrir um banco de dados para uso exclusivo, inclua EXCLUSIVO em BANCO DE DADOS ABERTO.  
  
 Se um banco de dados não estiver aberto quando você criar a nova tabela, incluindo as cláusulas NOME, CHECK, DEFAULT, FOREIGN KEY, PRIMARY KEY ou REFERENCES, gerará um erro.  
  
> [!NOTE]  
>  A sintaxe CREATE TABLE usa commas para separar certas opções de TABELA DE CRIAÇÃO. Além disso, a cláusula NULL, NOT NULL, CHECK, DEFAULT, PRIMARY KEY e UNIQUE deve ser colocada dentro dos parênteses que contenham as definições da coluna.  
  
## <a name="driver-remarks"></a>Observações do motorista  
 Quando seu aplicativo envia a declaração ODBC SQL CRIAR TABELA para a fonte de dados, o Driver Visual FoxPro ODBC traduz o comando para o comando Visual FoxProCREATE TABLE usando a sintaxe mostrada na tabela a seguir.  
  
|Sintaxe ODBC|Sintaxe Visual FoxPro|  
|-----------------|--------------------------|  
|CRIAR *TABELA nome de tabela-base*<br /><br /> (tipo*de dados identificador de coluna*<br /><br /> [NÃO NULO]<br /><br /> [,*tipo de dados identificador de coluna*<br /><br /> [NÃO NULO] ...)|CRIAR TABELA *Nomede tabela1* [NOME *LongTableName*]<br /><br /> (*Fieldname1* *FieldType*<br /><br /> [(*nFieldWidth* [, *nPrecision*]]]<br /><br /> [NÃO NULO])|  
  
 Quando você cria uma tabela usando o driver, o driver fecha a tabela imediatamente após a criação para permitir o acesso à tabela por outros usuários. Isso difere do Visual FoxPro, o que deixa a mesa aberta exclusivamente após a criação. No entanto, se um procedimento armazenado na sua fonte de dados contendo uma declaração CREATE TABLE for executado, a tabela será deixada aberta.  
  
 Se a fonte de dados for um banco de dados (arquivo.dbc), o Driver Visual FoxPro ODBC criará uma tabela chamada *LongTableName* com o mesmo nome do *nome da tabela base*.  
  
### <a name="using-data-definition-language-ddl"></a>Usando o DDL (Data Definition Language, linguagem de definição de dados)  
 Não é possível incluir o DDL nos seguintes lugares:  
  
-   Em uma declaração SQL em lote que requer uma transação  
  
-   No modo de confirmação manual, após uma declaração que exigia uma transação, a menos que seu aplicativo primeiro ligue **para o SQLTransact**.  
  
 Por exemplo, se você quiser criar uma tabela temporária, você deve criar a tabela antes de iniciar a declaração exigindo uma transação. Se você incluir a declaração CREATE TABLE em uma declaração SQL em lote que requer uma transação, o driver reameda uma mensagem de erro.  
  
## <a name="see-also"></a>Consulte Também  
 [TABELA ALTER - Comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [Tipos de dados suportados (driver Visual FoxPro ODBC)](../../odbc/microsoft/supported-data-types-visual-foxpro-odbc-driver.md)   
 [INSERT - Comando SQL](../../odbc/microsoft/insert-sql-command.md)   
 [SELECT – comando SQL](../../odbc/microsoft/select-sql-command.md)

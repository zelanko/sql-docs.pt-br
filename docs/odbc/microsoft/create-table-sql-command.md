---
title: Comando CREATE TABLE-SQL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f979ccb5a44ada8e86424e0f6134f39d28a021d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096597"
---
# <a name="create-table---sql-command"></a>CREATE TABLE – comando SQL
Cria uma tabela com os campos especificados.  
  
 O driver ODBC do Visual FoxPro dá suporte à sintaxe de linguagem nativa do Visual FoxPro para este comando. Para obter informações específicas do driver, consulte **comentários do driver**.  
  
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
 CREATE TABLE &#124; DBF *TableName1*  
 Especifica o nome da tabela a ser criada. As opções TABLE e DBF são idênticas.  
  
 NOME *LongTableName*  
 Especifica um nome longo para a tabela. Um nome de tabela longo só pode ser especificado quando um banco de dados está aberto, pois nomes de tabela longos são armazenados em bancos de dados.  
  
 Nomes longos podem conter até 128 caracteres e podem ser usados no lugar de nomes de arquivo curtos no banco de dados.  
  
 GRATUITO  
 Especifica que a tabela não será adicionada a um banco de dados aberto. GRATUITO não será necessário se um banco de dados não estiver aberto.  
  
 *(FieldName1 FieldType* [( *NFieldWidth* [, *nPrecision*])]  
 Especifica o nome do campo, o tipo de campo, a largura do campo e a precisão do campo (número de casas decimais), respectivamente.  
  
 *FieldType* é uma única letra que indica o [tipo de dados](../../odbc/microsoft/visual-foxpro-field-data-types.md)do campo. Alguns tipos de dados de campo exigem que você especifique *nFieldWidth* ou *nPrecision* ou ambos.  
  
 *nFieldWidth* e *nPrecision* são ignorados para os tipos D, G, I, L, M, P, T e Y. o padrão *nPrecision* será zero (sem casas decimais) se *nPrecision* não estiver incluído nos tipos B, F ou N.  
  
 NULO  
 Permite valores nulos no campo.  
  
 NOT NULL  
 Impede valores nulos no campo.  
  
 Se você omitir NULL e NOT NULL, a configuração atual de SET NULL determinará se os valores nulos são permitidos no campo. No entanto, se você omitir NULL e NOT NULL e incluir a chave primária ou a cláusula UNIQUE, a configuração atual de SET NULL será ignorada e o campo padrão não será nulo.  
  
 VERIFICAR *lExpression1*  
 Especifica uma regra de validação para o campo. *lExpression1* pode ser uma função definida pelo usuário. Sempre que um registro em branco é anexado, a regra de validação é verificada. Um erro será gerado se a regra de validação não permitir um valor de campo em branco em um registro anexado.  
  
 ERRO *cMessageText1*  
 Especifica a mensagem de erro que o Visual FoxPro exibe quando a regra de campo gera um erro. A mensagem é exibida somente quando os dados são alterados em uma janela de procura ou em uma janela de edição.  
  
 *EEXPRESSION1* padrão  
 Especifica um valor padrão para o campo. O tipo de dados de *eExpression1* deve ser igual ao tipo de dados do campo.  
  
 PRIMARY KEY  
 Cria um índice primário para o campo. A marca de índice principal tem o mesmo nome que o campo.  
  
 UNIQUE  
 Cria um índice candidato para o campo. A marca de índice candidato tem o mesmo nome que o campo.  
  
> [!NOTE]  
>  Os índices candidatos (criados com a inclusão da opção UNIQUE em CREATE TABLE ou ALTER TABLE-SQL) não são os mesmos que os índices criados com a opção UNIQUE no comando de índice. Um índice criado com a opção UNIQUE no comando de índice permite chaves de índice duplicadas; os índices candidatos não permitem chaves de índice duplicadas. Consulte o [índice](../../odbc/microsoft/index-command.md) para obter informações adicionais sobre sua opção exclusiva.  
  
 Valores nulos e registros duplicados não são permitidos em um campo usado para um índice primário ou candidato. No entanto, o Visual FoxPro não gerará um erro se você criar um índice primário ou candidato para um campo que ofereça suporte a valores nulos. O Visual FoxPro irá gerar um erro se você tentar inserir um valor nulo ou duplicado em um campo usado para um índice primário ou candidato.  
  
 REFERENCEs *TableName2*[tag *TagName1*]  
 Especifica a tabela pai à qual uma relação persistente é estabelecida. Se você omitir a marca *TagName1*, a relação será estabelecida usando a chave de índice primária da tabela pai. Se a tabela pai não tiver um índice primário, o Visual FoxPro gerará um erro.  
  
 Inclua a marca *TagName1* para estabelecer uma relação com base em uma marca de índice existente para a tabela pai. Os nomes de marcas de índice podem conter até 10 caracteres.  
  
 A tabela pai não pode ser uma tabela gratuita.  
  
 NOCPTRANS  
 Impede a conversão em uma página de código diferente para campos de caractere e memorando. Se a tabela for convertida em outra página de código, os campos para os quais NOCPTRANS foi especificado não serão traduzidos. NOCPTRANS pode ser especificado somente para campos de caracteres e memorando.  
  
 O exemplo a seguir cria uma tabela chamada MyTable contendo dois campos de caractere e dois campos de memorando. O segundo campo de caractere, char2 e o segundo campo de memorando, memo2, incluem NOCPTRANS para impedir a tradução.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 CHAVE primária *eExpression2* marca *TagName2*  
 Especifica um índice primário a ser criado. *eExpression2* Especifica qualquer campo ou combinação de campos na tabela. A marca *TagName2* especifica o nome da marca de índice primário que é criada. Os nomes de marcas de índice podem conter até 10 caracteres.  
  
 Como uma tabela pode ter apenas um índice primário, você não poderá incluir essa cláusula se já tiver criado um índice primário para um campo. O Visual FoxPro gerará um erro se você incluir mais de uma cláusula PRIMARY KEY em CREATE TABLE.  
  
 *TagName3* de marca *eExpression3*exclusiva  
 Cria um índice candidato. *eExpression3* Especifica qualquer campo ou combinação de campos na tabela. No entanto, se você tiver criado um índice primário com uma das opções de chave primária, não poderá incluir o campo que foi especificado para o índice primário. TAG *TagName3* especifica um nome de marca para a marca de índice candidato que é criada. Os nomes de marcas de índice podem conter até 10 caracteres.  
  
 Uma tabela pode ter vários índices candidatos.  
  
 *EExpression4*da marca Foreign Key *TagName4*[NODUP]  
 Cria um índice estrangeiro (não primário) e estabelece uma relação com uma tabela pai. *eExpression4* especifica a expressão de chave de índice estrangeiro e *TagName4* especifica o nome da marca de chave de índice estrangeiro que é criada. Os nomes de marcas de índice podem conter até 10 caracteres. Inclua NODUP para criar um índice estrangeiro candidato.  
  
 Você pode criar vários índices estrangeiros para a tabela, mas as expressões de índice estrangeiro devem especificar campos diferentes na tabela.  
  
 REFERENCEs *TableName3*[tag *TagName5*]  
 Especifica a tabela pai à qual uma relação persistente é estabelecida. Incluir marca *TagName5* para estabelecer uma relação com base em uma marca de índice para a tabela pai. Os nomes de marcas de índice podem conter até 10 caracteres. Por padrão, se você omitir a marca *TagName5,* a relação será estabelecida usando a chave de índice primária da tabela pai.  
  
 Verifique *eExpression2*[Error *cMessageText2*]  
 Especifica a regra de validação de tabela. ERRO *cMessageText2* especifica a mensagem de erro que o Visual FoxPro exibe quando a regra de validação de tabela é executada. A mensagem é exibida somente quando os dados são alterados em uma janela de navegação ou em uma janela de edição.  
  
 DA matriz *arrayName*  
 Especifica o nome de uma matriz existente cujo conteúdo é o nome, o tipo, a precisão e a escala de cada campo na tabela. O conteúdo da matriz pode ser definido com a função **AFIELDS**().  
  
## <a name="remarks"></a>Comentários  
 A nova tabela é aberta na área de trabalho mais baixa disponível e pode ser acessada por seu alias. A nova tabela é aberta exclusivamente, independentemente da configuração atual do conjunto exclusivo.  
  
 Se um banco de dados estiver aberto e você não incluir a cláusula FREE, a nova tabela será adicionada ao banco de dados. Você não pode criar uma nova tabela com o mesmo nome que uma tabela no banco de dados.  
  
 Se um banco de dados estiver aberto, o CREATE TABLE-SQL exigirá o uso exclusivo do banco de dados. Para abrir um banco de dados para uso exclusivo, inclua exclusivo no banco de dados aberto.  
  
 Se um banco de dados não estiver aberto quando você criar a nova tabela, a inclusão das cláusulas NAME, CHECK, padrão, FOREIGN KEY, PRIMARY KEY ou REFERENCEs gerará um erro.  
  
> [!NOTE]  
>  CREATE TABLE sintaxe usa vírgulas para separar determinadas opções de CREATE TABLE. Além disso, o valor nulo, não nulo, verificação, padrão, chave primária e cláusula UNIQUE devem ser colocados dentro dos parênteses que contêm as definições de coluna.  
  
## <a name="driver-remarks"></a>Comentários do driver  
 Quando o aplicativo envia a instrução SQL ODBC CREATE TABLE à fonte de dados, o driver ODBC do Visual FoxPro converte o comando no comando da tabela FoxProCREATE do Visual usando a sintaxe mostrada na tabela a seguir.  
  
|Sintaxe ODBC|Sintaxe do Visual FoxPro|  
|-----------------|--------------------------|  
|*Nome da tabela de base* CREATE TABLE<br /><br /> (*tipo de dados de identificador de coluna*<br /><br /> [NÃO NULO]<br /><br /> [,*tipo de dados de identificador de coluna*<br /><br /> [NÃO NULO]...)|CREATE TABLE *TableName1* [name *LongTableName*]<br /><br /> (*FieldName1* *FieldType*<br /><br /> [(*nFieldWidth* [, *nPrecision*])]<br /><br /> [NÃO NULO])|  
  
 Quando você cria uma tabela usando o driver, o driver fecha a tabela imediatamente após a criação para permitir o acesso à tabela por outros usuários. Isso difere do Visual FoxPro, o que deixa a tabela aberta exclusivamente na criação. No entanto, se um procedimento armazenado na fonte de dados que contém uma instrução CREATE TABLE for executado, a tabela será deixada aberta.  
  
 Se a fonte de dados for um banco de dado (arquivo. DBC), o driver ODBC do Visual FoxPro criará uma tabela chamada *LongTableName* com o mesmo nome que o *nome da tabela base*.  
  
### <a name="using-data-definition-language-ddl"></a>Usando DDL (linguagem de definição de dados)  
 Você não pode incluir DDL nos seguintes locais:  
  
-   Em uma instrução SQL do lote que requer uma transação  
  
-   No modo de confirmação manual, após uma instrução que exigia uma transação, a menos que seu aplicativo primeiro chame **SQLTransact**.  
  
 Por exemplo, se você quiser criar uma tabela temporária, deverá criar a tabela antes de começar a instrução que requer uma transação. Se você incluir a instrução CREATE TABLE em uma instrução SQL do lote que requer uma transação, o driver retornará uma mensagem de erro.  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE-comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [Tipos de dados com suporte (driver ODBC do Visual FoxPro)](../../odbc/microsoft/supported-data-types-visual-foxpro-odbc-driver.md)   
 [INSERIR-comando SQL](../../odbc/microsoft/insert-sql-command.md)   
 [SELECT – comando SQL](../../odbc/microsoft/select-sql-command.md)

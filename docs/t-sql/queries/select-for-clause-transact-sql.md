---
description: SELECT – Cláusula FOR (Transact-SQL)
title: Cláusula FOR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FOR
- FOR CLAUSE
- FOR_TSQL
- FOR_CLAUSE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- XML option [SQL Server]
- BROWSE option
- FOR clause [Transact-SQL]
ms.assetid: 08a6f084-8f73-4f2a-bae4-3c7513dc99b9
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: a3f8fb497c95bd7f1df6f1ea8a51be938bc1a555
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479444"
---
# <a name="select---for-clause-transact-sql"></a>SELECT – Cláusula FOR (Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Use a cláusula FOR para especificar uma das opções a seguir para os resultados da consulta.
  
-   Permita atualizações ao exibir os resultados da consulta em um cursor de modo de procura, especificando **FOR BROWSE**.  
  
-   Formate os resultados da consulta como XML, especificando **FOR XML**.  
  
-   Formate os resultados da consulta como JSON, especificando **FOR JSON**.  

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
[ FOR { BROWSE | <XML> | <JSON>} ]  
  
<XML> ::=  
XML   
{   
    { RAW [ ( 'ElementName' ) ] | AUTO }   
    [   
        <CommonDirectivesForXML>   
        [ , { XMLDATA | XMLSCHEMA [ ( 'TargetNameSpaceURI' ) ] } ]   
        [ , ELEMENTS [ XSINIL | ABSENT ]   
    ]  
  | EXPLICIT   
    [   
        <CommonDirectivesForXML>   
        [ , XMLDATA ]   
    ]  
  | PATH [ ( 'ElementName' ) ]   
    [  
        <CommonDirectivesForXML>   
        [ , ELEMENTS [ XSINIL | ABSENT ] ]  
    ]  
}   
  
<CommonDirectivesForXML> ::=   
[ , BINARY BASE64 ]  
[ , TYPE ]  
[ , ROOT [ ( 'RootName' ) ] ]  
  
<JSON> ::=  
JSON   
{   
    { AUTO | PATH }   
    [   
        [ , ROOT [ ( 'RootName' ) ] ]  
        [ , INCLUDE_NULL_VALUES ]  
        [ , WITHOUT_ARRAY_WRAPPER ]  
    ]  
  
}
```
  
## <a name="for-browse"></a>FOR BROWSE

 BROWSE  
 Especifica que as atualizações são permitidas ao exibir os dados em um cursor do modo de procura DB-Library. Será possível procurar em uma tabela em um aplicativo se ela incluir uma coluna **timestamp**, se ela tiver um índice exclusivo e a se opção FOR BROWSE estiver no final das instruções SELECT enviadas para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]
> Não é possível usar \<lock_hint> HOLDLOCK em uma instrução SELECT que inclua a opção FOR BROWSE.
  
 FOR BROWSE não pode se aparecer em instruções SELECT que sejam unidas pelo operador UNION.  
  
> [!NOTE]
> Quando as colunas de chaves de índice exclusivo de uma tabela permitirem valor nulo e a tabela estiver no lado interno de uma junção externa, o modo de procura não oferece suporte para o índice.  
  
 O modo de busca lhe permite verificar as linhas na tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e atualizar os dados uma linha de cada vez na tabela. Para acessar uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em seu aplicativo no modo de procura, use uma das duas opções a seguir:  
  
-   A instrução SELECT usada para acessar os dados na tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisa terminar com as palavras-chave **FOR BROWSE**. Quando você ativa a opção **FOR BROWSE** para usar o modo de procura, são criadas tabelas temporárias.  
  
-   Você precisa executar a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] para ativar o modo de procura usando a opção **NO_BROWSETABLE**:  
  
    ```sql
    SET NO_BROWSETABLE ON  
    ```  
  
     Quando você ativa a opção **NO_BROWSETABLE**, todas as instruções SELECT se comportam como se a opção **FOR BROWSE** estivesse acrescentada a elas. No entanto, a opção **NO_BROWSETABLE** não cria as tabelas temporárias que a opção **FOR BROWSE** geralmente usa para enviar os resultados para o aplicativo.  
  
 Quando você tenta acessar os dados de tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de procura usando uma consulta SELECT que envolve uma instrução de junção externa e quando um índice exclusivo está definido na tabela presente no interior de uma instrução de junção externa, o modo de procura não permite o índice exclusivo. O modo de busca somente dá suporte ao índice exclusivo quando todas as colunas de chave do índice exclusivo podem aceitar valores nulos. O modo de busca não dará suporte ao índice exclusivo se as seguintes condições forem verdadeiras:  
  
-   Você tenta acessar os dados de tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de procura usando uma consulta SELECT que envolve uma instrução de junção externa.  
  
-   Um índice exclusivo está definido na tabela presente no interior de uma instrução de junção externa.  
  
 Para reproduzir esse comportamento no modo de busca, siga estas etapas:  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], crie um banco de dados denominado SampleDB.  
  
2.  No banco de dados SampleDB, crie uma tabela tleft e uma tabela tright com uma única coluna denominada c1. Defina um índice exclusivo na coluna c1 na tabela tleft e defina a coluna para aceitar valores nulos. Para fazer isso, execute as seguintes instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] em uma janela de consulta apropriada:  
  
    ```sql
    CREATE TABLE tleft(c1 INT NULL UNIQUE) ;  
    GO   
    CREATE TABLE tright(c1 INT NULL) ;  
    GO  
    ```  
  
3.  Insira vários valores nas tabelas tleft e tright. Verifique se você inseriu um valor nulo na tabela tleft. Para fazer isso, execute as seguintes instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] na janela de consulta:  
  
    ```sql
    INSERT INTO tleft VALUES(2) ;  
    INSERT INTO tleft VALUES(NULL) ;  
    INSERT INTO tright VALUES(1) ;  
    INSERT INTO tright VALUES(3) ;  
    INSERT INTO tright VALUES(NULL) ;  
    GO  
    ```  
  
4.  Ative a opção **NO_BROWSETABLE**. Para fazer isso, execute as seguintes instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] na janela de consulta:  
  
    ```sql
    SET NO_BROWSETABLE ON ;  
    GO  
    ```  
  
5.  Acesse os dados nas tabelas tleft e tright usando uma instrução de junção externa na consulta SELECT. Verifique se a tabela tleft está dentro da instrução de junção externa. Para fazer isso, execute as seguintes instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] na janela de consulta:  
  
    ```sql
    SELECT tleft.c1   
    FROM tleft   
    RIGHT JOIN tright   
    ON tleft.c1 = tright.c1   
    WHERE tright.c1 <> 2 ;
    ```  
  
     Observe a seguinte saída no painel de Resultados:  
  
     c1  
  
     ---\-  
  
     NULO  
  
     NULO  
  
 Depois que você executar a consulta SELECT para acessar as tabelas no modo de busca, o conjunto de resultados da consulta SELECT conterá dois valores nulos da coluna c1 na tabela tleft devido à definição da instrução de junção externa direita. Assim, no conjunto de resultados, não é possível distinguir entre os valores nulos provenientes da tabela e os valores nulos introduzidos pela instrução de junção externa. Talvez você receba resultados incorretos se ignorar os valores nulos do conjunto de resultados.  
  
> [!NOTE]
> Se as colunas incluídas no índice exclusivo não aceitarem valores nulos, todos os valores nulos no conjunto de resultados foram introduzidos pela instrução de junção externa direita.  
  
## <a name="for-xml"></a>FOR XML

 XML  
 Especifica que os resultados de uma consulta serão retornados como um documento XML. Um dos seguintes modos XML precisa ser especificado: RAW, AUTO, EXPLICIT. Para obter mais informações sobre dados XML e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], confira [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md).  
  
 RAW [ **('** _ElementName_ **')** ]  
 Obtém o resultado da consulta e transforma cada linha do conjunto de resultados em um elemento XML com um identificador genérico \<row /> como a marca do elemento. Opcionalmente, é possível especificar um nome para o elemento de linha. A saída XML resultante usa o *ElementName* especificado como o elemento de linha gerado para cada linha. Para obter mais informações, consulte [Usar modo RAW com FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md).
  
 AUTO  
 Retorna os resultados da consulta em uma árvore XML simples e aninhada. Cada tabela na cláusula FROM, para a qual pelo menos uma coluna esteja listada na cláusula SELECT, é representada como um elemento XML. As colunas listadas na cláusula SELECT são mapeadas para os atributos apropriados do elemento. Para obter mais informações, consulte [Usar modo AUTO com FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md).  
  
 EXPLICIT  
 Especifica que a forma da árvore XML resultante está explicitamente definida. Ao usar este modo, as consultas devem ser gravadas de uma maneira específica para que as informações adicionais sobre o aninhamento desejado sejam especificadas explicitamente. Para obter mais informações, consulte [Usar modo EXPLICIT com FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md).  
  
 XMLDATA  
 Retorna o esquema XDR embutido, mas não adiciona o elemento raiz ao resultado. Se XMLDATA for especificado, o esquema XDR será anexado ao documento.  
  
> [!IMPORTANT]
> A diretiva XMLDATA foi **preterida**. Use geração de XSD no caso dos modos RAW e AUTO. Não há substituição para a diretiva XMLDATA no modo EXPLICIT. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  

_Suprimir quebras de linha indesejadas:_ Você pode usar o SSMS (SQL Server Management Studio) para emitir uma consulta que usa a cláusula FOR XML. Às vezes, uma grande quantidade de XML é retornada e exibida na célula de uma grade. A cadeia de caracteres XML pode ser mais longa que uma célula de grade do SSMS e reter em uma única linha. Nesses casos, o SSMS pode inserir caracteres de quebra de linha entre segmentos longos de toda a cadeia de caracteres XML. Essas quebras de linha podem ocorrer no meio de uma subcadeia de caracteres que não deve ser dividida entre linhas. Você pode impedir quebras de linha usando uma conversão como XMLDATA. Essa solução também pode se aplicar ao usar FOR JSON PATH. A técnica é discutida no Stack Overflow e é mostrada na seguinte instrução SELECT de exemplo do Transact-SQL:

- [Usando o SQL Server FOR XML: Converter o Tipo de Dados de Resultado em Texto/varchar/cadeia de caracteres o que for?](https://stackoverflow.com/questions/5655332/using-sql-server-for-xml-convert-result-datatype-to-text-varchar-string-whate/5658758#5658758)

    ```sql
    SELECT CAST(
        (SELECT column1, column2
            FROM my_table
            FOR XML PATH('')
        )
            AS VARCHAR(MAX)
    ) AS XMLDATA ;
    ```

<!-- The preceding Stack Overflow example is per MicrosoftDocs/sql-docs Issue 1501.  2019-01-06 -->

 XMLSCHEMA [ **('** _TargetNameSpaceURI_ **')** ]  
 Retorna o esquema XSD embutido. Opcionalmente, você pode especificar um URI de namespace de destino ao especificar esta diretiva, o que retorna o namespace especificado no esquema. Para obter mais informações, consulte [Gerar um esquema XSD embutido](../../relational-databases/xml/generate-an-inline-xsd-schema.md).  
  
 ELEMENTS  
 Especifica que as colunas são retornadas como subelementos. Caso contrário, elas serão mapeadas para atributos XML. O suporte a esta opção é oferecido somente nos modos RAW, AUTO e PATH. Para obter mais informações, consulte [Usar modo RAW com FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md).  
  
 XSINIL  
 Especifica que um elemento com o atributo **xsi:nil** definido como **True** será criado para valores de coluna NULL. Esta opção pode ser especificada somente com a diretiva ELEMENTS. Para obter mais informações, consulte:

- [Gerar elementos para valores NULL com o parâmetro XSINIL](../../relational-databases/xml/generate-elements-for-null-values-with-the-xsinil-parameter.md).
- [FOR XML na instrução SELECT](../../relational-databases/xml/for-xml-sql-server.md)
  
 ABSENT  
 Indica que para valores de coluna nulos, os elementos XML correspondentes não serão adicionados ao resultado do XML. Especifique esta opção somente com ELEMENTS.  
  
 PATH [ **('** _ElementName_ **')** ]  
 Gera um wrapper de elemento \<row> para cada linha no conjunto de resultados. Opcionalmente, você pode especificar um nome de elemento para o wrapper de elemento \<row>. Se uma cadeia de caracteres vazia for fornecida, como FOR XML PATH ( **''** ) ), um elemento de wrapper não será gerado. O uso de PATH pode fornecer uma alternativa mais simples a consultas escritas com o uso da diretiva EXPLICIT. Para obter mais informações, consulte [Usar modo PATH com FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md).  
  
 BINARY BASE64  
 Especifica que a consulta retorna os dados binários em formato binário codificado em base64. Ao recuperar dados binários usando o modo RAW e EXPLICIT, esta opção deve ser especificada. Este é o padrão no modo AUTO.  
  
 TYPE  
 Especifica que a consulta retorna os resultados como um tipo **XML**. Para obter mais informações, consulte [Diretiva TYPE em consultas FOR XML](../../relational-databases/xml/type-directive-in-for-xml-queries.md).  
  
 ROOT [ **('** _RootName_ **')** ]  
 Especifica que um único elemento de nível superior seja adicionado ao XML resultante. Opcionalmente, é possível especificar o nome do elemento raiz a ser gerado. Se o nome da raiz opcional não for especificado, o elemento padrão \<root> será adicionado.  
  
 Para obter mais informações, confira [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md).  
  
 **Exemplo de FOR XML**  
  
 O exemplo a seguir especifica `FOR XML AUTO` com as opções `TYPE` e `XMLSCHEMA`. Por causa da opção `TYPE`, o conjunto de resultados é retornado ao cliente como um tipo **XML**. A opção `XMLSCHEMA` especifica que o esquema XSD embutido é incluído nos dados XML retornados e a opção `ELEMENTS` especifica que o resultado XML é centrado em elemento.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.BusinessEntityID, FirstName, LastName, PhoneNumber AS Phone  
FROM Person.Person AS p  
JOIN Person.PersonPhone AS pph ON p.BusinessEntityID  = pph.BusinessEntityID  
WHERE LastName LIKE 'G%'  
ORDER BY LastName, FirstName   
FOR XML AUTO, TYPE, XMLSCHEMA, ELEMENTS XSINIL;  
```  
  
## <a name="for-json"></a>FOR JSON

 JSON  
 Especifique FOR JSON para retornar os resultados de uma consulta formatados como texto JSON. Especifique também um dos seguintes modos JSON: AUTO ou PATH. Para obter mais informações sobre a cláusula **FOR JSON**, confira [Formatar os resultados da consulta como JSON com o FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).  
  
 AUTO  
 Formatar a saída JSON automaticamente com base na estrutura da instrução **SELECT**  
            especificando **FOR JSON AUTO**. Para mais informações e exemplos, consulte [Formatar a saída JSON automaticamente com o modo AUTO &#40;SQL Server&#41;](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md).  
  
 PATH  
 Obter controle total sobre o formato da saída JSON especificando   
            **FOR JSON PATH**. O modo**PATH** permite criar objetos wrapper e aninhar propriedades complexas. Para mais informações e exemplos, consulte [Formatar a saída JSON aninhada com modo PATH &#40;SQL Server&#41;](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md).  
  
 INCLUDE_NULL_VALUES  
 Inclua valores nulos na saída JSON especificando a opção **INCLUDE_NULL_VALUES** com a cláusula **FOR JSON**. Se você não especificar essa opção, a saída não incluirá as propriedades JSON para valores nulo nos resultados da consulta. Para obter mais informações e exemplos, confira [Incluir valores nulos com a opção JSON INCLUDE_NULL_VALUES &#40;SQL Server&#41;](../../relational-databases/json/include-null-values-in-json-include-null-values-option.md).  
  
 ROOT [ **('** _RootName_ **')** ]  
 Adicione um único elemento de nível superior à saída JSON especificando a opção **ROOT** com a cláusula **FOR JSON**. Se você não especificar a opção **ROOT** , a saída JSON não terá um elemento raiz. Para obter mais informações e exemplos, confira [Adicionar um nó raiz à saída JSON com a opção ROOT &#40;SQL Server&#41;](../../relational-databases/json/add-a-root-node-to-json-output-with-the-root-option-sql-server.md).  
  
 WITHOUT_ARRAY_WRAPPER  
 Remova os colchetes que envolvem a saída JSON por padrão, especificando a opção **WITHOUT_ARRAY_WRAPPER** com a cláusula **FOR JSON**. Se você não especificar essa opção, a saída JSON será colocada entre colchetes. Use a opção **WITHOUT_ARRAY_WRAPPER** para gerar um único objeto JSON como saída.  Para obter mais informações, consulte [Remove Square Brackets from JSON Output with the WITHOUT_ARRAY_WRAPPER Option &#40;SQL Server&#41; (Remover os colchetes da saída JSON com a opção WITHOUT_ARRAY_WRAPPER &#40;SQL Server&#41;)](../../relational-databases/json/remove-square-brackets-from-json-without-array-wrapper-option.md).  
  
 Para obter mais informações, veja [Formatar resultados da consulta como JSON com FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).  
  
## <a name="see-also"></a>Consulte Também

 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)


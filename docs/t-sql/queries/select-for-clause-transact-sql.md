---
title: "Cláusula FOR (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 54
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f092e78608e8fa2b44061056ef4e5b9e7e1649a7
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="select---for-clause-transact-sql"></a>Selecione - a cláusula FOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Use a cláusula FOR para especificar uma das opções a seguir para resultados da consulta.  
  
-   Permitir atualizações ao exibir os resultados da consulta em um cursor de modo de procura, especificando **para procurar**.  
  
-   Formatar resultados da consulta como XML, especificando **FOR XML**.  
  
-   Formate os resultados da consulta como JSON, especificando **FOR JSON**.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
 Especifica que as atualizações são permitidas ao exibir os dados em um cursor do modo de procura DB-Library. Uma tabela pode ser pesquisada em um aplicativo se a tabela inclui uma **timestamp** coluna, a tabela tem um índice exclusivo, e a opção FOR BROWSE estiver no final das instruções SELECT enviadas a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Não é possível usar o \<lock_hint > HOLDLOCK em uma instrução SELECT que inclui a opção FOR BROWSE.
  
 FOR BROWSE não pode se aparecer em instruções SELECT que sejam unidas pelo operador UNION.  
  
> [!NOTE]  
>  Quando as colunas de chaves de índice exclusivo de uma tabela permitirem valor nulo e a tabela estiver no lado interno de uma junção externa, o modo de procura não oferece suporte para o índice.  
  
 O modo de busca lhe permite verificar as linhas na tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e atualizar os dados uma linha de cada vez na tabela. Para acessar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela em seu aplicativo no modo de busca, você deve usar uma das duas opções a seguir:  
  
-   A instrução SELECT que você usa para acessar os dados da sua [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela deve terminar com as palavras-chave **para procurar**. Quando você ativa o **para procurar** opção para usar o modo de procura, tabelas temporárias são criadas.  
  
-   Você deve executar o seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução para ativar o modo de busca usando o **NO_BROWSETABLE** opção:  
  
    ```  
    SET NO_BROWSETABLE ON  
    ```  
  
     Quando você ativa o **NO_BROWSETABLE** opção, todas as instruções SELECT se comportam como se o **para procurar** opção é anexada a elas. No entanto, o **NO_BROWSETABLE** opção não cria as tabelas temporárias que o **para procurar** opção geralmente usa para enviar os resultados para seu aplicativo.  
  
 Quando você tenta acessar os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelas no modo de procura, usando uma consulta SELECT que envolve uma instrução de junção externa e quando um índice exclusivo é definido na tabela que está presente no interior de uma instrução de junção externa, o modo de busca não sup o índice exclusivo da porta. O modo de busca somente dá suporte ao índice exclusivo quando todas as colunas de chave do índice exclusivo podem aceitar valores nulos. O modo de busca não dará suporte ao índice exclusivo se as seguintes condições forem verdadeiras:  
  
-   Tentar acessar os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelas no modo de procura, usando uma consulta SELECT que envolve uma instrução de junção externa.  
  
-   Um índice exclusivo está definido na tabela presente no interior de uma instrução de junção externa.  
  
 Para reproduzir esse comportamento no modo de busca, siga estas etapas:  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], crie um banco de dados denominado SampleDB.  
  
2.  No banco de dados SampleDB, crie uma tabela tleft e uma tabela tright com uma única coluna denominada c1. Defina um índice exclusivo na coluna c1 na tabela tleft e defina a coluna para aceitar valores nulos. Para fazer isso, execute as seguintes instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] em uma janela de consulta apropriada:  
  
    ```  
    CREATE TABLE tleft(c1 INT NULL UNIQUE) ;  
    GO   
    CREATE TABLE tright(c1 INT NULL) ;  
    GO  
    ```  
  
3.  Insira vários valores nas tabelas tleft e tright. Verifique se você inseriu um valor nulo na tabela tleft. Para fazer isso, execute as seguintes instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] na janela de consulta:  
  
    ```  
    INSERT INTO tleft VALUES(2) ;  
    INSERT INTO tleft VALUES(NULL) ;  
    INSERT INTO tright VALUES(1) ;  
    INSERT INTO tright VALUES(3) ;  
    INSERT INTO tright VALUES(NULL) ;  
    GO  
    ```  
  
4.  Ativar o **NO_BROWSETABLE** opção. Para fazer isso, execute as seguintes instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] na janela de consulta:  
  
    ```  
    SET NO_BROWSETABLE ON ;  
    GO  
    ```  
  
5.  Acesse os dados nas tabelas tleft e tright usando uma instrução de junção externa na consulta SELECT. Verifique se a tabela tleft está dentro da instrução de junção externa. Para fazer isso, execute as seguintes instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] na janela de consulta:  
  
    ```  
    SELECT tleft.c1   
    FROM tleft   
    RIGHT JOIN tright   
    ON tleft.c1 = tright.c1   
    WHERE tright.c1 <> 2 ;  
  
    ```  
  
     Observe a seguinte saída no painel de Resultados:  
  
     c1  
  
     ---\-  
  
     NULL  
  
     NULL  
  
 Depois que você executar a consulta SELECT para acessar as tabelas no modo de busca, o conjunto de resultados da consulta SELECT conterá dois valores nulos da coluna c1 na tabela tleft devido à definição da instrução de junção externa direita. Assim, no conjunto de resultados, não é possível distinguir entre os valores nulos provenientes da tabela e os valores nulos introduzidos pela instrução de junção externa. Talvez você receba resultados incorretos se ignorar os valores nulos do conjunto de resultados.  
  
> [!NOTE]  
>  Se as colunas incluídas no índice exclusivo não aceitarem valores nulos, todos os valores nulos no conjunto de resultados foram introduzidos pela instrução de junção externa direita.  
  
## <a name="for-xml"></a>FOR XML  
 XML  
 Especifica que os resultados de uma consulta serão retornados como um documento XML. Um dos seguintes modos XML deve ser especificado: RAW, AUTO, EXPLICIT. Para obter mais informações sobre dados XML e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [FOR XML &#40; SQL Server &#41; ](../../relational-databases/xml/for-xml-sql-server.md).  
  
 RAW [ **('***ElementName***')** ]  
 Obtém o resultado da consulta e transforma cada linha do conjunto de resultados em um elemento XML com um identificador genérico \<linhas / > como a marca do elemento. Opcionalmente, é possível especificar um nome para o elemento de linha. A saída XML resultante usa especificado *ElementName* como o elemento de linha gerado para cada linha. Para obter mais informações, consulte [usar modo RAW com FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md) e [usar modo RAW com FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md).  
  
 AUTO  
 Retorna os resultados da consulta em uma árvore XML simples e aninhada. Cada tabela na cláusula FROM, para a qual pelo menos uma coluna esteja listada na cláusula SELECT, é representada como um elemento XML. As colunas listadas na cláusula SELECT são mapeadas para os atributos apropriados do elemento. Para obter mais informações, consulte [Usar modo AUTO com FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md).  
  
 EXPLICIT  
 Especifica que a forma da árvore XML resultante está explicitamente definida. Ao usar este modo, as consultas devem ser gravadas de uma maneira específica para que as informações adicionais sobre o aninhamento desejado sejam especificadas explicitamente. Para obter mais informações, consulte [Usar modo EXPLICIT com FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md).  
  
 XMLDATA  
 Retorna o esquema XDR embutido, mas não adiciona o elemento raiz ao resultado. Se XMLDATA for especificado, o esquema XDR será anexado ao documento.  
  
> [!IMPORTANT]  
>  A diretiva XMLDATA foi preterida. Use geração de XSD no caso dos modos RAW e AUTO. Não há substituição para a diretiva XMLDATA no modo EXPLICIT. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 XMLSCHEMA [ **('***TargetNameSpaceURI***')** ]  
 Retorna o esquema XSD embutido. Opcionalmente, você pode especificar um URI de namespace de destino ao especificar esta diretiva, o que retorna o namespace especificado no esquema. Para obter mais informações, consulte [Gerar um esquema XSD embutido](../../relational-databases/xml/generate-an-inline-xsd-schema.md).  
  
 ELEMENTS  
 Especifica que as colunas são retornadas como subelementos. Caso contrário, elas serão mapeadas para atributos XML. O suporte a esta opção é oferecido somente nos modos RAW, AUTO e PATH. Para obter mais informações, consulte [Usar modo RAW com FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md).  
  
 XSINIL  
 Especifica que um elemento com **xsi: nil** atributo definido como **True** seja criado para valores de coluna NULL. Esta opção pode ser especificada somente com a diretiva ELEMENTS. Para obter mais informações, consulte [gerar elementos para valores NULL com o parâmetro XSINIL](../../relational-databases/xml/generate-elements-for-null-values-with-the-xsinil-parameter.md).  
  
 ABSENT  
 Indica que para valores de coluna nulos, os elementos XML correspondentes não serão adicionados ao resultado do XML. Especifique esta opção somente com ELEMENTS.  
  
 CAMINHO [ **('***ElementName***')** ]  
 Gera um \<linha > wrapper de elemento para cada linha no conjunto de resultados. Opcionalmente, você pode especificar um nome de elemento para o \<linha > wrapper de elemento. Se uma cadeia de caracteres vazia for fornecida, como FOR XML PATH (**'**)), um elemento wrapper não é gerado. O uso de PATH pode fornecer uma alternativa mais simples a consultas escritas com o uso da diretiva EXPLICIT. Para obter mais informações, consulte [Usar modo PATH com FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md).  
  
 BINARY BASE64  
 Especifica que a consulta retorna os dados binários em formato binário codificado em base64. Ao recuperar dados binários usando o modo RAW e EXPLICIT, esta opção deve ser especificada. Este é o padrão no modo AUTO.  
  
 TYPE  
 Especifica que a consulta retorna resultados como **xml** tipo. Para obter mais informações, consulte [Diretiva TYPE em consultas FOR XML](../../relational-databases/xml/type-directive-in-for-xml-queries.md).  
  
 RAIZ [ **('***RootName***')** ]  
 Especifica que um único elemento de nível superior seja adicionado ao XML resultante. Opcionalmente, é possível especificar o nome do elemento raiz a ser gerado. Se o nome raiz opcional não for especificado, o padrão \<raiz > elemento é adicionado.  
  
 Para obter mais informações, consulte [FOR XML &#40; SQL Server &#41; ](../../relational-databases/xml/for-xml-sql-server.md).  
  
 **Por exemplo, XML**  
  
 O exemplo a seguir especifica `FOR XML AUTO` com as opções `TYPE` e `XMLSCHEMA`. Devido a `TYPE` opção, o conjunto de resultados é retornado ao cliente como um **xml** tipo. A opção `XMLSCHEMA` especifica que o esquema XSD embutido é incluído nos dados XML retornados e a opção `ELEMENTS` especifica que o resultado XML é centrado em elemento.  
  
```  
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
 Especifique para JSON para retornar os resultados de uma consulta formatados como texto JSON. Você também precisa especificar um dos seguintes modos de JSON: AUTO ou caminho. Para obter mais informações sobre o **FOR JSON** cláusula, consulte [Formatar resultados da consulta como JSON com FOR JSON &#40; SQL Server &#41; ](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).  
  
 AUTO  
 Formatar a saída JSON automaticamente com base na estrutura do **selecione** instrução  
            especificando **FOR JSON AUTO**. Para mais informações e exemplos, consulte [Formatar a saída JSON automaticamente com o modo AUTO &#40;SQL Server&#41;](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md).  
  
 PATH  
 Obter controle total sobre o formato da saída JSON, especificando   
            **FOR JSON PATH**. O modo**PATH** permite criar objetos wrapper e aninhar propriedades complexas. Para mais informações e exemplos, consulte [Formatar a saída JSON aninhada com modo PATH &#40;SQL Server&#41;](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md).  
  
 INCLUDE_NULL_VALUES  
 Incluir valores nulos na saída JSON, especificando o **INCLUDE_NULL_VALUES** opção com o **FOR JSON** cláusula. Se você não especificar essa opção, a saída não inclui propriedades JSON para valores nulos nos resultados da consulta. Para obter mais informações e exemplos, consulte [incluir valores nulos na saída JSON com a opção INCLUDE_NULL_VALUES &#40; SQL Server &#41; ](../../relational-databases/json/include-null-values-in-json-include-null-values-option.md).  
  
 RAIZ [ **('***RootName***')** ]  
 Adicionar um único elemento de nível superior à saída JSON, especificando o **raiz** opção com o **FOR JSON** cláusula. Se você não especificar a opção **ROOT** , a saída JSON não terá um elemento raiz. Para obter mais informações e exemplos, consulte [adicionar um nó raiz à saída JSON com a opção ROOT &#40; SQL Server &#41; ](../../relational-databases/json/add-a-root-node-to-json-output-with-the-root-option-sql-server.md).  
  
 WITHOUT_ARRAY_WRAPPER  
 Remover os colchetes que envolvem a saída JSON por padrão, especificando o **WITHOUT_ARRAY_WRAPPER** opção com o **FOR JSON** cláusula. Se você não especificar essa opção, a saída JSON será colocada entre colchetes. Use o **WITHOUT_ARRAY_WRAPPER** opção para gerar um único objeto JSON como saída.  Para obter mais informações, consulte [Remove Square Brackets from JSON Output with the WITHOUT_ARRAY_WRAPPER Option &#40;SQL Server&#41; (Remover os colchetes da saída JSON com a opção WITHOUT_ARRAY_WRAPPER &#40;SQL Server&#41;)](../../relational-databases/json/remove-square-brackets-from-json-without-array-wrapper-option.md).  
  
 Para obter mais informações, veja [Formatar resultados da consulta como JSON com FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).  
  
## <a name="see-also"></a>Consulte também  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  


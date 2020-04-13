---
title: Sintaxe básica da cláusula FOR XML | Microsoft Docs
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- BINARY BASE64 directive
- ROOT directive
- FOR XML clause, BINARY BASE64 directive
- FOR XML clause, syntax
- FOR XML clause, ROOT directive
ms.assetid: df19ecbf-d28e-4e9c-aaa3-700f8bbd3be4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ebaf884d584f87afab1afaa4c30a50287d348284
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664736"
---
# <a name="basic-syntax-of-the-for-xml-clause"></a>Sintaxe básica da cláusula FOR XML

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

O modo FOR XML pode ser RAW, AUTO, EXPLICIT ou PATH. Ele determina a forma do XML resultante.  
  
> [!IMPORTANT]  
> A diretiva **XMLDATA** para a opção FOR XML foi **preterida**. Use geração de XSD no caso dos modos RAW e AUTO. Não há substituição para a diretiva XMLDATA no modo EXPLICIT. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]

## <a name="syntax"></a>Sintaxe

Veja a seguir a sintaxe básica descrita em [Cláusula FOR (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md).

```  
[ FOR { BROWSE | <XML> } ]  
<XML> ::=  
XML   
    {   
      { RAW [ ('ElementName') ] | AUTO }   
        [   
           <CommonDirectives>   
           [ , { XMLDATA | XMLSCHEMA [ ('TargetNameSpaceURI') ]} ]
           [ , ELEMENTS [ XSINIL | ABSENT ]   
        ]  
      | EXPLICIT   
        [   
           <CommonDirectives>   
           [ , XMLDATA ]   
        ]  
      | PATH [ ('ElementName') ]   
        [   
           <CommonDirectives>   
           [ , ELEMENTS [ XSINIL | ABSENT ] ]  
        ]  
     }   
  
 <CommonDirectives> ::=   
   [ , BINARY BASE64 ]  
   [ , TYPE ]  
   [ , ROOT [ ('RootName') ] ]  
```  

### <a name="syntax-for-azure-sql-database"></a>Sintaxe do Banco de Dados SQL do Azure

Para obter a documentação da cláusula SELECT...**FOR XML** que também se aplica ao Banco de Dados SQL do Azure, confira [FOR XML (SQL Server)](../../relational-databases/xml/for-xml-sql-server.md).

## <a name="arguments"></a>Argumentos

**RAW** [('_ElementName_')]  
 Pega o resultado da consulta e transforma cada linha no conjunto de resultados em um elemento XML com um identificador genérico, \<row/>, como a marca do elemento. Opcionalmente, é possível especificar um nome para o elemento de linha ao usar esta diretiva. O XML resultante usará o *ElementName* especificado como o elemento de linha gerado para cada linha. Para obter mais informações, consulte [Usar modo RAW com FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md).  
  
**AUTO**  
 Retorna os resultados da consulta em uma árvore XML simples e aninhada. Cada tabela na cláusula FROM para a qual pelo menos uma coluna está listada na cláusula SELECT é representada como um elemento XML. As colunas listadas na cláusula SELECT são mapeadas para os atributos apropriados do elemento. Para obter mais informações, consulte [Usar modo AUTO com FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md).  
  
**EXPLICIT**  
 Especifica que a forma da árvore XML resultante está explicitamente definida. Usando esse modo, as consultas devem ser escritas de uma maneira específica para que informações adicionais sobre o aninhamento desejado sejam especificadas explicitamente. Para obter mais informações, consulte [Usar modo EXPLICIT com FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md).  
  
**PATH**  
 Fornece um modo mais simples de misturar elementos e atributos e introduzir aninhamento adicional para representar propriedades complexas. É possível usar consultas em modo FOR XML EXPLICIT para construir esse tipo de XML a partir de um conjunto de linhas, mas o modo PATH fornece uma alternativa mais simples para as consultas em modo EXPLICIT que provavelmente são trabalhosas. O modo PATH, juntamente com a capacidade de escrever consultas FOR XML aninhadas e a diretiva TYPE para retornar instâncias do tipo **xml** , permite escrever consultas com menos complexidade. Ele fornece uma alternativa a escrita da maioria das consultas em modo EXPLICIT. Por padrão, o modo PATH gera um wrapper de elemento \<row> para cada linha do conjunto de resultados. Opcionalmente, é possível especificar um nome de elemento. Nesse caso, o nome especificado será usado como o nome do elemento wrapper. Se você fornecer uma cadeia de caracteres vazia (FOR XML PATH ('')), nenhum elemento wrapper será gerado. Para obter mais informações, consulte [Usar modo PATH com FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md).  
  
**MLDATA**  
 Especifica que um esquema XDR (XML-Data Reduced) será retornado. O esquema é pré-anexado ao documento como um esquema embutido. Para obter um exemplo de funcionamento, consulte [Usar modo RAW com FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md).  
  
**XMLSCHEMA**  
 Retorna um XSD (Esquema XML da W3C) embutido. Opcionalmente, é possível especificar um URI de namespace de destino especificando esta diretiva. Isso retorna o namespace especificado no esquema. Para obter mais informações, consulte [Gerar um esquema XSD embutido](../../relational-databases/xml/generate-an-inline-xsd-schema.md). Para obter um exemplo de funcionamento, consulte [Usar modo RAW com FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md).  
  
**ELEMENTS**  
 Se a opção ELEMENTS for especificada, as colunas serão retornadas como subelementos. Caso contrário, elas serão mapeadas para atributos XML. Essa opção tem suporte apenas nos modos RAW, AUTO e PATH. Opcionalmente, é possível especificar XSINIL ou ABSENT ao usar esta diretiva. XSINIL especifica que um elemento que tem um atributo **xsi:nil** definido como True seja criado para valores de colunas NULL. Por padrão, ou quando ABSENT está especificado junto com ELEMENTS, nenhum elemento é criado para obter valores NULL. Para obter um exemplo de funcionamento, consulte [Usar modo RAW com FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md) e [Usar o modo AUTO com FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md).  
  
**BINARY BASE64**  
 Se a opção BINARY Base64 for especificada, quaisquer dados binários retornados pela consulta serão representados no formato codificado na base64. Para recuperar dados binários usando o modo RAW e EXPLICIT, esta opção deve ser especificada. Em modo AUTO, por padrão, os dados binários são retornados como uma referência. Para obter um exemplo de funcionamento, consulte [Usar modo RAW com FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md).  
  
**TYPE**  
 Especifica que a consulta retorna os resultados como tipo **xml** . Para obter mais informações, consulte [Diretiva TYPE em consultas FOR XML](../../relational-databases/xml/type-directive-in-for-xml-queries.md).  
  
**ROOT** [('_RootName_')]  
 Especifica que um único elemento de nível superior seja adicionado ao XML resultante. Opcionalmente, é possível especificar o nome do elemento raiz a ser gerado. O valor padrão é `<root>`.  
  
## <a name="see-also"></a>Consulte Também  
 [Usar modo RAW com FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)   
 [Usar o modo AUTO com FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md)   
 [Usar o modo EXPLICIT com FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)   
 [Usar o modo PATH com FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  

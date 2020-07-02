---
title: sp_xml_preparedocument (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_xml_preparedocument_TSQL
- sp_xml_preparedocument
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xml_preparedocument
ms.assetid: 95f41cff-c52a-4182-8ac6-bf49369d214c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1232f5eb7917606d7f7e88c912be163d13de33ba
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85767487"
---
# <a name="sp_xml_preparedocument-transact-sql"></a>sp_xml_preparedocument (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Lê o texto XML fornecido como entrada, analisa o texto usando o analisador MSXML (Msxmlsql.dll) e fornece o documento analisado em um estado pronto para consumo. Esse documento analisado é uma representação em árvore dos vários nós no documento XML: elementos, atributos, texto, comentários e assim por diante.  
  
 **sp_xml_preparedocument** retorna um identificador que pode ser usado para acessar a representação interna recém-criada do documento XML. Esse identificador é válido para a duração da sessão ou até que o identificador seja invalidado executando **sp_xml_removedocument**.  
  
> [!NOTE]  
>  Um documento analisado é armazenado no cache interno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O analisador MSXML usa um oitavo da memória total disponível para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para evitar a execução de memória insuficiente, execute **sp_xml_removedocument** para liberar a memória.  
  
> [!NOTE]  
>  Para compatibilidade com versões anteriores, **sp_xml_preparedocument** recolhe os caracteres CR (Char (13)) e LF (Char (10)) em atributos, mesmo que esses caracteres sejam entidade definida.  
  
> [!NOTE]  
>  O analisador XML invocado por **sp_xml_preparedocument** pode analisar DTDs internos e declarações de entidade. Como as declarações de entidades e DTDs construídas de forma mal-intencionada podem ser usadas para executar um ataque de negação de serviço, é altamente recomendável que os usuários não transmitam diretamente documentos XML de fontes não confiáveis para **sp_xml_preparedocument**.  
>   
>  Para atenuar ataques de expansão de entidade recursiva, **sp_xml_preparedocument** limites para 10.000 o número de entidades que podem ser expandidas abaixo de uma única entidade no nível superior de um documento. O limite não se aplica a entidades numéricas ou caractere. Esse limite permite que documentos com muitas referências de entidade sejam armazenados, mas impede que qualquer entidade seja recursivamente expandida em uma cadeia com mais de 10.000 expansões.  
  
> [!NOTE]  
>  **sp_xml_preparedocument** limita o número de elementos que podem ser abertos de uma vez a 256.  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_xml_preparedocument  
hdoc   
OUTPUT  
[ , xmltext ]  
[ , xpath_namespaces ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *hdoc*  
 É o identificador do documento recém-criado. *hdoc* é um inteiro.  
  
 [ *XmlText* ]  
 É o documento XML original. O analisador MSXML analisa este documento XML. *XmlText* é um parâmetro de texto **: char**, **nchar**, **varchar**, **nvarchar**, **Text**, **ntext** ou **XML**. O valor padrão é NULL; nesse caso é criada uma representação interna de um documento XML vazio.  
  
> [!NOTE]  
>  **sp_xml_preparedocument** só pode processar texto ou XML não tipado. Se um valor de instância a ser usado como entrada já é XML digitado, primeiro converta-o em uma nova instância XML digitada ou uma cadeia de caracteres e, em seguida, passe esse valor como entrada. Para obter mais informações, consulte [Comparar XML digitado com XML não digitado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
 [ *xpath_namespaces* ]  
 Especifica as declarações de namespace usadas em expressões XPATH de linha e coluna em OPENXML. *xpath_namespaces* é um parâmetro de texto **: char**, **nchar**, **varchar**, **nvarchar**, **Text**, **ntext** ou **XML**.  
  
 O valor padrão é **\<root xmlns:mp="urn:schemas-microsoft-com:xml-metaprop">** . *xpath_namespaces* fornece os URIs de namespace para os prefixos usados nas expressões XPath no OPENXML por meio de um documento XML bem formado. *xpath_namespaces* declara o prefixo que deve ser usado para fazer referência ao namespace **urn: schemas-microsoft-com: xml-metaprop**; Isso fornece metadados sobre os elementos XML analisados. Embora você possa redefinir o prefixo de namespace para o namespace metaproperty usando essa técnica, esse namespace não será perdido. O **MP** de prefixo ainda é válido para **urn: schemas-microsoft-com: xml-metaprop** , mesmo que *xpath_namespaces* não contenha tal declaração.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou >0 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-preparing-an-internal-representation-for-a-well-formed-xml-document"></a>a. Preparando uma representação interna de um documento XML bem-formado  
 O exemplo a seguir retorna um identificador para a representação interna criada recentemente do documento XML que é fornecido como entrada. Na chamada para `sp_xml_preparedocument`, é usado um mapeamento de prefixo de namespace padrão.  
  
```  
DECLARE @hdoc int;  
DECLARE @doc varchar(1000);  
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5" OrderDate="1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3" OrderDate="1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>';  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @hdoc OUTPUT, @doc;  
-- Remove the internal representation.  
exec sp_xml_removedocument @hdoc;  
```  
  
### <a name="b-preparing-an-internal-representation-for-a-well-formed-xml-document-with-a-dtd"></a>B. Preparando uma representação interna para um documento XML bem-formado com um DTD  
 O exemplo a seguir retorna um identificador para a representação interna criada recentemente do documento XML que é fornecido como entrada. O procedimento armazenado valida o documento carregado contra o DTD incluído no documento. Na chamada para `sp_xml_preparedocument`, é usado um mapeamento de prefixo de namespace padrão.  
  
```  
DECLARE @hdoc int;  
DECLARE @doc varchar(2000);  
SET @doc = '  
<?xml version="1.0" encoding="UTF-8" ?>   
<!DOCTYPE root   
[<!ELEMENT root (Customers)*>  
<!ELEMENT Customers EMPTY>  
<!ATTLIST Customers CustomerID CDATA #IMPLIED ContactName CDATA #IMPLIED>]>  
<root>  
<Customers CustomerID="ALFKI" ContactName="Maria Anders"/>  
</root>';  
  
EXEC sp_xml_preparedocument @hdoc OUTPUT, @doc;  
```  
  
### <a name="c-specifying-a-namespace-uri"></a>C. Especificando um URI de namespace  
 O exemplo a seguir retorna um identificador para a representação interna criada recentemente do documento XML que é fornecido como entrada. A chamada para `sp_xml_preparedocument` preserva o `mp` prefixo para o mapeamento de namespace de metapropriedade e adiciona o `xyz` prefixo de mapeamento ao namespace `urn:MyNamespace` .  
  
```  
DECLARE @hdoc int;  
DECLARE @doc varchar(1000);  
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5"   
           OrderDate="1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3"   
           OrderDate="1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @hdoc OUTPUT, @doc, '<ROOT xmlns:xyz="urn:MyNamespace"/>';  
```  
  
## <a name="see-also"></a>Consulte Também  
 <br>[Procedimentos armazenados XML (Transact-SQL)](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)
 <br>[Procedimentos armazenados do sistema (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
 <br>[OPENXML (Transact-SQL)](../../t-sql/functions/openxml-transact-sql.md)
 <br>[sys. dm_exec_xml_handles (Transact-SQL)](../system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)
 <br>[sp_xml_removedocument (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql.md)
  
  

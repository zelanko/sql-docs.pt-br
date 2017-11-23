---
title: sp_xml_preparedocument (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_xml_preparedocument_TSQL
- sp_xml_preparedocument
dev_langs: TSQL
helpviewer_keywords: sp_xml_preparedocument
ms.assetid: 95f41cff-c52a-4182-8ac6-bf49369d214c
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: de3ff49a53061f7a804c44886535f764e445fb2e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spxmlpreparedocument-transact-sql"></a>sp_xml_preparedocument (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lê o texto XML fornecido como entrada, analisa o texto usando o analisador MSXML (Msxmlsql.dll) e fornece o documento analisado em um estado pronto para consumo. Esse documento analisado é uma representação em árvore dos vários nós no documento XML: elementos, atributos, texto, comentários e assim por diante.  
  
 **sp_xml_preparedocument** retorna um identificador que pode ser usado para acessar a representação interna recentemente criada do documento XML. Esse identificador é válido para a duração da sessão ou até que o identificador seja invalidado executando **sp_xml_removedocument**.  
  
> [!NOTE]  
>  Um documento analisado é armazenado no cache interno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O analisador MSXML usa um oitavo da memória total disponível para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para evitar ficar sem memória, execute **sp_xml_removedocument** para liberar a memória.  
  
> [!NOTE]  
>  Para versões anteriores compatibilidade, **sp_xml_preparedocument** recolhe CR (char(13)) e LF (char(10)) caracteres em atributos mesmo se esses caracteres tiverem entidade.  
  
> [!NOTE]  
>  O analisador XML invocado por **sp_xml_preparedocument** pode analisar DTDs internos e declarações de entidade. Porque construídos com má intenção DTDs e entidade declarações podem ser usadas para executar um ataque de negação de serviço, é altamente recomendável que os usuários não passem documentos XML diretamente de fontes não confiáveis para **sp_xml_preparedocument**.  
>   
>  Para atenuar os ataques de expansão de entidade recursiva, **sp_xml_preparedocument** limita a 10.000 o número de entidades que podem ser expandidas em uma única entidade no nível superior de um documento. O limite não se aplica a entidades numéricas ou caractere. Esse limite permite que documentos com muitas referências de entidade sejam armazenados, mas impede que qualquer entidade seja recursivamente expandida em uma cadeia com mais de 10.000 expansões.  
  
> [!NOTE]  
>  **sp_xml_preparedocument** limita o número de elementos que podem ser abertos de uma vez para 256.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
  
 [ *xmltext* ]  
 É o documento XML original. O analisador MSXML analisa este documento XML. *XMLTEXT* é um parâmetro de texto: **char**, **nchar**, **varchar**, **nvarchar**, **texto**, **ntext** ou **xml**. O valor padrão é NULL; nesse caso é criada uma representação interna de um documento XML vazio.  
  
> [!NOTE]  
>  **sp_xml_preparedocument** só pode processar XML não tipado ou texto. Se um valor de instância a ser usado como entrada já é XML digitado, primeiro converta-o em uma nova instância XML digitada ou uma cadeia de caracteres e, em seguida, passe esse valor como entrada. Para obter mais informações, consulte [Comparar XML digitado com XML não digitado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
 [ *xpath_namespaces* ]  
 Especifica as declarações de namespace usadas em expressões XPATH de linha e coluna em OPENXML. *xpath_namespaces* é um parâmetro de texto: **char**, **nchar**, **varchar**, **nvarchar**, **texto** , **ntext** ou **xml**.  
  
 O valor padrão é  **\<raiz xmlns:mp = "urn: schemas-microsoft-com: XML-metaprop" >**. *xpath_namespaces* fornece namespace URIs para os prefixos usados em expressões XPath em OPENXML por meio de um documento XML bem formado. *xpath_namespaces* declara o prefixo que deve ser usado para fazer referência ao namespace **urn: schemas-microsoft-com: XML-metaprop**; isso fornece metadados sobre os elementos XML analisados. Embora você possa redefinir o prefixo de namespace para o namespace metaproperty usando essa técnica, esse namespace não será perdido. O prefixo **mp** ainda é válido para **urn: schemas-microsoft-com: XML-metaprop** mesmo se *xpath_namespaces* não tiver tal declaração.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou >0 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-preparing-an-internal-representation-for-a-well-formed-xml-document"></a>A. Preparando uma representação interna de um documento XML bem-formado  
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
 O exemplo a seguir retorna um identificador para a representação interna criada recentemente do documento XML que é fornecido como entrada. A chamada para `sp_xml_preparedocument` preserva o `mp` do prefixo para o mapeamento de namespace metaproperty e adiciona o `xyz` prefixo de mapeamento para o namespace `urn:MyNamespace`.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [XML armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_xml_removedocument &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql.md)   
 [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)  
  
  

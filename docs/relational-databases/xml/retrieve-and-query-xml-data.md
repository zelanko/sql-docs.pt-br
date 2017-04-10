---
title: "Recuperar e consultar dados XML | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "dados XML [SQL Server], recuperando"
  - "recuperação de instância XML"
ms.assetid: 24a28760-1225-42b3-9c89-c9c0332d9c51
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# Recuperar e consultar dados XML
  Este tópico descreve as opções de consulta que você tem que especificar para consultar dados XML. Também descreve as partes de instâncias XML que não são preservadas quando são armazenadas em bancos de dados.  
  
##  <a name="features"></a> Recursos de uma Instância XML que não são preservados  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] preserva o conteúdo da instância XML, mas não preserva aspectos da instância XML que não são considerados significativos no modelo de dados XML. Isso significa que uma instância XML recuperada pode não ser idêntica à instância que foi armazenada no servidor, mas conterá as mesmas informações.  
  
### Declaração XML  
 A declaração XML em uma instância não é preservada quando a instância é armazenada no banco de dados. Por exemplo:  
  
```  
CREATE TABLE T1 (Col1 int primary key, Col2 xml)  
GO  
INSERT INTO T1 values (1, '<?xml version="1.0" encoding="windows-1252" ?><doc></doc>')  
GO  
SELECT Col2  
FROM T1  
```  
  
 O resultado é `<doc/>`.  
  
 A declaração XML, como `<?xml version='1.0'?>`, não é preservada ao armazenar dados XML em uma instância de tipo de dados **xml** . Isso ocorre por design. A declaração XML () e seus atributos (version/encoding/stand-alone) são perdidos após os dados serem convertidos para o tipo **xml**. A declaração XML é tratada como uma diretiva para o analisador XML. Os dados XML são armazenados internamente como ucs-2. Todos os outros PIs na instância XML são preservados.  
  
 [Neste tópico](#top)  
  
### Ordem dos atributos  
 A ordem dos atributos em uma instância XML não é preservada. Quando você consulta a instância XML armazenada na coluna de tipo **xml** , a ordem dos atributos no XML resultante pode ser diferente da instância XML original.  
  
 [Neste tópico](#top)  
  
### Aspas em torno de valores de atributos  
 Aspas simples e aspas duplas em torno de valores de atributos não são preservadas. Os valores de atributos são armazenados no banco de dados como um nome e par de valores. As aspas não são armazenadas. Quando uma XQuery é executada em uma instância XML, o XML resultante é serializado com aspas duplas em torno dos valores dos atributos.  
  
```  
DECLARE @x xml  
-- Use double quotation marks.  
SET @x = '<root a="1" />'  
SELECT @x  
GO  
DECLARE @x xml  
-- Use single quotation marks.  
SET @x = '<root a=''1'' />'  
SELECT @x  
GO  
```  
  
 As duas consultas retornam = `<root a="1" />`.  
  
 [Neste tópico](#top)  
  
### Prefixos de namespace  
 Prefixos de namespace não são preservados. Quando você especifica XQuery em uma coluna de tipo **xml** , o resultado de XML serializado pode retornar prefixos de namespace diferentes.  
  
```  
DECLARE @x xml  
SET @x = '<ns1:root xmlns:ns1="abc" xmlns:ns2="abc">  
            <ns2:SomeElement/>  
          </ns1:root>'  
SELECT @x  
SELECT @x.query('/*')  
GO  
```  
  
 O prefixo de namespace no resultado pode ser diferente. Por exemplo:  
  
```  
<p1:root xmlns:p1="abc"><p1:SomeElement/></p1:root>  
```  
  
 [Neste tópico](#top)  
  
##  <a name="query"></a> A configuração solicitou opções de consulta  
 Ao consultar variáveis ou colunas do tipo **xml** usando métodos de tipo de dados **xml** , as seguintes opções devem ser definidas conforme mostrado.  
  
|Opções SET|Valores necessários|  
|-----------------|---------------------|  
|ANSI_NULLS|ON|  
|ANSI_PADDING|ON|  
|ANSI_WARNINGS|ON|  
|ARITHABORT|ON|  
|CONCAT_NULL_YIELDS_NULL|ON|  
|NUMERIC_ROUNDABORT|DESATIVADO|  
|QUOTED_IDENTIFIER|ON|  
  
 Se as opções não estiverem definidas conforme mostrado, haverá falha em consultas e modificações em métodos de tipo de dados **xml** .  
  
 [Neste tópico](#top)  
  
## Consulte também  
 [Criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md)  
  
  
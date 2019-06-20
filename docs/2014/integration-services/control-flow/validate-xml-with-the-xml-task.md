---
title: Validar XML com a Tarefa XML | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- XML validation
- XML, validating
ms.assetid: 224fc025-c21f-4d43-aa9d-5ffac337f9b0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 76d84c3ea8da6d564db01fba3d02ac15a72fffc3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62829590"
---
# <a name="validate-xml-with-the-xml-task"></a>Validate XML with the XML Task
  Valide documentos XML e obtenha saída de erros completa habilitando a propriedade `ValidationDetails` da tarefa XML.  
  
 A captura de tela a seguir mostra o **Editor da Tarefa XML** com as configurações necessárias para a validação de XML com a saída de erros.  
  
 ![Propriedades da Tarefa XML no Editor da Tarefa XML](../media/xmltaskproperties.jpg "Propriedades da Tarefa XML no Editor da Tarefa XML")  
  
 Antes da disponibilidade da propriedade `ValidationDetails`, a validação do XML pela tarefa XML retornava apenas um resultado true ou false, sem informações sobre erros ou suas localizações. Agora, quando você define `ValidationDetails` como true, o arquivo de saída contém informações detalhadas sobre cada erro, incluindo o número de linha e a posição. Você pode usar essas informações para entender, localizar e corrigir erros em documentos XML.  
  
 A funcionalidade de validação de XML é facilmente dimensionada para documentos XML e grandes números de erros. Como o arquivo de saída é em formato XML, você pode consultar e analisar a saída. Por exemplo, se a saída contiver um grande número de erros, você poderá agrupar os erros usando uma consulta [!INCLUDE[tsql](../../../includes/tsql-md.md)] , conforme descrito neste tópico.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) introduziu a `ValidationDetails` propriedade em [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 2. A propriedade também está disponível no [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e no SQL Server 2016.  
  
## <a name="sample-output-for-xml-thats-valid"></a>Exemplo de saída de XML válida  
 Veja um arquivo de saída de exemplo com os resultados da validação para um arquivo XML válido.  
  
```xml  
  
<root xmlns:ns="https://schemas.microsoft.com/xmltools/2002/xmlvalidation">  
    <metadata>  
        <result>true</result>  
        <errors>0</errors>  
        <warnings>0</warnings>  
        <startTime>2015-05-28T10:27:22.087</startTime>  
        <endTime>2015-05-28T10:29:07.007</endTime>  
        <xmlFile>d:\Temp\TestData.xml</xmlFile>  
        <xsdFile>d:\Temp\TestSchema.xsd</xsdFile>  
    </metadata>  
    <messages />  
</root>  
```  
  
## <a name="sample-output-for-xml-thats-not-valid"></a>Exemplo de saída de XML que não é válido  
 Veja um arquivo de saída de exemplo com os resultados de validação para um arquivo XML que contém um pequeno número de erros. O texto dos elementos \<error> foi encapsulado para facilitar a leitura.  
  
```xml  
  
<root xmlns:ns="https://schemas.microsoft.com/xmltools/2002/xmlvalidation">  
    <metadata>  
        <result>false</result>  
        <errors>2</errors>  
        <warnings>0</warnings>  
        <startTime>2015-05-28T10:45:09.538</startTime>  
        <endTime>2015-05-28T10:45:09.558</endTime>  
        <xmlFile>C:\Temp\TestData.xml</xmlFile>  
        <xsdFile>C:\Temp\TestSchema.xsd</xsdFile>  
    </metadata>  
    <messages>  
        <error line="5" position="26">The 'ApplicantRole' element is invalid - The value 'wer3' is invalid  
    according to its datatype 'ApplicantRoleType' - The Enumeration constraint failed.</error>  
        <error line="16" position="28">The 'Phone' element is invalid - The value 'we3056666666' is invalid  
     according to its datatype 'phone' - The Pattern constraint failed.</error>  
    </messages>  
</root>  
```  
  
## <a name="analyze-xml-validation-output-with-a-transact-sql-query"></a>Analisar a saída de validação de XML com uma consulta Transact-SQL  
 Se o resultado da validação do XML contiver um grande número de erros, você poderá usar uma consulta [!INCLUDE[tsql](../../../includes/tsql-md.md)] para carregar a saída no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Em seguida, você pode analisar a lista de erros com todos os recursos da linguagem T-SQL, incluindo WHERE, GROUP BY, ORDER BY, JOIN e assim por diante.  
  
```sql  
DECLARE @xml XML;  
  
SELECT @xml = XmlDoc     
FROM OPENROWSET (BULK N'C:\Temp\XMLValidation_2016-02-212T10-41-00.xml', SINGLE_BLOB) AS Tab(XmlDoc);  
  
-- Query # 1, flat list of errors  
-- convert to relational/rectangular  
;WITH XMLNAMESPACES ('https://schemas.microsoft.com/xmltools/2002/xmlvalidation' AS ns), rs AS  
(  
SELECT col.value('@line','INT') AS line  
     , col.value('@position','INT') AS position  
     , col.value('.','VARCHAR(1024)') AS error  
FROM @XML.nodes('/root/messages/error') AS tab(col)  
)  
SELECT * FROM rs;  
-- WHERE error LIKE '%whatever_string%'  
  
-- Query # 2, count of errors grouped by the error message  
-- convert to relational/rectangular  
;WITH XMLNAMESPACES ('https://schemas.microsoft.com/xmltools/2002/xmlvalidation' AS ns), rs AS  
(  
SELECT col.value('@line','INT') AS line  
     , col.value('@position','INT') AS position  
     , col.value('.','VARCHAR(1024)') AS error  
FROM @XML.nodes('/root/messages/error') AS tab(col)  
)  
SELECT COALESCE(error,'Total # of errors:') AS [error], COUNT(*) AS [counter]  
FROM rs  
GROUP BY GROUPING SETS ((error), ())  
ORDER BY 2 DESC, COALESCE(error, 'Z');  
  
```  
  
 Veja o resultado no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] da consulta do segundo exemplo mostrada no texto anterior.  
  
 ![Consulta para agrupar erros de XML no Management Studio](../media/queryforxmlerrors.jpg "Consulta para agrupar erros de XML no Management Studio")  
  
## <a name="see-also"></a>Consulte também  
 [XML Task](xml-task.md)   
 [Editor da Tarefa XML &#40;página Geral&#41;](../xml-task-editor-general-page.md)  
  
  

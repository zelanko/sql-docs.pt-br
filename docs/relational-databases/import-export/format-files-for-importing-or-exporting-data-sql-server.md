---
title: "Arquivos de formato para importação ou exportação de dados (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bulk exporting [SQL Server], format files
- bulk importing [SQL Server], format files
- format files [SQL Server]
ms.assetid: b7b97d68-4336-4091-aee4-1941fab568e3
caps.latest.revision: "41"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 47bda013e165fb5907257642a023ae8455d5e413
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="format-files-for-importing-or-exporting-data-sql-server"></a>Arquivos de formato para importação ou exportação de dados (SQL Server)
  Na importação de dados em massa para uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou na exportação em massa de dados de uma tabela, você pode usar um *arquivo de formato* para armazenar todas as informações necessárias para exportar ou importar dados em massa. Isso inclui informações de formato para cada campo em um arquivo de dados relativo para essa tabela.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dá suporte a dois tipos de arquivos de formato: arquivos de formato XML e não XML. Os arquivos de formato XML e não XML contêm descrições de cada campo de um arquivo de dados, e arquivos de formato XML também contêm descrições das colunas das tabelas correspondentes. Geralmente, arquivos de formato XML e não XML são intercambiáveis. Entretanto, recomendamos que você use a sintaxe XML para novos arquivos de formato porque eles oferecem diversas vantagens em relação aos arquivos de formato não XML. Para obter mais informações, veja [Arquivos de formato XML &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md).  
  
  
##  <a name="Benefits"></a> Benefícios de arquivos de formato  
  
-   Fornece um sistema flexível para gravar arquivos de dados que exigem pouca ou nenhuma edição para estar em conformidade com outros formatos de dados ou para ler arquivos de dados de outro software.  
  
-   Habilita-o a importar dados em massa sem precisar adicionar ou excluir dados desnecessários, nem reordenar dados existentes no arquivo de dados. Os arquivos de formato são particularmente úteis quando existe uma incompatibilidade entre campos no arquivo de dados e as colunas na tabela.  
  
##  <a name="ExamplesOfFFs"></a> Exemplos de arquivos de formato  
 Os exemplos abaixo mostram o layout de um arquivo de formato não XML e de um arquivo de formato XML. Esses arquivos de formato correspondem à tabela `HumanResources.myTeam` no banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Essa tabela contém quatro colunas: `EmployeeID`, `Name`, `Title` e `ModifiedDate`.  
  
> [!NOTE]  
>  Para obter informações sobre essa tabela e como criá-la, veja [Tabela de exemplo HumanResources.myTeam &#40;SQL Server&#41;](../../relational-databases/import-export/humanresources-myteam-sample-table-sql-server.md).  
  
### <a name="a-using-a-non-xml-format-file"></a>A. Usando um arquivo de formato não XML  
 O arquivo de formato não XML seguinte usa o formato de dados nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a tabela `HumanResources.myTeam` . Esse arquivo de formato foi criado usando o comando `bcp` a seguir.  
  
```cmd 
bcp AdventureWorks.HumanResources.myTeam format nul -f myTeam.Fmt -n -T   
The contents of this format file are as follows: 9.0  
4  
1       SQLSMALLINT   0       2       ""   1     EmployeeID               ""  
2       SQLNCHAR      2       100     ""   2     Name                     SQL_Latin1_General_CP1_CI_AS  
3       SQLNCHAR      2       100     ""   3     Title                    SQL_Latin1_General_CP1_CI_AS  
4       SQLNCHAR      2       100     ""   4     Background               SQL_Latin1_General_CP1_CI_AS  
```  
  
 Para obter mais informações, veja [Arquivos de formato não XML &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md).  
  
  
### <a name="b-using-an-xml-format-file"></a>B. Usando um arquivo de formato XML  
 O seguinte arquivo de formato XML usa o formato de dados nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a tabela `HumanResources.myTeam` . Esse arquivo de formato foi criado usando o comando `bcp` a seguir.  
  
```cmd
bcp AdventureWorks.HumanResources.myTeam format nul -f myTeam.Xml -x -n -T   
```  
  
 O arquivo de formato contém:  
  
```xml
 <?xml version="1.0"?>  
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="NativePrefix" LENGTH="1"/>  
  <FIELD ID="2" xsi:type="NCharPrefix" PREFIX_LENGTH="2" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="NCharPrefix" PREFIX_LENGTH="2" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="4" xsi:type="NCharPrefix" PREFIX_LENGTH="2" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="EmployeeID" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Name" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="Title" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="Background" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
 Para obter mais informações, veja [Arquivos de formato XML &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md).  
  
  
##  <a name="WhenFFrequired"></a> Quando um arquivo de formato é necessário?  
 Uma instrução INSERT... A instrução SELECT * FROM OPENROWSET (BULK...) sempre requer um arquivo de formato.  
  
-   Para **bcp** ou BULK INSERT, em situações simples, usar um arquivo de formato é opcional e raramente necessário. No entanto, em situações complexas de importação em massa, um arquivo de formato é frequentemente necessário.  
  
 Os arquivos de formato serão necessários se:  
  
-   O mesmo arquivo de dados for usado como origem para diversas tabelas que têm esquemas diferentes.  
  
-   O arquivo de dados tiver um número diferente de campos do número de colunas da tabela de destino; por exemplo:  
  
    -   A tabela de destino contém pelo menos uma coluna para a qual há um valor padrão definido ou é permitido NULL.  
  
    -   Os usuários não têm permissões SELECT/INSERT em uma ou mais colunas na tabela.  
  
    -   Um único arquivo de dados é usado com duas ou mais tabelas que têm esquemas diferentes.  
  
-   A ordem de colunas é diferente para o arquivo de dados e a tabela.  
  
-   Os caracteres de terminação ou o comprimento dos prefixos diferem entre as colunas do arquivo de dados.  
  
> [!NOTE]  
>  Na ausência de um arquivo de formato, se um comando **bcp** especificar uma opção de formato de dados (**-n**, **-c**, **-w**ou **-N**), ou uma operação BULK INSERT especificar a opção DATAFILETYPE, o formato de dados especificado será usado como o método padrão de interpretação dos campos do arquivo de dados.  
  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criar um arquivo de formato &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)  
  
-   [Usar um arquivo de formato para importação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar um campo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos de formato não XML &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)   
 [Arquivos de formato XML &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)   
 [Formatos de dados para importação ou exportação em massa &#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)  
  
  

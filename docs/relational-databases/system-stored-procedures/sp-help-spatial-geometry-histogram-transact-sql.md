---
title: sp_help_spatial_geometry_histogram (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geometry_histogram
- sp_help_spatial_geometry_histogram_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geometry_histogram
ms.assetid: 036aaf61-df3e-40f7-aa4e-62983c5a37bd
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5acd841815df5329fe79624174c00e2694e65781
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="sphelpspatialgeometryhistogram-transact-sql"></a>sp_help_spatial_geometry_histogram (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Facilita o chaveamento da caixa delimitadora e dos parâmetros de grade de um índice espacial.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_spatial_geometry_histogram [ @tabname =] 'tabname'   
     [ , [ @colname = ] 'columnname' ]   
     [ , [ @resolution = ] 'resolution' ]  
     [ , [ @xmin = ] 'minx' ]   
     [ , [ @ymin = ] 'miny' ]   
     [ ,.[ @xmax = ] 'maxx' ]  
     [ , [ @ymax = ] 'maxy' ]  
     [ , [ @sample = ] 'sample' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@tabname =**] **'***tabname***'**  
 É o nome qualificado ou não da tabela para a qual o índice espacial foi especificado.  
  
 As aspas somente serão requeridas se uma tabela qualificada for especificada. Se um nome completamente qualificado, incluindo um nome de banco de dados, for fornecido, o nome do banco de dados deverá ser o nome do banco de dados atual. *tabname* é **sysname**, sem padrão.  
  
 [  **@colname =** ] **'***colname***'**  
 É o nome da coluna espacial especificada. *colName* é um **sysname**, sem padrão.  
  
 [  **@resolution =** ] **'***resolução***'**  
 É a resolução da caixa delimitadora. Os valores válidos são de 10 a 5000. *resolução* é um **tinyint**, sem padrão.  
  
 [  **@xmin =** ] **'***xmin***'**  
 É a propriedade de caixa delimitadora do mínimo de X. *xMin* é um **float**, sem padrão.  
  
 [  **@ymin =** ] **'***ymin***'**  
 É a propriedade de caixa delimitadora do mínimo de Y. *yMin* é um **float**, sem padrão.  
  
 [  **@xmax =** ] **'***xmax***'**  
 É a propriedade de caixa delimitadora do máximo de X. *xMax* é um **float**, sem padrão.  
  
 [  **@ymax =** ] **'***ymax***'**  
 É a propriedade de caixa delimitadora do máximo de Y. *yMax* é um **float**, sem padrão.  
  
 [  **@sample =** ] **'***exemplo***'**  
 É a porcentagem da tabela usada. Os valores válidos são de 0 a 100. *exemplo* é um **float**. Valor padrão é 100.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor de tabela é retornado. A grade a seguir descreve o conteúdo da coluna da tabela.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**cellid**|**int**|Representa a ID exclusiva de cada célula. A contagem é iniciada a partir de 1.|  
|**célula**|**geometria**|É um polígono retangular que representa cada célula. A forma de célula é idêntica à forma de célula usada para a indexação espacial.|  
|**row_count**|**bigint**|Indica o número de objetos espaciais que estão tocando ou contendo a célula.|  
  
## <a name="permissions"></a>Permissões  
 Usuário deve ser um membro do **pública** função. Requer permissão READ ACCESS no servidor e no objeto.  
  
## <a name="remarks"></a>Comentários  
 A guia SSMS espacial mostra uma representação gráfica dos resultados. Você pode consultar os resultados em relação à janela espacial para obter um número aproximado dos itens do resultado. Os objetos da tabela podem abranger mais de uma célula, portanto, a soma de células pode ser maior que o número de objetos reais.  
  
 Uma linha adicional pode ser adicionada ao conjunto de resultados que contém o número de objetos que estão fora da caixa delimitadora ou tocando a borda da caixa delimitadora. O **cellid** dessa linha é 0 e o **célula** dessa linha contém um **LineString** que representa a caixa delimitadora. Essa linha representa o espaço inteiro fora da caixa delimitadora.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma tabela de exemplo e, em seguida, chama **sp_help_spatial_geometry_histogram** na tabela.  
  
 `USE AdventureWorksDW2012`  
  
 `GO`  
  
 `-- Set database compatibility for circular arc segments`  
  
 `ALTER DATABASE AdventureWorksDW2012`  
  
 `SET COMPATIBILITY_LEVEL = 110;`  
  
 `GO`  
  
 `-- Create table to execute sp_help_spatial_geometry_histogram on`  
  
 `CREATE TABLE TownSites`  
  
 `(`  
  
 `Location geometry NULL,`  
  
 `SiteName nvarchar(50) NULL`  
  
 `)`  
  
 `GO`  
  
 `-- Insert site data into table`  
  
 `DECLARE @g geometry;`  
  
 `SET @g = geometry::Parse('POINT(0 0)');`  
  
 `INSERT INTO TownSites(Location, SiteName)`  
  
 `SELECT @g, N'Booth Map';`  
  
 `SET @g = geometry::Parse('POLYGON((1 1, 1 2, 2 2, 2 1, 1 1))');`  
  
 `INSERT INTO TownSites(Location, SiteName)`  
  
 `SELECT @g, N'Town Hall';`  
  
 `SET @g = geometry::Parse('CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(-1 0, 0 -1, 1 0),(1 0, 1 2, -1 0)))');`  
  
 `INSERT INTO TownSites(Location, SiteName)`  
  
 `SELECT @g, N'Main Park';`  
  
 `SET @g = geometry::Parse('CIRCULARSTRING(1 5, 2 2, 5 1)');`  
  
 `INSERT INTO TownSites(Location, SiteName)`  
  
 `SELECT @g, N'Main Road';`  
  
 `-- Call proc to see data within bounding box`  
  
 `EXEC sp_help_spatial_geometry_histogram @tabname = TownSites, @colname = Location, @resolution = 64, @xmin = -2, @ymin = -2, @xmax = 3, @ymax = 3, @sample = 100;`  
  
 `GO`  
  
 `DROP TABLE TownSites;`  
  
 `GO`  
  
## <a name="see-also"></a>Consulte também  
 [Índice espacial armazenados procedimentos &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)  
  
  

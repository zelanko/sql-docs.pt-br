---
title: CREATE SPATIAL INDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SPATIAL INDEX
- CREATE SPATIAL INDEX
- CREATE_SPATIAL_INDEX_TSQL
- SPATIAL_INDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- spatial indexes [SQL Server], creating
- index creation [SQL Server], spatial indexes
- CREATE SPATIAL INDEX statement
- CREATE INDEX statement
ms.assetid: ee6b9116-a7ff-463a-a9f0-b360804d8678
caps.latest.revision: 89
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 3ff094713faa5a399030b5470aa5af7df60371b7
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37790297"
---
# <a name="create-spatial-index-transact-sql"></a>CREATE SPATIAL INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cria um índice espacial em uma tabela e coluna especificadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um índice pode ser criado antes que haja dados na tabela. Podem ser criados índices em tabelas ou exibições em outro banco de dados mediante a especificação de um nome de banco de dados qualificado. Índices espaciais exigem que a tabela tenha uma chave primária clusterizada. Para obter informações sobre índices espaciais, veja [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- SQL Server Syntax  
  
CREATE SPATIAL INDEX index_name   
  ON <object> ( spatial_column_name )  
    {  
       <geometry_tessellation> | <geography_tessellation>  
    }   
  [ ON { filegroup_name | "default" } ]  
[;]   
  
<object> ::=  
    [ database_name. [ schema_name ] . | schema_name. ]  table_name  
  
<geometry_tessellation> ::=  
{   
  <geometry_automatic_grid_tessellation>   
| <geometry_manual_grid_tessellation>   
}  
  
<geometry_automatic_grid_tessellation> ::=  
{  
    [ USING GEOMETRY_AUTO_GRID ]  
          WITH  (  
        <bounding_box>  
            [ [,] <tessellation_cells_per_object> [ ,…n] ]  
            [ [,] <spatial_index_option> [ ,…n] ]  
                 )  
}  
  
<geometry_manual_grid_tessellation> ::=  
{  
       [ USING GEOMETRY_GRID ]  
         WITH (  
                    <bounding_box>  
                        [ [,]<tessellation_grid> [ ,…n] ]  
                        [ [,]<tessellation_cells_per_object> [ ,…n] ]  
                        [ [,]<spatial_index_option> [ ,…n] ]  
   )  
}   
  
<geography_tessellation> ::=  
{  
      <geography_automatic_grid_tessellation> | <geography_manual_grid_tessellation>  
}  
  
<geography_automatic_grid_tessellation> ::=  
{  
    [ USING GEOGRAPHY_AUTO_GRID ]  
    [ WITH (  
        [ [,] <tessellation_cells_per_object> [ ,…n] ]  
        [ [,] <spatial_index_option> ]  
     ) ]  
}  
  
<geography_manual_grid_tessellation> ::=  
{  
    [ USING GEOGRAPHY_GRID ]  
    [ WITH (  
                [ <tessellation_grid> [ ,…n] ]  
                [ [,] <tessellation_cells_per_object> [ ,…n] ]  
                [ [,] <spatial_index_option> [ ,…n] ]  
                ) ]  
}  
  
<bounding_box> ::=  
{  
      BOUNDING_BOX = ( {  
       xmin, ymin, xmax, ymax   
       | <named_bb_coordinate>, <named_bb_coordinate>, <named_bb_coordinate>, <named_bb_coordinate>   
  } )  
}  
  
<named_bb_coordinate> ::= { XMIN = xmin | YMIN = ymin | XMAX = xmax | YMAX=ymax }  
  
<tesselation_grid> ::=  
{   
    GRIDS = ( { <grid_level> [ ,...n ] | <grid_size>, <grid_size>, <grid_size>, <grid_size>  }   
        )  
}  
<tesseallation_cells_per_object> ::=  
{   
   CELLS_PER_OBJECT = n   
}  
  
<grid_level> ::=  
{  
     LEVEL_1 = <grid_size>   
  |  LEVEL_2 = <grid_size>   
  |  LEVEL_3 = <grid_size>   
  |  LEVEL_4 = <grid_size>   
}  
  
<grid_size> ::= { LOW | MEDIUM | HIGH }  
  
<spatial_index_option> ::=  
{  
    PAD_INDEX = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY = OFF  
  | STATISTICS_NORECOMPUTE = { ON | OFF }  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = OFF  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
    | DATA_COMPRESSION = { NONE | ROW | PAGE }  
}  
  
```  
  
```  
-- Windows Azure SQL Database Syntax   
  
CREATE SPATIAL INDEX index_name   
    ON <object> ( spatial_column_name )   
    {   
      [ USING <geometry_grid_tessellation> ]   
          WITH ( <bounding_box>   
                [ [,] <tesselation_parameters> [,... n ] ]   
                [ [,] <spatial_index_option> [,... n ] ] )   
     | [ USING <geography_grid_tessellation> ]   
          [ WITH ( [ <tesselation_parameters> [,... n ] ]   
                   [ [,] <spatial_index_option> [,... n ] ] ) ]   
    }  
  
[ ; ]  
  
<object> ::=  
{  
    [database_name. [schema_name ] . | schema_name. ]   
                table_name   
}  
  
<geometry_grid_tessellation> ::=   
{ GEOMETRY_GRID }  
  
<bounding_box> ::=   
BOUNDING_BOX = ( {  
        xmin, ymin, xmax, ymax   
   | <named_bb_coordinate>, <named_bb_coordinate>, <named_bb_coordinate>, <named_bb_coordinate>   
  } )  
  
<named_bb_coordinate> ::= { XMIN = xmin | YMIN = ymin | XMAX = xmax | YMAX=ymax }  
  
<tesselation_parameters> ::=   
{   
    GRIDS = ( { <grid_density> [ ,... n ] | <density>, <density>, <density>, <density>  } )   
  | CELLS_PER_OBJECT = n   
}  
  
<grid_density> ::=   
{  
     LEVEL_1 = <density>   
  |  LEVEL_2 = <density>   
  |  LEVEL_3 = <density>   
  |  LEVEL_4 = <density>   
}  
  
<density> ::= { LOW | MEDIUM | HIGH }  
  
<geography_grid_tessellation> ::=   
{ GEOGRAPHY_GRID }  
  
<spatial_index_option> ::=   
{  
    IGNORE_DUP_KEY = OFF  
  | STATISTICS_NORECOMPUTE = { ON | OFF }  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = OFF   
}  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *index_name*  
 É o nome do índice. Os nomes de índice devem ser exclusivos em uma tabela, mas não precisam ser exclusivos em um banco de dados. Os nomes de índice precisam seguir as regras para [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 ON \<object> ( *spatial_column_name* )  
 Especifica o objeto (banco de dados, esquema ou tabela) no qual o índice será criado e o nome da coluna espacial.  
  
 *spatial_column_name* especifica a coluna espacial no qual o índice está baseado. Apenas uma coluna espacial pode ser especificada em uma única definição de índice espacial; entretanto, vários índices espaciais podem ser criados em uma coluna **geometry** ou **geography**.  
  
 USING  
 Indica o esquema de mosaico do índice espacial. Este parâmetro usa o valor tipo-específico, mostrado na seguinte tabela:  
  
|Tipo de dados da coluna|Esquema de mosaico|  
|-------------------------|-------------------------|  
|**geometria**|GEOMETRY_GRID|  
|**geometria**|GEOMETRY_AUTO_GRID|  
|**geografia**|GEOGRAPY_GRID|  
|**geografia**|GEOGRAPHY_AUTO_GRID|  
  
 Um índice espacial pode ser criado apenas em uma coluna do tipo **geometria** ou **geografia**. Caso contrário, será gerado um erro. Além disso, se um parâmetro inválido de determinado tipo for transmitido, um erro será gerado.  
  
 Para obter informações sobre como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implementa o mosaico, veja [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md).  
  
 ON *filegroup_name*  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Cria o índice especificado no grupo de arquivos especificado. Se nenhum local for especificado e a tabela não for particionada, o índice utilizará o mesmo grupo de arquivos da tabela subjacente. O grupo de arquivos já deve existir.  
  
 ON "padrão"  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Cria o índice especificado no grupo de arquivos padrão.  
  
 Nesse contexto, default não é uma palavra-chave. É um identificador para o grupo de arquivos padrão e deve ser delimitado, como em ON "default" ou ON [default]. Se "padrão" for especificado, a opção QUOTED_IDENTIFIER deverá ser definida como ON para a sessão atual. Essa é a configuração padrão. Para obter mais informações, veja [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
 **\<object>::=**  
  
 É o objeto totalmente qualificado ou não totalmente qualificado a ser indexado.  
  
 *database_name*  
 É o nome do banco de dados.  
  
 *schema_name*  
 É o nome do esquema ao qual a tabela pertence.  
  
 *table_name*  
 É o nome da tabela a ser indexada.  
  
 O Banco de Dados SQL do Windows Azure oferece suporte ao formato de nome de três partes database_name.[schema_name].object_name quando o database_name é o banco de dados atual ou o database_name é tempdb e o object_name começa com #.  
  
### <a name="using-options"></a>Opções USING  
 GEOMETRY_GRID  
 Especifica o esquema de mosaico da grade **geometry** que está sendo usado. GEOMETRY_GRID só pode ser especificado em uma coluna do tipo de dados **geometria**.  GEOMETRY_GRID permite o ajuste manual do esquema de mosaico.  
  
 GEOMETRY_AUTO_GRID  
 **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Só pode ser especificado em uma coluna do tipo de dados geometry. Este é o padrão desse tipo de dados e não precisa ser especificado.  
  
 GEOGRAPHY_GRID  
 Especifica o esquema de mosaico da grade geográfica. GEOGRAPHY_GRID só pode ser especificado em uma coluna do tipo de dados **geografia**.  
  
 GEOGRAPHY_AUTO_GRID  
 **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Só pode ser especificado em uma coluna do tipo de dados geography.  Este é o padrão desse tipo de dados e não precisa ser especificado.  
  
### <a name="with-options"></a>Opções WITH  
BOUNDING_BOX  
Especifica quatro tuplas numéricas que definem as quatro coordenadas da caixa delimitadora: as coordenadas x mínima e y mínima do canto inferior esquerdo e as coordenadas x máxima e y máxima do canto superior direito.  
  
 *xmin*  
 Especifica a coordenada x do canto inferior esquerdo da caixa delimitadora.  
  
 *ymin*  
 Especifica a coordenada y do canto inferior esquerdo da caixa delimitadora.  
  
 *xmax*  
 Especifica a coordenada x do canto superior direito da caixa delimitadora.  
  
 *ymax*  
 Especifica a coordenada y do canto superior direito da caixa delimitadora.  
  
 XMIN = *xmin*  
 Especifica o nome da propriedade e o valor da coordenada x do canto inferior esquerdo da caixa delimitadora.  
  
 YMIN =*ymin*  
 Especifica o nome da propriedade e o valor da coordenada y do canto inferior esquerdo da caixa delimitadora.  
  
 XMAX =*xmax*  
 Especifica o nome da propriedade e o valor da coordenada x do canto superior direito da caixa delimitadora.  
  
 YMAX =*ymax*  
 Especifica o nome da propriedade e o valor da coordenada y do canto superior direito da caixa delimitadora.  
  
 > [!NOTE]
 > As coordenadas da caixa delimitadora só se aplicam em uma cláusula USING GEOMETRY_GRID.  
 >
 > *xMax* deve ser maior que *xmin* e *ymax* deve ser maior que *ymin*. É possível especificar qualquer representação válida do valor [float](../../t-sql/data-types/float-and-real-transact-sql.md) supondo que: *xmax* > *xmin* e *ymax* > *ymin*. Caso contrário, os erros apropriados serão gerados.  
 > 
 > Não há valores padrão.  
 >
 > Os nomes de propriedades da caixa delimitadora não diferenciam maiúsculas de minúsculas, independentemente do agrupamento de banco de dados.  
  
 Cada nome de propriedade deve ser especificado somente uma única vez. Você pode especificá-los em qualquer ordem. Por exemplo, as seguintes cláusulas são equivalentes:  
  
-   BOUNDING_BOX =( XMIN =*xmin*, YMIN =*ymin*, XMAX =*xmax*, YMAX =*ymax* )  
  
-   BOUNDING_BOX =( XMIN =*xmin*, XMAX =*xmax*, YMIN =*ymin*, YMAX =*ymax*)  
  
GRIDS  
Define a densidade da grade em cada nível de um esquema de mosaico. Quando GEOMETRY_AUTO_GRID e GEOGRAPHY_AUTO_GRID são selecionados, esta opção é desabilitada.  
  
 Para obter informações sobre mosaico, veja [visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md).  
  
 Os parâmetros GRIDS são os seguintes:  
  
 LEVEL_1  
 Especifica a grade de primeiro nível (superior).  
  
 LEVEL_2  
 Especifica a grade de nível secundário.  
  
 LEVEL_3  
 Especifica a grade de terceiro nível.  
  
 LEVEL_4  
 Especifica a grade de quarto nível.  
  
 LOW  
 Especifica a densidade mais baixa possível da grade em um determinado nível. LOW é igual a 16 células (uma grade 4x4).  
  
 **MEDIUM**  
 Especifica a densidade média da grade em um determinado nível. MEDIUM é igual a 64 células (uma grade 8x8).  
  
 HIGH  
 Especifica a densidade mais alta possível para a grade em um determinado nível. HIGH é igual a 256 células (uma grade 16x16).  
  
> [!NOTE] 
> O uso de nomes de nível permite especificar os níveis em qualquer ordem e omitir níveis. Se você utilizar o nome para qualquer nível, deverá usar o nome de qualquer outro nível especificado. Se um nível for omitido, o padrão da sua densidade será MEDIUM.  
  
> [!WARNING] 
> Se uma densidade inválida for especificada, um erro será gerado.  
  
CELLS_PER_OBJECT =*n*  
Especifica o número de células de mosaico por objeto, que pode ser usado para um único objeto espacial no índice pelo processo de mosaico. *n* pode ser qualquer inteiro entre 1 e 8192, inclusive. Se um número inválido for passado ou se o número for maior que o máximo de células para o mosaico especificado, um erro será gerado.  
  
 CELLS_PER_OBJECT tem os seguintes valores padrão:  
  
|Opção USING|Células padrão por objeto|  
|------------------|------------------------------|  
|GEOMETRY_GRID|**16**|  
|GEOMETRY_AUTO_GRID|**8**|  
|GEOGRAPHY_GRID|**16**|  
|GEOGRAPHY_AUTO_GRID|**12**|  
  
 No nível superior, se um objeto abranger mais células que o especificado por *n*, a indexação usará o número de células necessário para fornecer um mosaico de nível superior completo. Nesses casos, um objeto poderia receber mais que o número de células especificado. Nesse caso, o número máximo é o número de células geradas pela grade de nível superior, o que depende da densidade.  
  
 O valor CELLS_PER_OBJECT é usado pela regra de mosaico de células-por-objeto. Para obter informações sobre as regras de mosaico, veja [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md).  
  
PAD_INDEX = { ON | **OFF** }  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica o preenchimento do índice. O padrão é OFF.  
  
 ON  
 Indica que o percentual de espaço livre especificado por *fillfactor* é aplicado às páginas no nível intermediário do índice.  
  
 OFF ou *fillfactor* não está especificado  
 Indica que as páginas de nível intermediário são preenchidas até próximo de sua capacidade, deixando espaço suficiente para pelo menos uma linha do tamanho máximo que o índice pode ter, considerando o conjunto de chaves nas páginas intermediárias.  
  
 A opção PAD_INDEX só é útil quando FILLFACTOR é especificado, porque PAD_INDEX usa a porcentagem especificada por FILLFACTOR. Se a porcentagem especificada para FILLFACTOR não for grande o suficiente para permitir uma linha, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] substituirá a porcentagem internamente para permitir o valor mínimo. O número de linhas em uma página de índice intermediária nunca é menor do que dois, independentemente de quão baixo seja o valor de *fillfactor*.  
  
FILLFACTOR =*fillfactor*  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica uma porcentagem que indica quanto o [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve preencher o nível folha de cada página de índice durante a criação ou recriação do índice. *fillfactor* deve ser um valor inteiro de 1 a 100. O padrão é 0. Se *fillfactor* for 100 ou 0, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] criará índices com páginas folha preenchidas até a capacidade máxima.  
  
> [!NOTE]  
>  Os valores de fator de preenchimento 0 e 100 são iguais em todos os aspectos.  
  
 A configuração FILLFACTOR se aplica somente quando o índice é criado ou recriado. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] não mantém dinamicamente a porcentagem especificada de espaço vazio nas páginas. Para exibir a configuração do fator de preenchimento, use a exibição do catálogo [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
> [!IMPORTANT]  
> A criação de um índice clusterizado com FILLFACTOR inferior a 100 afeta a quantidade de espaço de armazenamento ocupado pelos dados, porque o [!INCLUDE[ssDE](../../includes/ssde-md.md)] redistribui os dados quando cria o índice clusterizado.  
  
 Para obter mais informações, veja [Especificar fator de preenchimento para um índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md).  
  
SORT_IN_TEMPDB = { ON | **OFF** }  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica se os resultados de classificação temporários devem ser armazenados em tempdb. O padrão é OFF.  
  
 ON  
 Os resultados de classificação intermediários usados para criar o índice são armazenados em tempdb. Isso pode reduzir o tempo necessário para criar um índice se tempdb estiver em um conjunto de discos diferente do banco de dados de usuário. Entretanto, isso aumenta o espaço em disco usado durante a criação do índice.  
  
 OFF  
 Os resultados intermediários de classificação são armazenados no mesmo banco de dados que o índice.  
  
 Além do espaço necessário no banco de dados de usuário para criar o índice, tempdb deve ter aproximadamente a mesma quantidade de espaço adicional para armazenar os resultados de classificação intermediários. Para obter mais informações, consulte a [Opção SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md).  
  
IGNORE_DUP_KEY =**OFF**  
Não tem nenhum efeito para índices espaciais porque o tipo de índice nunca é exclusivo. Não defina essa opção como ON; caso contrário, um erro será gerado.  
  
STATISTICS_NORECOMPUTE = { ON | **OFF**}  
Especifica se as estatísticas de distribuição são recomputadas. O padrão é OFF.  
  
 ON  
 As estatísticas desatualizadas não são recalculadas automaticamente.  
  
 OFF  
 A atualização automática de estatísticas está habilitada.  
  
 Para restaurar a atualização automática de estatísticas, defina STATISTICS_NORECOMPUTE como OFF ou execute UPDATE STATISTICS sem a cláusula NORECOMPUTE.  
  
> [!IMPORTANT]  
> Se o recálculo automático de estatísticas de distribuição for desabilitado, o otimizador de consulta possivelmente ficará impedido de selecionar planos de execução ideais para consultas que envolvam a tabela.  
  
DROP_EXISTING = { ON | **OFF** }  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica que o índice espacial nomeado preexistente seja removido e recriado. O padrão é OFF.  
  
 ON  
 O índice existente é removido e recriado. O nome de índice especificado deve ser igual ao índice existente atualmente; no entanto, a definição de índice pode ser modificada. Por exemplo, você pode especificar colunas, ordens de classificação, esquemas de partição ou opções de índice diferentes.  
  
 OFF  
 Um erro será exibido se o nome de índice especificado já existir.  
  
 O tipo de índice não pode ser alterado com DROP_EXISTING.  
  
ONLINE =**OFF**  
Especifica que as tabelas subjacentes e os índices associados não estão disponíveis para consultas e modificação de dados durante a operação de índice. Nesta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], não há suporte para a criação de índices espaciais online. Se esta opção for definida como ON para um índice espacial, um erro será gerado. Omita a opção ONLINE ou defina ONLINE como OFF.  
  
 Uma operação de índice offline que cria, recria ou remove um índice espacial adquire um bloqueio Sch-M (Modificação de esquema) na tabela. Isso evita o acesso de todos os usuários à tabela subjacente enquanto durar a operação.  
  
> [!NOTE]  
> As operações de índice online não estão disponíveis em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
ALLOW_ROW_LOCKS = { **ON** | OFF }  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica se bloqueios de linha são permitidos. O padrão é ON.  
  
 ON  
 Bloqueios de linha são permitidos ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de linha são usados.  
  
 OFF  
 Bloqueios de linha não são usados.  
  
ALLOW_PAGE_LOCKS = { **ON** | OFF }  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica se bloqueios de página são permitidos. O padrão é ON.  
  
 ON  
 Bloqueios de página são permitidos ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de página são usados.  
  
 OFF  
 Bloqueios de página não são usados.  
  
MAXDOP =*max_degree_of_parallelism*  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Substitui a opção de configuração `max degree of parallelism` para a duração da operação de índice. Use MAXDOP para limitar o número de processadores usados em uma execução de plano paralelo. O máximo é de 64 processadores.  
  
> [!IMPORTANT]  
> Embora a opção MAXDOP tenha suporte sintaticamente, CREATE SPATIAL INDEX utiliza sempre no momento apenas um único processador.  
  
 *max_degree_of_parallelism* pode ser:  
  
 1  
 Suprime a geração de plano paralelo.  
  
 \>1  
 Restringe o número máximo de processadores usados em uma operação de índice paralela ao número especificado, ou menos, com base na carga de trabalho atual do sistema.  
  
 0 (padrão)  
 Usa o número real de processadores, ou menos, com base na carga de trabalho atual do sistema.  
  
 Para obter mais informações, consulte [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!NOTE]  
> As operações de índice paralelas não estão disponíveis em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
DATA_COMPRESSION = {NONE | ROW | PAGE}  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Determina o nível de compactação de dados usado pelo índice.  
  
 Nenhuma  
 Nenhuma compactação de dados usada pelo índice  
  
 ROW  
 Compactação de dados de linha usada pelo índice  
  
 PAGE  
 Compactação de dados de página usada pelo índice  
  
## <a name="remarks"></a>Remarks  
 Todas as opções só podem ser especificadas uma única vez por instrução CREATE SPATIAL INDEX. A especificação de uma duplicata de qualquer opção gera um erro.  
  
 Você pode criar até 249 índices espaciais em cada coluna espacial em uma tabela. A criação de mais de um índice espacial na coluna espacial especificada pode ser útil, por exemplo, para indexar diferentes parâmetros de mosaico em uma única coluna.  
  
> [!IMPORTANT]  
> Existem várias outras restrições na criação de um índice espacial. Para obter mais informações, veja [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md).  
  
 Uma criação de índice não pode usar o paralelismo de processo disponível.  
  
## <a name="methods-supported-on-spatial-indexes"></a>Métodos com suporte em índices espaciais  
 Em algumas condições, os índices espaciais dão suporte a alguns métodos de geometria orientados a conjuntos. Para obter mais informações, veja [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md).  
  
## <a name="spatial-indexes-and-partitioning"></a>Índices espaciais e particionamento  
 Por padrão, se um índice espacial for criado em uma tabela particionada, ele será particionado de acordo com o esquema de partição da tabela. Isso garante que os dados do índice e a linha relacionada sejam armazenados na mesma partição.  
  
 Nesse caso, para alterar o esquema de partição da tabela base, é necessário remover o índice espacial antes de particionar a tabela base novamente. Para evitar essa restrição, ao criar um índice espacial, você pode especificar a opção "ON filegroup". Para obter mais informações, consulte “Índices espaciais e grupos de arquivos”, mais adiante neste tópico.  
  
## <a name="spatial-indexes-and-filegroups"></a>Índices espaciais e grupos de arquivos  
 Por padrão, os índices espaciais são particionados nos mesmos grupos de arquivos que a tabela na qual o índice é especificado. Isso pode ser substituído usando a especificação de grupo de arquivos:  
  
 [ ON { *filegroup_name* | "default" } ]  
  
 Se um grupo de arquivos for especificado para um índice espacial, o índice será colocado nesse grupo de arquivos, independentemente do esquema de particionamento da tabela.  
  
## <a name="catalog-views-for-spatial-indexes"></a>Exibições do catálogo para índices espaciais  
 As exibições do catálogo a seguir são específicas a índices espaciais:  
  
 [sys.spatial_indexes](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md)  
 Representa as principais informações dos índices espaciais.  
  
 [sys.spatial_index_tessellations](../../relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql.md)  
 Representa as informações sobre o esquema de mosaico e os parâmetros de cada um dos índices espaciais.  
  
## <a name="additional-remarks-about-creating-indexes"></a>Comentários adicionais sobre a criação de índices  
 Para obter mais informações sobre a criação de índices, veja a seção “Comentários” em [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ter a permissão ALTER na exibição de tabela ou indexada, ou ser membro da função de servidor fixa sysadmin ou das funções de banco de dados fixas db_ddladmin e db_owner.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-spatial-index-on-a-geometry-column"></a>A. Criando um índice espacial em uma coluna de geometria  
 O exemplo a seguir cria uma tabela nomeada `SpatialTable` que contém uma coluna do tipo **geometry**, `geometry_col`. Em seguida, o exemplo cria um índice espacial, `SIndx_SpatialTable_geometry_col1`, em `geometry_col`. O exemplo usa o esquema de mosaico padrão e especifica a caixa delimitadora.  
  
```sql  
CREATE TABLE SpatialTable(id int primary key, geometry_col geometry);  
CREATE SPATIAL INDEX SIndx_SpatialTable_geometry_col1   
   ON SpatialTable(geometry_col)  
   WITH ( BOUNDING_BOX = ( 0, 0, 500, 200 ) );  
```  
  
### <a name="b-creating-a-spatial-index-on-a-geometry-column"></a>B. Criando um índice espacial em uma coluna de geometria  
 O exemplo a seguir cria um segundo índice espacial, `SIndx_SpatialTable_geometry_col2`, em `geometry_col` na tabela `SpatialTable`. O exemplo especifica `GEOMETRY_GRID` como o esquema de mosaico. O exemplo também especifica a caixa delimitadora, diferentes densidades em diferentes níveis de grade e 64 células por objeto. O exemplo também define o preenchimento de índice como `ON`.  
  
```sql  
CREATE SPATIAL INDEX SIndx_SpatialTable_geometry_col2  
   ON SpatialTable(geometry_col)  
   USING GEOMETRY_GRID  
   WITH (  
    BOUNDING_BOX = ( xmin=0, ymin=0, xmax=500, ymax=200 ),  
    GRIDS = (LOW, LOW, MEDIUM, HIGH),  
    CELLS_PER_OBJECT = 64,  
    PAD_INDEX  = ON );  
```  
  
### <a name="c-creating-a-spatial-index-on-a-geometry-column"></a>C. Criando um índice espacial em uma coluna de geometria  
 O exemplo a seguir cria um terceiro índice espacial, `SIndx_SpatialTable_geometry_col3`, em `geometry_col` na tabela `SpatialTable`. O exemplo usa o esquema de mosaico padrão. O exemplo especifica a caixa delimitadora e usa diferentes densidades de célula no terceiro e no quarto níveis, usando o número padrão de células por objeto.  
  
```sql  
CREATE SPATIAL INDEX SIndx_SpatialTable_geometry_col3  
   ON SpatialTable(geometry_col)  
   WITH (  
    BOUNDING_BOX = ( 0, 0, 500, 200 ),  
    GRIDS = ( LEVEL_4 = HIGH, LEVEL_3 = MEDIUM ) );  
```  
  
### <a name="d-changing-an-option-that-is-specific-to-spatial-indexes"></a>D. Alterando uma opção que é específica a índices espaciais  
 O exemplo a seguir recria o índice espacial criado no exemplo anterior, `SIndx_SpatialTable_geography_col3`, especificando uma nova densidade `LEVEL_3` com DROP_EXISTING = ON.  
  
```sql  
CREATE SPATIAL INDEX SIndx_SpatialTable_geography_col3  
   ON SpatialTable(geography_col)  
   WITH ( BOUNDING_BOX = ( 0, 0, 500, 200 ),  
        GRIDS = ( LEVEL_3 = LOW ),  
        DROP_EXISTING = ON );  
```  
  
### <a name="e-creating-a-spatial-index-on-a-geography-column"></a>E. Criando um índice espacial em uma coluna de geografia  
 O exemplo a seguir cria uma tabela nomeada `SpatialTable2` que contém uma coluna do tipo **geography**, `geography_col`. Em seguida, o exemplo cria um índice espacial, `SIndx_SpatialTable_geography_col1`, em `geography_col`. O exemplo usa os valores de parâmetros padrão do esquema de mosaico GEOGRAPHY_AUTO_GRID.  
  
```sql  
CREATE TABLE SpatialTable2(id int primary key, object GEOGRAPHY);  
CREATE SPATIAL INDEX SIndx_SpatialTable_geography_col1   
   ON SpatialTable2(object);  
```  
  
> [!NOTE]  
>  Para índices de grade geográfica, não é possível especificar uma caixa delimitadora.  
  
### <a name="f-creating-a-spatial-index-on-a-geography-column"></a>F. Criando um índice espacial em uma coluna de geografia  
 O exemplo a seguir cria um segundo índice espacial, `SIndx_SpatialTable_geography_col2`, em `geography_col` na tabela `SpatialTable2`. O exemplo especifica `GEOGRAPHY_GRID` como o esquema de mosaico. O exemplo também especifica diferentes densidades de grade em diferentes níveis e 64 células por objeto. O exemplo também define o preenchimento de índice como `ON`.  
  
```sql  
CREATE SPATIAL INDEX SIndx_SpatialTable_geography_col2  
   ON SpatialTable2(object)  
   USING GEOGRAPHY_GRID  
   WITH (  
    GRIDS = (MEDIUM, LOW, MEDIUM, HIGH ),  
    CELLS_PER_OBJECT = 64,  
    PAD_INDEX  = ON );  
```  
  
### <a name="g-creating-a-spatial-index-on-a-geography-column"></a>G. Criando um índice espacial em uma coluna de geografia  
 O exemplo a seguir cria um terceiro índice espacial, `SIndx_SpatialTable_geography_col3`, em `geography_col` na tabela `SpatialTable2`. O exemplo usa o esquema de mosaico padrão, GEOGRAPHY_GRID e o valor padrão de CELLS_PER_OBJECT (16).  
  
```sql  
CREATE SPATIAL INDEX SIndx_SpatialTable_geography_col3  
   ON SpatialTable2(object)  
   WITH ( GRIDS = ( LEVEL_3 = HIGH, LEVEL_2 = HIGH ) );  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.spatial_index_tessellations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql.md)   
 [sys.spatial_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md)   
 [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
  

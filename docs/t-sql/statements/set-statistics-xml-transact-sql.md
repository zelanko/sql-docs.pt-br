---
title: SET STATISTICS XML (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET_STATISTICS_XML_TSQL
- SET STATISTICS XML
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], statement processing
- STATISTICS XML option
- SET STATISTICS XML statement
- statements [SQL Server], statistical information
- XML [SQL Server], statement execution information
ms.assetid: 2b6d4c5a-a7f5-4dd1-b10a-7632265b1af7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 311212016f42367f90095bf12858210a580b4798
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51698974"
---
# <a name="set-statistics-xml-transact-sql"></a>SET STATISTICS XML (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Faz com que o Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] execute instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] e gere informações detalhadas sobre como as instruções foram executadas na forma de um documento XML bem-definido.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET STATISTICS XML { ON | OFF }  
```  
  
## <a name="remarks"></a>Remarks  
 A configuração de SET STATISTICS XML é definida no momento da execução ou do tempo de execução, e não no momento da análise.  
  
 Quando SET STATISTICS XML estiver ON (acionado), o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna informações de execução para cada instrução, depois de executá-las. Depois que essa opção estiver definida como ON, as informações sobre todas as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] subsequentes serão retornadas até que a opção esteja definida como OFF. Note que SET STATISTICS XML não precisa ser a única instrução em um lote.  
  
 SET STATISTICS XML retorna a saída como **nvarchar(max)** para aplicativos, como o utilitário **sqlcmd**, em que a saída XML é posteriormente usada por outras ferramentas para exibir e processar as informações do plano de consulta.  
  
 SET STATISTICS XML retorna informações como um conjunto de documentos XML. Todas as instruções depois da instrução STATISTICS XML ON serão refletidas na saída por um único documento. Cada documento conterá o texto das instruções, seguido dos detalhes das etapas da execução. A saída mostra informações de tempo de execução como os custos, índices acessados e tipos de operações executadas, ordem de junção, o número de horas de execução de uma operação física, o número de linhas que cada operador físico produziu, e mais.  
  
 O documento que contém o esquema XML para a saída do XML por SET STATISTICS XML é copiado durante a instalação em um diretório local no computador no qual o Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado. Ele pode ser encontrado na unidade que contém os arquivos de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], em:  
  
 \Microsoft SQL Server\100\Tools\Binn\schemas\sqlserver\2004\07\showplan\showplanxml.xsd  
  
 O esquema do plano de execução também pode ser encontrado [neste site](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409).  
  
 SET STATISTICS PROFILE e SET STATISTICS XML são contrapartes um do outro. O primeiro produz saída textual; o último produz saída XML. Em versões futuras do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], novas informações do plano de execução de consultas serão exibidas apenas com a instrução SET STATISTICS XML, e não com a instrução SET STATISTICS PROFILE.  
  
> [!NOTE]  
>  Se **Incluir Plano de Execução Real** estiver selecionado no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], essa opção SET não produzirá a saída do plano de execução XML. Desmarque o botão **Incluir Plano de Execução Real** antes de usar esta opção SET.  
  
## <a name="permissions"></a>Permissões  
 Para usar SET STATISTICS XML e exibir a saída, os usuários devem ter as seguintes permissões:  
  
-   Permissões adequadas para executar as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   A permissão de SHOWPLAN em todos os bancos de dados que são referenciados pelas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Para instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que não produzem conjuntos de resultados STATISTICS XML, somente serão necessárias as permissões apropriadas para executar as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que produzem conjuntos de resultados STATISTICS XML, certifique-se de que ambas, a permissão de execução de instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] e a permissão SHOWPLAN sejam bem-sucedidas, ou a instrução de execução [!INCLUDE[tsql](../../includes/tsql-md.md)] será anulada e nenhuma informação Showplan será gerada.  
  
## <a name="examples"></a>Exemplos  
 As duas instruções a seguir usam as configurações SET STATISTICS XML para mostrar o modo como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] analisa e otimiza o uso de índices em consultas. A primeira consulta usa o operador de comparação Igual a (=), na cláusula WHERE, em uma coluna indexada. A segunda consulta usa o operador LIKE na cláusula WHERE. Isto força o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a usar uma verificação de índice clusterizado para localizar os dados que atendem à condição da cláusula WHERE. Os valores nos atributos **EstimateRows** e **EstimatedTotalSubtreeCost** são menores para a primeira consulta indexada, indicando que ela foi processada com maior rapidez e usou menos recursos que a consulta não indexada.  
  
```  
USE AdventureWorks2012;  
GO  
SET STATISTICS XML ON;  
GO  
-- First query.  
SELECT BusinessEntityID   
FROM HumanResources.Employee  
WHERE NationalIDNumber = '509647174';  
GO  
-- Second query.  
SELECT BusinessEntityID, JobTitle   
FROM HumanResources.Employee  
WHERE JobTitle LIKE 'Production%';  
GO  
SET STATISTICS XML OFF;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [SET SHOWPLAN_XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-xml-transact-sql.md)   
 [Utilitário sqlcmd](../../tools/sqlcmd-utility.md)  
  
  

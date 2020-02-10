---
title: Manter valores de identidade ao importar dados em massa (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- identity values [SQL Server], bulk imports
- data formats [SQL Server], identity values
- bulk importing [SQL Server], identity values
ms.assetid: 45894a3f-2d8a-4edd-9568-afa7d0d3061f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5bb2fbd3129475c5d712cd4d1fce8bbe29ea096f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66011912"
---
# <a name="keep-identity-values-when-bulk-importing-data-sql-server"></a>Manter valores de identidade ao importar dados em massa (SQL Server)
  Os arquivos de dados que contêm valores de identidade podem ser importados [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]em massa para uma instância do. Por padrão, os valores da coluna de identidade do arquivo de dados que é importado são ignorados e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribui valores exclusivos automaticamente. Os valores exclusivos são baseados nos valores de semente e incremento que são especificados durante a criação da tabela.  
  
 Se o arquivo de dados não contiver valores para a coluna de identificador na tabela, use um arquivo de formato para especificar que a coluna de identificador na tabela deve ser ignorada durante a importação dos dados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribui automaticamente valores exclusivos para a coluna.  
  
 Para impedir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a atribuição de valores de identidade durante a importação em massa de linhas de dados, use o qualificador de comando manter identidade apropriado. Quando você especificar um qualificador de manter identidade, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa os valores de identidade no arquivo de dados. Estes qualificadores são os seguintes:  
  
|Comando|Qualificador manter identidade|Tipo de qualificador|  
|-------------|------------------------------|--------------------|  
|`bcp`|**-E**|Opção|  
|BULK INSERT|KEEPIDENTITY|Argumento|  
|INSERT ... SELECT * FROM OPENROWSET(BULK...)|KEEPIDENTITY|Dica de tabela|  
  
 Para obter mais informações, consulte [Utilitário bcp](../../tools/bcp-utility.md), [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql), [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql), [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql), [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql) e [Dicas de tabela &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table).  
  
> [!NOTE]  
>  Para criar um número incrementado automaticamente, que possa ser usado em várias tabelas ou ser chamado de aplicativos, sem referenciar tabelas, consulte [Números de Sequência](../sequence-numbers/sequence-numbers.md).  
  
## <a name="examples"></a>Exemplos  
 Os exemplos neste tópico importam dados em massa usando INSERT... Selecione * de OPENROWSET (BULK...) e mantendo valores padrão.  
  
### <a name="sample-table"></a>Tabela de exemplo  
 Os exemplos de importação em massa requerem que uma tabela denominada tabela **myTestKeepNulls** seja criada no banco de dados do exemplo **AdventureWorks** no esquema **dbo**. Para criar essa tabela. No Editor de Consultas do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], execute:  
  
```  
USE AdventureWorks;  
GO  
SELECT * INTO HumanResources.myDepartment   
   FROM HumanResources.Department  
      WHERE 1=0;  
GO  
SELECT * FROM HumanResources.myDepartment;  
```  
  
 A tabela **Departamento** na qual o`myDepartment` é baseado tem IDENTITY_INSERT definido como OFF. Portanto, para importar dados para uma coluna de identidade, você deve especificar KEEPIDENTITY ou **-E**.  
  
### <a name="sample-data-file"></a>Arquivo de dados de exemplo  
 O arquivo de dados usado nos exemplos da importação em massa contém massa de dados exportada da tabela `HumanResources.Department` em formato nativo. Para criar esse arquivo de dados, no prompt de comando do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, digite:  
  
```  
bcp AdventureWorks.HumanResources.Department out myDepartment-n.Dat -n -T  
```  
  
### <a name="sample-format-file"></a>Arquivo de formato de exemplo  
 Estes exemplos de importação em massa usam um arquivo de formato XML, `myDepartment-f-x-n.Xml`, que usa formatos de dados nativos. Esse exemplo usa `bcp` para criar a geração desse arquivo de formato a partir da tabela `HumanResources.Department` do banco de dados `AdventureWorks`. No prompt de comando do Windows, digite:  
  
```  
bcp AdventureWorks.HumanResources.Department format nul -n -x -f myDepartment-f-n-x.Xml -T  
```  
  
 Para obter mais informações sobre como criar um arquivo de formato, consulte [Criar um arquivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md).  
  
### <a name="a-using-bcp-and-keeping-identity-values"></a>a. Usando bcp e mantendo valores de identidade  
 O exemplo a seguir demonstra como manter valores de identidade ao usar o `bcp` para realizar a importação em massa dos dados. O comando `bcp` usa o arquivo de formato `myDepartment-f-n-x.Xml` e contém as seguintes opções:  
  
|Qualificadores|DESCRIÇÃO|  
|----------------|-----------------|  
|**-E**|Especifica que o valor ou valores de identidade no arquivo de dados serão usados para a coluna de identidade.|  
|**-T**|Especifica que o `bcp` utilitário se conecta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao com uma conexão confiável.|  
  
 No prompt de comando do Windows, digite:  
  
```  
bcp AdventureWorks.HumanResources.myDepartment in C:\myDepartment-n.Dat -f C:\myDepartment-f-n-x.Xml -E -T  
  
```  
  
### <a name="b-using-bulk-insert-and-keeping-identity-values"></a>B. Usando BULK INSERT e mantendo valores de identidade  
 Os exemplos a seguir usam BULK INSERT para importar em massa dados do arquivo `myDepartment-c.Dat` na tabela `AdventureWorks.HumanResources.myDepartment` . A instrução usa o formato de arquivo `myDepartment-f-n-x.Xml` e inclui a opção de KEEPIDENTITY para assegurar que quaisquer valores de identidade no arquivo de dados são retidos.  
  
 No Editor de Consultas do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], execute:  
  
```  
USE AdventureWorks;  
GO  
DELETE HumanResources.myDepartment;  
GO  
BULK INSERT HumanResources.myDepartment  
   FROM 'C:\myDepartment-n.Dat'  
   WITH (  
      KEEPIDENTITY,  
      FORMATFILE='C:\myDepartment-f-n-x.Xml'  
   );  
GO  
SELECT * FROM HumanResources.myDepartment;  
  
```  
  
### <a name="c-using-openrowset-and-keeping-identity-values"></a>C. Usando OPENROWSET e mantendo valores de identidade  
 O exemplo abaixo usa o provedor de conjunto de linhas OPENROWSET para importar em massa dados do arquivo `myDepartment-c.Dat` na tabela `AdventureWorks.HumanResources.myDepartment` . A instrução usa o formato de arquivo `myDepartment-f-n-x.Xml` e inclui a dica de KEEPIDENTITY para assegurar que quaisquer valores de identidade no arquivo de dados são retidos.  
  
 No Editor de Consultas do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], execute:  
  
```  
USE AdventureWorks;  
GO  
DELETE HumanResources.myDepartment;  
GO  
  
INSERT INTO HumanResources.myDepartment  
   with (KEEPIDENTITY)  
   (DepartmentID, Name, GroupName, ModifiedDate)  
   SELECT *  
      FROM  OPENROWSET(BULK 'C:\myDepartment-n.Dat',  
      FORMATFILE='C:\myDepartment-f-n-x.Xml') as t1;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Manter valores nulos ou use os valores padrão durante a importação em massa &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Preparar dados para exportar ou importar em massa &#40;SQL Server&#41;](prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **Para usar um arquivo de formato**  
  
-   [Criar um arquivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [Usar um arquivo de formato para importação em massa de dados &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar um campo de dados &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **Para usar formatos de dados para importação ou exportação em massa**  
  
-   [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **Para especificar formatos de dados para compatibilidade ao usar bcp**  
  
1.  [Especificar terminadores de campo e linha &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
2.  [Especifique o tamanho do prefixo em arquivos de dados usando o bcp &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
3.  [Especifique o tipo de armazenamento de arquivo usando bcp &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Dicas de tabela &#40;&#41;Transact-SQL](/sql/t-sql/queries/hints-transact-sql-table)  
  
  

---
title: Usar o formato nativo Unicode para importar ou exportar dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Unicode [SQL Server], bulk importing and exporting
- data formats [SQL Server], Unicode native
ms.assetid: a6213308-f3d5-406e-9029-19d8bb3367f3
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 310234920939cfea19d6d17370bc3c427ff3fbcc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007938"
---
# <a name="use-unicode-native-format-to-import-or-export-data-sql-server"></a>Usar o formato nativo Unicode para importar ou exportar dados (SQL Server)
  O formato nativo Unicode é útil quando as informações devem ser copiadas de uma instalação [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a outra. O uso de formato nativo para dados do tipo não caractere economiza tempo, eliminando a conversão desnecessária de tipos de dados de e para o formato de caractere. O uso de formato de caractere Unicode para obter todos os dados de caractere impede a perda de qualquer caractere estendido durante a transferência de dados em massa entre servidores que usam páginas de código diferentes. Um arquivo de dados em formato nativo Unicode pode ser lido por qualquer método de importação em massa.  
  
 O formato nativo Unicode é recomendado para transferir em massa dados entre várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um arquivo de dados com caracteres estendidos DBCS. Para obter dados do tipo não caractere, o formato nativo Unicode usa tipos de dados nativos (banco de dados). Para dados de caracteres, como `char`, `nchar`, `varchar`, `nvarchar`, `text`, `varchar(max)`, `nvarchar(max)`, e `ntext`, o formato nativo Unicode usa formato de dados de caractere Unicode.  
  
 Os dados `sql_variant` que são armazenados como um SQLVARIANT em um arquivo de dados do formato nativo Unicode operam da mesma maneira como em um arquivo de dados do formato nativo, exceto os valores `char` e `varchar` que são convertidos para `nchar` e `nvarchar`os quais dobram a quantidade de espaço de armazenamento exigido para as colunas afetadas. Os metadados originais são preservados e os valores são convertidos para original `char` e `varchar` quando importados em massa em uma coluna de tabela de tipo de dados.  
  
## <a name="command-options-for-unicode-native-format"></a>Opções de comando para formato nativo Unicode  
 Você pode importar dados de formato nativo Unicode para uma tabela usando **bcp**, BULK INSERT ou INSERT... SELECIONE \* DE OPENROWSET(BULK...). Para uma **bcp** comando ou a instrução BULK INSERT, você pode especificar o formato de dados na linha de comando. Para uma instrução INSERT ... instrução SELECT * FROM OPENROWSET(BULK...); é necessário especificar o formato dos dados em um arquivo de formato.  
  
 O formato nativo Unicode é suportado pelas seguintes opções:  
  
|Comando|Opção|Description|  
|-------------|------------|-----------------|  
|**bcp**|**-N**|Faz com que o **bcp** os tipos de utilitário para usar o formato nativo Unicode, que usa dados nativos (banco de dados) para obter todos os dados e o formato de dados de caractere Unicode para todos os caracteres (`char`, `nchar`, `varchar`, `nvarchar`, `text`, e `ntext`) dados.|  
|BULK INSERT|DATAFILETYPE **='** widenative **'**|Usa o formato de caractere nativo Unicode na importação de dados em massa.|  
  
 Para obter mais informações, consulte [Utilitário bcp](../../tools/bcp-utility.md), [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) ou [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql).  
  
> [!NOTE]  
>  Como alternativa, você pode especificar a formatação por campo, em um arquivo de formato. Para obter mais informações, consulte [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md).  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir demonstram como exportar em massa dados nativos com o **bcp** e importar em massa os mesmos dados com BULK INSERT.  
  
### <a name="sample-table"></a>Tabela de exemplo  
 Os exemplos exigem que seja criada uma tabela denominada **myTestUniNativeData** no banco de dados de exemplo **AdventureWorks** sob o esquema **dbo**. Antes de executar os exemplos, é necessário criar essa tabela. No Editor de Consultas do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , execute:  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE myTestUniNativeData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 Para preencher esta tabela e exibir o conteúdo resultante, execute as seguintes instruções:  
  
```  
INSERT INTO myTestUniNativeData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3');  
INSERT INTO myTestUniNativeData(Col1,Col2,Col3)  
   VALUES(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestUniNativeData  
  
```  
  
### <a name="using-bcp-to-bulk-export-native-data"></a>Usando o bcp para exportar dados nativos em massa  
 Para exportar dados da tabela para o arquivo de dados, use **bcp** com a opção **out** e os seguintes qualificadores:  
  
|Qualificadores|Description|  
|----------------|-----------------|  
|**-N**|Especifica tipos de dados nativos.|  
|**-T**|Especifica que o utilitário **bcp** se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com uma conexão confiável usando segurança integrada. Se **-T** não for especificado, será necessário especificar **-U** e **-P** para que o logon tenha êxito.|  
  
 O exemplo a seguir exporta dados em massa no formato nativo da tabela `myTestUniNativeData` para um novo arquivo de dados denominado arquivo de dados `myTestUniNativeData-N.Dat`. No prompt de comando do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, digite:  
  
```  
bcp AdventureWorks..myTestUniNativeData out C:\myTestUniNativeData-N.Dat -N -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-native-data"></a>Usando BULK INSERT para importar dados nativos em massa  
 Os exemplos a seguir usam BULK INSERT para importar os dados no arquivo de dados `myTestUniNativeData-N.Dat` na tabela `myTestUniNativeData`. No Editor de Consultas do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , execute:  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT myTestUniNativeData   
    FROM 'C:\myTestUniNativeData-N.Dat'   
   WITH (DATAFILETYPE='widenative');   
GO  
SELECT Col1,Col2,Col3 FROM myTestUniNativeData;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para usar formatos de dados para importação ou exportação em massa**  
  
-   [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Tipos de dados &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)  
  
  

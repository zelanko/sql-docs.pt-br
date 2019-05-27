---
title: Usar o formato de caractere Unicode para importar ou exportar dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], Unicode character
- Unicode [SQL Server], bulk importing and exporting
ms.assetid: 74342a11-c1c0-4746-b482-7f3537744a70
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 34e8f4a5b49c9e023c224e62c23326864ef26f65
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66011646"
---
# <a name="use-unicode-character-format-to-import-or-export-data-sql-server"></a>Usar o formato de caractere Unicode para importar ou exportar dados (SQL Server)
  O formato de caractere Unicode é recomendado para transferir em massa dados entre várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um arquivo de dados com caracteres estendidos DBCS. O formato de dados de caractere Unicode permite exportar dados de um servidor usando uma página de código que difere da página de código usada pelo cliente que está executando a operação. Em tais casos, o uso do formato de caractere Unicode tem as seguintes vantagens:  
  
-   Se os dados de origem e destino forem tipos de dados Unicode, o uso do formato de caractere Unicode preservará todos os dados de caractere.  
  
-   se os dados de origem e destino não forem tipos de dados Unicode, o uso do formato de caractere Unicode minimizará a perda de caracteres estendidos nos dados de origem que não poderão ser representados no destino.  
  
 Os arquivos de dados em formato de caractere Unicode seguem as convenções para arquivos Unicode. Os primeiros dois bytes do arquivo são números hexadecimais, 0xFFFE. Esses bytes servem como marcas de ordem do byte, especificando se o byte de ordem alta é armazenado em primeiro ou por último no arquivo.  
  
> [!IMPORTANT]  
>  Para trabalhar com um arquivo de dados de caractere Unicode, todos os campos de entrada devem ser cadeias de caracteres de texto Unicode (isto é, sejam cadeias de caracteres Unicode de tamanho fixo ou terminadas por caractere).  
  
 Os dados `sql_variant` que são armazenados em um arquivo de dados no formato de caractere Unicode operam da mesma maneira que operam em um arquivo de dados no formato de caractere, exceto que os dados são armazenados como `nchar` em vez de dados `char`. Para obter mais informações sobre formato de caractere, consulte [Suporte a ordenação e Unicode](../collations/collation-and-unicode-support.md).  
  
 Para usar um campo ou terminador de linha diferente do padrão que é fornecido com formato de caractere Unicode, veja [Especificar terminadores de campo e linha &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md).  
  
## <a name="command-options-for-unicode-character-format"></a>Opções de comando para formato de caractere Unicode  
 Você pode importar dados de formato de caractere Unicode para uma tabela usando **bcp**, BULK INSERT ou INSERT... SELECIONE \* DE OPENROWSET. Para um comando **bcp** ou uma instrução BULK INSERT, você pode especificar o formato de dados na linha de comando. Para uma instrução INSERT ... instrução SELECT * FROM OPENROWSET(BULK...); é necessário especificar o formato dos dados em um arquivo de formato.  
  
 Há suporte ao formato de caractere Unicode nas seguintes opções da linha de comando:  
  
|Comando|Opção|Descrição|  
|-------------|------------|-----------------|  
|**bcp**|**-w**|Usa o formato de caractere Unicode.|  
|BULK INSERT|DATAFILETYPE **='** widechar **'**|Usa o formato de caractere Unicode na importação em massa de dados.|  
  
 Para obter mais informações, consulte [Utilitário bcp](../../tools/bcp-utility.md), [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) ou [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql).  
  
> [!NOTE]  
>  Como alternativa, você pode especificar a formatação por campo, em um arquivo de formato. Para obter mais informações, consulte [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md).  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir demonstram como exportar em massa dados de caractere Unicode usando **bcp** e importar em massa os mesmos dados usando BULK INSERT.  
  
### <a name="sample-table"></a>Tabela de exemplo  
 Os exemplos requerem que uma tabela denominada tabela `myTestUniCharData` seja criada no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] no esquema `dbo` . Antes de executar os exemplos, é necessário criar essa tabela. Para criar esta tabela, no Editor de Consultas do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , execute:  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestUniCharData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 Para preencher esta tabela e exibir o conteúdo resultante, execute as seguintes instruções:  
  
```  
INSERT INTO myTestUniCharData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3')   
        ,(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestUniCharData;  
  
```  
  
### <a name="using-bcp-to-bulk-export-unicode-character-data"></a>Usando o bcp para exportar em massa dados de caractere Unicode  
 Para exportar dados da tabela para o arquivo de dados, use **bcp** com a opção **out** e os seguintes qualificadores:  
  
|Qualificadores|Descrição|  
|----------------|-----------------|  
|**-w**|Especifica o formato de caractere Unicode.|  
|**-t** `,`|Especifica uma vírgula (`,`) como terminador de campo.<br /><br /> Observação: O terminador de campo padrão é a guia de caractere Unicode (\t). Para obter mais informações, veja [Especificar terminadores de campo e linha &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md).|  
|**-T**|Especifica que o utilitário **bcp** se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com uma conexão confiável usando segurança integrada. Se **-T** não for especificado, será necessário especificar **-U** e **-P** para que o logon tenha êxito.|  
  
 O exemplo seguinte exporta em massa dados em formato de caractere Unicode da tabela `myTestUniCharData` em um arquivo de dados novo nomeado arquivo de dados `myTestUniCharData-w.Dat` que usa a vírgula (`,`) como terminador de campo. No prompt de comando do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, digite:  
  
```  
bcp AdventureWorks2012..myTestUniCharData out C:\myTestUniCharData-w.Dat -w -t, -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-unicode-character-data"></a>Usando BULK INSERT para importar em massa dados de caractere Unicode  
 O exemplo a seguir usa `BULK INSERT` para importar os dados no arquivo de dados `myTestUniCharData-w.Dat` para a tabela `myTestUniCharData`. O terminador de campo de não padrão (`,`) deve ser declarado na instrução. No Editor de Consultas do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , execute:  
  
```  
USE AdventureWorks2012;  
GO  
BULK INSERT myTestUniCharData   
   FROM 'C:\myTestUniCharData-w.Dat'   
   WITH (  
      DATAFILETYPE='widechar',  
      FIELDTERMINATOR=','  
   );   
GO  
SELECT Col1,Col2,Col3 FROM myTestUniCharData;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para usar formatos de dados para importação ou exportação em massa**  
  
-   [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Tipos de dados &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [Suporte a ordenações e a Unicode](../collations/collation-and-unicode-support.md)  
  
  
